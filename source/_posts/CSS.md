title: CSS小Tips
date: 2015-08-06 17:31:07
tags:
---
###如何使iframe页面的内容在ios设备上滚动？###
最近做了一个弹窗的效果，弹窗层内嵌套的是iframe标签，但是发现在ios设备上iframe内容无法滚动，而在Android设备上却能够滚动，试验了很多方法都不行，最终找到了以下这篇文章解决了这个问题，谢谢作者的翻译[使IFRAME在iOS设备上支持滚动](http://blog.csdn.net/renfufei/article/details/37663355)
###图片和文字的对齐问题###
图片和文字并排时，默认情况下是不对齐的，如以下代码：
```html
<div>
	<img src="test.png"/>捉妖记
</div>
```
这种情况下发现图片比文字靠上，test.png的默认对齐是顶部对齐，而文字“捉妖记”的对齐方式是底对齐，我们可通过设置图片的vertical-align属性改变其对齐方式。[参考文章](http://blog.csdn.net/dududu01/article/details/7641270)
baseline：将支持valign特性的对象的内容与基线对齐
sub：垂直对齐文本的下标
super：垂直对齐文本的上标
top：将支持valign特性的对象的内容与对象顶端对齐
text-top：将支持valign特性的对象的文本与对象顶端对齐
middle：将支持valign特性的对象的内容与对象中部对齐
bottom：将支持valign特性的对象的文本与对象底端对齐
text-bottom：将支持valign特性的对象的文本与对象顶端对齐

