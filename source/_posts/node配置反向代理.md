---
title: node配置反向代理
date: 2019/04/12 18:43
tags:
  - node.js
categories:
  - node.js
---

## 安装依赖项

```js
cnpm install express
cnpm install http-proxy-middleware
```

## 新建proxy.js

```js
var express = require('express');
var app = express();
var proxy = require('http-proxy-middleware');

var port = '3000';
var proxyTarget = 'https://www.xxx.com';

app.use('/', function (request, response) {
  response.send('Hello World');
});

app.use('/api/*', proxy({
  target: proxyTarget,
  changeOrigin: true,
  ws: true,
  pathRewrite: {
    '^/api': ''
  }
}));

app.listen(port, function () {
  console.log("server is listen at http://localhost:%s", port);
});
```

## 启动服务

```js
node proxy.js
```