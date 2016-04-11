title: javascript事件冒泡与事件委托
date: 2016-04-11 18:38:58
tags: javascript
---

## 事件冒泡机制
事件开始时由最具体的元素接收，然后逐级向上传播到较为不具体的节点 -- js高级教程
现代浏览器会将事件一直冒泡到window对象
以如下结构为例
```
    <html>
        <body>
            <div>
                <span id="btn">
```
在span标签绑定click事件，则点击span元素时，事件会沿着DOM树向上传播，即`span` > `div` > `body` > `html` > `document`
        
        注意这里，window对象是一个顶层对象，代表浏览器中一个打开的窗口，而document是window的一个属性对象（本身是一个对象），为当前显示的文档

## 阻止事件冒泡
### DOM中的事件对象
支持DOM的浏览器会有一个event对象传入事件处理程序中。该event对象拥有`target`、`currentTarget`、`type`、`preventDefault()`、`stopPropagation()`等属性和方法。
注意`target`和`currentTarget`的不同。
>在事件处理程序内部，对象this始终等于currentTarget的值（注册事件的元素）
>target值包含事件的实际目标

下面两段代码：
```
    var btn = document.getElementById('btn');
    btn.addEventListener('click', function(e){
        console.log(this);              //btn                       
        console.log(e.currentTarget);   //btn
        console.log(e.target);          //btn （假设btn为底层节点，否则可能为btn的子节点）
    }, false);
```
```
    var btn = document.getElementById('btn');
    document.body.addEventListener('click', function(e){
        if(e.target.id == "btn"){
            console.log(this);              //body               
            console.log(e.currentTarget);   //body
            console.log(e.target);          //btn
        }
    }, false);
```

### event.stopPropagation()阻止冒泡
event事件的stopPropagation()方法的作用是`取消事件的进一步捕获或冒泡`。
这里，我们绑定事件的写法a.addEventListener('click',function(){},`false`)。最后一个参数是布尔值，指定事件流类型，`true`代表捕获事件，`false`代表冒泡事件。
```
    var btn = document.getElementById('btn');
    document.body.addEventListener('click', function(e){
        e.stopPropagation(); 
    }, false);
```
调用event对象的该方法后，btn触发click事件，click事件不会沿DOM树进行冒泡了，也就是说，即使在btn的父节点或祖先节点注册了click事件，也不会触发。

## 事件委托
事件委托利用事件冒泡机制，指定一个事件处理程序，就可以管理同一类型多个事件。
```
    var btn = document.getElementById('btn');
    document.body.addEventListener('click', function(e){
        e.stopPropagation();            //会生效吗？
        if(e.target.id == "btn"){
            do something...         
        }
    }, false);
```
原理就是，当被委托的元素上的事件（即此处document.body）触发时，判断e.target执行。点击btn后，并没有触发任何事件，而是click事件从btn向上一层层冒泡上去，沿途触发各个元素上的事件处理函数，冒泡到doucment.body时，才触发该事件处理函数，执行e.target判断，进而执行目标代码。
所以，代码中的e.stopPropagation()在事件从btn冒泡至body才会执行，执行的结果`仅仅是阻止事件由body进一步向上冒泡`。

## 总结
事件委托中的阻止冒泡，阻止的是从被委托元素向上的冒泡。也就是事件处理函数中e.currentTarget或者是this向上的冒泡。