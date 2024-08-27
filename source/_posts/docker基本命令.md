---
title: docker基本命令
date: 2019/05/17 09:21
tags:
  - docker
categories:
  - docker
---

## 镜像常用命令

```bash
docker images                                                                         # 查看所有镜像
docker rmi $(docker images -q)                                                        # 删除所有镜像
docker rmi <image id>                                                                 # 删除指定镜像
docker pull centos:7                                                                  # 拉取镜像
docker tag <image id> 仓库:标签                                                        # 镜像重命名
```

## 容器常用命令

```bash
docker ps                                                                             # 查看正在运行的容器
docker ps -a                                                                          # 查看所有容器
docker kill $(docker ps -a -q)                                                        # 杀死所有正在运行的容器
docker rm $(docker ps -a -q)                                                          # 删除所有已经停止的容器
docker run -it -p 22:22 -p 80:80 -p 443:443 -p 3306:3306 <image id> /bin/bash         # 创建容器
docker stop <container id>                                                            # 停止容器
docker start <container id>                                                           # 启动容器
docker exec -it <container id> /bin/bash                                              # 进入容器
docker commit <container id> <image name>                                             # 将容器打包成镜像
```