title: iOS 生成文档
author: incodingnowliu
date: 2018-06-02 20:22:39
tags:
---
# iOS 生成文档

文档

```bash
1. appledoc --output ./doc --project-name delegate  --project-company "com.pwcsdc.AIAMobile" --company-id "com.pwcsdc.AIAMobile" ./  

```

```bash
appledoc -o ./doc --project-name “AIAMobile_Swift” --project-company “pwcsdc.com” . 
```

```bash
appledoc --project-name AIAMobile --project-company “xxx” --company-id com.xxx [--output ./Users/xxx]  [includeFilePathOrFile] [--ignore excludeFilePathOrFile] .
```

Appledoc 生成xcode 注释文档

jazzy的使用
```bash
jazzy --min-acl internal
```