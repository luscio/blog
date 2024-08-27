---
title: git常用命令
date: 2019/03/19 15:23
tags:
  - git
categories:
  - git
---

## 忽略指定文件的改动

```bash
# 忽略 .htaccess 文件的改动
git update-index --assume-unchanged .htaccess

# 取消忽略
git update-index --no-assume-unchanged .htaccess

# 找出被忽略的文件
git ls-files -v | grep '^h\ '
```


## 配置换行符自动替换

```bash
git config --global core.autocrlf false
```