---
title: Github创建空白新分支备份数据
date: 2016-02-24 16:07:41
updated: 2017-03-13 16:07:41
categories:
- Git
tags:
- git
---

> 我经常把Github作为网盘使用,同步文件较小的文本数据,尤其是各种配置文件。

Workflow: [创建项目] ==> [确定主题:选择分支上传文件] ==> [新的分支上传新的内容] ==> ……

**使用方法:**
向分支提交一个初始的空commit，保证完全复位。

- 创建并切换新分支

```cmd
git branch <new_branch>
git checkout <new_branch>
git rm --cached -r . 
git clean -f -d
```

- 创建空的commit

```cmd
git commit --allow-empty -m "[empty] initial commit"
```

- 推送新分支

```cmd
git push origin <new_branch>
```
