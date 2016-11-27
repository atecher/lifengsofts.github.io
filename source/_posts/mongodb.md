---
title: MongoDB
date: 2016-11-27 00:30:38
categories: MongoDB
tags: 
    - MongoDB
---

# 为什么学mongodb

开源，免费，社区技术支持到位

## 优势

### 无标结构限制

1. 没有任何表结构，每条记录的结构可以完全不同
2. 业务开发方便
3. SQL数据库需要事先定义表结构在使用

### 完成的索引支持

redis只有key-value，hbase的二级索引还需要自己实现

1. 单键索引，多键索引
2. 数组索引
3. 全文索引
4. 地理位置索引

### 方便的冗余和扩展

1. 复制集保证数据安全
2. 分片扩展数据规模

### 良好的支持

1. 完善的文档
2. 齐全的驱动支持

## 相关工具

MongoDB：64Linux

MongoDB版本：2.6.5

ssh：xshell

文本编辑器：vim,sublime

# 常用学习网站

官网：https://www.mongodb.com/

github

jira:https://jira.mongodb.org/secure/Dashboard.jspa

https://groups.google.com/forum/#!forum/mongodb-user

mongodb中文社区：http://www.mongoing.com/

mongodb中文文档：http://docs.mongoing.com/manual-zh/

# 数据库概念

有组织的存放数据

按照不同的需求进行查询

# 数据库分类

SQL数据库：Oracle,Mysql

NoSQl数据库(Not Only SQL)：Redis,MongoDB



| SQL数据库 | NoSQL数据库   |
| ------ | ---------- |
| 实时移植性  | 有延迟        |
| 实务     | 默认不支持      |
| 多表联合查询 | 没有，提供更好的性能 |

# 安装Mongodb

## mac

```shell
brew update
brew install mongodb
```

# 常用命令

mongod：数据库执行程序

mongo：连接mongo数据库的客户端

mongoimport,mongoexport:数据库的导入导出

mongodump，mongorestore:也是导入导出，只是导出的是二进制文件，一般用来做数据的备份和恢复

mongooplog:日志

mongostat:用于查看数据库的状态

# 搭建一个简单的数据库服务器

1. 创建一个目录，用来存放数据库相关的文件
2. 创建data，用来存放数据库文件
3. 创建log，用来存放数据库日志文件
4. 创建bin，存放数据库可执行文件
5. 创建conf，存放数据库配置文件



## 创建配置文件

mongod.conf

```shell
port=12345
dbpath=data
logpath=log/mongod.log
fork=true
```

## 启动数据库服务器

```shell
mongod -f conf/mongod.conf 
```

如果看到如下信息表示服务区已成功开启

```shell
about to fork child process, waiting until server is ready for connections.
forked process: 23963
child process started successfully, parent exiting
```

启动成功后可以在data目录查看到一些文件，并且日志文件也已经生成了

```shell
tail log/mongod.log 
```

# 连接mongo

## 使用mongo命令

```shell
mongo 127.0.0.1:12345/test
```

数据库地址：127.0.0.1

端口：12345

数据库名：test

# 关闭mongo服务

直接kill相应的进程，15，或不带参数，不能使用9

```shell
use admin
db.shutdownServer()
```

# 基本使用

show dbs：查看数据库

use 数据库名：选择数据库，切换前不需要数据库一定存在

db.dropDatabase():删除数据库

show collections：显示集合，相当于一张表

## 增删改查

```shell
db.test_collection.insert({x:'1'})

//可以自定指定id,但不能重复，重复将报错
db.test_collection.insert({x:'1',_id:1})

//默认返回所有
db.test_collection.find()

//指定条件
db.test_collection.find({x:'1'})

//通过for循环，插入多条数据
for(i=3;i<100;i++)db.test_collection.insert({x:i})

//统计数据条数
db.test_collection.find().count()

//跳过3条，限制返回2条，按照x升排序
db.test_collection.find().skip(3).limit(2).sort({x:1})

//将x=1的第一条数据更新为x=888,如果这条数据原来还有自定，就会覆盖为只有x字段
db.test_collection.update({x:'1'},{x:'888'})

//更新指定字段,只更新z字段，其他的字段不变
db.test_collection.update({y:100},{$set:{z:10}})
```























