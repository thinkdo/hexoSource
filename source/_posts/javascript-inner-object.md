title: JavaScript内置对象
date: 2012-04-07 17:19:06
tags:
---
JavaScript只定义了两个内置对象。 
一、Global对象 
Global实际上根本不存在，它是ECMAScript中最特别的对象，因为像以下这样写是**错误**的： 
```javascript
var a  = Global;
```
isNaN(),isFinite(),parseInt(),parseFloat()等都是Gloal对象的方法。在ECMAScript中不存在单独的函数，所有的函数（方法）都是某个对象的方法。 

下面列出了Global的方法及属性 
**1、方法encodeURI(),encodeURIComponent() **
有效的Url不能包含某些字符，encodeURI()，encodeURIComponent()用于编码URL，转换其中的特殊字符，从而让浏览器能够接收他们。 
两个方法的主要区别是：encodeURI()不对冒号，前斜杠，问号，英镑字符进行编码， 而后者则对它发现的所有字符进行编码。
对应解码的函数为decodeURI()与decodeURIComponent(); 
**2、方法eval() **
```javascript
var hel = 'hi'; 
eval("alert(hel);");//内部可调用hel 
eval("function test(){alert('hi');}");test();//外部可调用该方法 
```
**3、属性 ** 
undefined，NaN，Infinity，Object的构造函数，Array的构造函数，Function的构造函数，Boolean的构造函数，String的构造函数，Number的构造函数，Date的构造函数，RegExp的构造函数，Error的构造函数，EvalError的构造函数，RangeError的构造函数，ReferenceError的构造函数，SyntaxError的构造函数，TypeError的构造函数，URIError的构造函数。 

二、Math对象 
**1、属性** 
> * E：       值e，自然对数的底 
> * LN10：    10的自然对数 
> * LN2：     2的自然对数 
> * LOG2E：   以2为底E的对数 
> * LOG10E：  以10为底E的对数 
> * PI：      值π 
> * SQRT1_2： 1/2的平方根 
> * SQRT2：   2的平方根 

**2、方法max(),min()**
用于判断一组数中最大的数和最小的数。例如： 
```javascript
var iMax = Math.max(1,23,3,133);//iMax等于133 
var iMin = Math.min(1,23,4,5);//iMin等于1 
```
**3、abs方法** 
返回数字的绝对值 Math.abs(-1); 
**4、舍入方法** 
ceil：表示向上舍入 
floor：表示向下舍入 
round：表示标准的舍入函数（如果数字与下一个整数的差不超过0.5，则向上舍入，否则向下舍入） 