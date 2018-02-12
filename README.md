## 该demo是使用阿里移动端适配方案 flexible

该demo主要参考该文，详细的介绍可以[点击这里](https://github.com/amfe/article/issues/17 "github")进行了解。

flexible方案主要做的事是：

1.动态改写<meta>标签
2.给<html>元素添加data-dpr属性，并且动态改写data-dpr的值
3.给<html>元素添加font-size属性，并且动态改写font-size的值

html的demo代码是

	<!DOCTYPE html>
	<html lang="en">
	    <head>
	        <meta charset="utf-8">
	        <meta content="yes" name="apple-mobile-web-app-capable">
	        <meta content="yes" name="apple-touch-fullscreen">
	        <meta content="telephone=no,email=no" name="format-detection">
	        <title>demo</title>
	        <script src="http://g.tbcdn.cn/mtb/lib-flexible/0.3.4/??flexible_css.js,flexible.js"></script>
	        <script type="text/javascript" src="lib/flexible.js"></script>
	        <link rel="stylesheet" type="text/css" href="lib/flexible.css">
	        <link rel="stylesheet" type="text/css" href="css/style.css">
	    </head>
	    <body>
	        <!-- 页面结构写在这里 -->
	    </body>
	</html>


### 使用方法

lib-flexible库的使用方法非常的简单，只需要在Web页面的<head></head>中添加对应的flexible_css.js,flexible.js文件：

>一种是直接加载阿里CDN的文件

	<script src="http://g.tbcdn.cn/mtb/lib-flexible/0.3.4/??flexible_css.js,flexible.js"></script>

>一种方法是将文件下载到你的项目中，然后通过相对路径添加:

	<script type="text/javascript" src="lib/flexible.js"></script>
	<link rel="stylesheet" type="text/css" href="lib/flexible.css">

>注意： 使用flexible方案 需引入，且必须放在<b>自己写的css的最前面</b> 

### flexible的实质

flexible实际上就是能过JS来动态改写meta标签，代码类似这样：

	var metaEl = doc.createElement('meta');
	var scale = isRetina ? 0.5:1;
	metaEl.setAttribute('name', 'viewport');
	metaEl.setAttribute('content', 'initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
	if (docEl.firstElementChild) {
	    document.documentElement.firstElementChild.appendChild(metaEl);
	} else {
	    var wrap = doc.createElement('div');
	    wrap.appendChild(metaEl);
	    documen.write(wrap.innerHTML);
	}

> 所以在html不用添加meta viewport,flexible会自动在html生成

### px转rem的方法

1.使用sublime的插件，CSSREM
2.使用css预处理sass的函数或mixin
3.使用构建工具gulp的插件postcss-px2rem,手动添加、配置任务