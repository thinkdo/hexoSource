title: java类加载器
date: 2012-03-10 15:57:52
tags:
---
java虚拟机就是用“类加载器”来加载一个类的，所有的java类都需要“类加载器”来加载。
所谓加载就是指jvm将编译生成的class文件按照一定的规则放入到内存并构造Class对象。 

一、Java虚拟机默认有三个类加载器： 
1、Bootstrap（根类加载器）：用c++实现的。它所有类加载器的最终父类加载器，它没有父类加载器，它负责加载虚拟机的核心类库（jre/lib/rt.jar），如java.lang.Object。 

2、ExtClassLoader（扩展类加载器）：用java语言实现的。是Launcher类的内部类。它是由Bootstrap加载的，但BootStrap不是java编写的，所以ExtClassLoader类的父类加载器是null。用于加载java运行环境扩展包中的类(jre/lib/ext/*.jar)。继承了ClassLoader类。 

3、AppClassLoader（应用类加载器）：用java语言实现的。是Launcher类的内部类。它是由Bootstrap加载的，父类加载器是ExtClassLoader。如果系统中没有指定类加载器或自定义类加载器，那么我们自己编写的所有的java类都是由该类加载器来加载(所有.classpath文件中指定的jar包和目录)。它是用户自定义的类加载器的父类加载器。继承了ClassLoader类。 
可通过ClassLoader.getSystemClassLoader()来调用。 

二、加载器的加载逻辑是，加载器首先委托其父加载器去加载需要加载的类，若父加载器能够顺利加载此类，则加载工作全部交给父加载器完成，否则将由加载器自身去完成加载工作。当自身也无法加载类时，则会抛出ClassNotFoundException。 

三、当需要编写自己的类加载器时： 
1、必须继承ClassLoader。 
2、重写loadClass方法与findClass方法。loadClass中先调用父类的loadClass，然后调用findClass，通常情况下只覆盖findClass就可以。 
3、重写defineClass方法。 

四、自定义加载器的用途： 
自定义的类加载器通常用于解密自己写的已加密的class字节码，否则即使别人拥有该class文件也无法被系统的类加载器正常加载。