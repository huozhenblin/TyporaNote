1.磁盘分区

2.winscp 文件拷贝工具  

xshell+xftp即远程连接工具和文件传输工具

secure	CRT8

## linux注意事项

### 	1.linux严格区分大小写

### 	2.系统中所有内容以文件的形式保存

硬盘文件时是 /dev/sd【a-p】[0-9]]    

a-p为各个硬盘

1-9 为各硬盘的分区

文件系统目录结构如下：

[root@192 ~]# df
文件系统                   1K-块    已用     可用 已用% 挂载点
devtmpfs                  485824       0   485824    0% /dev
tmpfs                     497888       0   497888    0% /dev/shm
tmpfs                     497888    7860   490028    2% /run
tmpfs                     497888       0   497888    0% /sys/fs/cgroup
/dev/mapper/centos-root 17811456 1477512 16333944    9% /
/dev/sda1                1038336  142408   895928   14% /boot
tmpfs                      99580       0    99580    0% /run/user/0
[root@192 ~]# 
[root@192 ~]# df
文件系统                   1K-块    已用     可用 已用% 挂载点
devtmpfs                  485824       0   485824    0% /dev
tmpfs                     497888       0   497888    0% /dev/shm
tmpfs                     497888    7852   490036    2% /run
tmpfs                     497888       0   497888    0% /sys/fs/cgroup
/dev/mapper/centos-root 17811456 1477384 16334072    9% /
/dev/sda1                1038336  142408   895928   14% /boot
tmpfs                      99580       0    99580    0% /run/user/0

### 3.linux不靠扩展名取份文件类型

但是也可以写上为管理员做服务

![image-20200320222039981](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200320222039981.png)

4.linux所有的存储设备都必须挂在之后用户才能使用，包括硬盘、U盘和光盘

5.Windows下的程序不能直接在linux中安装和运行

注：文件表示

-rw------- 文件或者目录 标识分10个  

第一个 d标识是一个文件夹 空标识文件

后面每三个一组 每组占位符 为rwx

每组对应 u用户 g 组 o其他

### 4.文件种类和扩展名

-rw-------  第一个标识类型

#### 4.1目录树

![img](D:\my\study\TyporaNote\工具的学习文档\imgs\20150827205149437.png)

4.2文件种类和扩展名

![image-20200410174002746](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200410174002746.png)

# 1、linux的常用命令



### 命令格式

格式：命令 [-选项] [参数]

例如 ls  -la  /etc

说明：

- 个别命令使用不遵循此格式
- 当多个选项时，可以写在一起
- 建华现象与完整选项  -a等于--all

### 目录命令**ls**

英文原意：list

命令所在路径：/bin/ls

执行权限：所有用户

功能描述：显示目录文件

语法：ls 选项[-ald] [文件或目录]

​					-a  显示所有文件，包括隐藏文件

​					-l [h] 详细信息显示  

​							例如 -rw-------. 1 root root 1274 3月  16 22:23 anaconda-ks.cfg

![image-20200322221703643](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200322221703643.png)

​					



​					-d 查看目录属性

 					/   显示所有的根目录文件

​					-i 查询任意文件的id号



## 1.1目录处理命令

#### mkdir

英文原意：make directoties

命令所在路径：/bin/mkdir

执行权限：所有用户

功能描述：创建新目录

- ​			-m 后面跟权限相关（比如数字） 设置该文件夹权限

​					-p 递归创建,即可创建多级目录

语法：mkdir -p [目录名]

范例：$mkdir -p /temp/japan/boduo

​			$mkdir -p /temp/japan/boduo/temp/japan/cangjing

#### cd

英文：change directory

路径：shell内置命令

权限：所有用户

语法：cd[目录]

功能： 切换目录

范例 ： cd /tmp/duoduo/woerzi

​			cd 。。 返回上级目录

#### pwd

英文:print working directory

路径：/bin/pwd

权限：所有用户

语法：pwd

功能描述：显示当前目录

#### rmdir

英文：remoe empty directories

路径：/bin/rmdir

权限:所有用户

语法：rmdir[目录名]

功能：删除空目录

#### cp

英文：copy

路径：/bin/cp

权限：所有用户

语法：cp -rp [源文件或者目录] 【目标目录】

​				-r 复制目录，递归赋值

​				-l 进行硬链接

​				-s 复制成为连接文件即快捷方式软连接

​				-p 保留文件属性

​				-i 若目标文件已经存在，在覆盖时会先询问操作的进行

功能： 复制文件或者目录，创建链接文件

注：可同时复制多个文件  最后一个是目的地址、

复制的同时可以改名 目的地址/新命名

![image-20200323204521421](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200323204521421.png)

#### mv

英文： move

路径：/bin/mv

权限：所有用户

语法：mv [源文件或者目录] 【 目标目录】

功能： 剪切文件，目录改名

注：在目录下，可直接  文件名 目标地址 进行剪切

改名时 直接在当前目录下    mv  文件名  新文件名 

#### rm

英文：remove

路径：/bin/rm

权限：所有用户

语法： rm -rf 【文件或者目录】

​					-r 删除目录

​					-f 强制执行

功能描述：删除文件或者目录【-r 才能删除】



### 文件处理命令

#### 文件的时间

在linux下面记录许多的参数，主要有三个时间

modification time：（mtime）文件内容被修改时，会更新这个时间

status time：（stime）当文件的权健和属性被更改时的都会更新时间

access time：（atime）当该内容被调用时 就会更新这个读取时间

更改时间 touch  参数 文件

#### touch

路径：/bin/touch

权限：所有用户

语法：touch 【文件名】

功能：创建空文件

示例：# touch japanlovestor.list

注：创建多个文件 加空格

​		创建带特殊符号的文件文件名两边加上双引号

#### cat/tac

路径：/bin/cat

权限：所有用户

语法：cat[文件名]

功能表述：显示文件内容

​				-n 显示行号

范例：# cat -n /etc/yum.conf 

同上：tac 反向现实文件的内容

#### more

路径：/bin/more

权限：所有用户

语法： more【文件名】

​			进入more命令行 

​			空格或者f    翻页

​				（enter） 换行

​				q或Q        退出



功能描述：分页显示文件内容

范例：# more /etc/services ^C

#### less

路径：/bin/less

权限：所有用户

语法： less【文件名】

pgup 向上翻页

向下的箭头 一行行翻

功能描述：分页显示文件内容

范例：# less   /etc/services

注： 可以进行搜索：在less显示下  直接输入要     **/**搜索的关键词  按n可以查找下一个

#### head/tail

路径：/usr/bin/head

权限：所有用户

语法：head【文件名】

功能：显示文件的前面几行

​		-n 指定行数    默认7行

范例 # head -n 2 /etc/services 

类似 tail 标识显示末尾的几行

​			-n 指定行数

​			-f   动态显示末尾的内容

### 链接命令

英文：link

路径：/bin/ln

执行权限：所有

语法：ln -s [源文件]【目标文件】

​				-s 创建软链接

功能：创建链接文件

![image-20200329201056168](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200329201056168.png)lrwxrwxrwx 软连接标识    类似于Windows快捷方式 源文件丢失 目标文件失效  独享inode

硬链接 ：两个链接的文件会同时更新  共享inode 

## 1.2.文件权限管理命令

#### chmod

英文：change the permissions mode of a file

语法：chmod [{ugoa}{+-=}{rwx}] [文件或目录] [mode=421] [文件或目录] 

​			-R 递归修改   可以将当前文件夹及其子文件夹全部更改

功能描述 改变文件或目录权限

 chmod u+x，。。。， jan.index  chmod u+x jan.index  多个用户授予用逗号隔开

数字形式

![image-20200329205214054](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200329205214054.png)

所有者 rwx 和为7

所属组rw-

所属其他人 r--

​						chmod 数字  加文件或者文件夹

​						chmod 640 jan.index 

权限说明

文件

r：cat more head tail less

w: vim

x:可执行文件 script command

目录

r：ls

w：touch、mkdir redir rm

x：cd

x代表了是否可以进入该目录并将该目录设置为工作目录 

##### 注：目录权限高于文件权限

#### chown

英文： change file ownership

权限：所有用户

语法：chown 【用户】【文件或目录】

功能描述：改变文件或目录的所有者

范例： chown 神超 fengjie

改变文件fengjie的所有者为神超

示例

-rw-r-----. 1 root root   0 3月  29 20:49 jan.index

useradd shenchao

chown shenchao jan.index

-rw-r-----. 1 shenchao root 0 3月  29 20:49 jan.index

#### chgrp 

 语法： chgrp 【用户组】【文件或者目录】

功能：改变文件或者目录的所有组

### 注：

在默认情况下 谁创建了文件或者 文件夹 所属就是谁 这个用户所属组就是这个文件所属组

#### umask

英文：the user file-creation mask

路径 shell内置命令

权限：所有用户

语法 umask【-s】

​					-s 以rwx形式显示新建文件缺省权限

功能描述 显示设置文件的缺省权限，创建普通文件时没有x

新建文件默认权限：-rw-rw-rw-

新建目录默认权限：drwxrwxrwx



直接执行umask出现022

![image-20200329213755850](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200329213755850.png)

可以更改umask +对应数字

### 1.3 文件搜索命令

#### find

语法：find 【搜索范围】【匹配条件】

功能：文件搜索

	$ find /etc -name init
在目录/etc中查找文件init
-iname 不区分大小写
$ find / -size +204800
在根目录下查找大于100MB的文件
+n 大于 -n 小于 n 等于
$ find /home -user shenchao
在根目录下查找所有者为shenchao的文件
-group 根据所属组查找  

$ find /etc -cmin -5
在/etc下查找5分钟内被修改过属性的文件和
目录
-amin 访问时间 access
-cmin 文件属性 change
-mmin 文件内容 modify  



$ find /etc -size +163840 -a -size -204800
在/etc下查找大于80MB小于100MB的文件
-a 两个条件同时满足
-o 两个条件满足任意一个即可
$ find /etc -name inittab -exec ls -l {} \;
在/etc下查找inittab文件并显示其详细信息
-exec/-ok 命令 {} \; 对搜索结果执行操作  

-type 根据文件类型查找
f 文件 d 目录 l 软链接文件
-inum 根据i节点查找  

## 1.4.帮助命令

### man

命令名称： man
命令英文原意： manual
命令所在路径： /usr/bin/man
执行权限：所有用户
语法： man [命令或配置文件]
功能描述：获得帮助信息
范例： $ man ls
查看ls命令的帮助信息
$ man services
查看配置文件services的帮助信息  

### help  

命令名称： help
命令所在路径： Shell内置命令
执行权限：所有用户
语法： help 命令
功能描述：获得Shell内置命令的帮助信息
范例： $ help umask
查看umask命令的帮助信息  

## 1.5.用户管理命令

### w 

这个命令可以查看当前在线的用户

## 1.6.压缩解压命令

## 1.7.网络命令

### write  

指令名称： write
指令所在路径： /usr/bin/write
执行权限：所有用户
语法： write <用户名>  信息
功能描述：给用户发信息，以Ctrl+D保存结束
范例： # write linzhiling  

### wall  

指令名称： wall
命令英文原意： write all
指令所在路径： /usr/bin/wall
执行权限：所有用户
语法： wall [message]
功能描述：发广播信息
范例： # wall ShenChao is a honest man!  

### ping  

命令名称： ping
命令所在路径： /bin/ping
执行权限：所有用户
语法： ping 选项 IP地址
-c 指定发送次数
功能描述：测试网络连通性
范例： # ping 192.168.1.156  

平的过程中 clt+c 退出

### ifconfig  

命令名称： ifconfig
命令英文原意： interface configure
命令所在路径： /sbin/ifconfig
执行权限： root
语法： ifconfig 网卡名称 IP地址
功能描述：查看和设置网卡信息
范例： # ifconfig eth0 192.168.8.250  

### mail  

命令名称： mail
命令所在路径： /bin/mail
执行权限：所有用户
语法： mail [用户名]
功能描述：查看发送电子邮件
范例： # mail root  

### last  

命令名称： last
命令所在路径： /usr/bin/last
执行权限：所有用户
语法： last
功能描述：列出目前与过去登入系统的用户信息
范例： # last  

### lastlog  

命令名称： lastlog
命令所在路径： /usr/bin/lastlog
执行权限：所有用户
语法： lastlog
功能描述：检查某特定用户上次登录的时间
范例： # lastlog
\# lastlog -u 502  

### traceroute  显示数据包到主机间的路径

命令名称： traceroute
命令所在路径： /bin/traceroute
执行权限：所有用户
语法： traceroute
功能描述：显示数据包到主机间的路径
范例： # traceroute www.lampbrother.net



### netstat  显示网络相关信息

命令名称： netstat
命令所在路径： /bin/netstat
执行权限：所有用户
语法： netstat [选项]
功能描述：显示网络相关信息

  ![image-20200405213400179](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405213400179.png)

### setup  配置网络

命令名称： setup
命令所在路径： /usr/bin/setup
执行权限： root
语法： setup
功能描述：配置网络
范例： # setup  

### 挂载命令  

命令名称： mount
命令位置： /bin/mount
执行权限：所有用户
命令语法： mount [-t 文件系统] 设备文件名 挂载点    固定 iso9660 /dev/sr0
范例： # mount -t iso9660 /dev/sr0 /mnt/cdrom  

### 网络重启

service network restart

## 1.8.关机重启命令

### shutdown命令  

[root@localhost ~]# shutdown [选项] 时间
选项：
-c： 取消前一个关机命令
-h： 关机
-r： 重启  

### 2、其他关机命令

[root@localhost ~]# halt
[root@localhost ~]# poweroff
[root@localhost ~]# init 0  

### 3、其他重启命令  

[root@localhost ~]# reboot
[root@localhost ~]# init 6  

![image-20200405220101690](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405220101690.png)

[root@localhost ~]# cat /etc/inittab
\#修改系统默认运行级别
id:3:initdefault:
[root@localhost ~]# runlevel
\#查询系统运行级别  

### 5、退出登录命令  

[root@localhost ~]# logout  

## VIM命令

### Vim工作模式

![image-20200405220932778](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405220932778.png)在命令模式下 :命令 

:SET NUM she zhi hanghao

### 命令模式命令

![image-20200405233438874](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405233438874.png)

插入命令是在命令模式下 使用的

### 定位命令  

![image-20200405233824820](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405233824820.png)

### 删除命令  

n1 n2为行号

![image-20200405233920674](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405233920674.png)

### 复制和剪切命令  

![image-20200405234223586](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405234223586.png)

### 替换和取消命令  

![image-20200405234242961](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405234242961.png)

### 搜索和搜索替换命令  

![image-20200405234430276](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405234430276.png)

### 保存和退出命令  

![image-20200405234544979](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200405234544979.png)

### vim使用技巧

导入命令执行结果 :r +文件名 会将导入的文本导入到当前光标所在位置

！which + 命令  查询这个命令的路径

定义快捷键 :map 快捷键 触发命令
范例： : map（ctrl v  ctrl p）^P I#<ESC>  后面的为你要设置的快捷键  esc前为你快捷键的内容 最后的表示快捷键插入后处于命令行
: map ^B 0x
 连续行注释 :n1,n2s/^/#/g
:n1,n2s/^#//g
:n1,n2s/^/\/\//g
 替换 :ab mymail samlee@lampbrother.net  

要写在配置文件中

具体地址为

![image-20200408214355285](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408214355285.png)

![image-20200408214408948](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408214408948.png)

在里面插入编辑配置

# 软件包管理

1、 RPM（二进制已编译）包命名原则  

![image-20200409084940825](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200409084940825.png)

2、 RPM包依赖性
树形依赖： a》b》c
环形依赖： a》b》c》a
模块依赖： 模块依赖查询网站：
www.rpmfind.ne  

# 2.bash

## 2.1bsah内置命令

## 2.2shell的变量功能

## 2.3命令别名和历史命令

## 2.4bash shell的操作环境

## 2.4数据流重定向

## 2.5管道命令（pipe）

~~~cmd
la -al /etc | less
~~~

说明：使用ls命令输出后的内容就能够被less读取，并且利用less功能，能够前后翻动，这个管道命令“|”仅能处理经由前面一个命令传来的正确信息，也就是standard output的信息，对于 standard error并没有直接处理能力。

注：每一个管道后面的第一个数据都必须是命令，而且这个命令必须能够接收standard output的数据才行，比如less，more，head，tail。

### 选取命令：cut,grep

将一段数据分析后，取出我们所想要的，或经由分析的关键粗选择我我们想要的行。

#### cut

语法

[root@localhost ~]# cut [选项] 文件名
选项：

| -f 列号：   | 提取第几列           |
| ----------- | -------------------- |
| -d 分隔符： | 按照指定分隔符分割列 |

这个分隔符是指使用原文内的符号进行分割

例如：

~~~cmd
# cut -d ":" -f 1,3/etc/passwd
~~~

#### grep

grep  [-acinv] '查找的字符串‘  文件名

​					-c 计算查找的字符串的次数

​					-i 忽略大小写的不同，所以大小相同

​					-n 顺便输出行号

​					-v 反向选择

​				--color=auto 将找到的关键字部分加上颜色显示

举例

~~~cmd
 last | grep 'www' | cut -d ' ' -f 1
~~~

### 字符处理命令

#### 排序命令sort

~~~cmd
[root@localhost ~]# sort [选项] 文件名
选项：
-f： 忽略大小写
-n： 以数值型进行排序，默认使用字符串型排序
-r： 反向排序
-t： 指定分隔符，默认是分隔符是制表符
-k n[,m]： 按照指定的字段范围排序。从第n字段开始，
m字段结束（默认到行尾）
~~~

例如  last | sort

~~~cmd
# sort -r /etc/passwd
# last | sort
~~~

uniq删除重复行只显示一个

~~~cmd
last | cut -d ' ' -f1 | sort | uniq 

~~~



#### wc 

输出信息的整体数据

~~~cmd
[root@localhost ~]# wc [选项] 文件名
选项：
-l： 只统计行数
-w： 只统计单词数
-m： 只统计字符数
~~~

示例

~~~cmd
cat 文件 | wc
~~~

输出三个数字分别代表 行，字数，字符数

### 双向重定向tee

tee会同时将数据流送与文件与屏幕

示例

~~~cmd
ls -l /home | tee ~/homefile |mor
~~~

这个范例则是将ls的数据存一份到~/homefile ，同时屏幕也有输出信息

### 字符转换命令：tr。col join paste expand

#### tr

 用来删除一段信息中的文字，或者对信息中的文字进行替换

tr [-ds] SET1 ...

-d 删除信息当中 SET1 这个字符串

-是替换掉重复的字符

示例

~~~cmd
last | tr ’[a-z]‘ '[A-Z]'
~~~

将输出信息中的所有小写字符变成大写字符   不加单引号也可在

#### col

col 【-xb】

-x 将tab键转换为对等的空格键

-b 将文字内有反斜巷 ’‘/"的仅保留反斜杠后面接的那个字符

#### join

处理两个文件的数据连接，将两个文件中相同的数据那一行加在一起

join 【-ti12】 file1 file2

-t：默认一空格符分离数据，并且对比，第一个字段的数据，如果两个文件相同，则将两个数据连接成一行，且第一字段放在第一个

-i：忽略大小写的差异

-1：整合数字的1 代表第一个文件要用哪个字段来分析的意思

-2：代表第二个文件要用哪个字段来分析

注 使用join之前最好 将文件用sort 进行排序

#### paste

类似 join 直接将相关的两行 用tab键 个烤站在一起

# 3.正则表达式

正则表达式用来在文件中匹配符合条件的
字符串， 正则是包含匹配。 grep、 awk、
sed等命令可以支持正则表达式。
通配符用来匹配符合条件的文件名，通配
符是完全匹配。 ls、 find、 cp这些命令不
支持正则表达式，所以只能使用shell自己
的通配符来进行匹配了。  

## 3.1正则表达式字符

| 元字符  | 作 用                                                        |
| ------- | ------------------------------------------------------------ |
| *       | 前一个字符匹配0次或任意多次。                                |
| .       | 匹配除了换行符外任意一个字符。                               |
| ^       | 匹配行首。 例如： ^hello会匹配以hello开头的行。              |
| $       | 匹配行尾。 例如： hello&会匹配以hello结尾的行。              |
| []      | 匹配中括号中指定的任意一个字符， 只匹配一个字符。 例如： [aoeiu] 匹配任意一个元音字母， [0-9] 匹配任意一位 数字， [a-z][0-9]匹配小写字和一位数字构成的两位字符。 |
| [^]     | 匹配除中括号的字符以外的任意一个字符。 例如： [^0-9] 匹配 任意一位非数字字符， [^a-z] 表示任意一位非小写字母。 |
| \       | 转义符。 用于取消讲特殊符号的含义取消。                      |
| \{n\}   | 表示其前面的字符恰好出现n次。 例如： [0-9]\{4\} 匹配4位数 字， [1][3-8][0-9]\{9\} 匹配手机号码。 |
| \{n,\}  | 表示其前面的字符出现不小于n次。 例如： [0-9]\{2,\} 表示两 位及以上的数字。 |
| \{n,m\} | 表示其前面的字符至少出现n次， 最多出现m次。 例如： [a z]\{6,8\} 匹配6到8位的小写字母 |

## 3.2字符说明

“*”前一个字符匹配0次，或任意多次  

grep "a*" test_rule.txt
\#匹配所有内容，包括空白行
grep "aa*" test_rule.txt
\#匹配至少包含有一个a的行
grep "aaa*" test_rule.txt
匹配最少包含两个连续a的字符串
grep "aaaaa*" test_rule.txt
\#则会匹配最少包含四个个连续a的字符串
“.” 匹配除了换行符外任意一个字符
grep "s..d" test_rule.txt
\#“s..d”会匹配在s和d这两个字母之间一定有两个字符的单词
grep "s.*d" test_rule.txt
\#匹配在s和d字母之间有任意字符
grep ".*" test_rule.txt
\#匹配所有内容
“^”匹配行首，“$”匹配行尾
grep "^M" test_rule.txt
\#匹配以大写“M”开头的行
grep "n$" test_rule.txt
\#匹配以小写“n”结尾的行
grep -n "^$" test_rule.txt
\#会匹配空白行
“[]” 匹配中括号中指定的任意一个
字符，只匹配一个字符
grep "s[ao]id" test_rule.txt
\#匹配s和i字母中，要不是a、要不是o
grep "[0-9]" test_rule.txt
\#匹配任意一个数字
grep "^[a-z]" test_rule.txt
\#匹配用小写字母开头的行
“[^]” 匹配除中括号的字符以外的
任意一个字符
grep "^[^a-z]" test_rule.txt
\#匹配不用小写字母开头的行
grep "^[^a-zA-Z]" test_rule.txt
\#匹配不用字母开头的行
“\” 转义符
grep "\.$" test_rule.txt
\#匹配使用“.”结尾的行
“\{n\}”表示其前面的字符恰好出现n次
grep "a\{3\}" test_rule.txt
\#匹配a字母连续出现三次的字符串
grep "[0-9]\{3\}" test_rule.txt
\#匹配包含连续的三个数字的字符串
“\{n,\}”表示其前面的字符出现不小于n次
grep "^[0-9]\{3,\}[a-z]" test_rule.txt
\#匹配最少用连续三个数字开头的行
“\{n,m\}”匹配其前面的字符至少出现n次，
最多出现m次
grep "sa\{1,3\}i" test_rule.txt
\#匹配在字母s和字母i之间有最少一个a，最多三个a  

## 3.3sed工具

## 3.4 扩展正则表达式

## 3.5格式化打印printf 与 数据处理工具 awk

printf不是管道命令