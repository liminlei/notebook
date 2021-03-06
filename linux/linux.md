---
title: linux1
date: 2017-03-27 21:55:01
tags: linux
---
# 一、linux常用命令
## 1、命令提示符
`[root@localhost ~]#`
root: 用户名
~： 当前目录，家目录
$: 普通用户；#：超级用户

## 2、命令格式
`命令 [选项] [参数]	//[]可选`
-a: 简化选项
--all: 完整选项
## 3、常用目录作用
`/:	根目录`
```
/bin：
/sbin：
/user/bin:
/user/sbin:保存系统命令
```
`/boot: 保存用户启动数据`
`/dev: 设备文件保存`
`/etc: 配置文件`
`/home: 普通用户家目录`
`/lib: 系统库`
`/mnt: 系统挂载`
`/media: 挂载`
`/proc 存放存储进程和系统信息,内存挂载 `

`/root 超级用户的主目录 `

`/tmp 存放临时文件的目录` 

`/usr 包含了一般不需要修改的应用程序，命令程序文件、程序库、手册和其它文档。 `

`/var 包含系统产生的经常变化的文件`

**建议：root目录和home目录，还有tmp目录可以随便动。别的新手慎重！**

## 4、图形界面
#### ①安装
```
# 先安装 MATE Desktop
yum groups install "MATE Desktop"

#安装好 MATE Desktop 后，再安装 X Window System。
yum groups install "X Window System"
```
#### 设置启动
```
vim /etc/inittab	查看启动方式
systemctl  set-default  graphical.target	设置启动方式
```

## 5、文件处理命令
### ① 查询目录中内容
 `ls [选项] [文件或目录]`
`例：ls -l /etc`
-a:all; 
-l:显示详细;
-d:查看目录属性
-h:人性化显示
-i:查看inode

### ②目录操作
#### 建立目录
`mkdir -p 目录名	//p代表递归创建`
#### 切换目录
```
cd 目录
cd ~/cd:进入家目录；
cd ..:返回上一级目录；
```
#### 显示当前位置
`pwd`
#### 删除目录
`rmdir 目录	//删除空目录,很少见`
`rm -rf 	//r代表删除目录，f代表强制， 慎重`
`rm -rf /* 	这是毁灭性打击`
#### 拷贝
`cp [选项] 原 目`
-r : 复制目录
-p : 文件属性一起复制
-d : 复制链接属性
-a : rpd全有
#### 剪切或改名
`mv 原 目`
此命令操作目录不需要-r
原、目在同一目录下，为改名
原、目不在同一目录下，为剪切
#### 链接命令


- 硬链接创建的文件其实是同一个文件，i节点号相同。两个文件指向同一块存储区域，修改一个，另外一个随之改变。但必须在同一个分区里面。如果删掉一个，另外一个不影响。
- 软链接相当于windows快捷方式。
`ln -s 源文件 目标文件	//s代表软链接`

## 6、文件搜索命令
#### 文件搜索locate
`locate 文件名`
此命令会搜素`/var/lib/mlocate`中的数据库，新建文件找不到，可以`updatedb`更新数据库。同名文件不能全部找到
#### 命令搜索whereis和which
`whereis 命令名	//搜索命令所在位置，和帮助文档`
`which 命令名	//搜索命令所在位置，如果有别名，可以看到别名`
#### 文件搜索命令find
完全匹配，文件名一模一样才找得到，除非使用通配符
```
find [搜索范围] [搜索条件]
find / -name install.log	//在/目录下按照文件名搜索install.log
```
可以使用通配符
```
* : 匹配任意内容
？： 匹配任意一个字符
[] : 匹配任意一个中括号内的字符
```
其他选项
```
-iname : 忽略大小写
-user：按照所有者搜索
-nouser：查找没有所有者的文件（比如外面拷过来的文件）
-mtime/ctime/actime +10/10/-10:
		mtime:修改文件内容
		ctime:改变文件属性
		atime:文件访问时间
		+10:10天前修改的文件
		10:10天当天修改的文件
		-10：10天内修改的文件
-size:按照文件大小
		-25k:小于25k;
		+25k:大于25k;
		注意：k小写，M大写
-inum:按照i节点
```
多条件
```
多种搜索条件一起用，用一下连接
-a:and
-o:or
最后可以加 -exec 命令 {}\ 来对查找结果执行一些操作
例：find /etc -size +20k -a -size -50k -exec ls -lh {}\;
```
#### 文件搜索命令grep
```
grep [选项] 字符串 文件名		//在文件中找字符串
-i：忽略大小写
-v：排除指定字符串
```
## 7.帮助命令
#### man命令
```
man 命令		//获取命令帮助
man -f 命令	//查看命令级别
		== whatis
```
#### 其他帮助命令
```
命令 --help		//只查看命令选项帮助
info 命令		//用的不多
```
## 8.压缩和解压缩
#### .zip
```
.zip压缩
zip 压缩文件名 源文件	//zip sample.zip sample
					//压缩目录的时候加上-r
```
```
.zip解压缩
unzip 压缩文件
```
#### .gz
```
.gz压缩
1. gzip 源文件 	//源文件会消失
2. gzip -c 源文件 > 压缩文件 		//源文件保留
3. gzip -r 目录 		//压缩目录下所有子文件，但是不能压缩目录
```
```
.gz解压缩
gzip -d 压缩文件
gunzip 压缩文件
```
#### .bz2
```
注意：不能压缩目录
.bz2压缩
bzip2 源文件 	//不保留源文件
bzip2 -k 源文件	//保留源文件
```
```
.bz2解压缩
bzip2 -d 压缩文件 	//带k保留压缩文件
bunzip2 压缩文件		//带k保留压缩文件
```
#### .tar
```
.tar打包
tar -cvf 打包文件名 源文件
		-c:打包
		-v:显示过程
		-f:指定打包后的文件名
打包后可以通过gzip和bz2再压缩，可以解决gzip不能压缩目录的问题
```
```
.tar解打包
tar -xvf 打包文件
		-v:解打包
```
#### .tar.gz
```
tar -zcvf 压缩包名.tar.gz 源文件	//压缩
tar -zxvf 压缩包名.tar.gz		//解压缩

```
#### .tar.bz2
```
tar -jcvf 压缩包名.tar.bz2 源文件	//压缩
tar -jxvf 压缩包名.tar.bz2		//解压缩
```
## 9.关机和重启
#### shutdown
```
此命令更加推介
shutdown [选项] 时间
		-c:取消前一个关机命令
		-h:关机		//少用远程关机，你怎么开？
		-r:重启
```
#### 其他关机
```
halt
poweroff
init 0
```
#### 其他重启
```
reboot
init 6
```
## 10、挂载
```
mount 		//查询系统中已经挂载的设备
mount -a 	//依据/etc/fstab的内容，自动挂载
```
#### 挂载命令格式
```
mount [-t 文件系统] [-o 特殊选项] 设备文件名 挂载点
```
![特殊选项](http://img.mukewang.com/58d60d2e0001814612800720.jpg)
#### 挂载光盘
```
mkdir /mnt/cdrom/ 		//建立挂载点（盘符）
mount -t iso9660 /dev/sr0 /mnt/cdrom/ 		//挂载光盘
```
#### 卸载光盘
```
umount 设备文件名或挂载点		//不可省略，切记
```
#### 挂载u盘
```
fdisk -l 		//查看U盘设备文件名
mount -t vfat /dev/sdb1 /mnt/usb/ 		//挂载举例，linux不支持NTFS
```
## 11、用户登录查看
```
w			//查看登录信息
who 		 //查看登录信息，低配版
last 		//查询所有登录记录
lastlog 	 //查看所有用户最后一次登录时间
```