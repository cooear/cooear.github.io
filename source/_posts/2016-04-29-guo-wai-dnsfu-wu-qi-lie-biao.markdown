---
layout: post
title: "国外DNS服务器列表"
date: 2016-04-29 18:13:51 +0800
comments: true
description:
keywords:
categories: 
---

###对付DNS劫持，就要国外DNS服务器：

	8.8.8.8    
	8.8.4.4
	
	##支持非标准端口(443、5353)
	208.67.222.222    
	208.67.220.220
	
	209.244.0.3    
	209.244.0.4
	
	156.154.70.1
	156.154.71.1

	4.2.2.1    
	4.2.2.2

	208.76.50.50
	208.76.51.51

	198.153.192.40
	198.153.194.40

	198.153.192.50
	198.153.194.50

	198.153.192.60    
	198.153.194.60

	8.26.56.26
	8.20.247.20

	184.169.143.224
	184.169.161.155

	67.138.54.100
	207.225.209.66
	
<!--more-->	
###配置方法：

控制面板——》网络和Internet——》网络和共享中心——》更改适配器设置——》找到本地连接（就是正在用的那个网络连接）——》右键属性——》Internet协议版本4——》双击打开之后把“自动获取DNS服务器地址”改为“使用下面的DNS服务器地址”并填上地址（从上面那堆里任选一个）。



###刷新DNS缓存：

WINDOWS：win+r之后输入cmd回车，再输入并点击回车键

		ipconfig/flushdns

OS X 10.10: 在［应用程序］［实用工具］［终端］运行命令 

		sudo discoveryutil udnsflushcaches

OS X 10.9: 在［应用程序］［实用工具］［终端］运行命令 

		dscacheutil -flushcache; sudo killall -HUP mDNSResponder

OS X 10.7 ~ 10.8: 在［应用程序］［实用工具］［终端］运行命令 

		sudo killall -HUP mDNSResponder
		
Linux: 在［终端］运行命令 

		/etc/rc.d/init.d/nscd restart		

Android、iOS: 重新启动设备

**注意**：由于地域的不同，相同的DNS解析速度差别可能会很大；Google尽管在服务器上有着无人不知的优势，但在你所处的地域速度可能不是最理想的。所以请根据自己的情况选择适合自己的DNS服务,DNS速度测试工具[DNSBench下载](http://g1c1i0.cooear.com/images/uploads/2015/03/DNSBench.rar)。
	
	







