---
title: es6转es5
date: 2019/04/15 13:35
tags:
  - js
categories:
  - js
---

## 新建.babelrc

```json
{
    "presets": [
        "es2015"
    ],
    "plugins": []
}
```

## 新建package.json

```json
{
  "devDependencies": {
    "babel-cli": "^6.26.0",
    "babel-preset-es2015": "^6.24.1"
  },
  "scripts": {
    "build": "babel src -d dist"
  }
}
```

## 将src目录的js代码转换成es2015

```bash
cnpm run build
```