---
title: Git
date: 2017-08-15 19:01:48
tags: [流程]
---

平时常用命令

```shell

git init //初始化版本库，执行完后会发现目录下多一个.git的目录

git remote add origin git@github.com:wangyuanlitin/blogsource.git　//添加已有仓库

git clone git@github.com:wangyuanlitin/blogsource.git //从仓库clone代码

git branch dev //创建分支

git checkout branch //切换分支

git checkout project/a //撤销修改

git status //查看当前修改状态

git diff project/a //比较文件和未修改前的差异

git add . //添加到索引库

git commit -m "提交" //提交到本地库

git push //提交到远程库

git merge dev //dev分支合并到当前分支

git log //查看提交记录

git reset log-commit //回退到某个版本

```

接下来需要看的

```shell
git rebase //

```