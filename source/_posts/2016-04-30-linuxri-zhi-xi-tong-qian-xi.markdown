---
layout: post
title: "Linux日志系统浅析"
date: 2013-08-23 15:47:25 +0800
comments: true
categories: 
tags: [Linux, 日志, 分析]
keywords: Liunx, 日志分析, debug, auth.log,系统日志
description: Linux日志系统深度剖析，快速了解系统中个类服务如：auth、dmesg、xferlog、cron等，定位解决系统中各种问题。
---

　　当我们使用的Linux系统正常运行时，花费一些时间去学习和了解Linux的日志系统/var/log 还是很有必要的;因为当你了解路Linux的日志系统时当服务器或者某项服务运行不正常时可以很方便的通过日志定位问题所在,所以正确的设置Linux的日志输出可以达到事半功倍的效果。通常情况下你可以使用less、more、cat、vi、grep或者tail命令来查看log文件的内容。

定义：

　　**log files:UNIX/LINUX**有一个严格的政策不报告错误消息到用户界面即使可能没有用户在阅读这些消息。而错误消息的交互命令发送到终端屏幕、错误或信息消息产生的非交互式命令是“记录”的文件在目录**/var/log/**;日志文件在**/var/log**通常可以无限增长,可能需要定期清洗。
　　
<!--more-->
* /var/log/auth.log

　　记录所有正常用户和系统进程的所有登录、登出.

* /var/log/btmp

　　记录错误的登录尝试，执行lastb命令可以查看到最后一个不成功的登录尝试.

* /var/log/debug

　　Debugging output from various packages.

* /var/log/dmesg

　　内核环缓冲区,此文件的内容是指由dmesg命令。

* /var/log/gdm/

　　GDM log files. Normally a subset of the last X log file. See /var/log/xdm.log for mode details.

* /var/log/wtmp

　　该日志文件永久记录每个用户登录、注销及系统的启动、停机的事件。因此随着系统正常 运行时间的增加，该文件的大小也会越来越大，增加的速度取决于系统用户登录的次数。该日志文件可以用来查看用户的登录记录，last命令就通过访问这个文 件获得这些信息，并以反序从后向前显示用户的登录记录，last也能根据用户、终端 tty或时间显示相应的记录。

* /var/log/xferlog

　　该日志文件记录FTP会话，可以显示出用户向FTP服务器或从服务器拷贝文件的记录。该文件会显示用户拷贝到服务器上的用来入侵服务器的恶意程序，以及该用户拷贝了哪些文件供他使用。

* /var/log/boot.log

　　该文件记录系统在引导过程中发生的事件，就是Linux系统开机自检过程显示的信息。

* /var/log/cron

　　该日志文件记录crontab守护进程crond所派生的子进程的动作，无论crontab(或crond)开始执行一个job该日志都将记录.

* /var/log/maillog

　　该日志文件记录服务器上mail服务的所有活动(邮件的发出和接收);它可以用来查看用户使用哪个系统发送工具或把数据发送到哪个系统.

* /etc/rsyslog.conf

　　controls what goes inside some of the log files. For example, following is the entry in rsyslog.conf for /var/log/messages.

	$ grep "/var/log/messages"                  /etc/rsyslog.conf
	*.info;mail.none;authpriv.none;cron.none      /var/log/messages　　
　　

* /var/log/lastlog

　　记录最近成功登录的事件和最后一次不成功的登录事件,该文件是二进制文件，需要使用 lastlog命令查看.

* /var/log/syslog

　　The 'system' log file. The contents of this file is managed via the syslogd daemon which more often than not takes care of all log manipulation on most systems.

* /var/log/xdm.log

　　XDM log file. Normally subset of the last X startup log and pretty much useless in light of the details the X logs is able to provide us with. Only consult this file if you have XDM specific issues otherwise just use the X logfile.

* /var/log/secure：

　　记录登入系统存取资料的日志，例如 pop3, ssh, telnet, ftp 等都都会记录在次日志文件中。
　　