---
title: mac安装brew
date: 2021/10/12 16:52
tags:
  - brew
categories:
  - brew
---

## 安装

自动脚本(全部国内地址)（在终端中复制粘贴回车下面脚本)
```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

## 卸载
```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/HomebrewUninstall.sh)"
```

## 常见错误去下方地址查看
https://gitee.com/cunkai/HomebrewCN/blob/master/error.md


### 常用命令
```bash
brew -v     # 查看brew版本
brew update # 更新brew版本

brew ls         # 本地软件库列表
brew search php # 查找软件（其中php为关键字）

brew install mysql@5.7      # 安装
brew uninstall mysql@5.7    # 卸载
brew install --cask firefox # 安装cask软件

brew services                   # 查看使用brew安装的服务列表
brew services start mysql@5.7   # 启动服务，并注册
brew services stop mysql@5.7    # 停止服务，并取消注册
brew services restart mysql@5.7 # 重启服务，并注册
brew services cleanup           # 清除已卸载应用的无用的配置
```
