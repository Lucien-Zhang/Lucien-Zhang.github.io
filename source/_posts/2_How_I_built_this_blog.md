---
title: 我是如何搭建个人博客的
date: 2017-06-09 15:24:40
category: 
 - Technology
toc: true
tags: 
 - Hexo
 - 教程
---
搭建blog的久来有之，未曾系统学习编程而今能实现，实属不易  

<!--more-->

**搭建博客使用到的一切如下：**

> 1. [Hexo][1]
> 2. [Github][6]的[Github Pages][2]
> 3. 代理软件,我使用的是[Shadowsocks][3]（以下简称为SS）
> 4. 一台能上网的电脑（推荐使用[Chrome浏览器][7]，翻墙的话最好SS配合SwitchyOmege插件实现）

## 什么是Hexo##
关于其简介，引用官方文档：
> Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown][4]（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

其官方文档有详细的安装及使用方法，具体请跳[Hexo文档简体中文版][5]
## 什么是Github和Github Pages##
什么是Github，引用百度百科的说法：
> GitHub 是一个面向开源及私有软件项目的托管平台，因为只支持 Git 作为唯一的版本库格式进行托管，故名 GitHub。

而Github，其官方文档为：
> GitHub Pages is designed to host your personal, organization, or project pages directly from a GitHub repository. 
> 
>You can create and publish GitHub Pages online using the Jekyll Theme Chooser. If you prefer to work locally, you can use GitHub Desktop or the command line.
GitHub Pages is a static site hosting service and doesn't support server-side code such as, PHP, Ruby, or Python.

我简陋翻译一下：Github是一种**静态站点托管服务**，可以在Github仓库里托管你的个人、组织或者项目页面。可以使用Jekyll之类的静态框架，但**不支持PHP、Ruby或者Python等服务端代码**

## 什么是Shadowsocks##
Wiki上是这样描述的：
> Shadowsocks是使用Python、C++、C#以及Go等语言开发、基于Apache许可证的开放源代码软件，用于保护网络流量、加密数据传输以及突破中国网络审查。

要使用Shadowscoks突破GFW，除了该有的软件和客户端外，还必须要有一台国外的服务器作为服务端，这台国外的服务器是用来中转数据的，有点类似于直接考公务员和走关系当公务员这样，服务端充当的就是这个中间人。
 
### **为什么一定要实现翻墙** ###
虽然Github、Hexo、可以不翻墙访问，但是访问速度很慢，特别是对某些地区的不同运营商不够友好，所以借助代理软件，可以更快地访问网站。当然啦，翻墙的作用远不止这些，这里不多提及。

## 搭建步骤 ##
### 一、安装Hexo ###
*必要时，请参考[Hexo文档][5]*
 (1). 安装Hexo有两个必须安装的东西：[Node.js][9]和[Git][8]   **(*Windows用户点击超链接跳转至下载界面，安装过程直接点击下一步即可，无法下载或者其他用户请参考文档* ）**  
 
 (2). 安装完后打开Git(马赛克的是我的用户名)
 
 ![Git界面][P2]
 
 输入以下命令安装Hexo： 
 

    $ npm install -g hexo-cli

 **安装完成后会再次出现这个绿红黄，才可以继续键入命令**
 
### 二、安装[Shadowscoks][3]（*无法翻墙的人从百度下载*，**解压即可用**）###
翻墙可以更快地访问Hexo、Github等网站
### 三、申请Github账号###
申请Github账号是因为这个网站有免费的静态页面托管项目可以用
 
 1). 打开[Github][6]主页，选择Sign up（注册账号）
 
![Github主页][P1]
![Github新建账户][P3]
 
**注意** ：
 **①. 申请的账号名将会是你的域名，所以要认真考虑。**
 **②. 注册Github账号的时候会要求验证邮箱，请验证，否则最后的域名可能显示404**
   
2). 登陆后在右上角“＋”图标右边有个向下的箭头，点击，选择`New repository`
 
![Github新建仓库][P4]
 
![建仓的时候的样子][P5]  

**注意**：`Respository name`那栏必须以前面的`Owner`一致，比如`Owner`是`uesrname`,那么`Respository name`就应该写作`uesrname.github.io`，请留意你的username，下面还会用到。  
 
我以ABC为例子建完仓库后，Github页面的样子，也是最开始没有上传代码的样子。
 
![建完仓库的样子][P6]
 
至此，Hexo的初步安装，Github账户以及仓库就弄好了，不过这才是刚开始
 
------
 
## 配置##
### 一、关联SSH###
 
 **关联SSH是为了把代码部署到Github上**
 
 1). 打开先前安装好的Git：在桌面鼠标右键，有"Git Bash here"的选项，点击即可。
 
![Git客户端界面][P2]

 2). 设置emai和github注册邮箱

    $ git config --global user.name "你的GitHub用户名"

    $ git config --global user.email "你的GitHub注册邮箱"
    
**注意**：需要等绿红黄的字母出现，才可以继续输入下一个命令

3). 生成ssh密钥:输入下面命令

    $ ssh-keygen -t rsa -c "生成SSH密匙"

一般情况下是不需要密码的，所以，接下来直接回车就好。  

此时，在系统盘用户文件夹下就会有一个新的文件夹.ssh（例如我的是C:\Users\Lucien\.ssh），里面有刚刚创建的ssh密钥文件id_rsa和id_rsa.pub。  

**注：id_rsa文件是私钥，要妥善保管，id_rsa.pub是公钥文件。**

4). 添加公钥到github：
 
点击Github用户头像，然后点击显示的Settings(设置)选项；
 
![Github setting图][P7]
  
在用户设置栏，点击SSH and GPG keys选项，然后点击New SSH key(新建SSH)按钮；  
  
![SSH and GPG keys][P9]
 
用笔记本打开id_rsa.pub，并将其中的内容复制到Key文本框中，然后点击Add SSH key(添加SSH)按钮  

弄完后，就可以来测试下SSH起作用没有了  
 
在Git里输入命令  

    $ ssh -T git@github.com
    
接下来会出来下面的确认信息：

    The authenticity of host 'github.com (207.97.227.239)' can't be established. 
    RSA key fingerprint is 17:24:ac:a5:76:28:24:36:62:1b:36:4d:eb:df:a6:45.
    Are you sure you want to continue connecting (yes/no)?
    
输入yes后回车。  
 
如果显示的显示如下信息，那么SSH就配置好了。  

    Hi username! You've successfully authenticated, 
    but GitHub does not provide shell access.

上面的都是前期工作，到这里就可以开始创建博客了

---
## 创建博客页面##
（关掉刚刚Git窗口），在任意你想放博客文件的地方右键`Git brush here`，因为接下来会生成一系列文件在这个文件夹里

在Git里输入命令如下：

    $ hexo init  //初始化Hexo（命令后面的斜杠是注释，不用打进去）
    $ npm install  //安装依赖包

完成之后再输入：

    $ hexo generate  //生成静态页面
    $ hexo server  //启动本地服务器
    
启动本地服务器后，打开浏览器，输入`localhost:4000`就能查看网页了，如果要关掉服务器，在Git里用Ctrl + C  
 
本地服务器可以让你调试页面，不用每次修改都上传到网络服务器才能查看，很方便。  
 
**虽然好不容易已经做到了这一步，但是生成的页面还是Hexo默认的页面，我们需要定制我们想要的页面不是？**
 

## 个性化博客##
放心，hexo上有很多开源主题，[戳这里][10]看好哪个选哪个，点进去之后，会跳转到主题github页面，往下拉，会看到这个：（这是我在Hexo上随便找的一个主题）
 
![hexo主题][P10]
 
复制这个地址，粘贴到Git里，就会开始自动下载了  
  
 下载完之后主题会出现在博客目录下的`themes`，这个时候在blog目录下的`_config.yml`把主题换为刚下载好的这个主题，然后upgrade，再部署一下就可以啦。（每个hexo主题都有安装教程，有些有中文教程，可以找找哩，[比如这篇][11]）  
  
  ---
  
 以上这篇教程不算面面俱到，而且也是参考网上其他教程和自己亲身经历写出来的，如果有什么错误还请各位指正。
 
 ---
 
 参考文章：
 > [在Github上面搭建Hexo博客（一）：部署到Github - by cherishzy][12]
 > [搭建hexo博客并部署到github上 - by xiaomiya][13]
 > [hexo教程系列——hexo安装教程 -  by 张学志の博客][14]
 > [手把手教从零开始在GitHub上使用Hexo搭建博客教程(一)-附GitHub注册及配置][15]
 > [手把手教从零开始在GitHub上使用Hexo搭建博客教程(二)-Hexo参数设置][16]
 > [手把手教从零开始在GitHub上使用Hexo搭建博客教程(三)-使用Travis自动部署Hexo(1)][17]
 > [5分钟 搭建免费个人博客][18]
 > [静态博客框架之Hexo & Jekyll][19]
 > [hexo 部署至Git遇到的坑][20]
 
 很感谢以上文章的作者，也很感谢开源的hexo、主题制作者、还有Github，啊，圆了一桩梦。


****
Change Log:
2017-06-09 完成文章
2018-02-25 增添细节
 
  [1]: https://hexo.io/zh-cn/
  [2]: https://pages.github.com/
  [3]: http://shadowsocks.org/en/index.html
  [4]: http://www.appinn.com/markdown/
  [5]: https://hexo.io/zh-cn/docs/
  [6]: https://github.com/
  [7]: http://www.google.cn/chrome/browser/desktop/index.html
  [8]: https://git-scm.com/download/win
  [9]: https://nodejs.org/en/
  [10]: https://hexo.io/themes/
  [11]: https://github.com/henryhuang/hexo-theme-aloha/wiki/zh_CN
  [12]: http://www.cnblogs.com/cherishzy/p/5694658.html
  [13]: http://xiaomiya.iteye.com/blog/2106972?utm_source=tuicool&utm_medium=referral
  [14]: http://blog.csdn.net/xuezhisdc/article/details/53130328
  [15]: http://www.jianshu.com/p/f4cc5866946b#
  [16]: http://www.jianshu.com/p/dd9ef08b12df
  [17]: http://www.jianshu.com/p/7f05b452fd3a
  [18]: http://www.jianshu.com/p/4eaddcbe4d12
  [19]: http://www.jianshu.com/p/ce1619874d34
  [20]: https://www.jianshu.com/p/67c57c70f275

  [P1]: 
  [P2]: \images\post\Giti_nterface.png
  [P3]: http://oqebkkb7i.bkt.clouddn.com/Github%E6%96%B0%E5%BB%BA%E8%B4%A6%E6%88%B7.png
  [P4]: http://oqebkkb7i.bkt.clouddn.com/%E6%96%B0%E5%BB%BA%E4%BB%93%E5%BA%93.jpg
  [P5]: http://oqebkkb7i.bkt.clouddn.com/%E5%BB%BA%E4%BB%93%E7%9A%84%E6%97%B6%E5%80%99%E7%9A%84%E6%A0%B7%E5%AD%90.png
  [P6]: http://oqebkkb7i.bkt.clouddn.com/%E5%BB%BA%E5%AE%8C%E4%BB%93%E5%BA%93%E5%90%8E%E7%9A%84%E6%A0%B7%E5%AD%90.png
  [P7]: http://oqebkkb7i.bkt.clouddn.com/%E8%AE%BE%E7%BD%AE.png
  [P8]: http://oqebkkb7i.bkt.clouddn.com/%E9%80%89%E6%8B%A9SSH.png
  [P9]: http://oqebkkb7i.bkt.clouddn.com/%E9%85%8D%E7%BD%AESSH.png
  [P10]: http://oqebkkb7i.bkt.clouddn.com/%E4%B8%BB%E9%A2%98.png