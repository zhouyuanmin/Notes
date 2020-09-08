---
title: Git
date: 2020-02-23 01:26:32
tags:
- Git
categories:
- Git
---
#### 查看不同

```shell
git diff
```

#### 回退

```shell
git reset --hard HEAD^ 
# HEAD 表示当前版本，^和^^, 或者直接是版本id号
```

```shell
git reset --hard 1094a
# git reset --hard commit_id
```

#### 查看日志

```shell
git log [--pretty=oneline]
# git log --graph命令可以看到分支合并图
git log --graph --pretty=oneline --abbrev-commit
```

#### 查看历史命令

```shell
git reflog
```

#### 查看工作区和版本库里面最新版本的区别

```shell 
git diff HEAD -- readme.txt
```

#### 丢弃修改

```shell
git checkout -- readme.txt
# git checkout -- file
# 只能丢弃未add的
```

```shell
# 如果已经add了，则需要使用git reset HEAD <file>命令，再调用git checkout -- readme.txt
git reset HEAD readme.txt # 撤销add的文件
git checkout -- readme.txt
```

#### 删除文件

```shell
# 先删除文件，再使用命令删除版本库里面的文件，并且再commit
git rm test.txt
git commit -m "remove test.txt"
# 如果误删则git checkout -- test.txt还原
git checkout -- test.txt
```

#### 关联仓库

```shell
git remote add origin "url"
# 把本地库的所有内容推送到远程库上
git push -u origin master
# 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
```

#### 推送代码

```shell
git push origin master
# master 是仓库
```

#### 创建分支

```shell
# 创建+切换分支
git checkout -b dev
# 创建分支
git branch <name>
```

#### 切换分支

```shell
git checkout <name>
```

#### 查看当前分支

```shell
# 会列出所有分支，当前分支前面会标一个*号
git branch
```

#### 合并分支

```shell
# 分支走在了主分支前面，并没有变成两个不同分支
git merge dev
# Fast-forward "快进模式"
# 切换回主分支，再合并（重点理解为什么）
```

#### 删除分支

```shell
git branch -d dev # 和查看当前分支相同
git branch -D feature-vulcan # 强制删除未合并的分支
```

#### 禁用Fast-forward ："快进模式"

```shell
git merge --no-ff -m "merge with no-ff" dev
# 因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。
```

#### 保存现场

```shell
git stash
# 查看保存的现场
git stash list
# 恢复现场方法一
git stash apply
git stash drop
git stash apply stash@{0} # 好像没什么区别
# 恢复现场方法二
git stash pop # 常用
```

#### 查看远程库信息

```shell
git remote [-v]
# 加上-v，信息更详细
```

#### 分支推送原则

- `master`分支是主分支，因此要时刻与远程同步；
- `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- `bug`分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
- `feature`分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

#### 拷贝远程分支到本地（远程合作常用）

```shell
git checkout -b dev origin/dev
# 设置dev和origin/dev的链接
git branch --set-upstream-to=origin/dev dev
# git branch --set-upstream-to <branch-name> origin/<branch-name>
git pull # 下载更新 
```

#### 特殊命令（多人合作）

```shell
git rebase
# rebase操作可以把本地未push的分叉提交历史整理成直线；
# rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。
```

#### 创建标签

```shell
git tag v1.0
# git tag <name>
```

#### 对commit打标签

```shell
git tag v0.9 f52c633  # id号
```

#### 查看标签

```shell
git tag # 查看标签
git show v0.9  # git show <tagname>查看标签信息
# 注意，标签不是按时间顺序列出，而是按字母排序的。

git tag -a v0.1 -m "version 0.1 released" 1094adb
# 还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字

# 标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签
```

#### 标签操作

```shell
# 删除标签
git tag -d v0.1  # 命令git tag -d <tagname>可以删除一个本地标签；
# git push origin <tagname> 推送标签到远程库
git push origin v1.0 # 某一个
git push origin --tags  # 所有标签

# 如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除
git tag -d v0.9
git push origin :refs/tags/v0.9
# 命令git push origin :refs/tags/<tagname>可以删除一个远程标签。
```

#### 技巧

```shell
# .gitignore文件（不想被git提示的，文件名写入其中即可）
git check-ignore # 查找错误规则
git add -f App.class # 强制添加
```

```shell
# 别名
git config --global alias.st status # git status改为git st (即status改为st)
# 丧心病狂
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
# 配置文件cat .git/config ,直接修改[alias]即可还原
```

