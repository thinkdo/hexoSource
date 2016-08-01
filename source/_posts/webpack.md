title: webpack+react
date: 2016-07-05 10:47:52
tags:
---
原项目背景：后端采用java开发，前端采用react+es5。jsx语法是线下通过babel-preset-react转化为普通的js文件。然后在html页面中引入转换后的js文件。
改造目标：通过webpack自动构建前端，采用es6进行开发。
过程如下：
<font color=#0099ff size=5 face="黑体">一、加载需要用到的依赖包</font>
1、我们需要使用package.json管理依赖包，如果之前没有该文件，请在终端输入*npm init*命令，初始化一个package.json文件。如果之前已经存在该文件，则对文件进行更改,增加如下依赖包。
```json
{
  "name": "wechat",
  "version": "1.0.0",
  "description": "wechat-zhongyou",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "cuican",
  "license": "ISC",
  "devDependencies": {
    "babel-core": "^6.10.4",
    "babel-loader": "^6.2.4",
    "babel-polyfill": "^6.9.1",
    "babel-preset-es2015": "^6.9.0",
    "babel-preset-react": "^6.11.1",
    "css-loader": "^0.23.1",
    "react": "^15.1.0",
    "react-dom": "^15.1.0",
    "react-hot-loader": "^1.3.0",
    "style-loader": "^0.13.1",
    "webpack": "^1.13.1",
    "webpack-dev-server": "^1.14.1"
  },
  "dependencies": {
    "react": "^15.1.0",
    "react-dom": "^15.1.0"
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
module.exports = {
    entry: {
      thinkdo: './js/component/src/myBusiness/test.js'
    },
    output: {
        path: './js/component/build',
        filename: "[name].js"
    },
    module: {
        loaders: [
            { test: /\.js?$/, exclude: /node_modules/, loaders: ['react-hot', 'babel-loader']},
            { test: /\.js$/, exclude: /node_modules/, loader: 'babel-loader'},
            { test: /\.css$/, loader: "style!css" }
        ]
    },
    resolve:{
        extensions:['','.js','.json']
    },
    plugins: [
        new webpack.NoErrorsPlugin(),
        new webpack.DefinePlugin({
            'process.env.NODE_ENV': '"development"'
        }),
        new webpack.HotModuleReplacementPlugin()
    ]
};

```
entry