---
title: Vagrant 常用命令
date: 2020/12/04 16:52
tags:
  - vagrant
categories:
  - vagrant
---

## 常用命令

```bash
vagrant box list                       # 查看box列表
vagrant box add laravel/homestead      # 安装box
vagrant box remove laravel/homestead   # 删除box

vagrant up                             # 启动box
vagrant reload --provision             # 重新加载配置
vagrant ssh                            # ssh登录
vagrant halt                           # 关机
vagrant destroy                        # 销毁
vagrant destroy --force                # 销毁
```


## 添加本地box
新建metadata.json文件
```json
{
    "name": "laravel/homestead",  # 添加后的box名称
    "versions": [{
        "version": "2.1.0", # 版本号
        "providers": [{
            "name": "virtualbox",
            "url": "file://E:/downloads/Laravel-Homestead.box"  # 下载到本地的box
        }]
    }]
}
```

```bash
vagrant box add D:/metadata.json
```