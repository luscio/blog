---
title: centos安装gitlab
date: 2019/02/15 18:43
tags:
  - git
categories:
  - git
---

## 安装并配置必要的依赖项

```bash
sudo yum install -y curl policycoreutils-python openssh-server
sudo systemctl enable sshd
sudo systemctl start sshd
sudo firewall-cmd --permanent --add-service=http
sudo systemctl reload firewalld
### 安装Postfix以发送通知电子邮件
sudo yum install postfix
sudo systemctl enable postfix
sudo systemctl start postfix
```

## 配置yum源

```bash
vim /etc/yum.repos.d/gitlab-ce.repo
[gitlab-ce]
name=Gitlab CE Repository
baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el$releasever/
gpgcheck=0
enabled=1
```

## 更新本地yum缓存

```bash
sudo yum makecache
```

## 安装GitLab社区版

```bash
sudo yum install -y gitlab-ce          # 安装最新版
sudo yum install -y gitlab-ce-x.x.x    # 安装指定版本
```

## 配置域名并启动

```bash
vi /etc/gitlab/gitlab.rb
# 修改为自己的域名
external_url 'http://192.168.50.233:9090'
gitlab-ctl reconfigure
```

## GitLab常用命令

```bash
sudo gitlab-ctl start                             # 启动所有 gitlab 组件；
sudo gitlab-ctl stop                              # 停止所有 gitlab 组件；
sudo gitlab-ctl restart                           # 重启所有 gitlab 组件；
sudo gitlab-ctl status                            # 查看服务状态；
sudo gitlab-ctl reconfigure                       # 启动服务；
sudo vim /etc/gitlab/gitlab.rb                    # 修改默认的配置文件；
gitlab-rake gitlab:check SANITIZE=true --trace    # 检查gitlab；
sudo gitlab-ctl tail                              # 查看日志；
```