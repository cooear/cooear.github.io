---
layout: post
title: "Linux下scp语法命令具体实例总结"
date: 2013-08-03 15:13:58 +0800
comments: true
categories: 
tags: [Linux, scp, rsync, 语法]
keywords: Liunx, scp, 同步, 语法, rsync
description: Linux下scp语法命令实现非rsync的文件同步
---

　　**scp**就是secure copy可以简单的理解为是利用SSH协议来传输数据的cp命令，使用和ssh相同的认证方式，提供相同的安全保证 。但是两者的区别在于cp命令是在同一台物理主机上使用的，而scp则可以在两台不同的物理主机上传输文件数据。

**SCP**命令语法:

	scp [-1245BCpqrv] [-c cipher] [F ssh_config] [-I identity_file] [-l limit] [-o ssh_option] [-P port] [-S program] [[user@]host1:] file1 […] [[suer@]host2:]file2

scp可选参数：

<!--more-->
|相关参数|解释|
|:----:|:----:|
|-v|和大多数 linux 命令中的 -v 意思一样 , 用来显示进度 . 可以用来查看连接 , 认证 , 或是配置错误 .|
|-C|使能压缩选项|
|-P| 选择端口 . 注意 -p 已经被 rcp 使用 .|
|-4| 强行使用 IPV4 地址 . |
|-6|强行使用 IPV6 地址 .|


scp是linux下的远程拷贝

命令：

1. 将本地文件拷贝到远程：scp  文件名 用户名@计算机IP或者计算机名称:远程路径

		scp local_file remote_username@remote_ip:remote_folder
2. 从远程将文件拷回本地：scp  用户名@计算机IP或者计算机名称:文件名 本地路径

		scp remote_username@remote_ip:remote_folder local_file
3. 将本地目录拷贝到远程：scp -r 目录名   用户名@计算机IP或者计算机名称:远程路径

		scp -r local_folder remote_username@remote_ip:remote_dir
4. 从远程将目录拷回本地：scp -r   用户名@计算机IP或者计算机名称:目录名本地路径

		scp -r remote_username@remote_ip:remote_folder local_dir
		
　　另外，作为网站管理员会经常涉及两天计算机间的文件传输，如：数据文件的异地备份，但作为脚本又不可能自己输入scp的用户密码，故总结了一下两张方法：		

* 方法一:

		sshpass -p 'password' scp file.gz root@xxx.xxx.xxx.1:/backup
	
* 方法二:

		#!/usr/bin/expect
		spawn scp  backup.sql.gz root@remote_ip:remote_folder
		set pass "password"
		expect {
			password: {send "$pass\r"; exp_continue}
		}	
	
	
* 执行这个脚本

		expect send_file.exp

<br /><br />
___	

**注**:网上还普遍有一种方法“建立两台计算机之间的安全信任关系”这样在脚本执行scp时也可不输入密码，但cooear不太喜欢这种方法所有没有介绍，需要的可以自行Google。		