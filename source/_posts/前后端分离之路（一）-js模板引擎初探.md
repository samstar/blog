title: 前后端分离之路（一） js模板引擎初探
date: 2016-02-02 20:44:51
tags: js模板引擎
category: 博客
---

## 浏览器端渲染模板流程

1、在浏览器端引入模板引擎（本文以doT为例） 

　　`<script src="doT.js"></script>`

2、获取数据，使用模板引擎生成html

　　1) 通过ajax或其他方式获取JSON数据data
　　2) 模板引擎渲染语法生成html

3、将html插入文档需要位置

### DOM结构

``` html
    <html>
        <head></head>
        <body>
            <div class="nav"></div>
            <div class="body"></div>
            <script type="text/template" id="nav">
<!--
        遍历对象，key->value  
        模板的it是调用渲染函数时传入的data参数生成的对象  
-->
                {{ for(var key in it){ }}
                    <li data-nav = "{{=key}}">{{=it[key]}}</li>
                {{ } }
            </script>
            <script type="text/template" id="body">
<!--    遍历数组，index->value   -->
                {{~it :value:index}}
                    <div data-body-id = "{{=index}}">{{=value}}</div>
                {{~}}
            </script>
        </body>
    </html>
```


### 模板渲染
```javascript
     // 假设获取到数据为JSON对象data
     ({
        init: function(){
            var data={
                nav: { first: 111, second: 222, third: 333 },
                body: { [5,6,7] }
            };
            this.rendered('#nav', data.nav, '.nav');   //第二个参数data.nav作为模板的it对象
            this.rendered('#body', data.body, '.body');
        },
        /**
        * el:页面上装载dot模板的容器选择器
        * data: 用来渲染模板的数据
        * container: 装载渲染后的html的容器
        */
        rendered: function(el, data, container){
            container = container || this.container;
            var htm = $(el).html();
            var temp = doT.template(htm);
            $(container).append(temp(data));
        }
        }).init();
```



### 总结
运行在浏览器端的js模板引擎工作机制大致相似，都是通过渲染数据生成html插入DOM中。doT的特点是快速，简洁，能快速运用到实际的开发工作中。有任何问题欢迎留言，随时交流~~

想对doT有更多了解欢迎访问[doT官网](http://olado.github.io/doT/)
想了解更多的js模板引擎推荐访问`@jogiter`总结的[前端模板引擎比较分析](https://github.com/Jogiter/frontend/blob/dev/blogs/template-engine.md)


