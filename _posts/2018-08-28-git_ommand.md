---
layout: post
title:  "git"
date:   2018-08-28 14:46:23 +0800
categories: git
---
### git 命令
-------------


当修改已经通过`git add <change file>`将其添加到stage，可以通过`git commit -m "<message>"`为这所有已经进入stage的改变添加一个commit信息。什么是在stage中？看下面



如果你的文件之前已经提交过，但这次的改动还没有进stage，如下：
 

可以直接使用`git commit -am "<message>"`，将所有修改，但未进stage的改动加入stage，并记录commit信息。(某种程度上相当于`git add`和`git commit -m`的组合技，前提是被改动文件已经是tracked)