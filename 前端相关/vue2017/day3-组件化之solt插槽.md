# **slot**插槽

## 1.插槽定义以及介绍

组件的插槽：

- 组件的插槽也是为了让我们封装的组件更加具有扩展性。
- 让使用者可以决定组件内部的一些内容到底展示什么。

栗子：移动网站中的导航栏。

- 移动开发中，几乎每个页面都有导航栏。
- 导航栏我们必然会封装成一个插件，比如nav-bar组件。
- 一旦有了这个组件，我们就可以在多个页面中复用了。

但是，每个页面的导航是一样的吗？No，我以京东M站为例

![image-20200307140933400](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200307140933400.png)

如何去封装这类的组件呢？

- 它们也很多区别，但是也有很多共性。
- 如果，我们每一个单独去封装一个组件，显然不合适：比如每个页面都返回，这部分内容我们就要重复去封装。
- 但是，如果我们封装成一个，好像也不合理：有些左侧是菜单，有些是返回，有些中间是搜索，有些是文字，等等。

如何封装合适呢？抽取共性，保留不同。

- 最好的封装方式就是将共性抽取到组件中，将不同暴露为插槽。
- 一旦我们预留了插槽，就可以让使用者根据自己的需求，决定插槽中插入什么内容。
- 是搜索框，还是文字，还是菜单。由调用者自己来决定。
- 这就是为什么我们要学习组件中的插槽slot的原因。

## 2.插槽的基本使用

- 在子组件中，使用特殊的元素<slot>就可以为子组件开启一个插槽。
- 该插槽插入什么内容取决于父组件如何使用。
- 可以设置默认值，并且在不命名时优先替换无名的

```html
<body>

<!--
1.插槽的基本使用 <slot></slot>
2.插槽的默认值 <slot>button</slot>
3.如果有多个值, 同时放入到组件进行替换时, 一起作为替换元素
-->

<div id="app">
  <cpn></cpn>

  <cpn><span>哈哈哈</span></cpn>
  <cpn><i>呵呵呵</i></cpn>
  <cpn>//会全部替换进入一个slot
    <i>呵呵呵</i>
    <div>我是div元素</div>
    <p>我是p元素</p>
  </cpn>
  <cpn></cpn>
  <cpn></cpn>
  <cpn></cpn>
  <cpn></cpn>
</div>
<template id="cpn">
  <div>
    <h2>我是组件</h2>
    <p>我是组件, 哈哈哈</p>
    <slot><button>按钮</button></slot>
      //可以设置默认值，没有替换元素时用这个。
    <!--<button>按钮</button>-->
  </div>
</template>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      cpn: {
        template: '#cpn'
      }
    }
  })
</script>

</body>
```

## **3.具名插槽****slot**

当子组件的功能复杂时，子组件的插槽可能并非是一个。

- 比如我们封装一个导航栏的子组件，可能就需要三个插槽，分别代表左边、中间、右边。
- 那么，外面在给插槽插入内容时，如何区分插入的是哪一个呢？
- 这个时候，我们就需要给插槽起一个名字

如何使用具名插槽呢？

- 非常简单，只要给slot元素一个name属性即可
- <slot name='myslot'></slot>

《--这个废弃

- 父组件使用时在替换的标签上添加slot属性如例<span slot="left">左边的插槽</span>
- <span slot="left">左边的插槽</span>

--》

- 最新的用法是，我们可以在一个 ` 元素上使用 `v-slot` 指令，并以 `v-slot` 的参数的形式提供其名称：
- 现在 ` 元素中的所有内容都将会被传入相应的插槽。任何没有被包裹在带有 `v-slot` 的 ` 中的内容都会被视为默认插槽的内容。

### 注意：

-  **`v-slot` 只能添加在<template>上** (只有[一种例外情况](https://cn.vuejs.org/v2/guide/components-slots.html#独占默认插槽的缩写语法))，这一点和已经废弃的 [`slot` attribute](https://cn.vuejs.org/v2/guide/components-slots.html#废弃了的语法) 不同。

- 一个不带 `name` 的 `` 出口会带有隐含的名字“default”。

### 我们来给出一个案例：

这里我们先不对导航组件做非常复杂的封装，先了解具名插槽的用法。

```html
<body>

<div id="app">
  <cpn>
    <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
  </cpn>
  <cpn></cpn>
</div>


<template id="cpn">
 <div class="container">
  <header>
    <!-- 我们希望把页头放这里 -->
  </header>
  <main>
    <!-- 我们希望把主要内容放这里 -->
  </main>
  <footer>
    <!-- 我们希望把页脚放这里 -->
  </footer>
</div>
</template>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      cpn: {
        template: '#cpn'
      }
    }
  })
</script>

</body>
```

上面的在最新版

## 4.[作用域插槽](https://cn.vuejs.org/v2/guide/components-slots.html#作用域插槽)

### 作用

让插槽内容能够访问子组件中才有的数据是很有用的

### 用法

例如，设想一个带有如下模板的 `<current-user/>` 组件：

```
<span>
  <slot>{{ user.lastName }}</slot>
</span>
```

我们可能想换掉备用内容，用名而非姓来显示。如下：

```
<current-user>
  {{ user.firstName }}
</current-user>
```

然而上述代码不会正常工作，因为只有 <current-user/> 组件可以访问到 `user` 而我们提供的内容是在父级渲染的。

为了让 `user` 在父级的插槽内容中可用，我们可以将 `user` 作为 <slot> 元素的一个 attribute 绑定上去：

```
<span>
  <slot v-bind:user="user">
    {{ user.lastName }}
  </slot>
</span>
```

绑定在 ``<slot> 元素上的 attribute 被称为**插槽 prop**。现在在父级作用域中，我们可以使用带值的 `v-slot` 来定义我们提供的插槽 prop 的名字：

```
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>
```

<template v-slot:default="slotProps"> v-slot: 后面是插槽名=“自定义名”

在这个例子中，我们选择将包含所有插槽 prop 的对象命名为 `slotProps`，但你也可以使用任意你喜欢的名字。



### **注**

**父组件模板的所有东西都会在父级作用域内编译；子组件模板的所有东西都会在子级作用域内编译。**