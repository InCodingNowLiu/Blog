title: 阿里云ubuntu安装mysql并且开启远程连接
author: incodingnowliu
date: 2018-10-16 18:06:24
tags:
---
# 安装mql
## 安装数据库
```
apt-get install mysql-server mysql-client
```
输入完密码之后, 执行下面的命令进入数据库
```
mysql -u root -p
```
## mysql的配置文件
一般情况下在
```
/etc/mysql/my.cnf
```
当然也包含/etc/mysql/conf.d/* 文件下的所有配置文件, 也可以自定义

这里需要注释: bind-address 属性

然后重新mysql -u root -p进入数据库, 执行GRANT ALL PRIVILEGES ON *.* TO <user>@"%" IDENTIFIED BY '<password>' WITH GRANT OPTION;, <user>换成你想设置的用户名, <password>换成密码, 然后再执行FLUSH PRIVILEGES刷新权限. 最后重启一下数据库.
  
开启mysql
```
service mysql start 开启
```
停止mysql
```
service mysql stop 停止
```
重启mysql
```
service mysql restart 重启
```

### 阿里云服务器配置
mysql配置完成之后, 需要登陆阿里云控制台 -> 安全组 -> 配置3306(这里有下拉列表可直接选, 不用手动输入) 注意出入口都需要配置

检测是否开启成功:
```
mysql -h remote_ip_adresss -u xxxx -p
```




