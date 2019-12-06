---
title: git
date: 2018-12-03 09:33:09
top:
categories:
   - 学习
   - git
tags: git
---

## git

版本管理

* 历史记录：能够记录开发过程中每一个版本，能够在每个版本之间来回穿梭
* 多人协作

## 版本管理软件类别

* 集中式：SVG
* 分布式：Git

## 使用GIt记录版本的步骤

初次使用Git

* 在项目代码文件夹空白位置，右键鼠标--->找到Git Bash Here
* 在弹出的窗口执行'git init',初始化。当前项目使用Git管理，执行完命令会产生一个隐藏文件.git

如何记录写好的代码

* 命令行窗口中，执行'git add .'//到暂存区，文件进入Git管理

* 命令行窗口中，执行'git commit -m '此次记录说明，类似注释''//文件提交到本地仓库

  

初次提交代码，会提示

* #--global会将配置保存到用户配置
* $git config --global user.name 'xxx'
* $git config --global user.email 'xxx'

如果你有GitHub账号，user.name和user.email最好设置成和·GitHub一致的名字

修改账号和邮箱在'C:\USERS\刘晓慧\.gitconfig'文件中存放

## 工作原理

文件提交

![1571379196316](C:\Users\刘晓慧\AppData\Roaming\Typora\typora-user-images\1571379196316.png)

文件恢复：

![1571386580088](C:\Users\刘晓慧\AppData\Roaming\Typora\typora-user-images\1571386580088.png)

## 文件状态

未跟踪：未被git管理过

已暂存：已经到暂存区

已修改：文件已添加暂存区，文件修改，但是没有提交到仓库区

已提交：到达仓库区



## 历史穿梭

查看每个版本的版本号

git log

git log --oneline

如何切换（穿梭）到历史的某个版本

git checkout 版本号

git checkout master --->到达最后的版本



## 分支

创建分支：git branch 分支名

切换分支：git checkout 分支名

创建并直接切换分支：git checout -b 分支名

合并分支：git merge 分支名（注意切换到master分支在进行合并）

删除分支：git branch -d 分支名（注意切换到master分支在进行删除）

查看所有分支：git branch



## 推送本地仓库到远程仓库

首次推送：

* 把本地仓库和远程仓库建立关系：（此时还没有推送）

  git remote add 远程仓库地址别名 远程仓库地址(origin https://github.com……)

* 首次推送：

  * git push -u 远程仓库地址别名 本地分支：远程分支(origin master:master),如果本地分支名和远程分支名一样，则省略：远程分支
  * git push -u origin master把本地仓库代码放到远程仓库（推送）
    * -u 记住推送地址，后面直接执行git push
    * 注意：**首次推送会弹出一个窗口，填写GitHub账号和密码**

## 多人协作

* 仓库拥有者：

  * 邀请合作者（远程仓库，设置权限，点击settings,点击左侧栏目第二项Collaborators）
  * 再次编写代码，然后先拉后推

* 合作者：

  * 克隆远程仓库代码到本地仓库
    * git clone 远程仓库地址(https://github.com……)
  * 把新写的代码或修改的文件，先提交到本地仓库
  * 先拉取代码
    * git pull
  * 后推送代码到远程仓库
    * git push

* 解决冲突：文件名冲突

  * 打开master文件，合作者进行协商，再做决定，决定好了进行重新管理与提交
  * 在合并分支或者拉取代码时候，如果出现confilct,说明文件有冲突
  * 解决办法协商，重新执行add,commit，最后push

* 出现Merge branch https//www.github……Please enter a commit message……

* 如果解决冲突，弹出这个画面，按i之后，可以输入一个说明，按q结束

* 设置readme解决方法：git pull --rebase 远程仓库别名 master

  

