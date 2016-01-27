title: 献给github和hexo
date: 2016-01-20 15:14:13
tags: github+hexo搭建个人博客
category: 博客
---
## 搭建历程
### github创建主页和项目页
一直想搭建一个自己的博客，这几天有时间，就折腾了一下。方案采用的是*github+hexo*，之前在*github*上建了一个较挫的主页，直接删掉换成博客的话有些舍不得，于是决定主页保留，博客页面创建在*gh-pages*分支，作为项目页面。
<p style="color:#f15b82">具体方法如下：</p>
1. github创建user pages 和project pages : User Pages创建：新建仓库，名称为`xxxx.github.io`,进入该仓库，点击`Setting`按钮，找到`GitHub Pages`部分，生成页面（不做赘述，不会者google之~）。Project pages创建：新建仓库，命名随意，备用。
2. 安装Node.js。windows下建议使用*git bash*作为命令行工具。npm命令行运行``npm install -g hexo``。任意目录创建文件夹hexo，*git bash*进入该文件夹，执行命令`hexo init`，即安装好。
hexo命令:  
>hexo g   　　生成静态页面（generate）
hexo s    　　启动server
hexo n    　　新建文章（new）
hexo d    　　发布（deployer）
3. 使用`hexo n "filename"` 创建文章。进入*source>_posts*文件夹找到创建的文件，随便写点什么吧。运行`hexo s`，看到如下console:


    Hexo is running at http://0.0.0.0:4000.

    打开浏览器，输入`localhost:4000`，文章出来了~~
[点击这里看看](http://samstar.github.io/blog)


### 先到这里，后面研究下怎么加入baidumap

### 备份以在不同环境下随时更新博客