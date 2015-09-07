title: 两种XML转JavaBean的方式
date: 2015-06-14 18:25:18
tags:
---
系统间的数据交互很多都是通过xml格式传输的，如果对方系统不提供解析报文的jar包，开发人员就需要自己解析xml。手动编写解析类不仅占用开发时间，而且容易出现数据校验不准确、解析代码受报文格式影响等问题。以下两种方式能够将xml自动转换为JavaBean，开发人员就可以直接使用JavaBean编写代码了。
#### 一、XMLBeans
XMLBeans是Apache的一个开源项目，可在官网下载jar包。使用XMLBeans生成JavaBean需要用到xml对应的schema，不幸的是对方系统竟然没有schema提供，那只能通过返回的xml生成schema了。我用的是Stylus Studio，该工具可以通过图形界面轻松将xml转换成xsd文件。
使用XMLBeans转换schema的教程参考的是：（[XMLBeans使用教程](http://samwalt.iteye.com/blog/1820600)）
我有多个xml需要转换为JavaBean，且多个Xml内有重复的节点名称，这样避免不了会生成同名但不同包名的类，假设这两个类分别为com.one.MessageDocument和com.two.MessageDocument，问题来了。。。。当我在代码中使用这个com.one.MessageDocument.Factory.parse(xml)时，会报错，原因是类加载器会将两个MessageDocument弄混，指定使用com.two.MessageDocument，但是加载器会去使用com.one.MessageDocument。删除掉com.one.MessageDocument，程序执行正确。
于是下载了最高版本的XMLBeans，验证后这个问题依然存在，不得已只能想其他方式了，于是开始使用xjc
#### 二、xjc
java自带的xjc命令可根据schema文件生成对应的java实体类，命令如下：* xjc -p 包路径 xsd路径 *
生成的java实体类会放置在当前目录下的包路径下，比如在c盘根目录执行了命令，包路径为com.xx,最终生成的java实体类会放置在c://com/xx下
下边就需要将对方系统返回的xml报文解析成实体类了，xml报文是以string字符串返回的，这里用到了java的JAXBContext试下，其中TestBean是
刚刚生成的java实体类，代码如下：
```java
public class XMLUtil{
	public static <T> T converyToJavaBean(String xml, Class<T> c) {  
		T t = null;  
		try {  
			JAXBContext context = JAXBContext.newInstance(c);  
			javax.xml.bind.Unmarshaller unmarshaller = context.createUnmarshaller();  
			t = (T) unmarshaller.unmarshal(new StringReader(xml));  
		} catch (Exception e) {  
			e.printStackTrace();  
		}  

		return t;  
	}
}
TestBean testBean = XMLUtil.converyToJavaBean("xml",TestBean.class);
```
