# 前端模块化之ES-6

模块作用域各模块内数据独立需要导出导入才能相互引用，引入html页面添加的属性和值如下

```javascript
<script src="aaa.js" type="module"></script>

```

### export指令用于导出变量，比如下面的代码

#### *导出方式一:*

也可以将类或者函数的名字放入其中导出

```javascript
export {
  flag, sum,person
}
```

#### *导出方式二:*

```javascriptj
export var num1 = 1000;
export var height = 1.88
```



#### *导出函数或者类*

注：es6 可以定制类 类内可以写方法如下

```javascript
export function mul(num1, num2) {
  return num1 * num2
}

export class Person {
  run() {
    console.log('在奔跑');
  }
}

```

类的使用和java一样

```javascript
const p = new Person();
p.run()
```

#### 默认导出

```javascript
export default function (argument) {
  console.log(argument);
}
```

### import指令用于导出变量，比如下面的代码

#### *方式一导入的{}中定义的变量*

```javascriptj
import{num1,sum} from "./aaa.js
```

#### *方式二直接导入export定义的变量*

```
import {num1, height} from "./aaa.js";
```

#### *方式三导入 export的function/class*

```
import {mul, Person} from "./aaa.js";
```

#### 方式四导入 export default中的内容

默认的导出只能有一个

导入默认到处时名字可以起别名

```javascript
import addr from "./aaa.js";
	addr('你好啊');
```

#### *方式五统一全部导入*

统一导入时这个文件声明导出的值用as后面的对象统一引用

```javascript
import * as aaa from './aaa.js'
onsole.log(aaa.flag);
console.log(aaa.height);
const p1= new aaa.Person();
console.log('这是运用统一');
```

注：导入时参数名要和导出的名一样