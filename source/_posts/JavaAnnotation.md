title: JavaAnnotation
date: 2015-07-31 14:31:43
tags:
---
什么是声明？java annotation！
####什么是annotation？
即java注解，常见的java注解有@overwrite、@Documented等，注解本身对业务逻辑不会产生任何影响，它是描述java语言的元数据。元数据即描述数据的数据。
比如@Documented，表示当前类是否会进入javadoc的注解
####开发者自定义annotation
开发者可自定义annotation，方式如下：
@interface：该标识表示“继承java.lang.annotation.Annotation接口”
```java
public @interface Car{
    String kilo();
}
public @interface Tool{
    String useIt();
}
@Tool(useIt="useTool")
public class Test {

        @Car(name = "123km")
        public String testCar()
        {
            return "i am a car!";
        }
}
public static void main(String[] args) {
	try {
			Class testClass = Class.forName("com.Test");
			boolean flag = testClass.isAnnotationPresent(Tool.class);
			
			if(flag)
			{
			    Method[] methods = testClass.getMethods();
				Tool tool = (Tool)testClass.getAnnotation(Tool.class);
				for(Method method : methods) {
					if(method.isAnnotationPresent(Car.class))
					{
						Car car = (Car)method.getAnnotation(Car.class);
						System.out.println(car.kilo());
						
					}
				}
			}
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
}
```