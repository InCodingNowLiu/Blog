title: ESLint + VSCode实现AutoFix
author: incodingnowliu
date: 2018-06-02 16:45:24
tags:
---
# ESLint + VSCode实现AutoFix

package.json 添加eslint
 添加eslint的rules 
[eslint rules](https://eslint.org/docs/rules/)

VSCode 首选项--> 设置 ---> 工作区设置  添加
```bash
{
    "eslint.autoFixOnSave": true
}
```