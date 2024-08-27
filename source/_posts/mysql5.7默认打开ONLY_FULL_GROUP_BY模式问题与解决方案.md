---
title: MySQL5.7默认打开ONLY_FULL_GROUP_BY模式问题与解决方案
date: 2019/04/17 14:57
tags:
  - mysql
categories:
  - mysql
---

## 解决方案一

* 查看当前数据库的sql_mode属性值

```sql
select @@sql_mode
```

* 去掉ONLY_FULL_GROUP_BY, 重新赋值

```sql
set sql_mode = (select replace(@@sql_mode, 'ONLY_FULL_GROUP_BY', ''));
```

* 但是这种方式设置的只是当前会话中的sql_model, 服务器重启后会失效。设置永久生效模式需修改mysql配置文件

## 解决方案二

* MySQL有any_value(field)函数, 他主要的作用就是抑制ONLY_FULL_GROUP_BY值被拒绝
* 官方有介绍, 地址：<https://dev.mysql.com/doc/refman/5.7/en/miscellaneous-functions.html#function_any-value>
* 我们可以把select语句中查询的属性(除聚合函数所需的参数外), 全部放入any_value(field)函数中
* 这样sql语句不管是在ONLY_FULL_GROUP_BY模式关闭状态还是在开启模式都可以正常执行, 不被mysql拒绝
* 例如:

```sql
SELECT
  `name`,
  any_value ( `sex` )
FROM
  `test_table`
GROUP BY
  `name`
```