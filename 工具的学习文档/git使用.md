# 1.常用命令

## 基本使用命令

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

## 其他命令

~~~shell
 # 删除工作区文件，并且将这次删除放入暂存区
 git rm [file1] [file2] ...
 # 停止追踪指定文件，但该文件会保留在工作区
 git rm --cached [file]
 # 改名文件，并且将这个改名放入暂存区
 git mv [file-original] [file-renamed]
~~~

### 标签

~~~shell
# 列出所有tag
 
$ git tag
 
 
 
# 新建一个tag在当前commit
 
$ git tag [tag]
 
 
 
# 新建一个tag在指定commit
 
$ git tag [tag] [commit]
 
 
 
# 删除本地tag
 
$ git tag -d [tag]
 
 
 
# 删除远程tag
 
$ git push origin :refs/tags/[tagName]
 
 
 
# 查看tag信息
 
$ git show [tag]
 
 
 
# 提交指定tag
 
$ git push [remote] [tag]
 
 
 
# 提交所有tag
 
$ git push [remote] --tags
 
 
 
# 新建一个分支，指向某个tag
 
$ git checkout -b [branch] [tag]
~~~

### 查看信息

~~~shell
 
 
 
# 显示有变更的文件
 
$ git status
 
 
 
# 显示当前分支的版本历史
 
$ git log
 
 
 
# 显示commit历史，以及每次commit发生变更的文件
 
$ git log --stat
 
 
 
# 搜索提交历史，根据关键词
 
$ git log -S [keyword]
 
 
 
# 显示某个commit之后的所有变动，每个commit占据一行
 
$ git log [tag] HEAD --pretty=format:%s
 
 
 
# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
 
$ git log [tag] HEAD --grep feature
 
 
 
# 显示某个文件的版本历史，包括文件改名
 
$ git log --follow [file]
 
$ git whatchanged [file]
 
 
 
# 显示指定文件相关的每一次diff
 
$ git log -p [file]
 
 
 
# 显示过去5次提交
 
$ git log -5 --pretty --oneline
 
 
 
# 显示所有提交过的用户，按提交次数排序
 
$ git shortlog -sn
 
 
 
# 显示指定文件是什么人在什么时间修改过
 
$ git blame [file]
 
 
 
# 显示暂存区和工作区的差异
 
$ git diff
 
 
 
# 显示暂存区和上一个commit的差异
 
$ git diff --cached [file]
 
 
 
# 显示工作区与当前分支最新commit之间的差异
 
$ git diff HEAD
 
 
 
# 显示两次提交之间的差异
 
$ git diff [first-branch]...[second-branch]
 
 
 
# 显示今天你写了多少行代码
 
$ git diff --shortstat "@{0 day ago}"
 
 
 
# 显示某次提交的元数据和内容变化
 
$ git show [commit]
 
 
 
# 显示某次提交发生变化的文件
 
$ git show --name-only [commit]
 
 
 
# 显示某次提交时，某个文件的内容
 
$ git show [commit]:[filename]
 
 
 
# 显示当前分支的最近几次提交
 
$ git reflog
~~~

### 远程同步

~~~shell
 
 
 
# 下载远程仓库的所有变动
 
$ git fetch [remote]
 
 
 
# 显示所有远程仓库
 
$ git remote -v
 
 
 
# 显示某个远程仓库的信息
 
$ git remote show [remote]
 
 
 
# 增加一个新的远程仓库，并命名
 
$ git remote add [shortname] [url]
 
 
 
# 取回远程仓库的变化，并与本地分支合并
 
$ git pull [remote] [branch]
 
 
 
# 上传本地指定分支到远程仓库
 
$ git push [remote] [branch]
 
 
 
# 强行推送当前分支到远程仓库，即使有冲突
 
$ git push [remote] --force
 
 
 
# 推送所有分支到远程仓库
 
$ git push [remote] --all
~~~

### 撤销

~~~shell
 
 
 
# 恢复暂存区的指定文件到工作区
 
$ git checkout [file]
 
 
 
# 恢复某个commit的指定文件到暂存区和工作区
 
$ git checkout [commit] [file]
 
 
 
# 恢复暂存区的所有文件到工作区
 
$ git checkout .
 
 
 
# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
 
$ git reset [file]
 
 
 
# 重置暂存区与工作区，与上一次commit保持一致
 
$ git reset --hard
 
 
 
# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
 
$ git reset [commit]
 
 
 
# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
 
$ git reset --hard [commit]
 
 
 
# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
 
$ git reset --keep [commit]
 
 
 
# 新建一个commit，用来撤销指定commit
 
# 后者的所有变化都将被前者抵消，并且应用到当前分支
 
$ git revert [commit]
 
 
 
# 暂时将未提交的变化移除，稍后再移入
 
$ git stash
 
$ git stash pop
~~~



# 2.所遇问题

## 2.1问题一 报错

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

## 2.2问题二：重复输入github账号密码

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

# 分支创建与合并

## 1.分支使用

### 步骤：

- 创建分支 git branch  分支名字
- 切换到该分支 git  checkout  分支名字
- 将本地分支推送到远程，即远程创建分支 git push origin [branch name]
- 在该分支内进行工作
- add 分支内的文件 然后 commit 
- push到远程分支
- 稳定后融合时，在工作区内切回到主分支
- 尽情融合命令，然后提交 再push到远程主分支

## 2.分支相关命令

创建切换分支命令：

```powershell
$ git branch [branch-name]  //创建分支
$ git checkout [branch-name]  # 切换到指定分支，并更新工作区
# 新建一个分支，并切换到该分支
$ git checkout -b [branch name]
# 新建一个分支，但依然停留在当前分支
 git branch [branch-name]
 # 切换到上一个分支
 $ git checkout -
 # 删除分支
  git branch -d [branch-name]
  # 删除远程分支
  $ git push origin --delete [branch-name]
```

将分支推送到github

```shell
git push origin [branch name]
```



查看本地分支：带星号的为当前工作目录

```shell
#查看当前分支
$ git branch
* dev
  master
$ git branch -r //查看远程分支
$ git branch -a  //查看所有分支，包括本地和远程
```



融合分支：将分支融合到另一个支（融合时，工作区要在目的分支即另一个分支）

```shell
$ git merge dev
```

删除分支

```shell
$ git branch -d [branch name]  
git push origin :[branch name]  //删除github远程分支
```

# idea中忽略不想提交的文件

在.gitignore中进行设置相关文件

```
下面是一些.gitignore文件忽略的匹配规则：

*.a       # 忽略所有 .a 结尾的文件
!lib.a    # 但 lib.a 除外
/TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/    # 忽略 build/ 目录下的所有文件
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

但是只对未跟踪文件有效，使用命令取消追踪

使用git rm --cached 文件名ming命令

即在commit时不用再担心忘记取消勾选不想上传git的文件了