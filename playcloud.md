##### 计算机硬件和软件的关系是什么？

### 关于内核和发行版本

##### 常见的 Linux 发行版本有哪些？它们的主要差别在什么地方？（*）
A: 
	Linux发行版则是Linux内核基础上添加了不同工具软件构成的一套操作系统。虽然内核都是一样的，但添加部分各不相同，这就构成了不同的发行版本。最常见的发行版本有：

**Debian/Ubuntu**： Debian系列，包括Debian和Ubuntu等.Debian最具特色的是`apt-get`/`dpkg`包管理方式。Ubuntu是基于Debian的unstable版本加强而来，由其搭载的Linux桌面系统界面非常友好。常见的是基于Gnome的Ubuntu，基于KDE的Kubuntu以及基于Xfc的Xubuntu。就易用性和兼容性而言,Ubuntu比较适合新手。
**RedHat**：redhat可以说是在国内使用最多的Linux版本。这个版本的特点就是使用人数多，资源多。
**CentOS**: CentOS的稳定性非常好，适合于服务器使用。
**Fedora**： Fedora Core的稳定性较差，最好只用于桌面应用
**Manjaro**：比较特别的一种发行版本，基于 Arch Linux 。 Manjaro 几乎为所有的程序都提供了桌面环境和窗口管理界面。

==Linux发行版本有许多，对于我们这种新手的确是两眼一抹黑地挑，这里一个知乎的回答或许可以有点启发==：[如何选择适合自己的Linux发行版本](https://www.zhihu.com/question/21411365)

**可以用 `lsb_release -a`查看发行版本型号**
```bash
(base) [openbiox01@z root]$ lsb_release -a
LSB Version:    :core-4.1-amd64:core-4.1-noarch
Distributor ID: CentOS
Description:    CentOS Linux release 7.3.1611 (Core)
Release:        7.3.1611
Codename:       Core
```
##### Manjaro Deepin Linux 是一个什么样的存在？
 A: Manjaro-deepin是以manjaro为基础的桌面系统。外观精美，但是Manjaro的软件安装方式会跟Debian系列和CentOS的不同。
 [Manjaro-deepn安装指南](https://zhuanlan.zhihu.com/p/43442012)



##### 什么是 Linux 系统的内核，如何查看内核版本号？
　Linux内核［kernel］是整个操作系统的最底层，它负责整个硬件的驱动，以及提供各种系统所需的核心功能。在内核基础上挂载不同软件便构成操作系统，Ubuntu、RedHat、Fedora、Debian等都是基于Linux内核(版本号可能不同)的不同操作系统。
方法一，用`cat/proc/version`：
```bash
(base) [openbiox01@izuf6btm1dq2w64mt5q889z root]$ cat /proc/version
Linux version 3.10.0-514.26.2.el7.x86_64 (builder@kbuilder.dev.centos.org) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-11) (GCC) ) #1 SMP Tue Jul 4 15:04:05 UTC 2017

```
方法二，用`uname -a`
```bash
(base) [openbiox01@izuf6btm1dq2w64mt5q889z root]$ uname -a
Linux izuf6btm1dq2w64mt5q889z 3.10.0-514.26.2.el7.x86_64 #1 SMP Tue Jul 4 15:04:05 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
```
### 关于Linux安装和配置

##### 如何组装服务器和安装Linux系统（*）

##### 在 Linux 下如何查看电脑的硬件信息（如内存、CPU、硬盘、显卡等）

##### Linux 系统常见的文件系统有哪几种？Windows系统上看到的C盘、D盘，在Linux 系统下是以什么样的形式存在？
##### Linux 系统如何设置开机自动挂载（mount）你的移动介质（如U盘、移动硬盘）
A:  **使用修改fstab文件的方法配置自动挂载：**
`/etc/fstab`是在开机引导的时候自动挂载到linux的文件系统。
首先可以用`fdisk -l`查看挂载信息：
```bash
[root@izuf6btm1dq2w64mt5q889z ~]# fdisk -l

Disk /dev/vda: 42.9 GB, 42949672960 bytes, 83886080 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x0008de3e

   Device Boot      Start         End      Blocks   Id  System
/dev/vda1   *        2048    83884031    41940992   83  Linux
```
查看`fstab`文件内容
```bash
[root@izuf6btm1dq2w64mt5q889z ~]# cat /etc/fstab
#
# /etc/fstab
# Created by anaconda on Fri Aug 18 03:51:14 2017
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=59d9ca7b-4f39-4c0c-9334-c56c182076b5 /                       ext4    defaults        1 1
```
然后用`vim /etc/fstab`编辑文件，在最后一行加上挂载信息，比如：
```bash
/dev/sdb1 /mnt/usb1 ntfs-3g defaults 0 0	#这里添加了一个NTFS
```
保存退出即可。

##### 在Linux 需要使用哪些命令来挂载一个移动硬盘？如果挂载时报错，一般会有哪几种情况？分别怎么解决？

### 关于目录和文件
##### 什么是“根目录“、“家目录”？

##### 简述文件的绝对路径和相对路径

##### Linux 系统在根目录（/）下一般会有哪些目录，它们分别有什么作用？

##### 如何查看隐藏文件
A: 在linux中以`.`开头的都是隐藏文件。可以通过`ls -a`查看隐藏文件。

##### Linux 系统中的 644、755、777 文件权限分别表示什么意思？他们的数字是怎么计算得来的？修改文件权限的命令是什么？怎么设置用户文件的默认权限？如何批量修改某个目录下的目录权限为755，文件权限为644？

##### `rsync`，`scp` 都可以用来在服务器之间传输文件，它们的主要区别是什么？

### 关于vim

##### 在命令行界面，如何用 Vim 编辑器打开一个文本文件、创建一个文件、对文件进行修改和保存？

 A：
   ```bash
   touch filename	#创建文件
   vim filename 	#用vim打开文件
   # 按 i 是编辑器进入 insert 状态后编辑文件；
   # 按 	Esc 推出编辑状态
   # 按 ：，输入 wq保存并退出。
```
##### 如何设置 Vim 编辑器，使其支持：a) 文件/目录路径提示和自动补全; b) Python 函数自动补全；c) 左侧显示目录树；d) 各种文件的语法高亮

##### 跟nano相比，vim的优势在哪里？在vim里，p 与 P 两种指令下粘贴的效果有什么区别？

##### 在vim中，编辑完文件后显示 E45: 'readonly' option is set 时，如何强制写入该档案并保存退出？

### 关于 `grep`

##### 管道在 Shell 中是一个什么样的角色？

##### 如何使用管道将上游的数据传入 Vim 编辑器？

##### 如何将程序的 stdout 和 stderr 通过管道输出到两个文件？

### 关于用户和权限设置
##### 如何新增一个用户并赋予该用户root权限？

##### 如何使用ROOT权限？如何切换不同的身份
A:
 - 在root时，通过`sudo`命令使用root权限。用`su - username`切换到普通用户
 - 在普通用户状态下用`su -`切换成root账号，需要密码。
 - 对于具有root权限的一般用户，用`sudo su`转换成root权限状态，需要密码。用`su username`切换回一般状态

### 关于shell
##### Linux 文件操作时，比较 awk/grep/sed 三剑客的用法
##### Linux 系统中哪个文件是黑洞，可以吃掉 Shell 管道中流动的信息
A: `/dev/null`
##### 如果输入的shell脚本过长，快速删除有哪些快捷键呢？如何快速调整光标位置
A：
删除字符：
 - `Ctrl+l` 清理屏幕
 - `Ctrl+U` 向前删除直到行首(整行删除)
 - `Ctrl+W` 执行向前删除，直到前一个字符是空格
 
调整光标位置：
 - `Ctrl+a` 移动到当前行的开头
 - `Ctrl+e` 移动到当前行的结尾


### 关于WSL

##### 在 Win10 自带的子系统下运行 Ubuntu，和独立使用 Ubuntu 系统，前者的优缺点如何？
##### Windows 子系统（WSL）的安装目录如何从迁移？
##### WSL 如何自动挂载硬盘使其目录保持755，文件保持644权限？ 
##### 在 Windows 桌面环境直接编辑 WSL 内的目录和文件（自动挂载的目录和文件除外）有什么后果？
### 其他
##### 什么是 X server?
##### Centos 系统如何开放指定端口的入和出的访问？
##### Centos 和 Ubuntu 系统如何查看当前服务器的 IP地址和 MAC 地址?###### Centos 和 Ubuntu 系统如何查看即时网速？
##### 如果你没有买域名，如何在本地模拟某个域名的访问？
##### 如何查看并设置当前环境的语言？en_us.utf-8和zh_cn.utf-8分别代表什么？


编程题
使用 bash 实现一个函数，输入整数 n，得到 1 到 n 的累加和
通过 Shell 命令提取 gtf 中编码基因的 gene symbol 和 gene id
假设有如下文件“sample.txt"，文件中包含有若干列重复列。请保留一列重复列，并不影响列顺序。
```bash
COL1,COL2,COL3,COL1,COL4,COL2
1,2,3,1,4,2
a1,a2,a3,a1,a4,a2
b1,b2,b3,b1,b4,b2
d1,d2,d3,d1,d4,d2
```
变为
```bash
COL1,COL2,COL3,COL4
1,2,3,4
a1,a2,a3,a4
b1,b2,b3,b4
d1,d2,d3,d4
```
使用 bash 编程实现时间戳功能，如下为 ngsjs 的 rtime_stamp 命令行程序（R语言）输出
```bash
$ rtime_stamp
[[1]]
[1] "2019_04_03_18_53_44_" "2019_04_03_18_53_"    "2019_04_03_18_"
[4] "2019_04_03_"          "2019_04_"             "2019_"

[[2]]
[1] "2019-04-03-18-53-44-" "2019-04-03-18-53-"    "2019-04-03-18-"
[4] "2019-04-03-"          "2019-04-"             "2019-"

[[3]]
[1] "2019/04/03/18/53/44/" "2019/04/03/18/53/"    "2019/04/03/18/"
[4] "2019/04/03/"          "2019/04/"             "2019/"

$ rtime_stamp -r 'x[[1]]'
2019_04_03_18_56_55_
2019_04_03_18_56_
2019_04_03_18_
2019_04_03_
2019_04_
2019_

$ rtime_stamp -r 'x[[1]][1]'
2019_04_03_18_57_18_
```
##### 尝试使用源码编译安装最新版本的 R，记录过程中遇到的问题。同时使用系统自带的包管理器（如 centos 的yum；Debian/Ubuntu 的 apt；arch、manjaro 的 pacman）、conda 和 spack 安装相同版本的 R。
###### 源码编译安装R 

这次安装遇到很多问题，查询了很多别人的安装教程，但主要为我解决关键性问题的有一下两个。

[史上最麻烦的linux下R源码安装](https://www.jianshu.com/p/edb234eed915)
[Installing R on Linux](https://stackoverflow.com/questions/38690232/installing-r-on-linux-configure-error-libcurl-7-28-0-library-and-headers-a)

首先下载R
```bash
wget https://mirrors.tuna.tsinghua.edu.cn/CRAN/src/base/R-3/R-3.5.3.tar.gz
```
解压文件
```bash
tar -zxvf R-3.5.3.tar.gz 
```
配置
```bash
cd R-3.5.3  #进入解压的文件
./configure
```
**第一次报错**
```bash
configure: error: --with-readline=yes (default) and headers/libs are not available
```
查了一下，发现需要安装`readline`。于是：
```bash
yum install readline-devel
./configure --with-readline=no 
```
**第二次报错**
```bash
configure: error: --with-x=yes (default) and X11 headers/libs are not available
```
继续查，发现需要安装 `libX11-devel`和`libXt-devel`
```bash
yum install libX11-devel 
yum install libXt-devel 
```
也有说可以设置`./configure --with-readline=no --with-x=no`

继续配置，**第三次报错**
```bash
configure: error: libcurl >= 7.22.0 library and headers are required with support for https
```
好吧，这次是没有安装`libcurl`
下载安装编译：
```bash
wget https://curl.haxx.se/download/curl-7.61.0.tar.gz
tar -zxvf curl-7.61.0.tar.gz
cd curl-7.61.0/
./configure
make
make install
```
继续`./configure --with-readline=no --with-x=no`
**第四次报错**
```bash
configure: error: libcurl >= 7.22.0 library and headers are required with support for https
```
一样的错误。再查询发现还需要安`libcurl-devel`
ok,那就继续安装：
```bash
yum install libcurl-devel
```
GO ON
```bash
./configure --with-readline=no --with-x=no	#继续编译,无报错但是有一个warning.
make
make install
```
Finally!
```bash

[root@izuf6btm1dq2w64mt5q889z openbiox01]# R

R version 3.5.2 (2018-12-20) -- "Eggshell Igloo"
Copyright (C) 2018 The R Foundation for Statistical Computing
Platform: x86_64-redhat-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

```

###### 用 yum 安装
在CentOS中，用`yum`下载软件可以解决很多问题，最大的好处就是会自动分析你要安装的软件的依赖关系，并会自动帮你安装必须的“依赖软件”。如如说在上面“源码编译方法”中遇到的报错，用`yum`时统统没有出现，并且还不需要配置环境，不需要编译，简直是新手友好。

首先在EPEL中下载R
```bash
yum install epel-release	#R已经被EPEL仓库管理着，EPEL是一个汇集了各种附加软件包的项目
yum install R
```
安装过程不长，完成后不需要编译直接输入`R`，检查安装成功！

###### 用conda安装

**首先要安装`conda`**

通过`wget`命令下载miniconda：
```bash
wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh
```
下载完后进行安装：
```bash
bash Miniconda-latest-Linux-x86_64.sh	#`bash` 命令安装软件？
```
输入yes确定后还要`source`一下
```bash
source ~/.bashrc
```
到此为止，`conda`已经顺利安装上了。可以直接输入 
```bash
conda
```
安装R，一步到位，无需手动编译：
```bash
conda install R
```
会自动开始安装所需要的文件
```bash
(base) [openbiox01@izuf6btm1dq2w64mt5q889z biosoft]$ conda install R
WARNING: The conda.compat module is deprecated and will be removed in a future release.
Collecting package metadata: done
Solving environment: done

## Package Plan ##

  environment location: /home/openbiox01/miniconda2

  added / updated specs:
    - r


The following packages will be downloaded:

    package                    |            build
...
...
...

```
最后也是直接在终端输入`R`确认安装成功。


使用 spack 在指定不同版本的 gcc 编译器（如8.3、5.4 和 4.8）情况下安装最新版本的R。并比较一些 R 基础函数的速度在计算较大数据量时是否有变化。

