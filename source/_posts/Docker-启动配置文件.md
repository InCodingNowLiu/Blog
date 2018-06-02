title: Docker 启动配置文件
author: incodingnowliu
date: 2018-06-02 18:44:51
tags:
---
# Docker 启动配置文件

```bash
sudo docker-compose -f docker-compose.sit.yml up --build 
```
```bash
sudo docker-compose -f docker-compose.sit.yml up --build -d(后台启动)
```

如果只是重启服务,只需

```bash
docker-compose up --build -d
```

使用autoScript 启动
```bash
bash deploy.sh 环境名称 git分支 是否打包
bash deploy.sh sit-plus master true
```

启动docker时候首先要启动base服务, 然后再启动对应环境的yml文件
