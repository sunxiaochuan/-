---
title: 结合 php 实现的 jsonp 前端小 demo
date: 2018-05-16 23:28:45
tags: [跨域,web前端,Cookie,jsonp,面试必会题]
categories: [代码/技能进阶]
---

# 资料

[参考原文--JSONP 教程](http://www.runoob.com/json/json-jsonp.html)
[github 源码地址](https://github.com/sunxiaochuan/simple-demo/tree/master/jsonp-demo)

# 环境

* 这里我使用的是 `xmapp` 集成软件，在本地起的 `apache` 服务进行测试的
* jsonp.php 文件是要放到 xmapp -> htdocs   目录下的

# 源码

- index.html

		```html
      <!DOCTYPE html>
    <html>

    <head>
        <meta charset="utf-8">
        <title>JSONP 实例</title>
    </head>

    <body>
        <div id="divCustomers"></div>
        <script type="text/javascript">
            function callbackFunction(result, methodName) {
                // result = ["customername1","customername2"]
                var html = '<ul>';
                for (var i = 0; i < result.length; i++) {
                    html += '<li>' + result[i] + '</li>';
                }
                html += '</ul>';
                document.getElementById('divCustomers').innerHTML = html;
            }
        </script>
        <script type="text/javascript" src="http://127.0.0.1:8008/jsonp.php?jsoncallback=callbackFunction"></script>
    </body>

    </html>
		```

- jsonp.php

		```php
		<?php
			header('Content-type: application/json');
			//获取回调函数名
			$jsoncallback = htmlspecialchars($_REQUEST ['jsoncallback']);
			//json数据
			$json_data = '["customername1","customername2"]';
		//输出jsonp格式的数据
		echo $jsoncallback . "(" . $json_data . ")";
		?>
		```

- 浏览器效果图
{% asset_img 浏览器效果图.png "浏览器效果图" %}
