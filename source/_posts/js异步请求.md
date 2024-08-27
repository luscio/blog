---
title: js异步请求
date: 2019/04/15 10:33
tags:
  - js
  - jquery
  - axios
categories:
  - js
---

## $.ajax异步请求demo

```js
$(function() {
  $.ajax({
    url: "http://localhost:3000/api/login",
    method: "POST",
    dataType: "json",
    data: {
      "user": "admin",
      "password": "123456",
    },
    headers: {
      "token": "123456789",
      "sign": "11",
    },
    beforeSend: function (jqXHR, settings) {}
  })
  .done(function (data, textStatus, jqXHR) {})
  .fail(function (jqXHR, textStatus, errorThrown) {})
  .always(function (data, textStatus, jqXHR) {
    // data|jqXHR, textStatus, jqXHR|errorThrown
  });
});
```

## axios异步请求

```js
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
  config.headers["platform"] = 1;
  config.headers["version"] = "1.0.0";
  config.headers["token"] = "";
  return config;
}, function (error) {
  return Promise.reject(error);
});

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
  return response.data;
}, function (error) {
  return Promise.reject(error);
});

// post请求
axios.post("http://localhost:3000/api/login", {
  user: "admin",
  password: "123456",
})
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```