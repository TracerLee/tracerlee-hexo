---
title: 开始你的electron
date: 2016-04-17 03:06:13
tags: [工具,学习]
---

使用electron开发桌面应用遇到的问题和tips记录。

* `$ electron .`没有作用，可能全局环境安装出现了一些问题

* ![](http://ww2.sinaimg.cn/large/68731f4agw1f2z57jnc97j20nv0eaae5.jpg)

  安装这个老是卡住

* 使用`electron-connect`和`gulp`来监听程序

  要在项目内安装`electron-connect`和`gulp`，否则会报错

  ```bash
  $ npm i -gd gulp --save
  ```

  ```javascript
  'use strict';
   
  var gulp = require('gulp');
  var electron = require('electron-connect').server.create();
   
  gulp.task('default', function () {
   
    // Start browser process 
    electron.start();
   
    // Restart browser process 
    gulp.watch('main.js', function () {
    	console.log('restart');
    	electron.restart();
    });
   
    // Reload renderer process 
    gulp.watch(['index.js', 'index.html'], function () {
    	console.log('reload');
    	electron.reload();
    });
  });	
  ```

* 在electron应用内可以用`ctrl+r`刷新页面，在控制台里面可以用`f5`

  不过`electron-connect`使用的`reload`方法不能刷新页面