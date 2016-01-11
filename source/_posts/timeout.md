title: ajax为什么进error？
date: 2015-09-22 17:15:56
tags:
---
最近遇到ajax会进入到error分支的情况，但往往网上的方法并不能解决问题，不同的项目部署、不同的后台处理逻辑使得解决方法不尽相同。从ajax的原理开始一点点的分析是哪里出现了问题。
###什么是AJAX？
AJAX 是一种用于创建快速动态网页的技术。
通过在后台与服务器进行少量数据交换，AJAX可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
###AJAX的原理
XMLHttpRequest对象是AJAX的核心，所有的浏览器（ie7以上、火狐、谷歌、）都支持该对象，XMLHttpRequest是js用于与后台服务器交互的对象。

###查看error里的报错信息
想知道为什么进入error，首先需获取error分支的报错信息，按照以下方法打印出来
```javascript
$.ajax({
		url:'/test',
		dataType:"json",
		type:"post",
		async:false,
		timeout:10000,
		beforeSend:function(){     
		},
		success:function(data){
		    alert("success");
		},
		error:function(data,textStatus,errorThrown){
			alert('textStatus='+textStatus+',status='+data.status+',readyState='+data.readyState);
		},
		complete: function() {
		}
}); 
``` 
textStatus有几种值，"null", "timeout", "error", "notmodified" 和 "parsererror"。
###超时

