---
title: 配置MySQL远程连接
date: 2019/03/19 10:18:25
tags:
  - mysql
categories:
  - mysql
---

## 云主机安全组端口开放3306端口

## 打开iptables 3306端口

```bash
# centos
iptables -I INPUT 4 -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
service iptables save # 保存iptables规则

# ubuntu
iptables -I INPUT 4 -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
iptables-save > /etc/iptables.up.rules # 保存iptables规则
```

## 数据库授权

```bash
# MySQL8.0版本
mysql -uroot -p
MySQL [(none)]> create user db_user@'%' identified by 'db_pass'; # 创建用户
MySQL [(none)]> grant all privileges on db_name.* to db_user@'%' with grant option; # 授权
MySQL [(none)]> exit; # 退出数据库控制台，特别注意有分号

# 其余MySQL版本
mysql -uroot -p
MySQL [(none)]> grant all privileges on db_name.* to db_user@'%' identified by 'db_pass'; # 授权
MySQL [(none)]> flush privileges;
MySQL [(none)]> exit; # 退出数据库控制台，特别注意有分号
```

### 撤销授权

```bash
mysql -uroot -p
MySQL [(none)]> revoke all on *.* from db_user@localhost; # 撤销授权
MySQL [(none)]> exit; # 退出数据库控制台，特别注意有分号
```