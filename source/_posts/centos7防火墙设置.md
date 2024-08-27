---
title: centos7防火墙设置
date: 2019/03/29 16:43
tags:
  - linux
categories:
  - centos7防火墙
---

## 禁用/停止自带的firewalld服务

```bash
firewall-cmd --state                   # 查看默认防火墙状态，关闭后显示not running，开启后显示running
yum install -y firewalld               # 安装firewalld
systemctl start firewalld.service      # 开启防火墙
systemctl stop firewalld.service       # 关闭防火墙
systemctl enable firewalld.service     # 允许firewall开机启动
systemctl disable firewalld.service    # 禁止firewall开机启动
# 如出现"Failed to start firewalld.service: Unit is masked"错误，执行"systemctl unmask firewalld.service"
```

## 安装iptable iptable-service

```bash
service iptables status          # 先检查是否安装了iptables
yum install -y iptables          # 安装iptables
yum update iptables              # 升级iptables
yum install iptables-services    # 安装iptables-services
```

## 设置现有规则

```bash
iptables -L -n                                                       # 查看iptables现有规则
iptables -P INPUT ACCEPT                                             # 允许所有
iptables -F                                                          # 清空所有默认规则
iptables -X                                                          # 清空所有自定义规则
iptables -Z                                                          # 所有计数器归0
iptables -A INPUT -i lo -j ACCEPT                                    # 允许来自于lo接口的数据包(本地访问)
iptables -A INPUT -p tcp --dport 22 -j ACCEPT                        # 开放22端口(SSH)
iptables -A INPUT -p tcp --dport 21 -j ACCEPT                        # 开放21端口(FTP)
iptables -A INPUT -p tcp --dport 80 -j ACCEPT                        # 开放80端口(HTTP)
iptables -A INPUT -p tcp --dport 443 -j ACCEPT                       # 开放443端口(HTTPS)
iptables -A INPUT -p icmp --icmp-type 8 -j ACCEPT                    # 允许ping
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT     # 允许接受本机请求之后的返回数据RELATED,是为FTP设置的
iptables -P INPUT DROP                                               # 其他入站一律丢弃
iptables -P OUTPUT ACCEPT                                            # 所有出站一律允许
iptables -P FORWARD DROP                                             # 所有转发一律丢弃
```

## 其他规则设定

```bash
iptables -A INPUT -p tcp -s 45.96.174.68 -j ACCEPT    # 如果要添加内网ip信任（接受其所有TCP请求）
iptables -I INPUT -s ***.***.***.*** -j DROP          # 要封停一个IP，使用下面这条命令：
iptables -D INPUT -s ***.***.***.*** -j DROP          # 要解封一个IP，使用下面这条命令:
```

## 保存规则设定

```bash
service iptables save    # 保存上述规则
```

## 开启iptables服务

```bash
systemctl disable iptables.service   # 禁用iptables服务
systemctl enable iptables.service    # 注册iptables服务
systemctl start iptables.service     # 开启服务
systemctl stop iptables.service      # 停止服务
systemctl status iptables.service    # 查看状态
```

## 映射端口（如将mysql默认的3306端口映射成1306对外提供服务）

```bash
iptables -t mangle -I PREROUTING -p tcp --dport 1306 -j MARK --set-mark 883306
iptables -t nat -I PREROUTING -p tcp --dport 1306 -j REDIRECT --to-ports 3306
iptables -I INPUT -p tcp --dport 3306 -m mark --mark 883306 -j ACCEPT
```