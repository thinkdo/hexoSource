title: MySql Engine
date: 2015-09-01 13:19:31
tags:
---
###什么是存储引擎
Mysql使用不同的技术存储数据，这些不同的技术被称为存储引擎，查看自己的mysql服务器可用的引擎命令：***show engines***
![show Engines查询结果](../../../../images/mysqlengine.png)
其中，InnoDB和MyISAM为常用的两种存储引擎。
###设置存储引擎的方式如下：
1、mysql的配置文件中设置默认存储引擎
2、启动mysql服务器时在命令行后边加上--default-storage -engine或--default-table-type
3、创建表时指定：在create table 后边加上engine=InnoDB
4、更改表的存储引擎：ALTER TABLE mytable ENGINE = MyISAM
###存储引擎的区别
1、核心功能