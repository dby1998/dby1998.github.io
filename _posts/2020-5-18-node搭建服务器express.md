---
layout: post
title: "node 搭建服务器"
date: 2020-05-18 
description: "HEXO配置，HEXO+Github，搭建自己的博客"

tag: 博客 
---   
## 一、Express本地安装

uniApp官网地址  https://uniapp.dcloud.io/

[官方IDE下载地址] https://uniapp.dcloud.io/quickstart

appid https://mp.weixin.qq.com/cgi-bin/loginpage?t=wxm2-login&lang=zh_CN



清除CSS样式 https://www.npmjs.com/package/reset-css



图标字体 http://at.alicdn.com/t/font_760782_hmtvl7u64w9.css



grid插件网址 https://ext.dcloud.net.cn/plugin?id=27

新建一个空白文件夹，如 `backend` ，先安装express 然后执行：

```js
npm i express --save-dev
npm init -y
```

## 二、返回数据给前端

得到 `package.json` 与 `node_modules` 之后，将 `houseSource.json` 放在文件夹根目录，并在根目录新建 `index.js` 文件，在其中写入：

```js
// 引入依赖 express 直接粘贴笔记上代码
const express = require("express");// 什么是const，就是用来声明常量的
const fs = require("fs");// fs模块是nodeJs中自带的模块，用于读取文件
const app = express();//express 自执行一次 并赋值给app
//设置跨域访问,这个跨域加上去就可以解决在浏览器上看页面了
app.all('*', function(req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
    res.header("X-Powered-By",' 3.2.1')
    res.header("Content-Type", "application/json;charset=utf-8");
    next();
});
// 监听路由
app.get('/mydata', function(req, res){
   // request代表请求，resspond代表响应
   // fs.readFile(url,callback(err,data)) 读取文件
   fs.readFile('./houseSource.json',function(err,data){
	  if(err) return;
	  //console.log(data) 
	   //console.log(JSON.parse(data)) 
	  res.send(JSON.parse(data)); //这样，去浏览器输入 `http://localhost:8020` ，即可看到数据。
   })
});
// 测试、监听端口号
app.listen(8002, ()=>{
    console.log('Server is running at http://localhost:8002');
})
```

这样，去浏览器输入 `http://localhost:8020/mydata` ，即可看到数据。