﻿title: 总结一点高性能架构的知识
date: 2015-04-16 15:46:33
tags:
---
#### 一、数据库访问性能优化
+ 对数据库表进行水平分割：按照某些条件将数据进行分类，放置在不同表中。如按年分表、按地区分表等
+ 对数据库表进行垂直分割：将常用字段和不常用字段分两个表存储
+ 对数据库表进行分区
+ 采用有负载能力的集群
+ 适当使用簇表（[散列聚簇表](http://www.cnblogs.com/feiyun126/archive/2013/06/28/3161127.html)，索引聚簇表）、Hit提示
+ 升级硬件（CPU、内存、高速磁盘、固态硬盘）

#### 二、高负载高并发网站性能优化
+ 高性能服务器（硬件）
+ 高性能数据库
+ 高效编程语言
+ 高性能web容器
+ HTML静态化：对于新闻、博客、论坛类网站，需要长期保存某些久不更新的网页，这种时候就可以将网页静态化，或者半静态化，即定期动态生成静态化网页并保存静态页面至缓存中，让静态页面分担一部分访问压力。推荐nginx服务器，因其占用系统资源小，可用来处理静态文件的大量请求。
+ 图片服务器分离：图片单独放置在图片服务器上。推荐lighttpd，因其轻量级且处理并发高效。
+ 数据库集群：如Mysql的master-slave
+ 缓存：Apache的mod_proxy或squid；memcached
+ 镜像
+ 负载均衡


