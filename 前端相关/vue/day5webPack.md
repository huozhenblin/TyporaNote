# Vue.js - Day5 - Webpack

## 1.概念

### 1.1在网页中会引用哪些常见的静态资源？

+ JS
 - .js  .jsx  .coffee  .ts（TypeScript  类 C# 语言）
+ CSS
 - .css  .less   .sass  .scss
+ Images
 - .jpg   .png   .gif   .bmp   .svg
+ 字体文件（Fonts）
 - .svg   .ttf   .eot   .woff   .woff2
+ 模板文件
 - .ejs   .jade  .vue【这是在webpack中定义组件的方式，推荐这么用】


### 1.2网页中引入的静态资源多了以后有什么问题？？？
1. 网页加载速度慢， 因为 我们要发起很多的二次请求；
2. 要处理错综复杂的依赖关系


### 1.3如何解决上述两个问题
1. 合并、压缩、精灵图、图片的Base64编码
2. 可以使用之前学过的requireJS、也可以使用webpack可以解决各个包之间的复杂依赖关系；

### 1.4什么是webpack?
webpack 是前端的一个项目构建工具，它是基于 Node.js 开发出来的一个前端工具；


### 1.5如何完美实现上述的2种解决方案
1. 使用Gulp， 是基于 task 任务的；
2. 使用Webpack， 是基于整个项目进行构建的；
+ 借助于webpack这个前端自动化构建工具，可以完美实现资源的合并、打包、压缩、混淆等诸多功能。
+ 根据官网的图片介绍webpack打包的过程
+ [webpack官网](http://webpack.github.io/)

## 2.webpack安装和使用

1. 运行`npm install webpack@版本号 -g`全局安装webpack，这样就能在全局使用webpack的命令
2. 在项目根目录中运行`npm i webpack --save-dev`安装到项目依赖中

### 2.1 简单的起步使用

基础的目录结构入下

![image-20200309114348090](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200309114348090.png)

- 我们创建如下文件和文件夹：

**文件和文件夹解析：**

- dist文件夹：用于存放之后打包的文件
- src文件夹：用于存放我们写的源文件
  - main.js：项目的入口文件。所有的文件都在这里面引入进行以来配置。
  - mathUtils.js：定义了一些数学工具函数，可以在其他地方引用，并且使用。具体内容查看下面的详情。

- index.html：浏览器打开展示的首页html

- package.json：通过npm init生成的，npm包管理的文件（暂时没有用上，后面才会用上）

- mathUtils.js文件中的代码：

- main.js文件中的代码
- 入口和出口作为参数
  - 入口函数例如main.js
  - 出口函数bundle.js

打包的指令示例如下

```cmd
 webpack .\src\main.js .\dist\bundle.js
```

打包完成后会在bundle文件重生成各种以来管理的配置文件

### 2.2初步使用webpack打包构建列表隔行变色案例

1. 运行`npm init`初始化项目，使用npm管理项目中的依赖包
2. 创建项目基本的目录结构
3. 使用`cnpm i jquery --save`安装jquery类库
4. 创建`main.js`并书写各行变色的代码逻辑：
```
	// 导入jquery类库
    import $ from 'jquery'

    // 设置偶数行背景色，索引从0开始，0是偶数
    $('#list li:even').css('backgroundColor','lightblue');
    // 设置奇数行背景色
    $('#list li:odd').css('backgroundColor','pink');
```
5. 直接在页面上引用`main.js`会报错，因为浏览器不认识`import`这种高级的JS语法，需要使用webpack进行处理，webpack默认会把这种高级的语法转换为低级的浏览器能识别的语法；
6. 运行`webpack 入口文件路径 输出文件路径`对`main.js`进行处理：
```
webpack src/js/main.js dist/bundle.js
```

### 2.3使用webpack的配置文件简化打包时候的命令
1. 在项目根目录中创建`webpack.config.js` 
2. 由于运行webpack命令的时候，webpack需要指定入口文件和输出文件的路径，所以，我们需要在`webpack.config.js`中配置这两个路径：
```javascript
    // 导入处理路径的模块，要有一个node包才能有效
    var path = require('path');

    // 导出一个配置对象，将来webpack在启动的时候，会默认来查找webpack.config.js，并读取这个文件中导出的配置对象，来进行打包处理
    module.exports = {
        resolve函数功能是拼接
        entry: path.resolve(__dirname,//应用上下文路径，也就是根路径 'src/js/main.js'), // 项目入口文件
        output: { // 配置输出选项
            path: path.resolve(__dirname, 'dist'), // 配置输出的路径
            filename: 'bundle.js' // 配置输出的文件名
        }
    }
```

### 2.4命令 npm run *  运行脚本

首先配置映射让这个命令和webpack连接起来

原理：在使用npm run 。。命令时 会在配置文件

package.json中寻找scripts脚本属性中。。的对应属性 并加入后面的值然后执行命令

注：和直接使用webpack不同 它直接使用本项目的东西

```json
{
  "name": "meetwebpack",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {//表示开发时依赖，Dependencies表示上线运行时的依赖
    "webpack": "^3.6.0"
  },
  "description": ""
}
```

### 2.5 具体的项目安装自己的本地webpack

具体命令为：

--save-dev 表示开发时依赖

```cmd
npm install --save-dev webpack@<version>
```

执行后会多一个node_modules配置文件与此同时package.json文件中的devDependencies开发时依赖属性也会多一个  "webpack": "^3.6.0"  键值对

### 2.6实现webpack的实时打包构建

1. 由于每次重新修改代码之后，都需要手动运行webpack打包的命令，比较麻烦，所以使用`webpack-dev-server`来实现代码实时打包编译，当修改代码之后，会自动进行打包构建。
2. 运行`cnpm i webpack-dev-server --save-dev`安装到开发依赖
3. 安装完成之后，在命令行直接运行`webpack-dev-server`来进行打包，发现报错，此时需要借助于`package.json`文件中的指令，来进行运行`webpack-dev-server`命令，在`scripts`节点下新增`"dev": "webpack-dev-server"`指令，发现可以进行实时打包，但是dist目录下并没有生成`bundle.js`文件，这是因为`webpack-dev-server`将打包好的文件放在了内存中
 + 把`bundle.js`放在内存中的好处是：由于需要实时打包编译，所以放在内存中速度会非常快
 + 这个时候访问webpack-dev-server启动的`http://localhost:8080/`网站，发现是一个文件夹的面板，需要点击到src目录下，才能打开我们的index首页，此时引用不到bundle.js文件，需要修改index.html中script的src属性为:`<script src="../bundle.js"></script>`
 + 为了能在访问`http://localhost:8080/`的时候直接访问到index首页，可以使用`--contentBase src`指令来修改dev指令，指定启动的根目录：
 ```
 "dev": "webpack-dev-server --contentBase src"
 ```
 同时修改index页面中script的src属性为`<script src="bundle.js"></script>`

### 2.7 loader的使用和概念

#### 概念

- loader是webpack中一个非常核心的概念。

- 在开发中我们不仅仅有基本的js代码处理，我们也需要加载css、图片，也包括一些高级的将ES6转成ES5代码，将TypeScript转成ES5代码，将scss、less转成css，将.jsx、.vue文件转成js文件等等。
- webpack本身的能力来说，对于这些转化是不支持的，给webpack扩展对应的loader就可以啦。

#### 使用

- 步骤一：通过npm安装需要使用的loader

例如css文件的使用

创建css文件并且引入到main函数中

导入的方式很多

```js
import style from './file.css';
```

安装对应的loader

```bash
npm install style-loader --save-dev
npm install css-loader --save-dev
```

在**webpack.config.js**配置文件中配置如下

1.   css-loader 只负责加载不负责解析
2.  style-loader 只负责将样式添加到dom中 
3.   使用多个loader时是从右从向左读

```js
module.exports = {
   entry: path.resolve(__dirname, 'src/main.js'),
   output: { 
     path: path.resolve(__dirname, 'dist'),
   },
   module: {
     rules: [{
       test: /\.css$/,
       use: ['style-loader', 'css-loader']
     }, ],
   }
 }
```

然后进行重新打包 npm run build

大部分loader我们都可以在webpack的官网中找到，并且学习对应的用法

https://webpack.docschina.org/loaders/

##### 2.7.1使用less文件

​	类似css文件的使用

编写.less文件

导入

```js

require('./css/special.less')
```

首先下载less 和对应的loader

```console
npm install less-loader less --save-dev 
```

然后，修改 `webpack.config.js`：

```js
module.exports = {
  ...
  module: {
    rules: [{
      test: /\.less$/,
      use: [{
        loader: 'style-loader' // creates style nodes from JS strings
      }, {
        loader: 'css-loader' // translates CSS into CommonJS
      }, {
        loader: 'less-loader' // compiles Less to CSS
      }]
    }]
  }
};
```

##### 2.7.2图片处理

首先安装对应的loader

```console
npm install url-loader --save-dev
npm install file-loader --save-dev
```

然后在配置文件中

注意小于文件大小限制时会将图片格式转化为base64格式，如果图片的大小大于配置中所限制的大小，那么就需要使用file-loader

但是在使用这个文件时会在dist文件中生成一个打包好的复制图片，然后引用的src会引用原来的，会导致引用地址失效，

```js
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/i,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192
            }
          }
        ]
      }
    ]
  }
}
```

为了正常显示打包中的图片需要配置如下

```javascript
output: { // 配置输出选项
       path: path.resolve(__dirname, 'dist'), // 配置输出的路径
       filename: 'bundle.js', // 配置输出的文件名
       publicPath: 'dist/'//这个会在生成的图片地址前面加上dist/
      },
```

更改打包的图片的名字

![image-20200310200958459](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200310200958459.png)未打包前

使用url-loader配置中的一个可选项，进行名字的改变会，然后进行重新打包

```javascript
{
          test: /\.(png|jpg|gif)$/i,
          use: [
            {
              loader: 'url-loader',
              options: {
                limit: 8000,
                name: 'imges/[name].[hash:8].[ext]'
              }
              
            }
          ]
        }
```

打包后![image-20200310201229660](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200310201229660.png)名字为images文件夹下原名+‘。’+八位哈希值的名字

##### 2.7.3es6转es5的babel

- 如果希望将ES6的语法转成ES5，那么就需要使用babel。

- 而在webpack中，我们直接使用babel对应的loader就可以了。

  指令为

  ```cmd
  npm install --save-dev babel-loader@7 babel-core babel-preset-es2015 本站老师的
  
  ```

  ```cmd
  npm install -D babel-loader @babel/core @babel/preset-env  官方的      webpack
  ```

  在配置文件中配置

  ```cmd
  {
        test: /\.m?js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env']
             //按照bzhan老师的 presets: ['es2015']
          }
        }
      }
  ```

#### 2.8webpack与vue

##### 简单使用：

首先需要导入vue依赖

```cmd
npm install vue --save
```

然后就可以在js文件向使用导入命令导入vue.js，然后开始书写相关的代码

```javascript
import Vue from 'vue'
```

vue的两个版本

- runtime-only->代码中，不可以有template
- runtime-compiler 代码中可以有template，因为有compiler可以用于编译template

上述如果不进行配置的话，默认使用运行版，如果需要完整版的话需在配置文件中加入下面的配置

```javascript



完整版：同时包含编译器和运行时的版本。

编译器：用来将模板字符串编译成为 JavaScript 渲染函数的代码。

运行时：用来创建 Vue 实例、渲染并处理虚拟 DOM 等的代码。基本上就是除去编译器的其它一切。

ES Module：从 2.6 开始 Vue 会提供两个 ES Modules (ESM) 构建文件：

为打包工具提供的 ESM：为诸如 webpack 2 或 Rollup 提供的现代打包工具。ESM 格式被设计为可以被静态分析，所以打包工具可以利用这一点来进行“tree-shaking”并将用不到的代码排除出最终的包。为这些打包工具提供的默认文件 (pkg.module) 是只有运行时的 ES Module 构建 (vue.runtime.esm.js)。

为浏览器提供的 ESM (2.6+)：用于在现代浏览器中通过 <script type="module"> 直接导入。

运行时 + 编译器 vs. 只包含运行时
如果你需要在客户端编译模板 (比如传入一个字符串给 template 选项，或挂载到一个元素上并以其 DOM 内部的 HTML 作为模板)，就将需要加上编译器，即完整版：

// 需要编译器
new Vue({
  template: '<div>{{ hi }}</div>'
})

// 不需要编译器
new Vue({
  render (h) {
    return h('div', this.hi)
  }
})
当使用 vue-loader 或 vueify 的时候，*.vue 文件内部的模板会在构建时预编译成 JavaScript。你在最终打好的包里实际上是不需要编译器的，所以只用运行时版本即可。

因为运行时版本相比完整版体积要小大约 30%，所以应该尽可能使用这个版本。如果你仍然希望使用完整版，则需要在打包工具里配置一个别名：

webpack
module.exports = {
  // ...
  resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js' 
    }
  }
}
```

##### **el**和**template区别**：

- 正常运行之后，我们来考虑另外一个问题：
  - 如果我们希望将data中的数据显示在界面中，就必须是修改index.html
  - 如果我们后面自定义了组件，也必须修改index.html来使用组件
  - 但是html模板在之后的开发中，我并不希望手动的来频繁修改，是否可以做到呢？

定义template属性：

- 在前面的Vue实例中，我们定义了el属性，用于和index.html中的#app进行绑定，让Vue实例之后可以管理它其中的内容	

- 这里，我们可以将div元素中的{{message}}内容删掉，只保留一个基本的id为div的元素

- 但是如果我依然希望在其中显示{{message}}的内容，应该怎么处理呢？

- 我们可以再定义一个template属性，代码如下：

这个 template属性有下面的功能 定义的模板会将#app这个属性的根标签内所有的东西整个替换掉

![image-20200311204141648](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200311204141648.png)

- 重新打包，运行程序，显示一样的结果和HTML代码结构
- 那么，el和template模板的关系是什么呢？
- 在我们之前的学习中，我们知道el用于指定Vue要管理的DOM，可以帮助解析其中的指令、事件监听等等。
- 而如果Vue实例中同时指定了template，那么template模板的内容会替换掉挂载的对应el的模板。
- 这样做有什么好处呢？
- 这样做之后我们就不需要在以后的开发中再次操作index.html，只需要在template中写入对应的标签即可
- 但是，书写template模块非常麻烦怎么办呢？
- 没有关系，稍后我们会将template模板中的内容进行抽离。
- 会分成三部分书写：template、script、style，结构变得非常清晰。

##### vue引入组件化开发

安装相应的mudel

```javascript
npm install vue-loader vue-template-compiler --save-dev

```

在配置文件中配置相应得配置

```cmd
 {
        test: /\.vue$/,
        use: ['vue-loader']
      }
```

然后将想用的代码抽出到一个 .vue文件中去

template标签内负责写模板代码。

script标签内负责写vue等代码

style标签内负责写样式

APP.vue

```html
<template>
  <div>
      <h1 class="tittle">fangzau .vuewenjian zhong 替换后的样子zhouquzaichouq</h1>
      {{message}}
    <button @click="myclick">按钮{{name}}</button>
    <Cpn></Cpn>
  </div>
</template>

<script type="text/ecmascript-6">

import Cpn from "./Cpn.vue";

export default {
  name: "App",
  components: {
    Cpn
  },
  data() {
    return {
      message: "hello webpack",
      name: "shilin"
    };
  },
  methods: {
    myclick() {
      this.name = "huodada";
    }
  }
};
</script>

<style scoped>
.tittle {
  color: rgb(50, 41, 184);
}
</style>

```

在入口函数中引入：

```html
import App from "./vue/App.vue";
new Vue({
  el: '#app',
  template: '<App/>',
  components:{
    App
  }
})
```

### 2.9 webpack与plugin

##### 概念

- plugin是插件的意思，通常是用于对某个现有的架构进行扩展。

- webpack中的插件，就是对webpack现有功能的各种扩展，比如打包优化，文件压缩等等。
- ploader主要用于转换某些类型的模块，它是一个转换器。
- plugin是插件，它是对webpack本身的扩展，是一个扩展器

##### plugin使用

- 步骤一：通过npm安装需要使用的plugins(某些webpack已经内置的插件不需要安装)

- 步骤二：在webpack.config.js中的plugins中配置插件。



使用`html-webpack-plugin`插件配置启动页面

由于使用`--contentBase`指令的过程比较繁琐，需要指定启动的目录，同时还需要修改index.html中script标签的src属性，所以推荐大家使用`html-webpack-plugin`插件配置启动页面.
1. 运行`cnpm i html-webpack-plugin --save-dev`安装到开发依赖
2. 修改`webpack.config.js`配置文件如下：
```
    // 导入处理路径的模块
    var path = require('path');
    // 导入自动生成HTMl文件的插件
    var htmlWebpackPlugin = require('html-webpack-plugin');

    module.exports = {
        entry: path.resolve(__dirname, 'src/js/main.js'), // 项目入口文件
        output: { // 配置输出选项
            path: path.resolve(__dirname, 'dist'), // 配置输出的路径
            filename: 'bundle.js' // 配置输出的文件名
        },
        plugins:[ // 添加plugins节点配置插件
            new htmlWebpackPlugin({
                template:path.resolve(__dirname, 'src/index.html'),//模板路径
                filename:'index.html'//自动生成的HTML文件的名称
            })
        ]
    }
```
3. 修改`package.json`中`script`节点中的dev指令如下：
```
"dev": "webpack-dev-server"
```
4. 将index.html中script标签注释掉，因为`html-webpack-plugin`插件会自动把bundle.js注入到index.html页面中！

## 3.搭建本地服务器

nwebpack提供了一个可选的本地开发服务器，这个本地服务器基于node.js搭建，内部使用express框架，可以实现我们想要的让浏览器自动刷新显示我们修改后的结果。

首先进行安装其模块

npm install --save-dev webpack-dev-server@2.9.1

然后砸其配置文件中进行配置

config.js中

```json
 devServer: {
    contentBase: './dist',
    inline: true
  }
```

devserver也是作为webpack中的一个选项，选项本身可以设置如下属性：

- contentBase：为哪一个文件夹提供本地服务，默认是根文件夹，我们这里要填写./dist

- port：端口号

- inline：页面实时刷新

- historyApiFallback：在SPA页面中，依赖HTML5的history模式



package.json中配置内部命令

~~~json
"dev": "webpack-dev-server --open"
~~~

## 4.配置文件的分离







## 实现自动打开浏览器、热更新和配置浏览器的默认端口号

**注意：热更新在JS中表现的不明显，可以从一会儿要讲到的CSS身上进行介绍说明！**
### 方式1：
+ 修改`package.json`的script节点如下，其中`--open`表示自动打开浏览器，`--port 4321`表示打开的端口号为4321，`--hot`表示启用浏览器热更新：
```
"dev": "webpack-dev-server --hot --port 4321 --open"
```

### 方式2：
1. 修改`webpack.config.js`文件，新增`devServer`节点如下：
```
devServer:{
        hot:true,
        open:true,
        port:4321
    }
```
2. 在头部引入`webpack`模块：
```
var webpack = require('webpack');
```
3. 在`plugins`节点下新增：
```
new webpack.HotModuleReplacementPlugin()
```

## 使用webpack打包css文件
1. 运行`cnpm i style-loader css-loader --save-dev`
2. 修改`webpack.config.js`这个配置文件：
```
module: { // 用来配置第三方loader模块的
        rules: [ // 文件的匹配规则
            { test: /\.css$/, use: ['style-loader', 'css-loader'] }//处理css文件的规则
        ]
    }
```
3. 注意：`use`表示使用哪些模块来处理`test`所匹配到的文件；`use`中相关loader模块的调用顺序是从后向前调用的；

## 使用webpack打包less文件
1. 运行`cnpm i less-loader less -D`
2. 修改`webpack.config.js`这个配置文件：
```
{ test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
```

## 使用webpack打包sass文件
1. 运行`cnpm i sass-loader node-sass --save-dev`
2. 在`webpack.config.js`中添加处理sass文件的loader模块：
```
{ test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
```

## 使用webpack处理css中的路径
1. 运行`cnpm i url-loader file-loader --save-dev`
2. 在`webpack.config.js`中添加处理url路径的loader模块：
```
{ test: /\.(png|jpg|gif)$/, use: 'url-loader' }
```
3. 可以通过`limit`指定进行base64编码的图片大小；只有小于指定字节（byte）的图片才会进行base64编码：
```
{ test: /\.(png|jpg|gif)$/, use: 'url-loader?limit=43960' },
```

## 使用babel处理高级JS语法
1. 运行`cnpm i babel-core babel-loader babel-plugin-transform-runtime --save-dev`安装babel的相关loader包
2. 运行`cnpm i babel-preset-es2015 babel-preset-stage-0 --save-dev`安装babel转换的语法
3. 在`webpack.config.js`中添加相关loader模块，其中需要注意的是，一定要把`node_modules`文件夹添加到排除项：
```
{ test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ }
```
4. 在项目根目录中添加`.babelrc`文件，并修改这个配置文件如下：
```
{
    "presets":["es2015", "stage-0"],
    "plugins":["transform-runtime"]
}
```
5. **注意：语法插件`babel-preset-es2015`可以更新为`babel-preset-env`，它包含了所有的ES相关的语法；**

## 相关文章
[babel-preset-env：你需要的唯一Babel插件](https://segmentfault.com/p/1210000008466178)
[Runtime transform 运行时编译es6](https://segmentfault.com/a/1190000009065987)