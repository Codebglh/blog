---
title: 数据库管理
date: 2021/03/03 08:53:25
categories:
- [爬虫]
tags:
---



# [Mac 上的 MySQL 管理工具 -- Sequel Pro](https://segmentfault.com/a/1190000006255923)

Sequel Pro 是 Mac 用户常用的 MySQL 管理软件，属于开源项目 CocoaMySQL 的一个分支。它支持包括索引在内的所有表管理功能，支持MySQL视图，可以同时使用多个窗口来操作多个数据库/表。完全可以媲美大家熟悉的 phpMyadmin。

Sequel Pro 的部分特性如下：

1. 操作快速，简单。通过简单的几个参数设定即可连接本地或远程MySQL。
2. 支持多窗口操作。在不同的个窗口中，对多数据库实施操作。
3. SQL语句的语法彩色、加亮显示。
4. SQL语句的关键字、表名、字段名的自动完成。
5. 支持30多种不同的字符编码。
6. 快速导入/恢复、导出/备份SQL及CSV格式的数据。
7. 兼容MySQL3、4、5。
8. 支持在MAMP/XAMP架构上连接数据库，支持SSH连接模式；
9. 免费使用，当然，如果你觉得不错，可以 Donate 支持一下作者。

## 通过 root 连接数据库

新建数据库和用户需要用到数据库的 root 用户权限，所以，我们用 root 进行登录，如下图：

![clipboard.png](https://segmentfault.com/img/bVApCt)

## 建立数据库

点击 `Choose Database`-> `Add Database`创建数据库

![clipboard.png](https://segmentfault.com/img/bVApBQ)

字符集选择默认的 `utf-8` 即可。

![clipboard.png](https://segmentfault.com/img/bVApBR)

## 建立数据库用户

点击右上角`User`，弹出下面用户操作对话框，建立 web 用户

![clipboard.png](https://segmentfault.com/img/bVApBU)

给刚才新建的 `laravel` 数据库赋予权限，此处权限全选了，大家也可以有目的的选择权限：
![clipboard.png](https://segmentfault.com/img/bVApBV)

## 用新建 web 用户连接 laravel 数据库

首先，退出用 root 登陆的 sequel pro，再重新打开。

![clipboard.png](https://segmentfault.com/img/bVApB1)

1. 如果非新建数据库界面，可以点击`1`添加收藏夹，下次可以直接点击该处进行连接；
2. 默认数据库连接方式为`Standard`标准模式，大家也可以选用`Socket`或`SSH`方式。选好方式，按照提示输入服务器、用户名、密码和数据库名，若端口有修改，输入端口号；
3. 点`3` `Add to Favorites` 则在`4` 处会新增一个数据库连接收藏，点`Save changes` 则保存到当前收藏；
4. 点击`5` `Connect`连接数据库。

## 增加、编辑、删除数据表

这部分和 phpMyadmin 等都类似，就不展开来介绍了，大概功能区如下图：

![clipboard.png](https://segmentfault.com/img/bVApB8)

## 删除数据库

貌似没有图形化删除数据库的地方，不过可以在`Query`选项下，执行

```
drop database dbname
```

进行删除，下面以删除 laravel 数据库为例，执行后，状态栏显示无错误，右上角数据库状态回到 `choose database`。点开就会看到已找不到 laravel 数据库。

![clipboard.png](https://segmentfault.com/img/bVApBP)

## 用 laravel 的 artisan 工具建立和更新数据表

### laravel 连接配置

找到项目 `.env` 文件，修改下面几个参数

![clipboard.png](https://segmentfault.com/img/bVApCj)

### migrate 文件编辑

找到 database/migrations 目录，查看或编辑目录下的 migrate 文件

![clipboard.png](https://segmentfault.com/img/bVApCk)

一般内容如下所示，调整为你需要的内容即可：

![clipboard.png](https://segmentfault.com/img/bVApCm)

### 命令行执行 migrate 操作

命令行模式进入项目根目录，执行下面命令，则数据库就会按照几个 migrate 文件要求，执行数据库操作。

```
php artisan migrate
```

### 数据库查看 migrate 命令执行结果

我们用 sequel pro 连接数据库，可以看到操作后如下：

![clipboard.png](https://segmentfault.com/img/bVApCo)

可见数据库和用户建立成功，项目已能正常连接数据库。

## 答用户问

### 如何调整主键

点到 Query 选项卡

#### 1. 如果原先没有主键，且需要增加的字段为 not null，可以执行下列命令

```
ALTER TABLE `users` ADD PRIMARY KEY ( `name` )
```

#### 2. 如果原先主键已存在，目的是改变主键，则执行如下步骤

- 如果原主键有外键依赖，要先删除外键依赖；

```
alter table `FK_Table` drop foreign key FK_Name;（FK_Table 为有外键关系的表，FK_Name 为外键约束名）
```

- 如果原主键为自动递增，要先去掉自动递增：

```
alter table `users` modify `id` int(10) unsigned NOT NULL;（根据实际字段属性来）
```

- 再删除主键

```
alter table `users` drop primary key;
```

- 然后再增加主键

```
alter table `users` add primary key(`name`);
```

[mysql](https://segmentfault.com/t/mysql)