---
title: Hexo部署Github博客
date: 2017-03-20 12:21:01
tags: Hexo
---
采用Hexo和Github部署博客。（Windows10环境）
# 一、环境配置
## 1.安装Node.js
   此项无难度。一直下一步安装即可。完成后cmd内输入`node -v`查看是否成功。
## 2.安装Git
   同上，无难度。
## 3.注册github
   注册完成后，参照Git本地操作一文，添加SSH。


# 二、搭建博客
## 1.安装HEXO
   

1. 本地任意地方新建Blog文件夹，文件夹内右键空白地方进入Git Bash
2. 输入指令`npm install -g hexo`,完成后输入`hexo`查看是否成功
3. 输入`hexo init hexo`初始化hexo,Bash显示Start blogging with hexo！同时，Blog文件夹内多出一个hexo文件夹
4. 进入hexo文件夹，`cd hexo`
5. 安装依赖文件`npm install`
6. 生成页面。`hexo g`
7. 启动本地服务器。`hexo s`。浏览器打开localhost:4000，成功即可。


## 2.Github创建仓库
1. 注意仓库名。yelvcx.github.io
2. setting里面选择模版
3. 浏览打开 yelvcx.github.io成功即可。

## 3.本地hexo项目托管到github


1. 打开hexo主目录下 **站点配置文件** _config.yml（后面theme里有同名文件，称为主题配置文件）
2. 修改**站点配置文件**，下面没有的项目就添加。
```
  type: git  
  repository: git@github.com:yelvcx/yelvcx.github.io.git
  branch: master
```
3. 安装hexo-deployer-git插件  
 `npm install hexo-deployer-git --save`

4. 最后一步，部署。

 ```
  hexo clean
  hexo generator #简写 hexo g
  hexo deploy #简写 hexo d
  ```

此时github博客可访问。部署后若出现CNAME文件消失，则将CNAME文件放入本地source文件夹下，下次hexo d后一同上传。

# 三、主题修改
采用好看的NexT主题，[教程参考。](http://theme-next.iissnan.com/)