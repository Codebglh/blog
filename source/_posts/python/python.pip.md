---
title: pip下载更改数据源
date: 2021/03/03 08:58:25
categories:
- [爬虫]
tags:
---





# Mac 修改pip 镜像源

1. 进入根目录：`cd ~/`
2. 进入.pip目录 `cd .pip`
3. 如果不存在文件夹就新建`mkdir .pip`
4. 进入 `cd .pip`
5. 创建pip.conf文件 `touch pip.conf`
6. 修改：`vim pip.conf`

## 暂时

```cpp
pip install*** -i https://pypi.douban.com/simple
```

## 永久修改内容：

```csharp
[global]
index-url=https://mirrors.aliyun.com/pypi/simple/
[install]
trusted-host=mirrors.aliyun.com
```



```csharp
[global]
timeout = 6000
index-url = https://pypi.douban.com/simple/ 
[install]
use-mirrors = true
mirrors = https://pypi.douban.com/simple/ 
trusted-host = pypi.douban.com
```

# 国内源：

- [http://pypi.douban.com/](https://link.jianshu.com/?t=http://pypi.douban.com/) 豆瓣
- [http://pypi.hustunique.com/](https://link.jianshu.com/?t=http://pypi.hustunique.com/) 华中理工大学
- [http://pypi.sdutlinux.org/](https://link.jianshu.com/?t=http://pypi.sdutlinux.org/) 山东理工大学
- [http://pypi.mirrors.ustc.edu.cn/](https://link.jianshu.com/?t=http://pypi.mirrors.ustc.edu.cn/) 中国科学技术大学

列出当前安装的包：

```python
pip3 list
```

列出可升级的包：

```python
pip3 list --outdate
```

升级一个包：

```python
pip3 install --upgrade requests  // mac,linux,unix 在命令前加 sudo -H
```

升级所有可升级的包：

```python
$ pip3 freeze --local | grep -v '^-e' | cut -d = -f 1  | xargs -n1 pip3 install -U
```

```python
pip3 list -o --format legacy|awk '{print $1}'` ; do pip install --upgrade $i; done
```