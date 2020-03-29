```powershell
git init  
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/huozhenblin/testmall.git
git push -u origin master
```

# 使用过程

1.首先进行初始化，讲你的项目变成git可以管理的仓库，这时会有一个隐藏的 .git文件  通过  ls -ah 可以开到 ，这个vscode脚手架创建的文件自带

2，git add .(文件name) //添加文件到本地仓库  git add .  这个命令可以保存你的修改的所有文件

3.git commit -m “first commit” //添加文件描述信息

4.git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支

5.git push -u origin master //把本地仓库的文件推送到远程仓库

# 所遇问题

## 问题一 报错

出现报错

Updates were rejected because the remote contains work that you do]

### 方法一

\1. git init //初始化仓库



\2. git add .(文件name) //添加文件到本地仓库



\3. git commit -m "first commit" //添加文件描述信息



\4. git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支



\5. git pull origin master // 把本地仓库的变化连接到远程仓库主分支



\6. git push -u origin master //把本地仓库的文件推送到远程仓库

### 方法二

git push -f origin master

强制push

## 问题二：重复输入github账号密码

在clone 项目的时候，使用了 https方式，而不是ssh方式。

远程连接时使用ssh



### github创建ssh的方法

##### 第一步、首先，检查下自己之前有没有已经生成：

在开始菜单中打开git下的git bash（当然，在其他目录下打开git bash也是一样的）：
然后执行

```
ls -al ~/.ssh 
1
```

##### 第二步、如果能进入到.ssh文件目录下 ，则证明，之前生成过.ssh秘钥，可以直接使用里面的秘钥。

如果不能进入到.ssh文件目录下，则：

检测下自己之前有没有配置：

```
git config user.name和git config user.email（直接分别输入这两个命令）
1
```

如果之前没有创建，则执行以下命令：

```
git config –global user.name ‘xxxxx’ 
git config –global user.email ‘xxx@xx.xxx’
12
```

生成秘钥

```
ssh-keygen -t rsa -C ‘上面的邮箱’
1
```

代码参数含义：

-t 指定密钥类型，默认是 rsa ，可以省略。
-C 设置注释文字，比如邮箱。
-f 指定密钥文件存储文件名。

接着按3个回车

```
[root@localhost ~]# ssh-keygen -t rsa       <== 建立密钥对，-t代表类型，有RSA和DSA两种
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):   <==密钥文件默认存放位置，按Enter即可
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase):     <== 输入密钥锁码，或直接按 Enter 留空
Enter same passphrase again:     <== 再输入一遍密钥锁码
Your identification has been saved in /root/.ssh/id_rsa.    <== 生成的私钥
Your public key has been saved in /root/.ssh/id_rsa.pub.    <== 生成的公钥
The key fingerprint is:
SHA256:K1qy928tkk1FUuzQtlZK+poeS67vIgPvHw9lQ+KNuZ4 root@localhost.localdomain
The key's randomart image is:
+---[RSA 2048]----+
|           +.    |
|          o * .  |
|        . .O +   |
|       . *. *    |
|        S =+     |
|    .    =...    |
|    .oo =+o+     |
|     ==o+B*o.    |
|    oo.=EXO.     |
+----[SHA256]-----+

1234567891011121314151617181920212223
```

最后在.ssh目录下(C盘用户文件夹下)得到了两个文件：id_rsa（私有秘钥）和id_rsa.pub（公有密钥）

##### 第三步、如果想登陆远端，则需要将rsa.pub里的秘钥添加到远端。

首先，去.ssh目录下找到id_rsa.pub这个文件夹打开复制全部内容。

接着：

1.登录GitHub，进入你的Settings
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061921352777.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NDk1MzM5,size_16,color_FFFFFF,t_70)
2.会看到左边这些目录，点击SSH and GPG keys
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190619213552339.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NDk1MzM5,size_16,color_FFFFFF,t_70)
3.创建New SSH key
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190619213619807.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NDk1MzM5,size_16,color_FFFFFF,t_70)
4.粘贴你的密钥到你key输入框中
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190619213715333.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1NDk1MzM5,size_16,color_FFFFFF,t_70)
5.点击Add SSH key
6.再弹出窗口，输入你的GitHub密码，点击确认按钮。
7.到此，就大功告成了。

##### 第四步 测试。

在命令窗口上输入 ssh -T ssh -T [git@github.com](mailto:git@github.com) 按回车键，如看到以下信息，那么就完美了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190619221201430.png)