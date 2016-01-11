title: react基础入门
date: 2015-10-22 17:18:23
tags:
---
###下载包
[react官网下载地址](https://facebook.github.io/react/downloads.html)
解压后在build文件夹下看到几个js文件，我们要使用的是react.min.js、react-dom.min.js
###编写react页面
react使用jsx语法（可选的），要将jsx语法转换为浏览器可识别的javascript有很多种方式，其中最简单的一种就是在html代码中引入browser.min.js。所以使用react只需引入react.min.js、react-dom.min.js、browser.min.js即可。

3、jsx语法
允许html和javascript混写
遇到<则用html解析，遇到{}则用javascript解析，所以当写javascript时用{}围起来
4、数组自遍历
{this.props}
5、所有组件都必须有自己的render方法，用于输出组件
6、添加组件属性，有一个地方需要注意，就是 class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。
7、this.props.children，表示组件的子节点
这里需要注意，只有当子节点多余1个时，this.props.children 才是一个数组，否则是不能用 map 方法的，会报错。
8、我们新建自己的组件时，要规定组件的属性值类型，比如age属性的类型必须是int，这样别人在使用我们的组件时，才不会胡乱给age赋值为“一万年”。
组件的属性可以接受任意值，字符串、对象、函数等等都可以。
http://facebook.github.io/react/docs/reusable-components.html
9、0.14版本中将react.js拆分为了react.js和react-dom.js。
ReactDOM对象是在0.14版本之后才出现的
当该构造函数调用的时候，应该会返回一个对象，该对象至少带有一个 render 方法。该对象指向一个 ReactComponent 实例。

var component = new MyComponent(props); // never do this
除非为了测试，正常情况下不要自己调用该构造函数。React 帮你调用这个函数。

相反，把 ReactComponent 类传给 createElement，就会得到一个 ReactElement 实例。

var element = React.createElement(MyComponent);
或者使用 JSX：

var element = <MyComponent />;

