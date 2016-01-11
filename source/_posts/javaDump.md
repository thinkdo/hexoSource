title: javaDump
date: 2015-09-17 15:22:21
tags:
---
###自动抓取heapDump日志
1、打开tomcat\bin\catalina.sh文件
2、找到JAVA_OPTS(如果没有找到，则找到“Execute The Requested Command”，在其下一行加入JAVA_OPTS)
3、设置JAVA_OPTS="$JAVA_OPTS -server -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath={目录}"      
4、参数说明  
   -XX:+HeapDumpOnOutOfMemoryError参数表示当JVM发生OutOfMemory时，会自动生成DUMP文件。  -XX:HeapDumpPath={目录}参数表示生成DUMP文件的路径，也可以指定文件名称，例如：-XX:HeapDumpPath=/tomcat/dump/java_heapDump.hprof。如果不指定文件名，默认为：java_<pid>_<date>_<time>_heapDump.hprof。
   