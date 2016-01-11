title: react小tips
date: 2015-10-30 15:48:06
tags:
---
react编写的过程中，有很多需要注意的地方
1. return和左括号要在一行，即return(
2. class要写为className
3. 每一个组件return的都是一个封闭的html标签，否则会报错
4. 在react的子函数中使用function时，this关键字要进行绑定，否则指向的就是function本身
5. createClass时，class的名字必须是首字母大写
6. 可通过e.target代替this.refs.
	
