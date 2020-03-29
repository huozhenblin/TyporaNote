# 五、Docker

## 1、简介

**Docker**是一个开源的应用容器引擎；是一个轻量级容器技术；

Docker支持将软件编译成一个镜像；然后在镜像中各种软件做好配置，将镜像发布出去，其他使用者可以直接使用这个镜像；

运行中的这个镜像称为容器，容器启动是非常快速的。

![](D:/my/study/Typora书写的各种笔记/spring相关学习笔记/Spring Boot 笔记+课件/images/搜狗截图20180303145450.png)



![](D:/my/study/Typora书写的各种笔记/spring相关学习笔记/Spring Boot 笔记+课件/images/搜狗截图20180303145531.png)

## 2、核心概念

docker主机(Host)：安装了Docker程序的机器（Docker直接安装在操作系统之上）；

docker客户端(Client)：连接docker主机进行操作；

docker仓库(Registry)：用来保存各种打包好的软件镜像；

docker镜像(Images)：软件打包好的镜像；放在docker仓库中；

docker容器(Container)：镜像启动后的实例称为一个容器；容器是独立运行的一个或一组应用

![](D:/my/study/Typora书写的各种笔记/spring相关学习笔记/Spring Boot 笔记+课件/images/搜狗截图20180303165113.png)

使用Docker的步骤：

1）、安装Docker

2）、去Docker仓库找到这个软件对应的镜像；

3）、使用Docker运行这个镜像，这个镜像就会生成一个Docker容器；

4）、对容器的启动停止就是对软件的启动停止；

## 3、安装Docker

#### 1）、安装linux虚拟机

​	1）、VMWare、VirtualBox（安装）；

​	2）、导入虚拟机文件centos7-atguigu.ova；

​	3）、双击启动linux虚拟机;使用  root/ 123456登陆

​	4）、使用客户端连接linux服务器进行命令操作；

​	5）、设置虚拟机网络；

​		桥接网络===选好网卡====接入网线；

​	6）、设置好网络以后使用命令重启虚拟机的网络

```shell
service network restart
```

​	7）、查看linux的ip地址

```shell
ip addr
```

​	8）、使用客户端连接linux；

​	9）、进入管理员权限



#### 2）、在linux虚拟机上安装docker

步骤：

```shell
1、检查内核版本，必须是3.10及以上
uname -r
2、安装docker
yum install docker
3、输入y确认安装
4、启动docker
[root@localhost ~]# systemctl start docker
[root@localhost ~]# docker -v
Docker version 1.12.6, build 3e8e77d/1.12.6
5、开机启动docker
[root@localhost ~]# systemctl enable docker
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
6、停止docker
systemctl stop docker  重启换成restart
7.systemctl status docker 查看docker状态
```

3）、linux常用的一些设置

首先是dock阿里云的镜像的配置

其次是要获得用户权限的方法 su root 然后输入root的密码

## 4、Docker常用命令&操作

### 1）、镜像操作

| 操作 | 命令                                            | 说明                                                     |
| ---- | ----------------------------------------------- | -------------------------------------------------------- |
| 检索 | docker  search 关键字  eg：docker  search redis | 我们经常去docker  hub上检索镜像的详细信息，如镜像的TAG。 |
| 列表 | docker images                                   | 查看所有本地镜像  加-q  可以查看本地所有镜像id           |
| 拉取 | docker pull 镜像名:tag                          | :tag是可选的，tag表示标签，多为软件的版本，默认是latest  |
| 删除 | docker rmi image-id                             | 删除指定的本地镜像                                       |
|      |                                                 |                                                          |
|      |                                                 |                                                          |
|      |                                                 |                                                          |

https://hub.docker.com/

### 2）、容器操作

软件镜像（QQ安装程序）----运行镜像----产生一个容器（正在运行的软件，运行的QQ）；

步骤：

````shell
1、搜索镜像
[root@localhost ~]# docker search tomcat
2、拉取镜像
[root@localhost ~]# docker pull tomcat
3、根据镜像启动创建容器
docker run --name mytomcat -d tomcat:latest  
可选项：-it（创建后立即进入容器并且分配终端，退出时就关闭这个容器）  /bin/bash 表示进入容器初始化命令 -d 后台运行，需要命令才能进入和关闭
3.1进入一个容器
docker exec -it 表示分配终端 容器名或者id /bin/bash
docker run 参数
参数说明：
• -i：保持容器运行。通常与 -t 同时使用。加入it这两个参数后，容器创建后自动进入容器中，退出容器后，容器自动关闭。
• -t：为容器重新分配一个伪输入终端，通常与 -i 同时使用。
• -d：以守护（后台）模式运行容器。创建一个容器在后台运行，需要使用docker exec 进入容器。退出后，容器不会关闭。
• -it 创建的容器一般称为交互式容器， -id 创建的容器一般称为守护式容器
• --name：为创建的容器命名
4、docker ps  
查看运行中的容器
5、 停止运行中的容器
docker stop  容器的id
6、查看所有的启动和未启动的容器
docker ps -a
7、启动容器
docker start 容器id
8、删除一个容器
 docker rm 容器id
查看容器信息  docker inspect 容器名称
9、启动一个做了端口映射的tomcat
[root@localhost ~]# docker run -d -p 8888:8080 tomcat
-d：后台运行
-p: 将主机的端口映射到容器的一个端口    主机端口:容器内部的端口

10、为了演示简单关闭了linux的防火墙
service firewalld status ；查看防火墙状态
service firewalld stop：关闭防火墙
11、查看容器的日志
docker logs container-name/container-id

更多命令参看
https://docs.docker.com/engine/reference/commandline/docker/
可以参考每一个镜像的文档

````

注：我是用的是阿里的镜像，在部署tomcat是他的root目录下的webapps中没有东西，而访问首页是默认访问这个文件夹的内容，而另外有一个文件夹webapps.dist 有文件 则将其copy到webapps里面

- docker exec -it 【tomcat的容器id】/bin/bash
- 然后cp  -r  webapps.dist/*  ./webapps 执行copy命令
- exit 可以退出文件系统

### 3）、安装MySQL示例

```shell
docker pull mysql
```

注：使用5.7版本  能成功连接navicat

错误的启动

```shell
[root@localhost ~]# docker run --name mysql01 -d mysql
42f09819908bb72dd99ae19e792e0a5d03c48638421fa64cce5f8ba0f40f5846

mysql退出了
[root@localhost ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                           PORTS               NAMES
42f09819908b        mysql               "docker-entrypoint.sh"   34 seconds ago      Exited (1) 33 seconds ago                            mysql01
538bde63e500        tomcat              "catalina.sh run"        About an hour ago   Exited (143) About an hour ago                       compassionate_
goldstine
c4f1ac60b3fc        tomcat              "catalina.sh run"        About an hour ago   Exited (143) About an hour ago                       lonely_fermi
81ec743a5271        tomcat              "catalina.sh run"        About an hour ago   Exited (143) About an hour ago                       sick_ramanujan


//错误日志
[root@localhost ~]# docker logs 42f09819908b
error: database is uninitialized and password option is not specified 
  You need to specify one of MYSQL_ROOT_PASSWORD, MYSQL_ALLOW_EMPTY_PASSWORD and MYSQL_RANDOM_ROOT_PASSWORD；这个三个参数必须指定一个
```

正确的启动

```shell
[root@localhost ~]# docker run --name mysql01 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
b874c56bec49fb43024b3805ab51e9097da779f2f572c22c695305dedd684c5f
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
b874c56bec49        mysql               "docker-entrypoint.sh"   4 seconds ago       Up 3 seconds        3306/tcp            mysql01
```

做了端口映射

```shell
[root@localhost ~]# docker run -p 3306:3306 --name mysql02 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
ad10e4bc5c6a0f61cbad43898de71d366117d120e39db651844c0e73863b9434
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
ad10e4bc5c6a        mysql               "docker-entrypoint.sh"   4 seconds ago       Up 2 seconds        0.0.0.0:3306->3306/tcp   mysql02
```



几个其他的高级操作

```
docker run --name mysql03 -v /conf/mysql:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
把主机的/conf/mysql文件夹挂载到 mysqldocker容器的/etc/mysql/conf.d文件夹里面
改mysql的配置文件就只需要把mysql配置文件放在自定义的文件夹下（/conf/mysql）

docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
指定mysql的一些配置参数
```



## 5.容器的数据卷

### 概念

数据卷是宿主机中的一个目录或文件
• 当容器目录和数据卷目录绑定后，对方的修改会立即同步
• 一个数据卷可以被多个容器同时挂载
• 一个容器也可以被挂载多个数据卷

![image-20200329101038596](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200329101038596.png)

### 数据卷作用

• 容器数据持久  

- 外部机器和容器间接通信
  • 容器之间数据交换  

### 配置数据卷  

创建启动容器时，使用 –v 参数 设置数据卷
docker run ... –v 宿主机目录(文件):容器内目录(文件) ...
⚫ 注意事项：
\1. 目录必须是绝对路径
\2. 如果目录不存在，会自动创建
\3. 可以挂载多个数据卷  

### 配置数据卷容器  

![image-20200329102933468](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200329102933468.png)

#### 1. 创建启动c3数据卷容器，使用 –v 参数 设置数据卷

```shell
docker run –it --name=c3 –v /volume centos:7 /bin/bash
```



v后不加数据宿主机会自动分配目录

#### 2. 创建启动 c1 c2 容器，使用 –-volumes-from 参数(数据卷容器名) 设置数据卷

```shell
docker run –it --name=c1 --volumes-from c3 centos:7 /bin/bash
docker run –it --name=c2 --volumes-from c3 centos:7 /bin/bash  
```



### 数据卷小结

#### 1. 数据卷概念

• 宿主机的一个目录或文件

#### 2. 数据卷作用

• 容器数据持久化
• 客户端和容器数据交换
• 容器间数据交换

#### 3. 数据卷容器

• 创建一个容器，挂载一个目录，让其他容器继承自该容器( --volume-from )。
• 通过简单方式实现数据卷配置  

## 6.应用的部署

### MySQL部署  

• 容器内的网络服务和外部机器不能直接通信
• 外部机器和宿主机可以直接通信
• 宿主机和容器可以直接通信
• 当容器中的网络服务需要被外部机器访问时，可以将容器中提供服务的端口映射到宿主机的端口上。外部机
器访问宿主机的该端口，从而间接访问容器的服务。
• 这种操作称为： 端口映射  

![image-20200329105854523](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200329105854523.png)