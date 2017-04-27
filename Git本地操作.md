---
title: Git本地操作
date: 2017-03-20 12:21:01
tags: Git
---
内容来自[廖雪峰先生的博客](http://www.liaoxuefeng.com/)。
# 一、Git的安装
1.安装完成后需要配置
```
git config --global user.name "liminlei"
git config --global user.name "liminleichn@gmail.com"
```
# 二、创建版本库
1、创建空目录
```
mkdir learnGit
cd learnGit
pwd    //显示当前目录
```
2.初始化
```
git init	//完成后生成 .git 文件夹
```
# 三、添加文件
1.添加文件（工作区-->暂存区）
```
git add readme.txt
```
2.提交文件（暂存区-->版本区）
```
git commit -m "此处为提示"
```
# 四、版本操作
1.查看仓库状态
```
git status
```
2.查看文件的修改内容
```
git diff
```
3.查看历史纪录
```
git log
```
4.HEAD表示当前版本，HEAD^表示上一个
```
git reset --hard HEAD^  //回退到上个版本
git reset --hard id号	//回退到指定版本
```
5.撤销工作区修改
```
git checkout -- 文件名.后缀	//撤销工作区的修改
```
6.撤销暂存区修改
```
git checkout HEAD 文件	//修改了工作区，还add到了暂存区，可撤销
```
7.删除文件
```
git rm 文件
```
# 五、总结


- 文件编辑在工作区，add进入暂存区，commit进入版本区
- 撤销工作区修改 checkout -- 文件
- 撤销暂存区修改 checkout HEAD 文件
- 误删文件  版本回退

git管理的是修改

