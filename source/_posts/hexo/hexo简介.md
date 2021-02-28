---
title: 第1周 计算
date: 2020/04/12 20:46:25
categories:
- [博客,hexo简介]
tags:
---


# 用hexo搭建一个静态站点

### 1.下载必须文件

A.[nodejs](https://nodejs.org/en/)
B.[git](http://git-scm.com/)
C.hexo

```bash
$ npm install -g hexo-cli
```

### 2.创建一个文件夹并在此文件夹中打开终端初始化hexo创建网页

第一步：

```bash
$ hexo init			#初始化文件夹
```

第二步：

```bash
$ hexo g      	#编译文件
$ hexo s				#本地部署
$ hexo d				#部署网页
$ hexo server		#本地部署但不生成文件可修改看变化
$ hexo clean		#清除垃圾文件
```

### 3.部署

A.部署到服务器

```bash
yum install gcc -y							  #先安装好 Nginx安装环境
yum install pcre pcre-devel -y
yum install zlib zlib-devel -y  
```

```bash
wget http://nginx.org/download/nginx-1.16.0.tar.gz      #下载
tar zxvf nginx-1.16.0.tar.gz
cd nginx-1.16.0./configure --prefix=/usr/local/nginx 

```

```bash
./configure --prefix=/usr/local/nginx #编译
```

```bash
make && make install  #安装   
```

```bash
cd /usr/local/nginx/sbin/./nginx B.  #启动 nginx
```

```bash
npm install hexo-deployer-sftp --save  #首先得在 hexo 目录下安装 sftp 插件
```

```yaml
deploy:
  type: "sftp"
  host: "192.168.0.100"
  user: "root"
  pass: "123456"
  remotePath: "/usr/local/nginx/html"
  port: 22 		
  ###然后在 _config.yml 中配置 deploy
```

B.部署到[GitHub](www.github.com)

```bash
npm install hexo-deployer-git --save  #先添加 git 插件
```

```yaml
deploy:
  type: "git"
  repo: "https://github.com/ITAbyss/itabyss.github.io.git"
  branch: "master"
```

