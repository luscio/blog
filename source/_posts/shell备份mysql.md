---
title: shell备份mysql
date: 2019/06/01 09:53
tags:
  - linux
---

## 新建shell脚本
```bash
#!/bin/bash
DB_USER="root"                             # mysql用户名
DB_PASS="root"                             # mysql密码
DB_HOST="127.0.0.1"                        # mysql主机地址
DB_PORT="3306"                             # mysql端口
DB_NAME="test"                             # mysql需要备份的数据库名称
BACK_DIR="/home/backup/mysql"              # 备份文件存放的位置
BACK_FILE=${DB_NAME}_`date +%Y%m%d`.sql    # 备份文件名称
BIN_DIR="/usr/bin"
# 备份
${BIN_DIR}/mysqldump --opt -u${DB_USER} -p${DB_PASS} -h${DB_HOST} -P${DB_PORT} ${DB_NAME} > ${BACK_DIR}/${BACK_FILE}
# 删除30天前的备份
OLD_BACK_FILE=${BACK_DIR}/${DB_NAME}_`date -d "30 days ago" +%Y%m%d`.sql
rm -rf ${OLD_FILE}
```

## shell脚本可执行权限
```bash
chmod +x mysql.sh
```

## crontab定时任务执行脚本
```bash
00 01 * * * /home/backup/mysql.sh     # 每天凌晨1点备份
```

## crontab基本格式
```bash
*    *    *    *    *    command
分   时   日   月   周    命令

05 * * * * command     # 每5分钟执行
30 00 * * * command    # 每天凌晨0点30分钟执行
```