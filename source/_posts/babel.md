title: react代码组件化--独立封装js文件
date: 2015-11-09 10:02:20
tags:
---
[参考文档](http://facebook.github.io/react/docs/getting-started.html)
在浏览器端用browser.min.js编译jsx的方式很消耗时间，以下方式可将jsx语法的react代码在服务器端转换为普通的js文件，也就实现了react组件化。
**一、在终端中执行命令：npm install \-\-global babel-cli**
如果出现错误类似错误：
npm ERR! error rolling back   code: 'EEXIST',
npm ERR! error rolling back   path: '/Users/hanfeng/.nvm/v0.11.13/bin/babel' }
npm ERR! Refusing to delete: /Users/hanfeng/.nvm/v0.11.13/bin/babel not in /Users/hanfeng/.nvm/v0.11.13/lib/node_modules/babel-cli
File exists: /Users/hanfeng/.nvm/v0.11.13/bin/babel
则rm掉相关文件夹
**二、在终端中执行命令： npm install babel-preset-react**
大家可能注意到了这个babel-preset-react不是全局安装的，即使为其加上--global标识进行全局安装，然后在工作目录中去执行第四个命令也是不行的，会报错，说找不到react命令。所以只能在工作目录中去安装该插件并在该工作目录下使用它。如果有其他人知道可以global中执行的话，请留言，不胜感激。
**三、这里，要拆分的helloworld.html如下：**
```html
<!DOCTYPE html>
<html>
	<head>
		<meta http-equiv='Content-type' content='text/html; charset=utf-8'>
		<script src="../build/react.js"></script>
   		<script src="../build/react-dom.js"></script>
   		<script src="../build/browser.min.js"></script>
	</head>
	<body>
		<div id="container"></div>
		<script type="text/babel">
			var HelloWorld = React.createClass({
				render:function(){
					return <p>第一个react程序！</p>;
				}
			});
			ReactDOM.render(<HelloWorld />,document.getElementById('container'));
		</script>
	</body>
</html>
```
首先将jsx代码拆分出来单独放置在helloworld.js文件中，helloworld.js代码如下
```javascript
var HelloWorld = React.createClass({
	render:function(){
		return <p>第一个react程序！</p>;
	}
});
ReactDOM.render(<HelloWorld />,document.getElementById('container'));
```
**四、切换到工作目录，运行命令：babel \-\-presets react helloworld.js \-\-watch \-\-out-dir build**
这句命令的意思是，将helloworld.js转换成普通的javascript文件，放置为build文件夹下，名字仍为helloworld.js,并且其中的--watch属性表示会时刻监控源文件的变化，自动将最新的源文件进行转换。命令执行完毕后，将会在build文件夹下看到生成了一个helloworld.js文件。
如果想批量编译，只需将helloworld.js换成想要编译的源文件的父目录名称即可，比如helloworld.js在src目录下，就执行命令babel \-\-presets react src \-\-watch \-\-out-dir build

**五、更改helloworld.html文件如下：**
```html
<!DOCTYPE html>
<html>
	<head>
		<meta http-equiv='Content-type' content='text/html; charset=utf-8'>
		<script src="../build/react.js"></script>
   		<script src="../build/react-dom.js"></script>
	</head>
	<body>
		<div id="container"></div>
		<script src="../build/helloworld.js"></script><!--此处引入了转换后的js文件-->
	</body>
</html>
```
这时的helloworld.html与最开始的通过browser.min.js编译的helloworld.html效果是等同的


