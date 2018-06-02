title: shell 命令
author: incodingnowliu
date: 2018-06-02 18:59:26
tags:
---
# shell 命令

## scp 传输文件
```bash
scp 文件 root@目标服务器:/目标路径
```
```bash
scp root@服务器:/文件路径 目标路径
```

## mongodump

```bash
mongodump -h dbhost -d dbname -o dbdirectory
```
```bash
mongodump --host=xxxx --username=xxx --password=xxxx --db=xxx --collection=product
mongorestore --host xxxx  --username xxx --password xxx  --db xxx --collection product dump /xxx/product.bson
mongorestore --host xxx  --username xxx --password xxx  --db xxx --collection product   /xxx/xxx/dump/xxx/product.bson
```

