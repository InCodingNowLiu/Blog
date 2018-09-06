title: mongodb 详解
author: incodingnowliu
date: 2018-08-19 14:48:22
tags:
---
# mongodb 介绍

1.mongodb 是一个开放的文件数据库, 提供了高性能, 高可用性, 以及自动缩放

## 文件数据库
一条记录在mongodb是一个文件, 一条数据的结构依赖于键值对. mongodb 文档跟json对象很类似, 字段的值可能包含其他文档, 数组, 文档数组.

使用文档的好处