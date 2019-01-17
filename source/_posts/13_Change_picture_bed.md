---
title: 备份七牛云图床，回归本地图片部署
date: 2018-11-20 17:38:26
tags:
- 教程
- Blog
- 七牛云图床
- qshell
category: Technology
---

八月份七牛云发邮件说要取消测试域名，那时并不在意，直到最近发现博客上的图片全部挂了，才想起来测试域名被取消，于是有了这一篇备份七牛云图床内容的文章，算是在找了网络上那么多坑之后做的总结。
<!--more-->

# 新建一个相同地区的对象储存空间
因为老的储存空间的测试域名已经被收回，无法通过公开链接或者官方命令行工具qshell下载，所以新建一个储存空间是为了获得新的测试域名，域名有效期30天

# 下载官方命令行工具

我的环境是WIN10 x64 bit，所以我下载了WIN版，往下的步骤都是在WIN10 下操作
[命令行工具（qshell）工具链接在此](https://developer.qiniu.com/kodo/tools/1302/qshell)

# 添加环境变量
目的是为了使qshell在目录下可以直接使用，因为我把qshell放在桌面，所以我直接在path里添加了桌面的目录
![13](\images\post\13.png)

# 将qshell改名
由`qshell_windows_x64.exe`改为`qshell.exe`，方面之后输入命令行方便

# 使用CMD工具链接七牛云帐户
**从这一步开始所有动作都在WIN 的CMD命令工具里执行**
不懂的可以看account命令官方文档](https://github.com/qiniu/qshell/blob/master/docs/account.md)

1. 右击开始菜单图标 - 运行，输入`CMD`，弹出命令行窗口
2. 输入`qshell account <Your AccessKey> <Your SecretKey> <Your Account Name>`。（`AccessKey`和`SecretKey`在七牛云个人中心 - 密匙管理 中有，`Account Name`是登录邮箱，输入的时候`<` `>`符号要去掉）

# 用listbucket命令生成空间内容列表文件
获取老储存空间的内容列表[不懂或进阶要求可以看listbucket命令官方文档](https://github.com/qiniu/qshell/blob/master/docs/listbucket.md)

1. 输入`qshell listbucket <老的储存空间名称> -o D:\cp.txt`

这里的`D:\cp.txt`是列表文件输出位置，可以自己定义。命令运行完以后，这个目录下就有`cp.txt`文件了

打开`cp.txt`文件，里面的内容应该是
```
hello.jpg   1710619   FlUqUK7zqbqm3NPwzq2q7TMZ-Ijs   14209629320769140   image/jpeg   1`
```
删除除了`hello.jpg`以外的东西,另存为`changedcp.txt`
>
在这里可以用awk命令，但是因为我没有安装，所以是手动删除的。删除错，留有空格，都会导致该内容无法正确转移
在此奉上awk命令。在WIN上使用awk命令需要安装环境，在此不详细介绍。
```
awk '{print $1}' cp.txt > changedcp.txt
```

# 使用batchcopy命令复制老储存空间到心储存空间
[不懂的或者进阶要求请看batchcopy命令官方文档](https://github.com/qiniu/qshell/blob/master/docs/batchcopy.md)，这个步骤可以用batchmove命令代替，batchmove命令是将老储存空间的内容转移到新储存空间

1. 输入`qshell batchcopy <老储存空间> <新储存空间> -i D:\changedcp.txt`
2. 输入验证码

**记住：命令行里的`<` `>`符号要去掉

命令行跑完以后就OK了。如果有复制错误，在命令行里会有体现

这个时候，在网页上查看新的储存空间，应该就能看到内容了。

# 使用qdownload命令下载储存空间内容到本地
[不懂的或者进阶要求请看batchcopy命令官方文档](https://github.com/qiniu/qshell/blob/master/docs/qdownload.md)

## 设置下载配置文件
在随意目录新建一个txt文件，名字随意。我在D盘根目录下新建一个`down.conf`文件，完整地址为`D:\down.conf`

用记事本打开，
添加内容如下
```
{
    "dest_dir"   :   "<LocalBackupDir>",         //数据下载路径，为全路径
    "bucket"     :   "<Bucket>",                 //下载内容的空间名称
    "prefix"     :   "image/",                   //同步指定前缀的文件，默认为空
    "suffixes"   :   ".png,.jpg",                //同步指定后缀的文件，默认为空
    "cdn_domain" :   "down.example.com",         //设置下载的CDN域名
    "referer"    :   "http://www.example.com",   //
    "log_file"   :   "download.log",
    "log_level"  :   "info",
    "log_rotate" :   1,
    "log_stdout" :   false
}
```
我的设置如下：
```
{
    "dest_dir"   :   "D:\\SDDD",      //注意，路径里的\一定要有两个，否则会出错
    "bucket"     :   "silenttwice",   //新储存空间名称
    "prefix"     :   "",          //留空
    "suffixes"   :   "",          //留空
    "cdn_domain" :   "pidnuhcam.bkt.clouddn.com", //新建储存空间的测试域名
    "referer"    :   "http://www.example.com",      //不变 
    "log_file"   :   "download.log",      //不变
    "log_level"  :   "info",     //不变
    "log_rotate" :   1,          //不变
    "log_stdout" :   false       //不变
}
```
**注意，路径里的\一定要有两个，否则会出错**
如果是`C:\Users\SHJOI\Desktop\SDDD`就应该改成`C:\\Users\\SHJOI\\Desktop\\SDDD`

`cdn_domain`为新建储存空间的测试域名

因为我要把所有内容都转移过来，所以没有指定同步的前缀和后缀

配置文件到这里就设置好了。

## 运行qdownload命令
[不懂的或者进阶要求请看batchcopy命令官方文档](https://github.com/qiniu/qshell/blob/master/docs/qdownload.md)
输入`qshell qdownload -c 10 D:\down.conf`

`D:\down.conf`为配置文件完整地址
`-c 10`为下载线程数，不输入的话默认为5

到这里全部东西就都下载好，可以和七牛云说拜拜了，我又回到了本地部署图片的日子，虽然部署和推送的时候会比较慢，但也还能接受啦，找个时间把图片压缩一下嘿嘿嘿。