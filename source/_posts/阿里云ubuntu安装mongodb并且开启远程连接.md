title: 阿里云ubuntu安装mongodb并且开启远程连接
author: incodingnowliu
date: 2018-10-16 13:37:26
tags:
---
# ubuntu 安装mongodb

下载
```
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1404-3.4.2.tgz
```

解压
```
tar zxf mongodb-linux-x86_64-ubuntu1404-3.4.2.tgz
```
安装
```
将mongodb移动到/usr/local/server/mongdb文件夹
```

```
mv mongodb-linux-x86_64-ubuntu1404-3.4.2 /usr/local/mongodb
```
创建数据库文件夹与日志文件, 需要根据config file相match
```
mkdir /usr/local/mongodb/data
touch /usr/local/mongodb/logs
```
设置开机自启动
将mongodb启动项目追加入rc.local保证mongodb在服务器开机时启动

```
echo "/usr/local/mongodb/bin/mongod --dbpath=/usr/local/mongodb/data –logpath=/usr/local/mongodb/logs –logappend  --auth –port=27017" >> /etc/rc.local

```
启动mongodb
下面这个是需要权限的登录方式, 用户连接需要用户名和密码

```
/usr/local/mongodb/bin/mongod --dbpath=/usr/local/mongodb/data --logpath=/usr/local/mongodb/logs --logappend  --auth  --port=27017 --fork
```

这个是不需要密码的
```
/usr/local/mongodb/bin/mongod --dbpath=/usr/local/mongodb/data --logpath=/usr/local/mongodb/logs --logappend  --port=27017 --fork
```
参数解释
```
--dbpath 数据库路径(数据文件)
--logpath 日志文件路径
--master 指定为主机器
--slave 指定为从机器
--source 指定主机器的IP地址
--pologSize 指定日志文件大小不超过64M.因为resync是非常操作量大且耗时，最好通过设置一个足够大的oplogSize来避免resync(默认的 oplog大小是空闲磁盘大小的5%)。
--logappend 日志文件末尾添加
--port 启用端口号
--fork 在后台运行
--only 指定只复制哪一个数据库
--slavedelay 指从复制检测的时间间隔
--auth 是否需要验证权限登录(用户名和密码)
 
 
-h [ --help ]             show this usage information
--version                 show version information
-f [ --config ] arg       configuration file specifying additional options
--port arg                specify port number
--bind_ip arg             local ip address to bind listener - all local ips
                           bound by default
-v [ --verbose ]          be more verbose (include multiple times for more
                           verbosity e.g. -vvvvv)
--dbpath arg (=/data/db/) directory for datafiles    指定数据存放目录
--quiet                   quieter output   静默模式
--logpath arg             file to send all output to instead of stdout   指定日志存放目录
--logappend               appnd to logpath instead of over-writing 指定日志是以追加还是以覆盖的方式写入日志文件
--fork                    fork server process   以创建子进程的方式运行
--cpu                     periodically show cpu and iowait utilization 周期性的显示cpu和io的使用情况
--noauth                  run without security 无认证模式运行
--auth                    run with security 认证模式运行
--objcheck                inspect client data for validity on receipt 检查客户端输入数据的有效性检查
--quota                   enable db quota management   开始数据库配额的管理
--quotaFiles arg          number of files allower per db, requires --quota 规定每个数据库允许的文件数
--appsrvpath arg          root directory for the babble app server 
--nocursors               diagnostic/debugging option 调试诊断选项
--nohints                 ignore query hints 忽略查询命中率
--nohttpinterface         disable http interface 关闭http接口，默认是28017
--noscripting             disable scripting engine 关闭脚本引擎
--noprealloc              disable data file preallocation 关闭数据库文件大小预分配
--smallfiles              use a smaller default file size 使用较小的默认文件大小
--nssize arg (=16)        .ns file size (in MB) for new databases 新数据库ns文件的默认大小
--diaglog arg             0=off 1=W 2=R 3=both 7=W+some reads 提供的方式，是只读，只写，还是读写都行，还是主要写+部分的读模式
--sysinfo                 print some diagnostic system information 打印系统诊断信息
--upgrade                 upgrade db if needed 如果需要就更新数据库
--repair                  run repair on all dbs 修复所有的数据库
--notablescan             do not allow table scans 不运行表扫描
--syncdelay arg (=60)     seconds between disk syncs (0 for never) 系统同步刷新磁盘的时间，默认是60s
 
Replication options:
--master              master mode 主复制模式
--slave               slave mode 从复制模式
--source arg          when slave: specify master as <server:port> 当为从时，指定主的地址和端口
--only arg            when slave: specify a single database to replicate 当为从时，指定需要从主复制的单一库
--pairwith arg        address of server to pair with
--arbiter arg         address of arbiter server 仲裁服务器，在主主中和pair中用到
--autoresync          automatically resync if slave data is stale 自动同步从的数据
--oplogSize arg       size limit (in MB) for op log 指定操作日志的大小
--opIdMem arg         size limit (in bytes) for in memory storage of op ids指定存储操作日志的内存大小
 
Sharding options:
--configsvr           declare this is a config db of a cluster 指定shard中的配置服务器
--shardsvr            declare this is a shard db of a cluster 指定shard服务器
```
进入数据库的CLI管理界面
cd到mongodb目录下的bin文件夹，执行命令./mongo
图片描述

若数据库出现如不能连上，则是一个data目录下的mongod.lock文件的问题，可以用如下的修复的命令，
```
mongod --repair
```
这个安装过程是参考了其他人的步骤, 详细见: https://segmentfault.com/a/1190000008554757

# 好mongod之后, 避免不了暂停操作
#使用MongoDB的shell客户端进行关闭
```
$ mongo
> use admin
> db.shutdownServer()
```
#Linux发送命令
```
$ ps -A |grep mongod #查找mongod对应的PID
$ kill -2 PID #发送关闭命令
```


# 阿里云服务器开启端口
进入阿里云云服务控制台 -> 安全组 -> 出入口打开27017端口(根据提示) -> 将mongo配置文件中的bind_ip改为0.0.0.0(127.0.0.1只能内部访问) -> 使用mongo命令或者可视化工具就可以从外部连接服务器的mongo了




