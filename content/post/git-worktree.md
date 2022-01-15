---
title: "Git Worktree"
date: 2022-01-12T22:37:08+08:00
subtitle:    "不要再疯狂切分支啦"
description: "git worktree 的使用方式"
author: Zac
image:       "/img/git-worktree.jpg"
tags:        ["Git"]
categories:  ["Tech"]
---

在工作中，经常需要在开发需求的同时，还要兼顾修复 Bug，所以需要频繁的来回切换分支。

稍微懒人一点的办法，就是将仓库多克隆几个，比如 A 和 B，A 用于开发需求，B 用于 bugfix。这样虽然可以解决频繁切换分支的痛苦，但是还是显得有些「笨重」。比如 A 推送的代码，还需要在 B 中拉取。所以，要隆重推荐 Git 的一个指令：`git worktree`

## Git Worktree 能做什么？

它可以让一个 git 仓库拥有多个工作目录。它实际创建了一个连接到仓库的额外的工作目录。每一个创建出的工作目录都是一个和常规 git 仓库结构一样的一个伪仓库。它的`.git`文件实际上是引用了主仓库的`.git`文件。

也可以简单粗暴的理解为：通过指定的分支，创建一个新的工作目录，且这个目录能够和主仓库互相同步状态。在主仓库中拉取的代码，新的工作目录中可以直接看得到；新的工作目录提交、合并、推送的代码，在主仓库也无需拉取。

## 怎么用？

### 为已存在的分支建立工作目录

```bash
git worktree add <folder_path> <source_branch>
```

这种方式将不会再创建新的分支，而是为指定的分支创建工作目录

### 从指定的源分支迁出新分支，并创建工作目录

```bash
git worktree add -b <new_branch_name> <folder_path> <source_branch>
```

`<new_branch_name>`：新的分支名（基于 <source_branch>）

`<folder_path>`：指定新的工作区的目录位置

`<source_branch>`：源分支

### 查看已存在的工作区

```bash
git worktree list
或
git worktree list --porcelain
```

### 删除工作区

首先，在工作区内的工作完成后，将该工作目录（指文件夹）删除；然后，执行下方的指令：

```bash
git worktree prune
```

