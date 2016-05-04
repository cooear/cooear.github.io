---
layout: post
title: "linux踢出在线用户"
date: 2013-08-30 14:37:46 +0800
comments: true
categories: 
tags: [Linux, 查看用户, pkill]
keywords: Liunx, 查看登陆用户, 踢用户, pkill
description: Linux查看并踢出登陆用户命令
---

###linux踢出远程登录用户命令：

查看当前自己的终端：

	[root@belen ~]# who am i
	root     pts/1        2013-01-22 10:45 (192.168.250.110)
	
**一、** 输入w命令查看已登录用户信息
	<!--more-->

	[root@belen ~]# who
	root     pts/0        2013-01-22 09:56 (192.168.250.27)
	root     pts/1        2013-01-22 10:45 (192.168.250.110)
	[root@belen ~]# w
	10:46:13 up 4 days, 16:28,  2 users,  load average: 0.36, 0.38, 0.29
	USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
	root     pts/0    192.168.250.27   09:56   12:03   0.02s  0.02s -bash
	root     pts/1    192.168.250.110  10:45    0.00s  0.02s  0.01s w	
	

**二、** 踢出用户:pkill -kill -t 用户tty

	[root@belen ~]# pkill -kill -t pts/0
	
**三、** 验证操作是否成功	

	[root@belen ~]# w
	10:48:17 up 4 days, 16:30,  1 user,  load average: 0.32, 0.35, 0.28
	USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
	root     pts/1    192.168.250.110  10:45    0.00s  0.03s  0.02s w

<br /><br /><br />
	
***	
**w命令的属性解释**：
***

* USER：显示登陆用户帐号名。用户重复登陆，该帐号也会重复出现。
* TTY：用户登陆所用的终端。
* FROM：显示用户在何处登陆系统。
* LOGIN@：是LOGIN AT的意思，表示登陆进入系统的时间。
* IDLE：用户空闲时间，从用户上一次任务结束后，开会记时。
* JCPU：一终端代号来区分，表示在摸段时间内，所有与该终端相关的进程任务所耗费的CPU时间。
* PCPU：指WHAT域的任务执行后耗费的CPU时间。
* WHAT：表示当前执行的任务	