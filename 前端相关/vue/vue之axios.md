# 安装

npm install axios -save  运行时依赖

import axios from 'axios'  进行引用 就可以使用了

# 全局引入

在main.js中引入  然后挂载到原型中

Vue.prototype.$http = axious

然后在组建中即可通过this.$http访问到这个请求模型



# 创建一个请求封装

避免框架的过度侵入

