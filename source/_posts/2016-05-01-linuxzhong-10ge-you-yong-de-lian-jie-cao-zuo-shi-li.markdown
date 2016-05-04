---
layout: post
title: "Linux中10个有用的链接操作示例"
date: 2013-02-20 00:01:08 +0800
comments: true
categories: 
tags: [Linux, 命令, 语法]
keywords: Liunx, 符号命令, 管道命令, 优先执行命令
description: Linux中10个有用的链接操作示例，使用符号命令、管道命令和优先执行命令达到各种特性化的需求。
---

Linux中的链接命令意味着几个命令联合在一起使用，他们在执行命令时依据彼此之间执行的结果。Linux中的链接命令就像你使用shell语言写的能在命令行中直接执行的shell脚本。链接命令是程序的自动化成为可能。此外，在链接命令的作用下一台无人操作的机器可以有序的运行多个系统。

本文旨在对常用的链接命(command­-chaining)令通过简要分析描述和相应的例子来提高我们码代码的能力，使我们能够写出更精炼更高效的代码从而降低系统负载。

<!--more-->
1. **&符号**

	**‘&’**符号作用是使命令可以后台运行而不中断执行。在命令行终端中键入下面命令并以空格和**'&'**符号隔开。另外，你可以一行执行多个后台命令。
	
	后台执行1条命令如下：
	
		belen@localhost:~$ ping -c3 www.cooear.com &
		
	后台同时执行2条命令如下：
	
		root@localhost:/home/belen# apt-get update & apt-get upgrade &
		

2. **分号命令(;)**

	分号命令是为了使在一行中执行的多个命令可以有序的单独执行。
	
		root@localhost:/home/belen# apt-get update ; apt-get upgrade ; mkdir test

	上面一块执行的命令中地一个执行**update**命令，然后执行**upgrade**命令最后执行在当前目录下创建‘test’目录的命令。

3. **&&符号命令**

	**&&**命令只有在地一个命令执行成功后才会执行第二个命令，即只有第一个命令的退出状态为1时。这个命令对于检查最后一个命令的执行状态非常有用。

	例如，我想访问网站 **cooear.com**于是使用命令行访问，在访问前我需要先检查下网站所在主机是否可以正常访问。
	
		root@localhost:/home/belen# ping -c3 www.cooear.com && links www.cooear.com

4. **||符号命令**

	或命令(**OR Operator**)和程序中的‘**else**’类似。上面的命令告诉我们只有在第一个命令正确执行后才能执行第二个命令，即第一个命令的退出状态值为‘1’。
	
	例如，当我们想使用非root用户执行'apt-get update'，当第一个命令执行失败再执行第二个名'links www.cooear.com'时可以使用下面的代码。
	
		belen@localhost:~$ apt-get update || links cooear.com
	
	上面的命令因为当前用户不能执行系统的**update**操作，所以第一个命令执行失败因此最后一个命令'**links cooear.com**'被执行
	
		belen@localhost:~$ mkdir test || links cooear.com	

5. **!符号命令**

	**!**符合命令(**NOT Operator**)和程序中的'**except**'类似。这个命令将执行所有除了提供的条件。为了更好的理解我们将在你的home目录创建目录'belen'然后‘**cd**’到该目录。
	
		belen@localhost:~$ mkdir belen 
		belen@localhost:~$ cd belen

	接下来在'belen'目录中创建各种类型的文件。	
	
		belen@localhost:~/belen$ touch a.doc b.doc a.pdf b.pdf a.xml b.xml a.html b.html
	
	我们已经在'belen'目录中创建了各种文件。
	
		belen@localhost:~/belen$ ls 
		a.doc  a.html  a.pdf  a.xml  b.doc  b.html  b.pdf  b.xml		
	
	现在使用一种简单的方法删除除'html'结尾的所有文件。
	
		belen@localhost:~/belen$ rm -r !(*.html)
		
	最后为了验证结果，在命令行中执行ls 命令列出所有的文件列表。
	
		belen@localhost:~/belen$ ls 
		a.html  b.html		

6. **AND-OR 符号命令(&& – ||)**

	当前符号命令(**AND-OR operator**)是使用'AND'(**&&**)和'OR'(**||**)结合的命令，这个命令和if-else类似。
	
	例如，我们执行ping **cooear.com**，如果成功则输出'**Verified**'否则输出'Host Down'。
	
		belen@localhost:~/belen$ ping -c3 www.cooear.com && echo "Verified" || echo "Host Down"
		
	代码输出：
	
		PING www.cooear.com (220.181.136.225) 56(84) bytes of data. 
		64 bytes from www.cooear.com (220.181.136.225): icmp_req=1 ttl=55 time=216 ms 
		64 bytes from www.cooear.com (220.181.136.225): icmp_req=2 ttl=55 time=224 ms 
		64 bytes from www.cooear.com (220.181.136.225): icmp_req=3 ttl=55 time=226 ms 

		--- www.cooear.com ping statistics --- 
		3 packets transmitted, 3 received, 0% packet loss, time 2001ms 
		rtt min/avg/max/mdev = 216.960/222.789/226.423/4.199 ms 
		Verified	

	现在断开你的网络连接执行同样的命令试试。
	
		belen@localhost:~/belen$ ping -c3 www.cooear.com && echo "verified" || echo "Host Down"
		
	代码输出：
	
		ping: unknown host www.tecmint.com 
		Host Down			

7. **管道符号命令(|)**

	当我们想将上一个输出的命令作为下一个命令的输入值时那么管道命令(|)将是十分有用的。例如，将'**ls -l**'输出的值通过管道命令传给**less**命令。
	
		belen@localhost:~$ ls -l | less

8. **组合符号命令{}**

	两个或者更多的命令联合执行，第二个命令的执行依据第一个命令的执行结果。
	
	例如，检查我的'Downloads'目录下是否存在文件'xyz.txt'和'xyz1.txt'，并输出相应的结果。
	
		belen@localhost:~$ [ -f /home/belen/Downloads/xyz.txt ] || echo "The file does not exist"
		belen@localhost:~$ [ -f /home/belen/Downloads/xyz1.txt ] || echo "The file does not exist" 
		"The file does not exist"

9. **优先执行符号命令()**

	这个符号()允许命令按照一定的优先级执行。
	
		Command_x1 && Command_x2 || Command_x3 && Command_x4.
		
	上面的命令如果**Command_x1**执行失败会怎样？**Command_x2**,**Command_x3**,**Command_x4**这个几个命令一个也不会执行，因此我们应该使用优先执行符号：	
	
		(Command_x1 && Command_x2) || (Command_x3 && Command_x4)
		
	上面这个命令即使**Command_x1**和**Command_x2**都执行失败，**Command_x3**和**Command_x4**也会根据**Command_x3**的退出状态执行	

10. **Concatenation Operator (\)**

	The Concatenation Operator (\) as the name specifies, is used to concatenate large commands over several lines in the shell. For example, The below command will open text file test(1).txt.
	
		belen@localhost:~/Downloads$ nano test\(1\).txt