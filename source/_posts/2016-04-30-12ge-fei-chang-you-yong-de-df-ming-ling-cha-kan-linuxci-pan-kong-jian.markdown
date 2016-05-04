---
layout: post
title: "12个非常有用的”df”命令查看Linux磁盘空间"
date: 2014-02-25 16:20:32 +0800
comments: true
categories: 
tags: [Linux, 命令, 语法]
keywords: Liunx, df, 磁盘命令, 语法
description: Linux下查看磁盘空间命令，监控磁盘状态
---

　　你也许会在网上发现很用用于检查**Linux**磁盘空间的工具。然而，Linux拥有强大的内置磁盘空间检查工具"df"。"df"是"disk filesystem"的缩写，用于检查**Linux**系统上有效的可用磁盘空间。
　　
　　使用"-h"参数即(df -h)以对人友好的数据格式(kb,mb,GB)展示磁盘使用情况。这篇文章将用"df"命令全面的展示一种检查磁盘空间的方法。

1. 检查磁盘使用情况。

	"df"命令显示设备名称，总数据块，总磁盘空间，使用的磁盘空间，可用的磁盘空间和挂载的文件系统节点。

	<!--more-->	
		[root@belen ~]# df

		Filesystem           1K-blocks      Used Available Use% Mounted on
		/dev/cciss/c0d0p2     78361192  23185840  51130588  32% /
		/dev/cciss/c0d0p5     24797380  22273432   1243972  95% /home
		/dev/cciss/c0d0p3     29753588  25503792   2713984  91% /data
		/dev/cciss/c0d0p1       295561     21531    258770   8% /boot
		tmpfs                   257476         0    257476   0% /dev/shm



2. 显示磁盘使用情况的所有信息。

	和上面类似，但它也显示了虚拟文件系统的信息以及所有文件系统的磁盘使用情况和内存利用率。

		[root@belen ~]# df -a

		Filesystem           1K-blocks      Used Available Use% Mounted on
		/dev/cciss/c0d0p2     78361192  23186116  51130312  32% /
		proc                         0         0         0   -  /proc
		sysfs                        0         0         0   -  /sys
		devpts                       0         0         0   -  /dev/pts
		/dev/cciss/c0d0p5     24797380  22273432   1243972  95% /home
		/dev/cciss/c0d0p3     29753588  25503792   2713984  91% /data
		/dev/cciss/c0d0p1       295561     21531    258770   8% /boot
		tmpfs                   257476         0    257476   0% /dev/shm
		none                         0         0         0   -  /proc/sys/fs/binfmt_misc
		sunrpc                       0         0         0   -  /var/lib/nfs/rpc_pipefs

3. 以对人友好易都的格式显示磁盘使用情况。

	你是否注意到上面显示的数据信息不易都，因为我们习惯于使用mb，gb等格式读取和记忆数据大小信息。

	"df"命令使用"-h"参数可用以对人友好和易都的格式显示磁盘使用情况（如: 1k 2M 3G）。
	
		[root@belen ~]# df -h

		Filesystem            Size  Used Avail Use% Mounted on
		/dev/cciss/c0d0p2      75G   23G   49G  32% /
		/dev/cciss/c0d0p5      24G   22G  1.2G  95% /home
		/dev/cciss/c0d0p3      29G   25G  2.6G  91% /data
		/dev/cciss/c0d0p1     289M   22M  253M   8% /boot
		tmpfs  

4. 显示/home目录下的文件系统信息

		[root@belen ~]# df -hT /home

		Filesystem		Type    Size  Used Avail Use% Mounted on
		/dev/cciss/c0d0p5	ext3     24G   22G  1.2G  95% /home

5. 以字节(Bytes)的形式展示文件系统信息。

		[root@belen ~]# df -k

		Filesystem           1K-blocks      Used Available Use% Mounted on
		/dev/cciss/c0d0p2     78361192  23187212  51129216  32% /
		/dev/cciss/c0d0p5     24797380  22273432   1243972  95% /home
		/dev/cciss/c0d0p3     29753588  25503792   2713984  91% /data
		/dev/cciss/c0d0p1       295561     21531    258770   8% /boot
		tmpfs                   257476         0    257476   0% /dev/shm

6. 以MB的形式展示文件系统信息。

		[root@belen ~]# df -m

		Filesystem           1M-blocks      Used Available Use% Mounted on
		/dev/cciss/c0d0p2        76525     22644     49931  32% /
		/dev/cciss/c0d0p5        24217     21752      1215  95% /home
		/dev/cciss/c0d0p3        29057     24907      2651  91% /data
		/dev/cciss/c0d0p1          289        22       253   8% /boot
		tmpfs                      252         0       252   0% /dev/shm

7. 以GB的形式展示文件系统信息。

		[root@belen ~]# df -h

		Filesystem            Size  Used Avail Use% Mounted on
		/dev/cciss/c0d0p2      75G   23G   49G  32% /
		/dev/cciss/c0d0p5      24G   22G  1.2G  95% /home
		/dev/cciss/c0d0p3      29G   25G  2.6G  91% /data
		/dev/cciss/c0d0p1     289M   22M  253M   8% /boot
		tmpfs                 252M     0  252M   0% /dev/shm

8. 展示文件系统索引节点。

	"df"使用"-i"参数显示文件系统已经使用的索引信息和百分比。
	
		root@tecmint ~]# df -i

		Filesystem            Inodes   IUsed   IFree IUse% Mounted on
		/dev/cciss/c0d0p2    20230848  133143 20097705    1% /
		/dev/cciss/c0d0p5    6403712  798613 5605099   13% /home
		/dev/cciss/c0d0p3    7685440 1388241 6297199   19% /data
		/dev/cciss/c0d0p1      76304      40   76264    1% /boot
		tmpfs                  64369       1   64368    1% /dev/shm

9. 展示文件类型。

		[root@belen ~]# df -T

		Filesystem		Type   1K-blocks  Used      Available Use% Mounted on
		/dev/cciss/c0d0p2	ext3    78361192  23188812  51127616  32%   /
		/dev/cciss/c0d0p5	ext3    24797380  22273432  1243972   95%   /home
		/dev/cciss/c0d0p3	ext3    29753588  25503792  2713984   91%   /data
		/dev/cciss/c0d0p1	ext3    295561     21531    258770    8%    /boot
		tmpfs			tmpfs   257476         0    257476    0%   /dev/shm
		
	从上面的输出你可以看到并没有文件类型的信息，当你使用"-T"可以查看相关的文件类型。

10. 展示特定的文件类型。

	如果你想只显示特定的文件类型可以使用"-t"参数。例如：
	
		[root@belen ~]# df -t ext3

		Filesystem           1K-blocks      Used Available Use% Mounted on
		/dev/cciss/c0d0p2     78361192  23190072  51126356  32% /
		/dev/cciss/c0d0p5     24797380  22273432   1243972  95% /home
		/dev/cciss/c0d0p3     29753588  25503792   2713984  91% /data
		/dev/cciss/c0d0p1       295561     21531    258770   8% /boot

11. 展示排除特定的文件类型。

		[root@belen ~]# df -x ext3

		Filesystem           1K-blocks      Used Available Use% Mounted on
		tmpfs                   257476         0    257476   0% /dev/shm

12. "df"命令的帮助信息。

		[root@belen ~]# df --help

		Usage: df [OPTION]... [FILE]...
		Show information about the file system on which each FILE resides,
		or all file systems by default.

		Mandatory arguments to long options are mandatory for short options too.
		-a, --all             include dummy file systems
		-B, --block-size=SIZE use SIZE-byte blocks
		-h, --human-readable  print sizes in human readable format (e.g., 1K 234M 2G)
		-H, --si              likewise, but use powers of 1000 not 1024
		-i, --inodes          list inode information instead of block usage
		-k                    like --block-size=1K
		-l, --local           limit listing to local file systems
		--no-sync         do not invoke sync before getting usage info (default)
		-P, --portability     use the POSIX output format
		--sync            invoke sync before getting usage info
		-t, --type=TYPE       limit listing to file systems of type TYPE
		-T, --print-type      print file system type
		-x, --exclude-type=TYPE   limit listing to file systems not of type TYPE
		-v                    (ignored)
		--help     display this help and exit
		--version  output version information and exit

		SIZE may be (or may be an integer optionally followed by) one of following:
		kB 1000, K 1024, MB 1000*1000, M 1024*1024, and so on for G, T, P, E, Z, Y.

		Report bugs to .
　　
