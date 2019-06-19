---
title: git cheatsheet
date: 2019-06-19 09:16:38
tags:
---

# 配置
设置用户名：
```
git config --global user.name "[firstname lastname]"
```
设置用户邮箱：
```
git config --global user.email "[valid-email]"
```
设置git命令输出为彩色：
```
git config --global color.ui auto
```

# 本地修改
把当前分支中未提交的修改移动到其他分支：
```
git stash
git checkout branch2
git stash pop
```
修改上次提交的author：
```
git commit --amend --author "user <user@gmail.com>
```
修改上次提交的日期：
```
git commit --amend --date="$(date -d '2019-06-03 12:19:01' -R)"
```

# 合并与重置（Rebase）
合并提交：
```
git rebase -i <commit-just-before-first>

# 把上面的内容替换为下面的内容：
# 原内容：
pick <commit_id>
pick <commit_id2>
pick <commit_id3>

# 替换为：
pick <commit_id>
squash <commit_id2>
squash <commit_id3>
```

# 撤销
将HEAD重置到上一次提交的版本，并将之后的修改标记为未添加到缓存区的修改：
```
git reset <commit>
```
将HEAD重置到当前提交的版本，并将之后的修改标记为未添加到缓存区的修改：
```
git rebase [-i] --root <commit>
```