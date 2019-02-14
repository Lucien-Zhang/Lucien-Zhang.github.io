---
title: HEXO源文件部署到Github Pages后本地如何部署、修改
date: 2019-01-17 13:47:34
tags: 
 - Github Pages
 - Hexo
category: Technology
---

# 将HEXO的源文件部署到Github Pages后，如果在新电脑上想要编写博客
<!--more-->
## 部署基本编写环境

1. 安装Git和Node.js
2. 添加电脑和Github账户的SSH Key
3. 克隆仓库分支到本地
```
git clone git@github.com:username/username.github.io.git
```

4. 用cd命令进入分支的根目录，安装hexo
```
$ cd username.github.io

$npm install -g hexo-cli
```

5. 安装依赖(依赖项目根据目录下的packge.json安装)
```
npm install
```

## 部署文章、修改主题之后的提交代码

```
按照顺序

git add .
git commit -m 'back up hexo files'（引号内容可改）
git push
```
此时存放源文件的Hexo分支已经更新。

再输入
```
hexo d -g 
```
渲染静态页面并推送到Master分支