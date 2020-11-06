---
layout: post
title:  "git"
date:   2018-08-28 14:46:23 +0800
categories: git
---
### git 命令
-------------

#### *    git commit -am ####

当修改已经通过`git add <change file>`将其添加到stage，可以通过`git commit -m "<message>"`为这所有已经进入stage的改变添加一个commit信息。什么是在stage中？看下面

    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

    modified:   _posts/2018-08-28-git_ommand.md
 
如果你的文件之前已经提交过，但这次的改动还没有进stage，如下：


    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   _posts/2018-08-28-git_ommand.md

	no changes added to commit (use "git add" and/or "git commit -a")


可以直接使用`git commit -am "<message>"`，将所有修改，但未进stage的改动加入stage，并记录commit信息。(某种程度上相当于`git add`和`git commit -m`的组合技，前提是被改动文件已经是tracked)


#### git remote -v 查看远程路径
