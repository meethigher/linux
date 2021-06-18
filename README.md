---
title: Linux学习
comments: false
tags: linux
date: 2021-01-17 20:42:12
---


假期想玩玩linux服务器，学习一下linux

<!--more-->

小技巧：在Linux中，可以通过按tab键补全名字。

学习笔记[linux](https://gitee.com/meethigher/linux)

# 一、Linux认识

## 1.1 简介

Linux是一种开源的、免费的操作系统，安装在计算机硬件上、用来管理计算机的硬件和软件资源的系统软件。

Linux注重安全性、稳定性、高并发处理能力，没有人性化的可视化界面。

Windows多数用于个人计算机，Linux多数用于企业服务器上。

## 1.2 版本

Linux的发行版本：linus在1991年开发，linux的内核程序，后来很多软件开发组织以及软件公司在内核程序基础上，陆续推出很多不同版本的linux操作系统：Ubuntu（乌班图）、RedHat（红帽）、CentOS、Debian（蝶变）等等

[Linux目录结构](https://www.runoob.com/linux/linux-system-contents.html)

{% asset_img 1.png %}

我安装的是centos8.3，[网易镜像](http://mirrors.163.com/)，[搜狐镜像](http://mirrors.sohu.com/)

安装Xshell可以远程连接Linux，但是只限于控制终端。linux下，通过命令ifconfig -a可以查看ip地址

{% asset_img 2.png %}

安装Xftp可以远程向Linux传输文件，同类型的还有FileZilla，我用他在向windows服务器传输文件，[FileZilla删除自动检测更新](https://blog.csdn.net/baidu_27989705/article/details/84580232)，[FileZilla关闭自动更新](https://jingyan.baidu.com/article/a17d5285d8443b8098c8f21e.html)

## 1.3 Vi和Vim

Vi和Vim是Linux中的文本编辑器，用来在Linux中查看或者编辑文本文件的，就像windows中的记事本。

Vim是Vi的增强版，Vi的绝大多数用法适用于Vim。

Vi 文件名：如果有文件，就打开，如果没有，就创建。

Vi/Vim的三种模式

* 一般模式：用Vi/Vim命令打开文件（Vim test.txt），进入一般模式，可以查看文件内容，不能编辑。可以通过上下左右键来查看内容。
* 编辑模式：在一般模式下，按下i键或者a键或者I键或者A键，就能进入编辑模式。可以编辑文件内容，但是不能保存。按esc键回到一般模式。
* 命令模式：在一般模式下，按下:键，就能进入到命令模式。输入q!表示不保存并强制退出编辑器。输入wq表示保存并且退出编辑器。

Vi/Vim的快捷键

* 复制粘贴当前行：在一般模式下，按yy键（大写表示向上），就将光标所在行复制到剪贴板。在一般模式下，按p即可将剪贴板内容，粘贴到光标所在行。
* 复制当前往下n行：在一般模式下，按5，再按yy键（大写表示向上），即可将光标所在行往下5行复制到剪贴板。
* 在文本文件中搜索关键字：在命令模式下，按下/，再输入关键字，回车即可。按n表示从当前光标依次向下找。
* 删除光标所在的当前行：在一般模式下，按dd键，即可删除。
* 删除光标所在的行往下五行：在一般模式下，按5，再按dd键（大写表示向上），即可。
* 撤销上次编辑：一般模式下，按u，即可。
* 显示行号：命令模式下，输入set nu，取消行号是set nonu

多说无益，直接上图得了。

{% asset_img 3.png %}

# 二、Linux权限

## 2.1 用户管理

任何使用Linux的系统资源的用户，都必须用一个合法的账号和密码，账号和密码一般都是向系统管理员申请。

root是Linux系统安装时，默认创建的系统管理员账号，由root来创建普通的账号。

添加用户：useradd 用户名

* 在linux中，任何一个用户都至少属于一个组，新建用户时，如果不指定组，则会新建一个组，组名跟用户名相同，并且把该用户添加到该组。
* 创建的用户根目录会存放在home目录下面，与用户名相同

添加指定根目录的用户：useradd -d /home/目录名 用户名

设置密码：passwd 用户名

删除用户：usedel 用户名

* 删除之后，用户名的主目录还是存在的，但是里面的数据也不存在。
* 删除用户以及主目录：userdel -r 用户名

查看用户：id 用户名

切换用户：su 用户名（su表示switch user）

* 权限高向权限低的切换，不需要密码
* 权限低向权限高的切换，需要密码

## 2.2 组管理

Linux中的组，相当于角色的概念，可以对有共性的用户进行统一管理。每一个用户至少属于一个组，不能独立于组存在，也可以属于多个组。

新建用户时，如果不指定组，则会新建一个组，组名跟用户名相同，并且把该用户添加到该组中。

添加组：groupadd 组名

删除组：groupdel 组名

把用户添加到组中：gpasswd -a 用户名 组名

把用户从组中移除：gpasswd -d 用户名 组名

创建用户时，指定所属的组（主组）：useradd -g 组名 用户名，如果不指定，那就默认是在以用户名命名的组中。

## 2.3 系统及帮助操作

关机

* shutdown now：立即关机
* shutdown -h xxx：定时关机
* shutdown -r now：立即重启

重启：reboot

同步数据：sync

* sync命令是在关闭Linux系统时使用的，将缓存中的数据，强制写入硬盘，防止数据丢失。

查看Linux系统手册上的帮助信息：man 命令名称，命令太多时，按空格可以翻一屏，按q退出。

查看命令的内置帮助信息（可以理解为开发时写的注释）：help

* 如 help cd

## 2.4 文件及目录操作

查看当前所在目录路径：pwd

查看目录下的文件及目录：ls 指定目录

* 如：ls /home
* 如果不指定就是当前目录
* 以详细列表展示：ls -l 指定目录
* 列出所有目录，包括隐藏的：ls -a 指定目录

切换目录：cd 指定目录

创建目录：mkdir 目录名称

* 创建多级目录：mkdir -p /home/test/hh

删除空目录：rmdir 目录名

创建一个或者多个空文件：touch 文件名1 文件名2 ...

复制文件或者目录：cp 源 目标

* 复制文件夹连同子目录：cp -r 源 目标

删除文件或者目录：rm 文件名或目录

* 强力删除文件：rm -f 文件
* 删除目录及子目录：rm -r 目录

移动目录或者文件：mv 源 目标

* mv test1.txt test2.txt，相当于对test1.txt进行重命名，如果test2.txt不存在时。

查看文件内容：cat 文件名

* 显示行号：cat -n 文件名

全屏分页显示查看文件：more 文件名

分屏查看文件内容：less 文件名

查看文件头10行：head 文件名

* 查看头5行：head -n 5 文件

查看文件尾10行：tail 文件名

* 查看尾5行：tail -n 5 文件

输出系统变量或者常量的值到终端：echo

* 如：echo $JAVA_HOME，echo $PATH

存储前一个查看命令的输出结果到文件中：查看命令 > 文件

* ls > test.txt

查看当前完整时间：date

* 年份：date +%Y
* 月份：date +%m
* 当前日期：date +%d
* 按指定格式显示时间：date '+%Y-%m-%d %H:%M:%S'
* 设置时间：date -S '2021-12-12 12:12:12'

搜索当前目录下的文件或者目录：find \[搜索范围][搜索标准] 关键字

* 搜索当前目录下txt文件：find *.txt
* 搜索当前目录下名称含e的文件：find \*e\*
* 搜索指定目录下文件：find 路径 关键字
* 搜索大于5M的：find 路径 -size +5M
* -size：按大小
* -name：按名字
* -user：按文件所有者

搜索目录树下的所有文件或者目录，都是根据名称搜索

* 先同步数据到目录树：updatedb
* 再查找：locate 关键字

过滤：grep \[选项] 查找内容

* -n：显示匹配行和行号
* -i：忽略大小写
* cat test.txt|grep etc：在test.txt的内容中，查找etc

压缩文件：gzip 文件

* 将文件压缩为.gz，压缩成功后会把原文件删除

解压文件：gunzip 文件

* 解压，成功后把原文件删除

压缩指定文件：zip [选项] xxx.zip 要压缩的目录或文件

* -r：递归压缩

解压指定文件：unzip xxx.zip

* 解压到指定目录：unzip xxx.zip -d 目录

压缩或者解压多个文件和目录：tar [选项] 压缩包名称(如：xxx.tar.gz) [选项] 文件或者目录列表 

* -c：压缩，如：tar -zcvf abc.tar.gz /opt，将opt目录打包成abc.tar.gz
* -x：解压，如：tar -zxvf abc.tar.gz -C /opt，将abc.tar.gz解压到opt目录
* -v：显示详细信息
* -f：指定压缩后的文件名
* -z：打包同时压缩
* -C: 指定解压到哪个目录

## 2.5 文件与组

在Linux中，每一个用户都至少属于一个组，用户不能独立于（没有）组存在，一个用户可以属于多个组。

在Linux中，每一个文件（目录）也都属于一个组，并且只能属于一个组；文件（目录）可以通过组来控制哪些用户，即文件（目录）的访问权限。 

在文件（目录）看来，linux系统中所有的用户分为三类

* 文件（目录）所有者：默认是创建者，可以修改。
* 同组用户：跟文件（目录）属于同一个组的用户
* 其他组用户

查看文件的所有者和所在的组：ls -l，查看详细信息

修改文件的所有者：chown 新的所有者 文件名

> 默认不会修改子目录的所有者

修改文件的所有者和所在组：chown 所有者:所在组 文件名

* 如果要将子目录的所有者和组也进行修改，则需要加-R
* chown -R 所有者:所在组 文件名

{% asset_img 4.png %}

修改文件的所在组：chgrp 新的组 文件(目录)

* 连同修改子目录：chgrp -R 新的组 文件(目录)

## 2.6 文件权限管理

在Linux中，任何文件或者目录都有三种权限：读（read）、写（write）、执行（execute）

> Windows中可执行文件是exe，Linux中可执行文件是shell

对于文件而言

* 读（read）：读取、查看文件内容，比如cat、more、less、head、tail等
* 写（write）：修改文件内容，比如vi和vim等
* 执行（execute）：如果文件是可执行文件（.sh），可以直接运行，比如：./xxx.sh

对于目录而言

* 读（read）：读取、查看目录下边内容，比如ls等
* 写（write）：修改目录内容，比如mkdir、rmdir、rm、mv等
* 执行（execute）：可以进入该目录，比如cd等

在Linux中，任何文件或者目录都有三部分权限：所有者权限、同组用户权限、其他组用户权限，输入ls -l可以查看

* 所有者权限：除去第一个的前三个
* 同组用户权限：中三个
* 其他组用户权限：后三个

> 第一位如果是d，就是目录
>
> 第一位如果是-，就是文件

{% asset_img 5.png %}

修改文件或者目录的权限

1. 通过r、w、x变更变更权限
   * chmod u=rwx,g=rx,o=x 文件目录名
   * chmod o+w 文件目录名
   * chmod a-x 文件目录名
   * u、g、o、a分别代表文件所有者、文件所在组用户、其它组用户、所有用户
   * =、+、-分别代表设置权限、增加权限、去掉权限

2. 通过数字变更权限
   * chmod 一组三个数字 文件目录名
   * 说明：r=4 w=2 x=1 rwx=4+2+1=7

# 三、网络配置

Linux中的配置文件：/etc/sysconfig/network-scripts/ifcfg-ens33

{% asset_img 6.png %}

# 四、进程及服务管理

## 4.1 进程管理

线程：一个程序的执行线路

进程：一个程序的执行

一个进程会占一个端口，一个进程可以有多个线程。

查看进程：ps（只会显示应用进程）

* 显示所有进程：ps -e
* 全格式显示所有进程：ps -ef

关闭进程：kill [选项] 进程ID

* -9：强制停止
* 增强版关闭进程：killall 进程（支持正则）

## 4.2 服务管理

服务是支持Linux运行的一些必要程序，本质上是进程，也叫守护进程。

守护进程通常默默地运行在后台，为应用程序提供必要支撑，比如sshd、防火墙等。

操作服务：systemctl [选项] 服务名称

* 启动：start
* 停止：stop
* 重启：restart
* 重新加载配置：reload
* 查看状态：status
* 设置自启：enable

如，查看防火墙状态

```shell
systemctl status firewalld
```

# 五、软件包管理

就好比Windows上的安装软件。

## 5.1 RPM包管理

RPM包：一种Linux软件包的打包和安装工具。它操作的软件包都是.rmp结尾。

使用RPM：rpm命令。

查看当前系统中已经安装的rpm软件包：rpm -qa

* rpm -qa|grep chrome：过滤出chrome关键字的

卸载rpm软件包：rpm -e 关键字

安装rpm包：rpm -ivh xxx.rpm

* 去官网下载到linux中，用命令安装

## 5.2 YUM管理

YUM包：一种基于RPM的软件包管理工具，它能够从指定服务器上自动下载RPM包并且自动安装，可以自动处理软件包之间的关系。

rpm安装虽然用的人多，但是经常出现安装一个rpm，结果这个rpm依赖另一个包，结果另一个包又依赖于另另一个包，就导致安装失败，也很麻烦。我在centos安装

yum就解决了上述问题，就像maven，自己搭建服务器，将所有包放到自己的服务器上，在安装过程中，自动安装依赖包，由此进行安装。**必须有外网**

查看当前系统已经安装的RPM包：yum list installed

* yum list installed|grep chrome：过滤出chrome关键字的

卸载rpm软件包：yum remove 软件名

安装rpm软件包：yum install 软件名或rpm包名

# 六、搭建JavaEE环境

## 6.1 安装JDK

官网下载jdk，以[下载jdk12.0.2](https://www.oracle.com/java/technologies/javase/jdk12-archive-downloads.html)为例

首先将下载的jdk.tar.gz解压到opt目录

```shell
[root@localhost 下载]# tar -zxvf jdk-12.0.2_linux-x64_bin.tar.gz -C /opt
jdk-12.0.2/bin/jaotc
jdk-12.0.2/bin/jar
...
```

配置环境变量，进入/etc/下编辑profile，添加下面的代码块。jdk1.5之后，[不需要配置classpath](https://meethigher.top/blog/2019/jdk/)。

```shell
JAVA_HOME=/opt/jdk-12.0.2
PATH=$JAVA_HOME/bin:$PATH #Linux(Windows)中用$(%)引用变量，用:(;)分割，
export JAVA_HOME PATH
```

**重启电脑之后**，输入命令查看版本信息。

```shell
[guest@localhost ~]$ java -version
java version "12.0.2" 2019-07-16
Java(TM) SE Runtime Environment (build 12.0.2+10)
Java HotSpot(TM) 64-Bit Server VM (build 12.0.2+10, mixed mode, sharing)
[guest@localhost ~]$ javac -version
javac 12.0.2
```

如果不想重启电脑，也可以让Linux重新加载配置文件

```shell
source profile
```

## 6.2 安装Tomcat

解压Tomcat

```shell
tar -zxvf apache-tomcat-9.0.41.tar.gz -C /opt
```

找到tomcat的bin目录，运行命令

```shell
./startup.sh
```

浏览器输入localhost:8080即可访问。

如果无法通过外部的机器访问linux，那么关闭防火墙

```shell
systemctl stop firewalld
```

## 6.3 安装MySQL

查看是否安装mariadb，有则卸载，否则冲突。

```shell
yum list installed|grep mariadb
yum remove xxx
```

下载MySQL，并解压。

两个小问题

* [CentOS下载版本](https://blog.csdn.net/dxyzhbb/article/details/109511218)
* [CentOS安装解压版MySQL8](https://www.cnblogs.com/h--d/p/9556758.html)

```shell
tar -zxvf mysql-8.0.12.tar.gz -C /opt
```

名字如果太长，可以重命名

```shell
mv mysql-8.0.12 mysql
```

创建数据文件夹data，用来存放mysql数据库文件，默认没有，需要手动创建。

```shell
mkdir data
```

创建用来执行mysqld命令的Linux用户，最好创建一个专用的账号

```shell
groupadd mysql #创建mysql组
useradd -g mysql mysql #创建一个组为mysql的mysql用户
```

在etc下面创建编辑一个my.cnf文件，用来存放mysql的配置

```ini
[mysql]

# 设置mysql客户端默认字符集
default-character-set=utf8

[mysqld]

# 设置3306端口
port=3306

# 设置mysql的安装目录
basedir=/opt/mysql-8.0.12
datadir=/opt/mysql-8.0.12/data

# 允许最大连接数
max_connections=20

# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8

# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
default_authentication_plugin=mysql_native_password
```

使用 mysql 的 mysqld 命令初始化数据库的基本信息。切换到 mysql/bin 目录下执行。

```shell
./mysqld --initialize --user=mysql --datadir=/opt/mysql/data --basedir=/opt/mysql #设置用户和路径
```

参数说明： 

* --initialize 初始化 mysql，创建 mysql 的 root, 随机生成密码。记住密码，登录 msyql 使用。 
* --user 执行 msyqld 命令的 linux 用户名 
* --datadir : mysql 数据文件的存放位置，目录位置参照本机的设置。 
* --basedir : msyql 安装程序的目录，目录位置参照本机的设置。 该命令执行后，会生成一个临时的 mysql 数据库 root 用户的密码，请先拷贝出来记住，后续第一次登录 mysql 需要使用

> 碰到个错误，这边直接安装缺少的东西即可。

{% asset_img 7.png %}

会生成一个临时密码，保存下来。

启用安全功能：在服务器与客户机之间来回传输的所有数据进行加密，通过mysql_ssl_rsa_setup开启数据加密，生成数字证书，证书提供身份验证机制。如果不开启，则会明文传输。

```shell
./mysql_ssl_rsa_setup --datadir=/opt/mysql-8.0.12/data # 对data下的数据进行加密传输
```

修改mysql整个安装目录权限，更改所属的用户和组为之前创建的用户和组

```shell
chown -R mysql:mysql /opt/mysql-8.0.12
chmod 000 /opt/mysql-8.0.12
chmod u=rwx,g=rwx /opt/mysql-8.0.12
```

启动mysql服务：./mysqld_safe &（带&表示后台启动）

通过进程查看是否启动：ps -ef|grep mysql

关闭mysql服务：./mysqladmin -uroot -p shutdown

进入mysql客户端：./mysql -uroot -p

> 缺少libncurses.so.5库，[解决方案](https://blog.csdn.net/qq_44028464/article/details/103944018)

修改密码：alter user 'root'@'localhost' identified by '密码'

> dnf命令还未整理















