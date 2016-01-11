title: linux常用命令
date: 2011-09-11 17:20:30
tags:
---
**ps -ef|grep tomcat**
查看与关键字“tomcat”相关的进程信息
**tail -f test.log**
查看test.log文件，并实时加载该日志最新的写入信息
**kill -3 pid**
输出一次Thread Dump，结束进程  
**kill -9 pid**
3秒之后强制kill 进程  
**kill 0**
结束所有的进程
**kill -9 $(ps -ef|grep test)**
将“ps -ef|grep test”命令查出来的所有进程都强制终止，
**kill -u test**
发出命令终止“test用户下的进程”
**find . -name "my*" **
搜索当前目录下，名字以my开头的文件
**unzip -o test.jar**
在当前目录下解压test.jar并覆盖重名文件
**unzip test.jar -d /test/floder**
将test.jar解压到指定目录/test/floder下
**zip test.zip testfloder1 testfloder2**
压缩当前文件夹下的两个文件夹testfloder1和testfloder2，命名为test.zip
**tar -xvf test.jar**
将test.jar解压到当前目录下
-c ：压缩
-x ：解压
-t ：查看内容
-z ：用gzip压缩
-j ：用bzip2压缩
-v ：显示压缩或解压过程
-f ：文档名。该参数位置为参数中的最后一个
-p ：保留原文件的原来属性
-P ：可以使用绝对路径来压缩！
-N ：比后面接的日期(yyyy/mm/dd)还要新的才会被打包进新建的文件中！





 
