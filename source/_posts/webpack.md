title: webpack+react
date: 2016-07-05 10:47:52
tags:
---
原项目背景：后端采用java开发，前端采用react+es5。jsx语法是线下通过babel-preset-react转化为普通的js文件。然后在html页面中引入转换后的js文件。
改造目标：通过webpack自动构建前端，组件均采用es6语法。
过程如下：
<font color=#0099ff size=5 face="黑体">一、加载需要用到的依赖包</font>
1、我们需要使用npm管理依赖包，如果之前没有初始化npm，请在终端输入*npm init*命令，初始化后会生成一个package.json文件，如下。如果之前已经存在该文件，则对文件进行更改,增加对应依赖包。
```json
{
  "name": "cuican",
  "version": "1.0.0",
  "description": "cuican",
  "main": "index.js",
  "scripts": {
    //此处设置了npm脚本命令，通过在终端执行 npm start 就可以启动webpack-dev-server了，
    //webpack-dev-server是一个开发辅助工具，只需ctrl+s后即可在浏览器看到最新效果，不用
    //刷新也不用重构建
    "start": "webpack-dev-server --hot --inline --progress --colors",
    // 通过webpack构建命令进行构建，生成最终文件
    "build": "webpack --progress --colors",
    //set NODE_ENV=production用于区分生产环境和测试环境，可以在webpack.config.js中根
    //据此变量写一些测试代码
    "publish-win": "set NODE_ENV=production&&webpack -p --progress --colors"
  },
  "author": "cuican",
  "license": "ISC",
  "devDependencies": {
    //babel用于将es6转换为es6、将jsx语法解析为js
    "babel-core": "^6.10.4",
    "babel-loader": "^6.2.4",
    "babel-polyfill": "^6.9.1",
    "babel-preset-es2015": "^6.9.0",
    "babel-preset-react": "^6.11.1",
    //用于在js文件中加载css
    "css-loader": "^0.23.1",
    //分离css，将css单独加载
    "extract-text-webpack-plugin": "^1.0.1",
    "file-loader": "^0.9.0",
    "fs": "0.0.2",
    "glob": "^7.0.5",
    //自动根据模板生成html文件
    "html-webpack-plugin": "^2.22.0",
    "path": "^0.12.7",
    "react": "^15.1.0",
    "react-dom": "^15.1.0",
    "react-hot-loader": "^1.3.0",
    "style-loader": "^0.13.1",
    "url-loader": "^0.5.7",
    "webpack": "^1.13.1",
    "webpack-dev-server": "^1.14.1"
  },
  "dependencies": {
    "jquery": "^2.2.2",
    "react": "^15.1.0",
    "react-dom": "^15.1.0",
    "react-redux": "^4.4.5",
    "redux": "^3.5.2"
  }
}

```
2、使用命令*npm install*安装所有依赖包。
windows下如果安装babel-preset-es2015的时候报错为：某某文件exists，这时候有可能是node的版本过低，需在官网下载最新版本的node并安装。
3、webpack和webpack-dev-server除了安装在本地项目下外，还需安装到全局中，这样才能使用webpack命令。执行命令**npm install webpack-dev-server --global**和**npm install webpack --global**进行安装
<font color=#0099ff size=5 face="黑体">二、配置webpack.config.js</font>
在项目的根目录下手动新建一个webpack.config.js文件，内容配置如下：
```javascript
var webpack = require('webpack');
var path = require('path');
var glob = require('glob');
var HtmlWebpackPlugin = require('html-webpack-plugin');
const debug = process.env.NODE_ENV !== 'production';
//如果css文件很大，不想构建到入口文件中，则使用extract-text-webpack-plugin进行单独加载
var ExtractTextPlugin = require("extract-text-webpack-plugin");
function entries (globPath) {
    var files = glob.sync(globPath);
    var entries = {}, entry, basename;

    for (var i = 0; i < files.length; i++) {
        entry = files[i];
        basename = path.basename(entry, '.js');
        entries[basename] = './' + entry;
    }
    entries['react']= ['React'];
    entries['react-dom']= ['React-dom'];
    entries['jquery']= ['jquery'];
    return entries;
}
module.exports = {
    //加载所有入口文件，这里实现了根据目录自动读取entryJs下的所有文件，react、jquery文件太大，所以要单独加载，不构建到入口文件中
    entry: entries('component/src/entryJs/*.js'),
    output: {
        //入口文件的最终输出目录
        path: path.join(__dirname,'component','build'),
        filename: '[name]'  + (debug ? '' : '-[chunkhash]') + '.js',
        chunkFilename: '[id]' + (debug ? '' : '-[chunkhash]') + '.js'
    },
    module: {
        //加载各种文件的loader，不同类型的文件用不同的loader进行解析转换
        loaders: [
            { test: /\.js?$/, exclude: /node_modules/, loaders: ['react-hot', 'babel-loader']},
            { test: /\.js$/, exclude: /node_modules/, loader: 'babel-loader'},
            { test: /\.css$/, loader: ExtractTextPlugin.extract("style-loader", "css-loader")},
            {test: /\.(gif|jpg|png|woff|svg|eot|ttf)\??.*$/, loader: 'url-loader?limit=50000&name=[path][name].[ext]'}
        ]
    },
    resolve:{
        extensions:['','.js','.json']
    },
    plugins: [
        new webpack.NoErrorsPlugin(),
        new ExtractTextPlugin("page.css"),
        new webpack.DefinePlugin({
            'process.env.NODE_ENV': '"development"'
        }),
        new webpack.optimize.CommonsChunkPlugin({
            name: ['react', 'react-dom','jquery'],
            minChunks: Infinity
        }),/*
        new HtmlWebpackPlugin({
            title: 'test',
            filename: path.join(__dirname,'html','search.html'),
            inject: 'body',
            template:  path.join(__dirname,'template.html'), // Load a custom template
            chunks: ['react','react-dom','jquery','bindNumber']
        })*/
    ]
};

```
<font color=#0099ff size=5 face="黑体">三、将组件改写为es6风格</font>
1、以前是在html中引入要用到的组件，这里改为在js中通过import引入组件模块。语法为**import defaultMethod, { otherMethod }  from '某某组件名字'**。比如下边的弹出框组件依赖react，则写为import React from 'react'。
2、类创建采用**class 组件名称 extends React.Component{}**，如果需要将该组件导出在需要导出的类、方法、变量前加入export,一个模块内只能有一个export default，用default导出的不需要通过大括号进行import。
3、用构造器constructor代替getInitialState，并需在构造函数内写入super(props)
4、当使用 React.createClass 来定义组件时，React 允许你随意在此组件的类中定义方法，而在方法中调用的 this 会自动绑定到组件自身，但对于es6的类 来说，自动绑定并不适用。es6使用箭头函数**=>**自动绑定this关键字，语法**param => expression**，**([param] [, param]) => { statements}**
```javascript
import React, { Component, PropTypes } from 'react';
export default class AlertBoxComponent extends Component{
	constructor(props){
	    super(props);
	}
	render(){
		return (
			<div className={this.props.unShow?'undis':'dis'}>
				<div className='dialogMask'></div>
				<section className='dialog'>
					<p className="info-notice">{this.props.content}</p>
					<div className="close-btn">
						<button onClick={() => { this.props.handleAlertCloseButton() }}>关闭</button>
					</div>
				</section>
			</div>
		);
	}
}
AlertBoxComponent.propTypes = {
	handleAlertCloseButton: PropTypes.func.isRequired
}
```
