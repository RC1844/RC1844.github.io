---
title: 清除所有的COMMITS
author: RC1844
date: 2021-02-28 20:00:00 +0800
categories: [git]
tags: [git] # TAG names should always be lowercase
pin: true
---

清除所有的 COMMITS（提交记录/历史版本）

commit 多了，有大量的多余数据，这时需要清理

过程挺麻烦，建议整合成一个 sh 脚本

```sh
git checkout --orphan latest_branch
git add -A
git commit -am "commit message"
git branch -D master
git branch -m master
git push -f origin master
git branch --set-upstream-to origin/master master
```

解释：

1. 将当前分支切换到 latest_branch
1. 把所有文件添加到当前分支
1. 设置 commit 注释
1. 删除主分支 master（此时只剩下 latest_branch）
1. 将 latest_branch 重命名为 master
1. 强制 push，用当前内容，冲刷掉 git 的内容（此处无法反悔）
1. 重新初始化分支结构（？不太清楚，反正缺少这一步就出错）

亲测这些命令是可以清除掉commits的，但是不能反悔，建议备份。

从<https://tetsai.net/556.html>处抄袭
