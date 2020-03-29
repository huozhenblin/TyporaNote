# Vue.js - 路由

## 1.什么是路由

1. **后端路由：**对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源；

2. **前端路由：**对于单页面应用程序来说，主要通过URL中的hash(#号)来实现不同页面之间的切换，同时，hash有一个特点：HTTP请求中不会包含hash相关的内容；所以，单页面程序中的页面跳转主要用hash实现；

3. 在单页面应用程序中，这种通过hash改变来切换页面的方式，称作前端路由（区别于后端路由）；

## 2.url的hash

- URL的hash也就是锚点(#), 本质上是改变window.location的href属性.

- 我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新

## 3.路由的简单配置步骤

1.在src文件内创建router文件夹，并创建index.js文件

2.引入  import Router from 'vue-router'

3.对于插件要用Vue.use(Router) 

4.创建Routher对象,bingjinxing daochu 

```
export default new Router({
  //配置路由与组件的映射关系
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld
    }
  ]
})
```

5.在入口函数main中引入import router from './router'   可以不用加index.js 会自动找

6.然后再vue实例中进行挂载

```
new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```

## 4.使用vue-router的步骤:

### 第一步: 创建路由组件.vue文件

```
<template>
  <div>
    <h1>我是about</h1>
  </div>
</template>

<script>
export default {
  name: "about"
}
</script>

<style>

</style>
```



### 第二步: 配置路由映射: 组件和路径映射关系

```
import Vue from 'vue'
import Router from 'vue-router'
import home from '../components/home.vue'
import about from '../components/about.vue'
//1.vue.use（插件），安装插件

Vue.use(Router)
//2.创建Router对象
export default new Router({
  //配置路由与组件的映射关系
  routes: [
    {
      path: '/home',
      name: 'home',
      component: home
    },
    {
      path: '/about',
      name: 'about',
      component: about
    }
  ]
})
```

在router文件夹的index。js文件中

### 第三步: 使用路由: 通过<router-link>和<router-view>

在app。vue中

```
<template>
<div id="app">

  <router-view></router-view>
  <router-link to="/home">首页</router-link>
  <router-link to="/about">关于</router-link>
  
</div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
</style>
```



### 4.1示例

在 vue 中使用 vue-router

1. 导入 vue-router 组件类库：
```
<!-- 1. 导入 vue-router 组件类库 -->
  <script src="./lib/vue-router-2.7.0.js"></script>
```
2. 使用 router-link 组件来导航
```
<!-- 2. 使用 router-link 组件来导航 -->
<router-link to="/login">登录</router-link>
<router-link to="/register">注册</router-link>
```
3. 使用 router-view 组件来显示匹配到的组件
```
<!-- 3. 使用 router-view 组件来显示匹配到的组件 -->
<router-view></router-view>
```
4. 创建使用`Vue.extend`创建组件
```
    // 4.1 使用 Vue.extend 来创建登录组件
    var login = Vue.extend({
      template: '<h1>登录组件</h1>'
    });

    // 4.2 使用 Vue.extend 来创建注册组件
    var register = Vue.extend({
      template: '<h1>注册组件</h1>'
    });
```
5. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则
```
// 5. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则
    var router = new VueRouter({
      routes: [
        { path: '/login', component: login },
        { path: '/register', component: register }
      ]
    });
```
6. 使用 router 属性来使用路由规则
```
// 6. 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      router: router // 使用 router 属性来使用路由规则
    });
```

## 5.默认路由和history模式

```js
export default new Router({
  //配置路由与组件的映射关系
  routes: [

    {
      path: '/', //定制默认路由组件
      redirect: home
    },
    {
      path: '/home',
      name: 'home',
      component: home
    },
    {
      path: '/about',
      name: 'about',
      component: about
    }
  ],
  mode: 'history'  //这个表示是用什么方式的路由
})

```

## 6.router-link标签的属性介绍

### to：

用于替换组件，根据to后的路径再配置的路由文件中找到对应的组件通过router-view显示

### tag：

属性指定router-link渲染的标签类型，在标签内写上要指定的标签名

### replace:

可以消除history ，即浏览器的前进后退，只要在便签内加上这个属性名即可

### linkActiveClass:

- 可以帮助点击时，该标签出现特定样式，因为在选用哪个link时会自动在该标签上添加router-link-active 类属性，依照这个即可添加相应的css
- 可以定制活跃时的类名

<router-link to="/home" tag="button" replace active-class="active">首页</router-link>

全局配置：

在路由的配置属性中更改添加属性

linkActiveClass:'active'

### 用代码代替link属性跳转

![image-20200320100818439](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200320100818439.png)

## 7.动态路由

### 在路由规则中定义参数

1. 在规则中定义参数：
```
{ path: '/register/:id', component: register }
```
2. 通过 `this.$route.params`来获取路由中的参数：

$route 和这个东西就是取出定义的路由对象，当前哪一个组件处于活跃就会对那个组件进行操作

```
var register = Vue.extend({
      template: '<h1>注册组件 --- {{this.$route.params.id}}</h1>'
    });
    
computed: {
    userid(){
      return this.$route.params.userid
    }
  }
```

8.路由的懒加载

- 路由懒加载的主要作用就是将路由对应的组件打包成一个个的js代码块.

- 只有在这个路由被访问到的时候, 才加载对应的组件

### **懒加载的方式**

方式一: 结合Vue的异步组件和Webpack的代码分析.

```
const Home = resolve => { require.ensure(['../components/Home.vue'], () => { resolve(require('../components/Home.vue')) })};

```

方式二: AMD写法

```
const About = resolve => require(['../components/About.vue'], resolve);
```

方式三: 在ES6中, 我们可以有更加简单的写法来组织Vue异步组件和Webpack的代码分割.

```
const Home = () => import('../components/Home.vue')
```

### **路由懒加载的效果**

![image-20200320114113112](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200320114113112.png)

![image-20200320114128353](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200320114128353.png)



## 8.路由的嵌套

使用 `children` 属性实现路由嵌套

```
  <div id="app">
    <router-link to="/account">Account</router-link>

    <router-view></router-view>
  </div>

  <script>
    // 父路由中的组件
    const account = Vue.extend({
      template: `<div>
        这是account组件
        <router-link to="/account/login">login</router-link> | 
        <router-link to="/account/register">register</router-link>
        <router-view></router-view>
      </div>`
    });

    // 子路由中的 login 组件
    const login = Vue.extend({
      template: '<div>登录组件</div>'
    });

    // 子路由中的 register 组件
    const register = Vue.extend({
      template: '<div>注册组件</div>'
    });

    // 路由实例
    var router = new VueRouter({
      routes: [
        { path: '/', redirect: '/account/login' }, // 使用 redirect 实现路由重定向
        {
          path: '/account',
          component: account,
          children: [ // 通过 children 数组属性，来实现路由的嵌套
            { path: 'login', component: login }, // 注意，子路由的开头位置，不要加 / 路径符
            { path: 'register', component: register }
          ]
        }
      ]
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      components: {
        account
      },
      router: router
    });
  </script>
```

## 命名视图实现经典布局
1. 标签代码结构：
```
<div id="app">
    <router-view></router-view>
    <div class="content">
      <router-view name="a"></router-view>
      <router-view name="b"></router-view>
    </div>
  </div>
```
2. JS代码：
```
<script>
    var header = Vue.component('header', {
      template: '<div class="header">header</div>'
    });

    var sidebar = Vue.component('sidebar', {
      template: '<div class="sidebar">sidebar</div>'
    });

    var mainbox = Vue.component('mainbox', {
      template: '<div class="mainbox">mainbox</div>'
    });

    // 创建路由对象
    var router = new VueRouter({
      routes: [
        {
          path: '/', components: {
            default: header,
            a: sidebar,
            b: mainbox
          }
        }
      ]
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      router
    });
  </script>
```
3. CSS 样式：
```
  <style>
    .header {
      border: 1px solid red;
    }

    .content{
      display: flex;
    }
    .sidebar {
      flex: 2;
      border: 1px solid green;
      height: 500px;
    }
    .mainbox{
      flex: 8;
      border: 1px solid blue;
      height: 500px;
    }
  </style>
```

## `watch`属性的使用
考虑一个问题：想要实现 `名` 和 `姓` 两个文本框的内容改变，则全名的文本框中的值也跟着改变；（用以前的知识如何实现？？？）

1. 监听`data`中属性的改变：
```
<div id="app">
    <input type="text" v-model="firstName"> +
    <input type="text" v-model="lastName"> =
    <span>{{fullName}}</span>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'jack',
        lastName: 'chen',
        fullName: 'jack - chen'
      },
      methods: {},
      watch: {
        'firstName': function (newVal, oldVal) { // 第一个参数是新数据，第二个参数是旧数据
          this.fullName = newVal + ' - ' + this.lastName;
        },
        'lastName': function (newVal, oldVal) {
          this.fullName = this.firstName + ' - ' + newVal;
        }
      }
    });
  </script>
```
2. 监听路由对象的改变：
```js
<div id="app">
    <router-link to="/login">登录</router-link>
    <router-link to="/register">注册</router-link>

    <router-view></router-view>
  </div>

  <script>
    var login = Vue.extend({
      template: '<h1>登录组件</h1>'
    });

    var register = Vue.extend({
      template: '<h1>注册组件</h1>'
    });

    var router = new VueRouter({
      routes: [
        { path: "/login", component: login },
        { path: "/register", component: register }
      ]
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      router: router,
      watch: {
        '$route': function (newVal, oldVal) {
          if (newVal.path === '/login') {
            console.log('这是登录组件');
          }
        }
      }
    });
  </script>
```

## 9.vue-routher传递参数

### 方法一，使用$route.params

路由配置文件示例如下

```js
const User = {
  template: '<div>User {{ $route.params.id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User }
  ]
})
```

```js
 <router-link :to="'/user/'+userid" tag="button" replace >用户</router-link>
```

页面跳转如上

### 方法二使用 `props` 将组件和路由解耦：

在组件中使用 `$route` 会使之与其对应路由形成高度耦合，从而使组件只能在某些特定的 URL 上使用，限制了其灵活性。

使用 `props` 将组件和路由解耦取代与 `$route` 的耦合通过 `props` 解耦

```js
const User = {
  props: ['id'],
  template: '<div>User {{ id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User, props: true },

    // 对于包含命名视图的路由，你必须分别为每个命名视图添加 `props` 选项：
    {
      path: '/user/:id',
      components: { default: User, sidebar: Sidebar },
      props: { default: true, sidebar: false }
    }
  ]
})
```

### 方法三 使用**query****的类型**

配置路由格式: /router, 也就是普通配置

传递的方式: 对象中使用query的key作为传递方式

传递后形成的路径: /router?id=123, /router?id=abc

前面配置如下

![image-20200321141547145](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200321141547145.png)

组件中使用如下，直接$route.query 来使用

![image-20200321141654180](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200321141654180.png)



### 方式四 在js中传参

![image-20200321141817586](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200321141817586.png)

### 获取参数

获取参数通过$route对象获取的.

在使用了 vue-router 的应用中，路由对象会被注入每个组件中，赋值为 this.$route ，并且当路由切换时，路由对象会被更新。

### $route和$router是有区别的

$router为VueRouter实例，想要导航到不同URL，则使用$router.push方法

$route为当前router跳转对象里面可以获取name、path、query、params等那个活跃用的就是那个 

![image-20200321141959878](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200321141959878.png)



## 10.全局导航守卫

正如其名，`vue-router` 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。有多种机会植入路由导航过程中：全局的, 单个路由独享的, 或者组件级的。

记住**参数或查询的改变并不会触发进入/离开的导航守卫**。你可以通过[观察 `$route` 对象](https://router.vuejs.org/zh/guide/essentials/dynamic-matching.html#响应路由参数的变化)来应对这些变化，或使用 `beforeRouteUpdate` 的组件内守卫。

###  全局前置守卫

```js
const router = new VueRouter({ ... })

router.beforeEach((to, from, next) => {
  
    
    next()//这个必须要调用，以进下一步
    // ...
})
```

每个守卫方法接收三个参数：

- **`to: Route`**: 即将要进入的目标 [路由对象](https://router.vuejs.org/zh/api/#路由对象)调用‘to’对象可以得到当前路由中的参数
- **`from: Route`**: 当前导航正要离开的路由
- **`next: Function`**: 一定要调用该方法来 **resolve** 这个钩子。执行效果依赖 `next` 方法的调用参数。
  - **`next()`**: 进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 **confirmed** (确认的)。
  - **`next(false)`**: 中断当前的导航。如果浏览器的 URL 改变了 (可能是用户手动或者浏览器后退按钮)，那么 URL 地址会重置到 `from` 路由对应的地址。
  - **`next('/')` 或者 `next({ path: '/' })`**: 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。你可以向 `next` 传递任意位置对象，且允许设置诸如 `replace: true`、`name: 'home'` 之类的选项以及任何用在 [`router-link` 的 `to` prop](https://router.vuejs.org/zh/api/#to) 或 [`router.push`](https://router.vuejs.org/zh/api/#router-push) 中的选项。
  - **`next(error)`**: (2.4.0+) 如果传入 `next` 的参数是一个 `Error` 实例，则导航会被终止且该错误会被传递给 [`router.onError()`](https://router.vuejs.org/zh/api/#router-onerror) 注册过的回调。

**确保要调用 `next` 方法，否则钩子就不会被 resolved。**

### 全局后置钩子

你也可以注册全局后置钩子，然而和守卫不同的是，这些钩子不会接受 `next` 函数也不会改变导航本身：

```js
router.afterEach((to, from) => {
  // ...
})
```

### 路由独享的守卫

你可以在路由配置上直接定义 `beforeEnter` 守卫：

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

这些守卫与全局前置守卫的方法参数是一样的。

### 组件内的守卫

最后，你可以在路由组件内直接定义以下路由导航守卫：

- `beforeRouteEnter`
- `beforeRouteUpdate` (2.2 新增)
- `beforeRouteLeave`

```js
const Foo = {
  template: `...`,
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }
}
```

`beforeRouteEnter` 守卫 **不能** 访问 `this`，因为守卫在导航确认前被调用,因此即将登场的新组件还没被创建。

不过，你可以通过传一个回调给 `next`来访问组件实例。在导航被确认的时候执行回调，并且把组件实例作为回调方法的参数。

```js
beforeRouteEnter (to, from, next) {
  next(vm => {
    // 通过 `vm` 访问组件实例
  })
}
```

注意 `beforeRouteEnter` 是支持给 `next` 传递回调的唯一守卫。对于 `beforeRouteUpdate` 和 `beforeRouteLeave` 来说，`this` 已经可用了，所以**不支持**传递回调，因为没有必要了。

```js
beforeRouteUpdate (to, from, next) {
  // just use `this`
  this.name = to.params.name
  next()
}
```

这个离开守卫通常用来禁止用户在还未保存修改前突然离开。该导航可以通过 `next(false)` 来取消。

```js
beforeRouteLeave (to, from, next) {
  const answer = window.confirm('Do you really want to leave? you have unsaved changes!')
  if (answer) {
    next()
  } else {
    next(false)
  }
}
```

### 完整的导航解析流程

1. 导航被触发。
2. 在失活的组件里调用离开守卫。
3. 调用全局的 `beforeEach` 守卫。
4. 在重用的组件里调用 `beforeRouteUpdate` 守卫 (2.2+)。
5. 在路由配置里调用 `beforeEnter`。
6. 解析异步路由组件。
7. 在被激活的组件里调用 `beforeRouteEnter`。
8. 调用全局的 `beforeResolve` 守卫 (2.5+)。
9. 导航被确认。
10. 调用全局的 `afterEach` 钩子。
11. 触发 DOM 更新。
12. 用创建好的实例调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数。

### **keep-alive**遇见**vue**-router

keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。

它们有两个非常重要的属性:

include - 字符串或正则表达，只有匹配的组件会被缓存

exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存

 <keep-alive exclude="Profile,User">

   <router-view/>

  </keep-alive>

属性名为 组件中定义的name

router-view 也是一个组件，如果直接被包在 keep-alive 里面，所有路径匹配到的视图组件都会被缓存：

![image-20200322094242013](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200322094242013.png)

## 11.TabBar（布局）实现思路

### 在style中引用 通用配置的css文件

示例  分号不能省略

@import "./assets/css/basecss.css"；

# 路径问题起别名

cli2  中 在baseconfig中 配置

![image-20200324111220499](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200324111220499.png)

然后关于路径引用的地方就可以用这些东西替换  如果使用 src属性  前面要加一个 ~  波浪线

![image-20200324111008984](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200324111008984.png)

![image-20200324110843744](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200324110843744.png)









## 相关文件

1. [URL中的hash（井号）](http://www.cnblogs.com/joyho/articles/4430148.html)