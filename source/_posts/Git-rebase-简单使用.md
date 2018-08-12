title: Git rebase 简单使用
author: incodingnowliu
date: 2018-08-12 19:17:57
tags:
---
# Git rebase 常规使用详解

## git pull

git pull = git fetch + git merge
git pull --rebase = git fetch + git rebase 
```bash
git pull --rebase
```

## rebase版merge分支
日常工作中我们需要将我们的develop 分支merge到master上面(当然严格来说要提pull requestQAQ), 这里只是举个范例

1.拉取到最新代码
```bash
git checkout master
git pull --rebase
```
2.将develop分支代码rebase + merge 到master分支
```bash
git rebase develop
git push origin master
```

## rebase 冲突解决
日常开发中多个人会同事修改同一个文件, 这样就避免不了冲突, 但是rebase 解决冲突其实很简单

```bash
git rebase develop
```
rebase 的时候出现下面冲突
```bash
<<<<<<< HEAD
rebase first commit
rebase test2
=======
rebase second commit
>>>>>>> rebase commit 2
```

此时我们只需要先解决冲突,
```bash
rebase first commit
rebase test2
rebase second commit
```
然后
```bash
git add .
git rebase --continue
git push
```
成功将我们的develop分支完美rebase + merge到master上面

效果如下图, 是不是治愈了你的强迫症QAQ
![upload successful](/images/pasted-0.png)

之前的你的分支可能是这样
![upload successful](/images/pasted-1.png)

当然你也可以skip 恢复到rebase 之前的状态
```bash
git rebase --skip
```

以上是楼主花了一点时间研究的成果, 如果有什么错误的地方, 欢迎大家提意见


