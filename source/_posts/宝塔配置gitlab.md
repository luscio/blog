---
title: 配置gitlab
date: 2019/11/04 10:42
tags:
  - gitlab
categories:
  - gitlab
---

# 配置邮件发送

* 编辑/etc/gitlab/gitlab.rb（加到文件最后面就好了）
```
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = 'smtp.exmail.qq.com'
gitlab_rails['smtp_port'] = 465
gitlab_rails['smtp_user_name'] = 'admin@1234xiss.com'
gitlab_rails['smtp_password'] = '************'
gitlab_rails['smtp_authentication'] = 'login'
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_tls'] = true
gitlab_rails['gitlab_email_from'] = 'admin@1234xiss.com'
```

* 有的教程可能会说去改/opt/gitlab/etc/gitlab.rb，是错的，一切以官网文档为准。

* 重新配置gitlab  
gitlab-ctl reconfigure


* 通过命令行测试邮件是否发送成功  
gitlab-rails console  
Notify.test_email('**@qq.com', 'Message Subject', 'Message Hello Gitlab').deliver_now



## 宝塔上GitLab修改配置后nginx无法启动，查找原因
```bash
gitlab-ctl tail
```

## 错误信息
```
```


## 解决办法
宝塔为了防止nginx冲突, 把gitlab的nginx启动文件名改成了gitlab-web, 但有个配置文件没改造成的。
修改nginx启动文件
```
vi /opt/gitlab/sv/nginx/run
把
exec chpst -P /opt/gitlab/embedded/sbin/nginx -p /var/opt/gitlab/nginx
改为
exec chpst -P /opt/gitlab/embedded/sbin/gitlab-web -p /var/opt/gitlab/nginx
```

## 重启 gitlab 的 nginx 服务