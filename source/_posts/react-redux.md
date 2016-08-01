title: react-redux+es6
date: 2016-07-10 21:22:06
tags:
---
redux的原理大家去网上搜吧，但是一般来说不容易看懂，动手后才能慢慢理解，这里讲一下我是怎么使用react-redux开发一个alert框的，都是比较基础的写法。
1、首先当然是安装react-redux，使用npm命令：npm install --save react-redux
2、接下来写展示组件，文件名为alertBox.js，内容如下：
```javascript
//“展示组件”不需要知道数据怎么变化，只需要标记出需要动态展示的地方！
export default class AlertBox extends React.Component{
	constructor(props){
	    super(props);
	    autoBind(this);
	}
	render(){
		return (
			//unShow用于确定是否展示该alert框
			<div className={this.props.unShow?'undis':'dis'}>
				<div className='dialogMask'></div>
				<section className='dialog'>
					//contents用于展示alert框的内容
					<p className="info-notice">{this.props.contents}</p>
					<div className="close-btn">
						//handleAlertCloseButton为点击关闭按钮时的回调函数
						<button onClick={this.props.handleAlertCloseButton}>关闭</button>
					</div>
				</section>
			</div>
		);
	}
	AlertBox.propTypes = {
		handleAlertCloseButton: PropTypes.func.isRequired
	}
}
```