---
title: Navicat Premium 无限试用
date: 2023/01/09 11:11
tags:
  - Navicat
categories:
  - Navicat
---

# Navicat Premium 16 for mac

## 下载地址
https://download.navicat.com.cn/download/navicat160_premium_cs.dmg

# 无限试用脚本
```
/usr/libexec/PlistBuddy -c "Delete :91F6C435D172C8163E0689D3DAD3F3E9" ~/Library/Preferences/com.navicat.NavicatPremium.plist

/usr/libexec/PlistBuddy -c "Delete :B966DBD409B87EF577C9BBF3363E9614" ~/Library/Preferences/com.navicat.NavicatPremium.plist

rm -rf ~/Library/Application\ Support/PremiumSoft\ CyberTech/Navicat\ CC/Navicat\ Premium/.*
```
