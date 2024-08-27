---
title: composer常用命令
date: 2019/05/04 09:21
tags:
  - php
  - composer
categories:
  - composer
---

## 检查更新

```bash
composer selfupdate
```

## 切换中国镜像

```bash
composer config -g repo.packagist composer https://packagist.phpcomposer.com    # phpcomposer镜像         已停用
composer config -g repo.packagist composer https://packagist.laravel-china.org  # Laravel China镜像       已停用
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer  # 阿里云Composer全量镜像   建议使用
```

## 解除镜像并恢复到packagist官方源

```bash
composer config -g --unset repos.packagist
```

## 仅更新单个库

```bash
composer update foo/bar
```

## 全局安装

```bash
composer global require foo/bar
```

## 全局更新

```bash
composer global update
```

## composer autoload 自动加载性能优化

```bash
composer dump-autoload -o
```