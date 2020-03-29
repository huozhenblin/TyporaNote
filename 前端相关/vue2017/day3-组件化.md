---

---

# Vue.js - Day3

## 组件的定义及使用
什么是组件： 组件的出现，就是为了拆分Vue实例的代码量的，能够让我们以不同的组件，来划分不同的功能模块，将来我们需要什么样的功能，就可以去调用对应的组件即可；
组件化和模块化的不同：

 + 模块化： 是从代码逻辑的角度进行划分的；方便代码分层开发，保证每个功能模块的职能单一；

 + 组件化： 是从UI界面的角度进行划分的；前端的组件化，方便UI组件的重用；

 + n我们将一个完整的页面分成很多个组件。

   n每个组件都用于实现页面的一个功能块。

   n而每一个组件又可以进行细分。
### 组件定义的三种方式
### 1.使用 Vue.extend 配合 Vue.component 方法定义全局组件：

![image-20200305150220676](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200305150220676.png)

####         1.1使用Vue.extend创建组建的构造器

- p调用Vue.extend()创建的是一个组件构造器。 
- p通常在创建组件构造器时，传入template代表我们自定义组件的模板。
- p该模板就是在使用到组件的地方，要显示的HTML代码。
- p事实上，这种写法在Vue2.x的文档中几乎已经看不到了，它会直接使用下面我们会讲到的语法糖，但是在很多资料还是会提到这种方式，而且这种方式是学习后面方式的基础。

```javascript
var login = Vue.extend({
      template: '<h1>登录</h1>'
    });
    
```
#### 		1.2直接使用 Vue.component 方法注册组件：

- p调用Vue.component()是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名称。

- p所以需要传递两个参数：

  1、注册组件的标签名 

  2、组件构造器

```javascript
   Vue.component('login', login);
```
####         1.3在vue实例的作用范围内使用组件

​		组件必须挂载在某个Vue实例下，否则它不会生效

```html
<login></login>
```

#### 1.4使用 Vue.component语法糖来定义全局组件：

```javascript
Vue.component('account', {
      template: '<h1>lalal</h1>
    });
```

> 注意：
>
> 组件中的DOM结构，有且只能有唯一的根元素（Root Element）来进行包裹！
>
> 当我们通过调用Vue.component()注册组件时，组件的注册是全局的，这意味着该组件可以在任意Vue示例下使用。



### 2.子父组件的定义

也就是说组件是可以嵌套定义的

```javascript
<script>
  // 1.创建第一个组件构造器(子组件)
  const cpnC1 = Vue.extend({
    template: `
      <div>
        <h2>我是标题1</h2>
        <p>我是内容, 哈哈哈哈</p>
      </div>
    `
  })


  // 2.创建第二个组件构造器(父组件)
  const cpnC2 = Vue.extend({
    template: `
      <div>
        <h2>我是标题2</h2>
        <p>我是内容, 呵呵呵呵</p>
        <cpn1></cpn1>//编译到这时，
      </div>
    `,
    components: {
      cpn1: cpnC1
    }
  })

  // root组件
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      cpn2: cpnC2
    }
  })
</script>
```

### 3.利用语法糖注册局部组件

#### 方式一：普通定义

```javascript
<script>
  // 1.创建组件构造器
  const cpnC = Vue.extend({
    template: `
      <div>
        <h2>我是标题</h2>
        <p>我是内容,哈哈哈哈啊</p>
      </div>
    `
  })

  // 2.注册组件(全局组件, 意味着可以在多个Vue的实例下面使用)
  // Vue.component('cpn', cpnC)

  // 疑问: 怎么注册的组件才是局部组件了?

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      // cpn使用组件时的标签名
      cpn: cpnC//这个便是局部的 只能在这个vue示例中运用
    }
  })
```

#### 方式二：注册局部组件语法糖使用`components`属性定义局部子组件

```javascript
// 2.注册局部组件的语法糖
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      'cpn2': {
        template: `
          <div>
            <h2>我是标题2</h2>
            <p>我是内容, 呵呵呵</p>
          </div>
    `
      }
    }
  })		
```

```javascript
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      components: { // 定义子组件
        account: { // account 组件
          template: '<div><h1>这是Account组件					{{name}}</h1><login><						/login></div>', // 在这里							使用定义的子组件
         				 components: { // 定义子组件的子组件
                				login: { //                                      login 组件
             						                                             template:                                   "<h3>这是登录组件</h3>"
            }
          }
        }
      }
    });
  </script>
```
2. 引用组件：
```
<div id="app">
    <account></account>
  </div>
```

### 4.组件模板分离

#### 	创建方式

```javascript
<script>

  // 1.注册一个全局组件
  Vue.component('cpn', {
    template: '#cpn'
  })

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    }
  })
</script>
```

#cpn的templates模板如下语法形式，通过<script type="text/x-template" id="cpn">

和template标签

```html
<!-- 1.script标签, 注意:类型必须是text/x-template-->
<script type="text/x-template" id="cpn">
<div>
  <h2>我是标题</h2>
  <p>我是内容,哈哈哈</p>
</div>
</script>

<!--2.template标签-->
<template id="cpn">
  <div>
    <h2>我是标题</h2>
    <p>我是内容,呵呵呵</p>
  </div>
</template>
```

局部方式定义在具体vue中的components中即可

**注**：template模板中必须有一个根标签

### 5.组件中展示数据和响应事件

- 组件是一个单独功能模块的封装：
  - 这个模块有属于自己的HTML模板，也应该有属性自己的数据data。

- 组件对象也有一个data属性(也可以有methods等属性，下面我们有用到)

在组件中，`data`需要被定义为一个方法，例如：

```javascript
<template id="cpn">
  <div>
    <h2>{{title}}</h2>
    <p>我是内容,呵呵呵</p>
  </div>
</template>

Vue.component('account', {
      template: '#cpn',
   	  data() {
      	return {
       	 title: 'abc'
     	 },
      methods:{
        login(){
          alert('点击了登录按钮');
        }
      }
    });
    
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      // title: '我是标题'
    }
  })
```

**注**：

- 只是这个data属性必须是一个函数

- 而且这个函数返回一个对象，对象内部保存着数据

- 为什么data在组件中必须是一个函数呢?

  - 首先，如果不是一个函数，Vue直接就会报错。

  - 其次，原因是在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响

### 6.计时示例（data返回函数原因）

**注**：

- 在使用组件时，每引用一个就会将这个组件创建出来一个引用实例
- 组件内部可以引用外面定义的全局变量或者对象比如下述

```html
<!--组件实例对象-->
<div id="app">
  <cpn></cpn>
  <cpn></cpn>
  <cpn></cpn>
</div>

<template id="cpn">
  <div>
    <h2>当前计数: {{counter}}</h2>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
  </div>
</template>
<script src="../js/vue.js"></script>
<script>
  // 1.注册组件
  const obj = {
    counter: 0
  }
  Vue.component('cpn', {
    template: '#cpn',
    data() {//内部定义 所有实例独享自己的各个数据，因为每次调用都会返回一个函数对象，单独的对象单独的内存地址
      return {
        counter: 0
      }
    },
    // data() { 应用外部的所有实例共用一个对象，因为返回的对象指向的地址是相同的
    //   return obj
    // },
    methods: {
      increment() {
        this.counter++
      },
      decrement() {
        this.counter--
      }
    }
  })

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    }
  })
</script>
```



### 7.父组件和子组件传值通信

- 子组件是不能引用父组件或者Vue实例的数据的。子组件是不能引用父组件或者Vue实例的数据的。

- 在开发中，往往一些数据确实需要从上层传递到下层：
  - 比如在一个页面中，我们从服务器请求到了很多的数据。
  - 其中一部分数据，并非是我们整个页面的大组件来展示的，而是需要下面的子组件进行展示。
  - 这个时候，并不会让子组件再次发送一个网络请求，而是直接让**大组件**(父组件)**将数据传递给**小组件(子组件)。

- 如何进行父子组件间的通信呢？Vue官方提到

  - 通过props向子组件传递数据

  - 通过事件向父组件发送消息

    ![image-20200306094106839](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200306094106839.png)

#### 7.1利用props由父组件向子组件传递参数

![image-20200306101833969](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200306101833969.png)

步骤：

1. 首先在子组件中利用props定义用来接受的值（包括类型限制默认值之类的）
2. 然后再调用组件时进行数据绑定<cpn v-bind:cmovies="movies"></cpn>其中等号左边是步骤一中定义的接收变量，等号右边为父组件中要传递过来的数据
3. 引用：进行绑定后template模板就可以使用这些值（调用的是等号左边的）<li v-for="item in cmovies">{{item}}</li>

```html
<body>

<div id="app">
  <!--<cpn v-bind:cmovies="movies"></cpn>-->
  <!--<cpn cmovies="movies" cmessage="message"></cpn>-->

  <cpn :cmessage="message" :cmovies="movies"></cpn>
</div>



<template id="cpn">
  <div>
    <ul>
      <li v-for="item in cmovies">{{item}}</li>
    </ul>
    <h2>{{cmessage}}</h2>
  </div>
</template>

<script src="../js/vue.js"></script>
<script>
  // 父传子: props
  const cpn = {
    template: '#cpn',
    // props: ['cmovies', 'cmessage'],其中的值可以当做变量里面会接收父组件的值比如下面的引用
   //<!--<cpn v-bind:cmovies="movies"></cpn>-->
    props: {
      // 1.类型限制
      // cmovies: Array,
      // cmessage: String,
      // 2.提供一些默认值, 以及必传值
      cmessage: {
        type: String,
        default: 'aaaaaaaa',
        required: true//调用的父组件必须传递这个参数
      },
      // 类型是对象或者数组时, 默认值必须是一个函数
      cmovies: {
        type: Array,
        default() {
          return []
        }
      }
    },
    data() {
      return {}
    },
    methods: {

    }
  }

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      movies: ['海王', '海贼王', '海尔兄弟']
    },
    components: {
      cpn //es6增强写法
    }
  })
</script>

</body>
```

**注**：

- 类型是对象或者数组时, 默认值必须是一个函数

- 使用驼峰命名法时，由于vue不支持所有在数据绑定时在对应的大写字母前添加“-”，后面变小写比如

  :child-my-message="message" ，原本在props中的定义为childMyMessage，template中可以正常调用

  在脚手架中就没有影响了

#### 7.2由子组件向父组件传递数据利用自定义事件

1. 原理：父组件将方法的引用，传递到子组件内部，子组件在内部调用父组件传递过来的方法，同时把要发送给父组件的数据，在调用方法的时候当作参数传递进去；
2. 父组件将方法的引用传递给子组件，其中，cpnClick是父组件中`methods`中定义的方法名称，’item-click‘是子组件调用传递过来方法时候的方法名称
```
<!--父组件模板-->
<div id="app">
  <cpn @item-click="cpnClick"></cpn>
</div>
//加一个监听事件 等号左边为子组件自定义事件名称，右边为父组件定义的函数，表示子组件监听父组件的某个方法
```
3. 子组件内部通过`this.$emit('事件名', 要传递的数据)`定义事件，来监听调用父组件中的方法，同时把数据传递给父组件使用

   ```javascript
   methods: {
         btnClick(item) {
           // 发射事件: 自定义事件
           this.$emit('item-click', item)
         }
       }//第一个参数为创建的事件名称，第二个为给这个事件的参数
   ```

   
```html
<!--父组件模板-->
<div id="app">
  <cpn @item-click="cpnClick"></cpn>
</div>

<!--子组件模板-->
<template id="cpn">
  <div>
    <button v-for="item in categories"
            @click="btnClick(item)">
      {{item.name}}
    </button>
  </div>
</template>

<script src="../js/vue.js"></script>
<script>

  // 1.子组件
  const cpn = {
    template: '#cpn',
    data() {
      return {
        categories: [
          {id: 'aaa', name: '热门推荐'},
          {id: 'bbb', name: '手机数码'},
          {id: 'ccc', name: '家用家电'},
          {id: 'ddd', name: '电脑办公'},
        ]
      }
    },
    methods: {
      btnClick(item) {
        // 发射事件: 自定义事件
        this.$emit('item-click', item)
      }
    }
  }

  // 2.父组件
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      cpn
    },
    methods: {
      cpnClick(item) {
        console.log('cpnClick', item);
      }
    }
  })
</script>

</body>
```

### 8.父子组件的访问方式

#### 父组件访问子组件：使用$children或$refs reference(引用)

使用$children；

- this.$children是一个数组类型，它包含所有子组件对象。

  1. 我们这里通过一个遍历，取出所有子组件的message状态。

     ![image-20200307135353567](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200307135353567.png)

$refs的使用：

- $refs和ref指令通常是一起使用的。
- 首先，我们通过ref给某一个子组件绑定一个特定的ID。
- 其次，通过this.$refs.ID就可以访问到该组件了。

如果我们想在子组件中直接访问父组件，可以通过$parent

```html

<body>

<div id="app">
  <cpn></cpn>
  <cpn></cpn>

  <my-cpn></my-cpn>
  <y-cpn></y-cpn>

  <cpn ref="aaa"></cpn>
  <button @click="btnClick">按钮</button>
</div>

<template id="cpn">
  <div>我是子组件</div>
</template>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    methods: {
      btnClick() {
        // 1.$children
        // console.log(this.$children);
        // for (let c of this.$children) {
        //   console.log(c.name);
        //   c.showMessage();
        // }
        // console.log(this.$children[3].name);

        // 2.$refs => 对象类型, 默认是一个空的对象 ref='bbb'
        console.log(this.$refs.aaa.name);
      }
    },
    components: {
      cpn: {
        template: '#cpn',
        data() {
          return {
            name: '我是子组件的name'
          }
        },
        methods: {
          showMessage() {
            console.log('showMessage');
          }
        }
      },
    }
  })
</script>

</body>
```



```
  <div id="app">
    <div>
      <input type="button" value="获取元素内容" @click="getElement" />
      <!-- 使用 ref 获取元素 -->
      <h1 ref="myh1">这是一个大大的H1</h1>

      <hr>
      <!-- 使用 ref 获取子组件 -->
      <my-com ref="mycom"></my-com>
    </div>
  </div>

  <script>
    Vue.component('my-com', {
      template: '<h5>这是一个子组件</h5>',
      data() {
        return {
          name: '子组件'
        }
      }
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {
        getElement() {
          // 通过 this.$refs 来获取元素
          console.log(this.$refs.myh1.innerText);
          // 通过 this.$refs 来获取组件
          console.log(this.$refs.mycom.name);
        }
      }
    });
  </script>
```

#### 使用`flag`标识符结合`v-if`和`v-else`切换组件

1. 页面结构：

```
<div id="app">
    <input type="button" value="toggle" @click="flag=!flag">
    <my-com1 v-if="flag"></my-com1>
    <my-com2 v-else="flag"></my-com2>
  </div>
```

2. Vue实例定义：

```
<script>
    Vue.component('myCom1', {
      template: '<h3>奔波霸</h3>'
    })

    Vue.component('myCom2', {
      template: '<h3>霸波奔</h3>'
    })

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        flag: true
      },
      methods: {}
    });
  </script>
```

#### 使用`:is`属性来切换不同的子组件,并添加切换动画

##### 组件实例定义方式：

```
  // 登录组件
    const login = Vue.extend({
      template: `<div>
        <h3>登录组件</h3>
      </div>`
    });
    Vue.component('login', login);

    // 注册组件
    const register = Vue.extend({
      template: `<div>
        <h3>注册组件</h3>
      </div>`
    });
    Vue.component('register', register);

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: { comName: 'login' },
      methods: {}
    });
```

2. 使用`component`标签，来引用组件，并通过`:is`属性来指定要加载的组件：

```
  <div id="app">
    <a href="#" @click.prevent="comName='login'">登录</a>
    <a href="#" @click.prevent="comName='register'">注册</a>
    <hr>
    <transition mode="out-in">
      <component :is="comName"></component>
    </transition>
  </div>
```

3. 添加切换样式：

```css
  <style>
    .v-enter,
    .v-leave-to {
      opacity: 0;
      transform: translateX(30px);
    }

    .v-enter-active,
    .v-leave-active {
      position: absolute;
      transition: all 0.3s ease;
    }

    h3{
      margin: 0;
    }
  </style>
```
