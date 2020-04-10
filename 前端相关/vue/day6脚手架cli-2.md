# 1.什么是vue cli

## 1.1n**CLI****是什么意思****?**

CLI是Command-Line Interface, 翻译为命令行界面, 但是俗称脚手架.

Vue CLI是一个官方发布 vue.js 项目脚手架

使用 vue-cli 可以快速搭建Vue开发环境以及对应的webpack配置.

## 1.2**Vue** **CLI****使用前提** **-** **Node**

### 1.2.1**安装****NodeJS**

##### 注：cnpm安装

由于国内直接使用 npm 的官方镜像是非常慢的，这里推荐使用淘宝 NPM 镜像。

你可以使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:

npm install -g cnpm --registry=https://registry.npm.taobao.org

这样就可以使用 cnpm 命令来安装模块了：

cnpm install [name]

#### 1.2.2**什么是****NPM****呢****?**

NPM的全称是Node Package Manager

是一个NodeJS包管理和分发工具，已经成为了非官方的发布Node模块（包）的标准。

后续我们会经常使用NPM来安装一些开发过程中依赖包.

# **2.Vue** **CLI****的使用**

## 2.1安装Vue脚手架

安装一个全局的就行

对应命令 npm install -g @vue/cli

#### 注意：

上面安装的是Vue CLI3的版本，如果需要想按照Vue CLI2的方式初始化项目时不可以的。

![image-20200315144356919](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200315144356919.png)

### Vue CLI2初始化项目

vue init webpack my-project

### Vue CLI3初始化项目

vue create my-project

# **3.Vue** **CLI2****详解**

#### 创建过程中的各个选项

![image-20200315144552335](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200315144552335.png)

#### 生成的目录结构

![image-20200315144623389](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200315144623389.png)

# 4.**Runtime-Compiler**和**Runtime-only**的区别

![image-20200316133721709](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316133721709.png)



- 如果在之后的开发中，你依然使用template，就需要选择Runtime-Compiler

- 如果你之后的开发中，使用的是.vue文件夹开发，那么可以选择Runtime-only

执行流程

![image-20200316162026268](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316162026268.png)

![image-20200316162112206](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316162112206.png)

![image-20200316162124643](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316162124643.png)

**![image-20200316162131695](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316162131695.png)**

## npm run build运行流程

![image-20200316164307156](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316164307156.png)

## npm run dev 运行流程

![image-20200316164346046](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316164346046.png)

# 5.脚手架3

## 1.cli2和3的区别

- vue-cli 3 是基于 webpack 4 打造，vue-cli 2 还是 webapck 3

- vue-cli 3 的设计原则是“0配置”，移除的配置文件根目录下的，build和config等目录

- vue-cli 3 提供了 vue ui 命令，提供了可视化配置，更加人性化

- 移除了static文件夹，新增了public文件夹，并且index.html移动到public中

2.创建过程

执行 npm create myprojectname

过程如下图

![	](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316164630860.png)

3.目录结构

![image-20200316164653029](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316164653029.png)

4.配置管理

脚手架三的配置与会是一个本地服务的形式以往也得型市场线

只需要在终端执行命令 npm ui 即可

![image-20200317090956857](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200317090956857.png)

5.自定义配置：起别名

自己创建一个vue.config.js文件

![image-20200317093247660](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200317093247660.png)









































