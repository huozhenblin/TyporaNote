# **axiox****请求方式**

axios(config)

axios.request(config)

axios.get(url[, config])

axios.delete(url[, config])

axios.head(url[, config])

axios.post(url[, data[, config]])

axios.put(url[, data[, config]])

axios.patch(url[, data[, config]])

# **全局配置**

这个时候我们可以进行一些抽取, 也可以利用axiox的全局配置

```js
axios.defaults.baseURL = ‘123.207.32.32:8000’
axios.defaults.headers.post[‘Content-Type’] = ‘application/x-www-form-urlencoded’;

```

# **常见的配置选项**

![image-20200326161531081](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200326161531081.png)

![image-20200326161543931](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200326161543931.png)

# **axios****的实例**

当我们从axios模块中导入对象时, 使用的实例是默认的实例.

当给该实例设置一些默认配置时, 这些配置就被固定下来了.

但是后续开发中, 某些配置可能会不太一样.

比如某些请求需要使用特定的baseURL或者timeout或者content-Type等.

这个时候, 我们就可以创建新的实例, 并且传入属于该实例的配置信息.

![image-20200326161649916](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200326161649916.png)![image-20200326161710312](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200326161710312.png)