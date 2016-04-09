---
title: sublime text 常用插件
date: 2016-04-09 03:16:34
tags: [工具]
---

sublime text之所以强大其中一个原因就是强大的插件支持，具体如何安装Package Control请参考官网说明（https://packagecontrol.io/installation）。

此文默认读者拥有一定sublime text插件安装经验，只介绍我认为实用的一些插件。

# 语法检测

## SublimeLinter

只是一个管理工具

## SublimeLinter-jshint 

SublimeLinter的JavaScript检测的扩展插件

依赖jshint，需要用node.js全局安装：

```bash
$ node i jshint -gd
```



jshint配置自定义依赖父深度为3的文件夹下.jshintrc文件的配置

{
  "asi": true,
  "curly": true,
  "immed": true,
  "newcap": true,
  "noarg": true,
  "sub": true,
  "boss": true,
  "eqnull": true,
  "trailing": true,
  "undef": true,
  "browser": true,
  "jquery": true,
  "globals": {
    "angular": false,
    // For Jasmine
    "after"      : false,
    "afterEach"  : false,
    "before"     : false,
    "beforeEach" : false,
    "describe"   : false,
    "expect"     : false,
    "jasmine"    : false,
    "module"     : false,
    "spyOn"      : false,
    "inject"     : false,
    "it"         : false
  }
}

深度可言在SublimeLinter用户设置中设置"rc_search_limit": 3。

新建一个无文件名文件的方法，比如新建".jshintrc"，就直接新建".jshintrc."，多了个"."就可以了

## SublimeLinter-contrib-eslint

JS/ES6/JSX等语法检测插件，较为强大

依赖：eslint、babel-eslint，需要npm全局安装

.eslintrc文件例子：

{
"env": {
"browser": true,
"node": true,
"es6": true
},
"parser": "babel-eslint",
"ecmaFeatures": {
"jsx": true
},
"rules": {
"semi": [2, "always"],
"quotes": [2, "single"]
}
}