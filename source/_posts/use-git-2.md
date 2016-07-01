---
title: Git使用笔记(二)
date: 2016-06-30 18:00:55
categories: Git
tags: 
    - Git
---
# 远程仓库的使用

## 查看远程仓库
git remote

显示链接地址
git remote -v

显示远程仓库详细信息(当前分支，远程分支，本地分支)
git remote show origin

## 添加远程仓库
git remote add pb https://github.com/paulboone/ticgit

## 从远程仓库中抓取与拉取

不会自动合并(如果有分支，他只会创建origin/new，不会再本地创建副本)
git fetch [remote-name]

可以合并到当前分支(https://git-scm.com/book/zh/v2/Git-分支-远程分支)
git merge origin/serverfix

也可以创建一个副本分支，在上面工作
git checkout -b serverfix origin/serverfix

自动合并
git pull

推送到远程仓库
git push origin master

重名了远程名称
git remote rename pb paul

删除远程
git remote rm paul

更改origin为test
git clone -o test https://github.com/lifengsofts/TestMvp.git

# 标签

## 创建标签

查看所有标签
git tag

git tag -l 'v1.8.5*'

## 创建标签

Git 使用两种主要类型的标签：轻量标签（lightweight）与附注标签（annotated）。

轻量标签：很像一个不会改变的分支 - 它只是一个特定提交的引用
附注标签：是存储在 Git 数据库中的一个完整对象。 它们是可以被校验的；其中包含打标签者的名字、电子邮件地址、日期时间；还有一个标签信息；并且可以使用 GNU Privacy Guard （GPG）签名与验证。 

**通常建议创建附注标签**

git tag -a v1.4 -m 'my version 1.4'

git tag -a v1.4

创建轻量标签
git tag v1.0.1

查看这个标签的提交信息
git show v1.4

给过去的提交添加标签
git tag v1.0.2 bceebb55[47da220c63eecc6a9793486c387b8475]

push标签
git push origin v1.5

git push origin --tags

检出标签(比如：某个tag的出现bug，需要在当前bug创建一个分支)
git checkout -b fix-v2.0.0 v2.0.0

检出远程分支
 git checkout --track origin/serverfix

等同于上面
git checkout -b serverfix origin/serverfix

# 别名

查看配置
git config --list

git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status

# 分支

## 创建分支

git branch test1

在当前分支上创建分支，并切换到新分支
git checkout -b test2

check出远程分支
git checkout -b test2 origin/test2

## 查看分支

git branch

显示远程和本地分支
git branch -a

查看各个分支当前所指的对象
git log --oneline --decorate

分支切换
git checkout test2

查看分叉历史
git log --oneline --decorate --graph --all

查看远程分支，包括远程tag
git ls-remote 

## 合并分支

先切换到要合并到的分支

比如：要讲fix-255分支合并到master

git checkout master

先拉去远程的内容，因为在这其他有可能其他更改了
git pull

快速合并
git merge fix-255

git merge --no-ff fix-255

查看每个分支最后一次提交
git branch -v

查看问未合并分支(实现，一直在合并的分支)
https://git-scm.com/book/zh/v2/Git-分支-分支管理

## 推送分支

git push origin serverfix

将本地分支server fix推送到远程为awesomebranch
git push origin serverfix:awesomebranch

## 删除远程分支

删除本地分支
git branch -d fix1

删除服务端分支
git push origin --delete serverfix

## 上游分支

https://git-scm.com/book/zh/v2/Git-分支-远程分支

查看所有跟踪分支
git branch -vv

先获取，在查看
git fetch --all
git branch -vv
