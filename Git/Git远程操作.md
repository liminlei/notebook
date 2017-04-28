---
title: Git远程操作
date: 2017-03-20 21:30:30
tags: Git
---
# 六、本地-->远程
## 1、创建SSH Key
`ssh-keygen -t rsa -C "youremail@example.com"`
.ssh目录下会生成id_rsa私钥和id_rsa.pub公钥。
将id_rsa.pub复制进github。
## 2.添加远程库
在github上创建新的仓库

## 3.本地push
`git push -u origin master 	//-u代表本地和远程的master分支关联，第一次push使用`
`git push origin master 	//第二次以后使用`


# 七、远程-->本地
## 1.clone到本地
`git clone git@github.com:yelvcx/库.git`

# 八、分支管理
![master分支](http://i1.piimg.com/519918/d27b8b5be9899afb.png)master分支
![创建新分支dev](http://i1.piimg.com/519918/82822c479df6ab40.png)创建新分支dev
![新分支dev提交修改](http://i1.piimg.com/519918/dbc7af4d88dd4269.png)新分支dev提交修改
![合并分支](http://p1.bpimg.com/519918/13b221d13909abec.png)合并分支
![删除分支](http://i1.piimg.com/519918/ea49b643d9054b36.png)删除分支

## 1、创建分支
下面所有dev代表分支
`git checkout -b dev 	//-b代表创建并切换`
`git branch dev 	//单独创建`
`git checkout dev 	//单独切换`
`git branch	 			//查看当前所有分支，带星号的为当前`
分支之间不会相互影响修改
## 2、合并分支
`git merge dev //把dev分支合并到master分支`
## 3、删除分支
`git branch -d dev	//	删除dev分支`

**讲道理吧，分支冲突、管理策略、多人协作、标签什么的暂时用不到，先不学了。以后在更新，估计也不会。**