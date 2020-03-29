## YAML

YAML是 "YAML Ain't a Markup Language" （YAML不是一种置标语言）的递归缩写。

在开发的这种语言时，YAML 的意思其实是："Yet Another Markup Language"（仍是一种置标语言）

YAML A Markup Language ：是一个标记语言

YAML isnot Markup Language ：不是一个标记语言

**标记语言**

 以前的配置文件，大多数都是使用xml来配置；比如一个简单的端口配置，我们来对比下yaml和xml

yaml配置：

```
server：
    prot: 8080
```

xml配置：

```
<server>
    <port>8081<port>
</server>
```

### YAML语法

**基础语法：**

```yaml
k:(空格) v   
```

以此来表示一对键值对（空格不能省略）；**以空格的缩进来控制层级关系，只要是左边对齐的一列数据都是同一个层级的。**

注意 ：属性和值的大小写都是十分敏感的。例子：

```
server:
    port: 8081
    path: /hello
```

### **值的写法**

**字面量：普通的值 [ 数字，布尔值，字符串 ]**

```
k: v
```

字面量直接写在后面就可以 ， 字符串默认不用加上双引号或者单引号；

“” 双引号，不会转义字符串里面的特殊字符 ， 特殊字符会作为本身想表示的意思；

比如 ： name: "kuang \n shen"  输出 ： kuang 换行  shen

'' 单引号，会转义特殊字符 ， 特殊字符最终会变成和普通字符一样输出

比如 ： name: ‘kuang \n shen’  输出 ： kuang \n  shen

 

**对象、Map（键值对）**

```
k: 
    v1:
    v2:
```

 

在下一行来写对象的属性和值得关系，注意缩进；比如：

```
student:
    name: qinjiang
    age: 3
```

行内写法

```
student: {name: qinjiang,age: 3}
```

 

**数组（ List、set ）**

用 - 值表示数组中的一个元素,比如：

```
pets:
 - cat
 - dog
 - pig
```

行内写法

```
pets: [cat,dog,pig]
```

### 修改SpringBoot的默认端口号

 配置文件中添加，端口号的参数，就可以切换端口；

```
server.port=8081
```

## 在springboot中加载的位置

springboot 启动会扫描以下位置的application.properties或者application.yml文件作为Spring boot的默认配置文件

–file:./config/

–file:./

–classpath:/config/

–classpath:/

优先级由高到底，高优先级的配置会覆盖低优先级的配置；

SpringBoot会从这四个位置全部加载主配置文件；**互补配置**；



==我们还可以通过spring.config.location来改变默认的配置文件位置==

**项目打包好以后，我们可以使用命令行参数的形式，启动项目的时候来指定配置文件的新位置；指定配置文件和默认加载的这些配置文件共同起作用形成互补配置；**

java -jar spring-boot-02-config-02-0.0.1-SNAPSHOT.jar --spring.config.location=G:/application.properties