---
title: vmware+centos7+bt搭建本地php开发环境
date: 2019/09/24 10:37
tags:
  - vmware
categories:
  - vmware
---

## 安装vmware

## 安装centos7，配置共享目录

## 安装vmtools
```bash
yum -y install perl gcc gcc-c++ make cmake kernel kernel-headers kernel-devel net-tools  # 安装依赖包
mkdir -p /mnt/cdrom                                                                      # 创建CD-ROM挂载目录
mount -t auto /dev/cdrom /mnt/cdrom                                                      # 将CD-ROM挂载到指定目录
cp /mnt/cdrom/VMwareTools-10.0.5-3228253.tar.gz /home                                    # 拷贝安装包到home目录
umount /dev/cdrom                                                                        # 解除挂载
tar -zxvf VMwareTools-10.0.5-3228253.tar.gz                                              # 解压安装包
cd vmware-tools-distrib/                                                                 # 进入安装包目录
./vmware-install.pl                                                                      # 安装
```

## 配置目录映射，实现虚拟机与客户机文件同步
```bash
yum install open-vm-tools open-vm-tools-desktop                                          # 安装工具
vmware-hgfsclient                                                                        # 查看共享的目录
vmhgfs-fuse .host:/ /mnt/hgfs                                                            # 挂载目录
vi /etc/fstab                                                                            # 开机自动挂载
.host:/ /mnt/hgfs fuse.vmhgfs-fuse allow_other,defaults 0 0
mount -a                                                                                 # 测试配置是否正确
```

## 安装宝塔面板
```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```