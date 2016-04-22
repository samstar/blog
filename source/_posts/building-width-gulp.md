title: 'building width gulp '
date: 2016-04-19 13:19:59
tags: gulp
---
## 使用gulp构建工具
### 使用场景
`需求`：项目开发过程中，一些重复或者繁琐的工作，如静态文件压缩、合并、错误检查等工作，往往会占用大量时间，极大地限制了开发效率。因此，我们需要一个自动化的开发流程去完成这些工作。gulp就是这样一个自动化的工具，用于打造我们高度集成化的开发环境。
常用功能：
`版本控制`
`检查js`
`图片合并`
`压缩CSS`
`压缩js`
`CSS预编译`
### 安装和使用
全局安装    
  
        npm install -g gulp
作为项目的开发依赖安装

    
        npm install --save-dev gulp
创建gulpfile.js文件，放在项目根目录下

安装依赖插件
`npm install gulp-uglify –save-dev` //将具体的gulp功能插件局部安装项目下

### 语法
1、gulp.src(globs[,options])

    gulp.src('client/templates/*.jade')
        .pipe(jade())
        .pipe(minify())
        .pipe(gulp.dest('build/minified_templates'));
glob作为匹配模式，负责输出符合条件的文件，返回的流可以被piped到其他插件中。

2、gulp.dist(path[,options])
数据能pipe进来，会写文件，会重新输出所有数据。因此可以用gulp.dist将数据pipe到多个文件夹。如果文件夹不存在，会自动创建。
    
    gulp.src('./client/template/*.jade')
        .pipe(jade())
        .pipe(gulp.dist('./build/templates'))
        .pipe(minify())
        .pipe(gulp.dist('./build/minified_templates'))

3、gulp.task(name[,deps],fn)
定义任务
name指任务的名字,deps是一个Array，包含任务列表，这些任务会在当前任务运行之前完成，
fn任务要执行的操作
  
    gulp.task('mytask',['array','of','task','names'], function(){
        // do something
    });


### 实际运用
实例
``` 
    //引入要使用的gulp插件
    var gulp = require('gulp'),
        uglify = require('gulp-uglify'),  //js压缩
        rename = require('gulp-rename'),  //文件重命名
        clean = require('gulp-clean'),    //清空文件夹
        rev = require('gulp-rev'),        //版本号更改
        rev-collector = require('gulp-rev-collector'), //gulp-rev的插件
        minifyCss = require('gulp-minify-css'),   //压缩CSS
        revAll = require('gulp-rev-all');         //替换引用到加版本号文件的所有引用路径
```