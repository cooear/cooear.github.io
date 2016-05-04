---
layout: post
title: "GAE(Google App Engine)+goagent+chrome浏览器+switchysharp图文教程"
date: 2014-05-03 10:37:34 +0800
comments: true
categories: 
tags: [GAE, VPN, Lantern, 翻墙, switchysharp, Proxy SwitchyOmega, Gmail, GFW]
keywords: GAE, VPN, Lantern, 翻墙, switchysharp, Proxy SwitchyOmega, GFW
description: GoAgent是google开发的一个基于Google Appengine的代理工具，永久免费，且速度快、运行稳定，兼容IE，Firefox，chrome都是可以正常使用的，自此可以使用云梯翻越GFW。
---

作为一个技术宅、IT男，同时为了满足我们的好奇心，求知欲，或不可告人的目的，我们常常需要看看“墙外”的风光。Windows下方便的有自由门、逍遥游等可以满足这个小小的要求，可会不定时的遭到“暗杀”，且网速慢、不稳定，用着十分的不爽。

现在推荐一个基于GAE（Google App Engine）+ goagent + switchysharp + chrome的翻墙之法，请不要害怕这过长的篇幅，设置的过程是相当的简单的，按部就班的来10分钟左右搞定。设置过程如下：

###一、简单介绍###

1. GAE（Google App Engine）是一个开发、托管网络应用程序的平台；
2. goagent是一个使用Python和Google Appengine SDK编写的代理软件；
3. switch sharp是一个chrome插件，具体功能类似于Firefox的AutoProxy.

###二、确保自己拥有一个Google账户###

**step1**: 创建Google账号，并登录[Google App Engine](https://appengine.google.com/start/createapp)按下图操作(已有账号的请跳过);

<!--more-->
![创建Google Application ID](http://g1c1i0.cooear.com/images/uploads/2013/07/1.png '创建Google Application ID')

**step2**: 创建自己的application

完成step1的验证操作后界面如下：

![创建Google Application应用](http://g1c1i0.cooear.com/images/uploads/2013/07/3.png '创建Google Application应用')

**注**：Application ID允许使用英文字母和短横线；填写完毕Application ID点击Check Available，检查是否可用

一切正常的话就会看到下面的界面（告诉你App已经申请成功了）

![Google Application应用创建成功](http://g1c1i0.cooear.com/images/uploads/2013/07/4.png 'Google Application应用创建成功')

<br/>
**注**:每个Gmail账户最多只能创建10个Google App Engine应用，每个应用每天有1GB的免费流量。如果你经常下载或者观看视频建议多创建几个Google App Engine应用

###三、下载设置goagent###

step1: 下载[goagent客户端](https://github.com/phuslu/goagent/tags)

step2: 按图中“简单教程”中的步骤一步步来。

![GoAgent简单教程](http://g1c1i0.cooear.com/images/uploads/2013/07/5.png 'GoAgent简单教程')

step3: 修改local\proxy.ini中[gae]下的appid=你的appid(多个appid请用|隔开)，即前面创建的Application所设定的Application ID;

![GoAgent的proxy.ini设置](http://g1c1i0.cooear.com/images/uploads/2013/07/6.jpg 'GoAgent的proxy.ini设置')

step4: 打开server\uploader.bat,根据提示一次输入Application ID,邮箱地址和密码（如果设置了Gmail的两步验证请输入两步验证中生成的16位密码，即为独立应用单独生成的随机16位字符，而不是你的邮箱密码，[Gmail两步验证](http://cooear.com/blog/2013/07/gu-ge-zhang-hu-liang-bu-yan-zheng-she-zhi/)在这里详细介绍）

![GoAgent配置登录](http://g1c1i0.cooear.com/images/uploads/2013/07/7.jpg 'GoAgent配置登录')

<br/>
**注**: 使用GoAgent上网前，必须运行local\goagent.exe

###四、安装chrome浏览器的SwitchySharp插件###

安装chrome浏览器的[SwitchySharp插件](https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm?hl=zh-CN)，具体过程在第三步的step2的简单教程中已经有过介绍。最新版Proxy SwitchyOmega[下载地址](https://github.com/FelisCatus/SwitchyOmega/releases/)。

###五、设置switchsharp插件###

**注意**：Proxy SwitchySharp升级为 [Proxy SwitchyOmega](http://pan.baidu.com/s/1i3rHHGT) 主要设置和Proxy SwitchySharp相似，会在Proxy SwitchySharp设置后简单介绍。

step1: 按下图填写

![chrome浏览器switchsharp设置](http://g1c1i0.cooear.com/images/uploads/2013/07/8.jpg 'chrome浏览器switchsharp设置')

step2: 导入文件

![chrome浏览器switchsharp配置文件导入](http://g1c1i0.cooear.com/images/uploads/2013/07/9.png 'chrome浏览器switchsharp配置文件导入')

step3:选择“代理”或者“自动切换模式”

![chrome浏览器switchsharp代理模式切换](http://g1c1i0.cooear.com/images/uploads/2013/07/10.jpg 'chrome浏览器switchsharp代理模式切换')

<br/>
[Proxy SwitchyOmega](http://pan.baidu.com/s/1i3rHHGT)简介	

![Proxy SwitchyOmega升级下载](http://g1c1i0.cooear.com/images/uploads/2015/03/unnamed1.png 'Proxy SwitchyOmega升级下载')

![Proxy SwitchyOmega升级下载](http://g1c1i0.cooear.com/images/uploads/2015/03/unnamed2.png 'Proxy SwitchyOmega升级下载')

![Proxy SwitchyOmega升级下载](http://g1c1i0.cooear.com/images/uploads/2015/03/unnamed3.png 'Proxy SwitchyOmega升级下载')

###六、友情提示###

Google App Engine并非毫无限制，正如上文所说每个Gmail账号只能创建10个应用程序（最多10个AppID）。对于创建过的AppID，可以手动删除（72小时后生效，期间可以反悔）,AppID一旦删除，同名账号就不能再申请。

Google App Engine提供给每个AppID每天是1GB的流量，可以[登录](https://appengine.google.com/)  点击你创建的AppID，可以查看你的流量图，以及每天免费配额还剩多少，如图：

![Google Application应该流量图](http://g1c1i0.cooear.com/images/uploads/2013/07/11.jpg 'Google Application应该流量图')

<font color=red>注: 每天的流量重新清零的时间是北京时间16点整，而非0点。</font>

至此大功告成，切接每次运行local\goagent.exe,打开chrome，你就可以畅游于互联网的任何角落

![云梯](http://g1c1i0.cooear.com/images/uploads/2013/07/Over.jpg '云梯')

**<font color=red>注意</font>**：~~如果不想操作以上设置可以直接修改本机HOSTS文件达到相同效果，点击查看~~;从个人使用情况再分享个Lantern翻墙，个人觉得Lantern的访问更稳定、速度更快。

<br />

[Lantern快速稳定翻墙教程地址](http://cooear.com/blog/2014/08/lantern-deng-long-an-zhuang-he-shi-yong-jiao-cheng/)