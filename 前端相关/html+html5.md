# 1.html基础

## 1.1元素

指从开始标签到借宿标签的所有代码

## 1.2属性

属性以键值对的形式出现

### 通用属性

class ：元素类名	

id  ：唯一id

style：元素样式

title：元素的额外信息

### 常用的标签的属性

#### h标题标签

align：表题的位置

#### bady标签

background：设置背景颜色

#### a标签

target：

## 1.3文本格式化

![image-20200408091912784](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408091912784.png)

## 1.4样式的使用

当浏览器读到一个样式表，它就会按照这个样式表来对文档进行格式化。有以下三种方式来插入样式表：

### 基本含义

<style>:样式定义   <link>:资源引用
</style>

标签属性 

rel="stylesheet":外部样式表

type=“”text/css":引入文档类型

href：链接文件路径

### 外部样式表

当样式需要被应用到很多页面的时候，外部样式表将是理想的选择。使用外部样式表，你就可以通过更改一个文件来改变整个站点的外观。

```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

### 内部样式表

当单个文件需要特别样式时，就可以使用内部样式表。你可以在 head 部分通过 <style> 标签定义内部样式表。

```
<head>

<style type="text/css">
body {background-color: red}
p {margin-left: 20px}
</style>
</head>
```

### 内联样式

当特殊的样式需要应用到个别元素时，就可以使用内联样式。 使用内联样式的方法是在相关的标签中使用样式属性。样式属性可以包含任何 CSS 属性。以下实例显示出如何改变段落的颜色和左外边距。

```
<p style="color: red; margin-left: 20px">
This is a paragraph
</p>
```

## 1.5链接

### 连接数据：文本链接，图片链接

### 属性：

href属性：指向另一个文档链接

name属性：创建文档内连接

比如：

《a name=‘top’》文档内跳转地址《/a》

《a href=‘#top’》点击此处会跳转到上面这个声明对应name的a标签处《/a》



### img标签属性：

alt：替换文本属性，当图片报错不显示时，这个文本信息会显示

width，height 这不是样式 而是图片的属性

## 1.6表格

### 标签

### ![image-20200408094524525](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408094524525.png)

### 属性

边框boder

如果不定义边框属性，表格将不显示边框。有时这很有用，但是大多数时候，我们希望显示边框。

使用边框属性来显示一个带有边框的表格：

```
<table border="1">
<tr>
<td>Row 1, cell 1</td>
<td>Row 1, cell 2</td>
</tr>
</table>
```

单元格大小cellpadding

单元格间距cellpacing

表格背景颜色 bgcolor

背景图片 background

## 1.7列表

### 标签

![image-20200408095743825](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408095743825.png)

### 属性

![image-20200408095856942](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408095856942.png)



在ul或者ol标签上  type=“属性名”

start就直接使用 start=数字在ol中 可以规定从几开始排序

## 1.8html块

块元素在显示时会以新行显示：h1 p ul ol li div

内联元素：不会以新行开始：a img span（作为文本容器）

## 1.9表单

### 标签

![image-20200408101755199](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408101755199.png)

### form属性

### 

![image-20200408101731528](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408101731528.png)

```
<form action="action_page.php" method="GET" target="_blank" accept-charset="UTF-8"
ectype="application/x-www-form-urlencoded" autocomplete="off" novalidate>
.
form elements
 .
</form> 
```

### input标签属性

#### 不同的type属性

![image-20200408101956639](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408101956639.png)

text就是正常输入文本信息

radio则是单选框

```
<form>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form> 
```

submit主要用于提交表单用于form表单的提交

password 输入时会变为不可见

checkbox标识复选框

```
<form>
<input type="checkbox" name="vehicle" value="Bike">I have a bike
<br>
<input type="checkbox" name="vehicle" value="Car">I have a car 
</form> 
```

#### name属性

这个必须有，才能被正确被form表单提交

#### value

*value* 属性规定输入字段的初始值

#### readonly 属性

*readonly* 属性规定输入字段为只读（不能修改）：

readonly 属性不需要值。它等同于 readonly="readonly"。

#### disabled 属性

*disabled* 属性规定输入字段是禁用的。

被禁用的元素是不可用和不可点击的。

被禁用的元素不会被提交

disabled 属性不需要值。它等同于 disabled="disabled"。

#### size 属性

*size* 属性规定输入字段的尺寸（以字符计）

### maxlength 属性

*maxlength* 属性规定输入字段允许的最大长度

如设置 maxlength 属性，则输入控件不会接受超过所允许数的字符。

该属性不会提供任何反馈。如果需要提醒用户，则必须编写 JavaScript 代码。

**注释：**输入限制并非万无一失。JavaScript 提供了很多方法来增加非法输入。如需安全地限制输入，则接受者（服务器）必须同时对限制进行检查。

### select 元素

```html
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab" selected>Saab</option>
<option value="fiat">Fiat</option>
<option value="audi">Audi</option>
</select>
```

##### option元素

option元素定义待选择的选项。

列表通常会把首个选项显示为被选选项。

您能够通过添加 selected 属性来定义预定义选项。

<option value="saab" selected>Saab</option>

### textarea> 元素

** 元素定义多行输入字段（*文本域*）：注意其属性

### 实例

```
<textarea name="message" rows="10" cols="30">
The cat was playing in the garden.
</textarea>
```

## 1.10实体

用于书写不显示的关键字![image-20200408105300388](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408105300388.png)

# 2.html5

## 新增元素

![image-20200408110508840](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408110508840.png)

![image-20200408110523413](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408110523413.png)

## 新增输入类型

![image-20200408110630251](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408110630251.png)

required=“required”  表示这个输入框需要数据

### labal标签

## 实例

带有两个输入字段和相关标记的简单 HTML 表单：

```
<form>
  <label for="male">Male</label>
  <input type="radio" name="sex" id="male" />
  <br />
  <label for="female">Female</label>
  <input type="radio" name="sex" id="female" />
</form>
```

<label> 标签为 input 元素定义标注（标记）。

label 元素不会向用户呈现任何特殊效果。不过，它为鼠标用户改进了可用性。如果您在 label 元素内点击文本，就会触发此控件。就是说，当用户选择该标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。

### 注：

<label> 标签的 for 属性应当与相关元素的 id 属性相同。

placehold属性后面的值为预填充

## 新的属性语法

![image-20200408110742058](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408110742058.png)

## HTML5 图像

| 标签     | 描述                             |
| :------- | :------------------------------- |
| <canvas> | 定义使用 JavaScript 的图像绘制。 |
| <svg>    | 定义使用 SVG 的图像绘制。        |

## 新的媒介元素

| 标签     | 描述                                 |
| :------- | :----------------------------------- |
| <audio>  | 定义声音或音乐内容。                 |
| <embed>  | 定义外部应用程序的容器（比如插件）。 |
| <source> | 定义 <video> 和 <audio> 的来源。     |
| <track>  | 定义 <video> 和 <audio> 的轨道。     |
| <video>  | 定义视频或影片内容。                 |

## HTML5 语义元素

语义元素清楚地向浏览器和开发者描述其意义。

*非语义*元素的例子：<div> 和 <span> - 无法提供关于其内容的信息。

*语义*元素的例子：<form>、<table> 以及 <img> - 清晰地定义其内容。

HTML5 定义了八个新的*语义* HTML 元素。所有都是*块级*元素。

您可以把 CSS *display* 属性设置为 *block*，以确保老式浏览器中正确的行为：

### 实例

```
header, section, footer, aside, nav, main, article, figure {
    display: block; 
}
```

HTML5 提供了定义页面不同部分的新语义元素：可以代替div使用可以明确对这块包含信息

![image-20200408111542846](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408111542846.png)

### HTML5 语义元素

![HTML5 语义元素](https://www.w3school.com.cn/i/ct_sem_elements.png)

## 全局属性

![image-20200408112022122](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408112022122.png)

contenteditable写有改属性的标签可以编辑 赋值时Boolean值

hidden属性 表示课件或者不可见

第三个拼写检查

第四个赋值属性值位数字可以使用tab建根据数字大小获取焦点