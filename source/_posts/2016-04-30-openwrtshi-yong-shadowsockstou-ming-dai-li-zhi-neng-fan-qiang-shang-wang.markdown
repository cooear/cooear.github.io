---
layout: post
title: "OpenWrt使用ShadowSocks透明代理智能翻墙上网"
date: 2015-02-14 10:00:09 +0800
comments: true
categories: 
tags: [Openwrt, ShadowSocks, VPN, Lantern]
keywords: Openwrt, ShadowSocks, 透明代理, 智能翻墙, Lantern, 云梯, 代理, VPN
description: OpenWrt使用ShadowSocks透明代理智能翻墙上网，实现家庭各类设备方便无缝异翻墙
---

　　<font color=red >本教程前提是需要有一个ShadowSocks账号或安装ShadowSocks服务的VPS（墙外的）</font>。

###一、安装**OpenWrt**并配置上网###

1. telnet 192.168.1.1 至Openwrt并修改root密码

		telnet 192.168.1.1	
2. 配置上网参数

		uci set network.wan.proto=pppoe
		uci set network.wan.username=name
		uci set network.wan.password=123456
		uci commit network ifup wan
3. 安装luci界面，并配置开机启动
	
		opkg update
		opkg install luci
		/etc/init.d/uhttpd start
		/etc/init.d/uhttpd enable 
4. 修改luci界面端口号

		vim /etc/config/uhttpd
		
	<!--more-->					
5. 修改ssh默认的22端口号

		vim /etc/config/dropbear
6. 自定义DNS

	*a.* 创建 /etc/config/sec_resolv.conf
	
		vim /etc/config/sec_resolv.conf
		nameserver 8.8.8.8
		nameserver 8.8.4.4
		nameserver 208.67.222.222
	*b.*  编辑 /etc/config/dhcp
	
	找到 option resolvfile 选项，替换/tmp/resolv.conf.auto为/etc/config/sec_resolv.conf.

###二、软件包安装###

执行命令：

	opkg update
shadowsocks-libev[下载](http://sourceforge.net/projects/openwrt-dist/files/shadowsocks-libev/)：

必须包安装：

olarssl版本的shadowsocks（polarssl体积更小）：

	opkg install iptables-mod-nat-extra ipset libpolarssl

普通版本（openssl）的shadowsocks，那么(openssl兼容性更好)：

	opkg install iptables-mod-nat-extra ipset libopenssl
	
卸载dnsmasq并安装dnsmasq-full以及相应的扩展包(dnsmasq没有ipset功能)

	opkg remove dnsmasq && opkg install dnsmasq-full
	cd /tmp
	opkg install shadowsocks-libev_x.x.x-x_ar71xx.ipk


###三、配置###

1. 配置/etc/shadowsocks.json

		{
			"server": "X.X.X.X",
			"server_port": "443",
			"password": "password",
			"local_port": "1080",
			"method": "aes-256-cfb"
		}
2. 修改/etc/init.d/shadowsocks ，其实就是把Client Mode注释掉再把Proxy Mode的注释去掉

		#!/bin/sh /etc/rc.common

		START=95
		
		SERVICE_USE_PID=1
		SERVICE_WRITE_PID=1
		SERVICE_DAEMONIZE=1
		SERVICE_PID_FILE=/var/run/shadowsocks.pid
		CONFIG=/etc/shadowsocks.json
		
		start() {
			# Client Mode
			#service_start /usr/bin/ss-local -c $CONFIG -f $SERVICE_PID_FILE
			# Proxy Mode
			service_start /usr/bin/ss-redir -c $CONFIG -f $SERVICE_PID_FILE
		}
		
		stop() {
			# Client Mode
			#service_stop /usr/bin/ss-local
			# Proxy Mode
			service_stop /usr/bin/ss-redir
		}
3. 启动shadowsocks，并设置开机运行：

		/etc/init.d/shadowsocks enable
		/etc/init.d/shadowsocks start

###四、配置dnsmasq和ipset###

1. 将iptables规则加入防火墙中（添加至/etc/rc.local可开机启动）

		ipset -N gfwlist iphash
		iptables -t nat -A PREROUTING -p tcp -m set –match-set gfwlist dst -j REDIRECT –to-port 1080
		iptables -t nat -A OUTPUT -p tcp -m set –match-set gfwlist dst -j REDIRECT –to-port 1080
2. 修改/etc/dnsmasq.conf，在最后加入 conf-dir=/etc/dnsmasq.d ，新建并进入目录/etc/dnsmasq.d，并将my_dnsmasq.conf放入该目录。

	my_dnsmasq.conf具体格式如下：
	
		#使用不受污染干扰的DNS解析该域名 可以将此IP改为自己使用的DNS服务器
		server=/google.com/208.67.222.222#443
		#将解析出来的IP保存到名为gfwlist的ipset表中
		ipset=/google.com/gfwlist

###五、ss-tunnel转发UDP的DNS的请求###

	#!/bin/sh /etc/rc.common

	START=95

	SERVICE_USE_PID=1
	SERVICE_WRITE_PID=1
	SERVICE_DAEMONIZE=1
	SERVICE_PID_FILE=/var/run/shadowsocks.pid
	CONFIG=/etc/shadowsocks.json
	DNS=8.8.8.8:53
	TUNNEL_PORT=5353

	start() {
		# Client Mode
		#service_start /usr/bin/ss-local -c $CONFIG -f $SERVICE_PID_FILE
		# Proxy Mode
		service_start /usr/bin/ss-redir -c $CONFIG -f $SERVICE_PID_FILE
		# Tunnel
		service_start /usr/bin/ss-tunnel -c $CONFIG -u -l $TUNNEL_PORT -L $DNS
	}

	stop() {
		# Client Mode
		#service_stop /usr/bin/ss-local
		# Proxy Mode
		service_stop /usr/bin/ss-redir
		# Tunnel
		service_stop /usr/bin/ss-tunnel
	}



**注**：至此路由器已经my_dnsmasq.conf里面的域名已经会自动使用ss代理翻墙