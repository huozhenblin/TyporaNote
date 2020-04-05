样式插入三种样式

外部样式表

当样式需要应用于很多页面时，外部样式表将是理想的选择。在使用外部样式表的情况下，你可以通过改变一个文件来改变整个站点的外观。每个页面使用 标签链接到样式表。 标签在（文档的）头部

~~~html
<head> <link rel="stylesheet" type="text/css" href="https://www.w3cschool.cn/css/mystyle.css"> </head>
~~~

内部样式表

当单个文档需要特殊的样式时，就应该使用内部样式表。你可以使用 <style> 标签在文档头部定义内部样式表，就像这样:

~~~html
<head>
<style>
hr {color:sienna;}
p {margin-left:20px;}
body {background-image:url("images/back40.gif");}
</style>
</head>
~~~

内联样式

由于要将表现和内容混杂在一起，内联样式会损失掉样式表的许多优势。请慎用这种方法，例如当样式仅需要在一个元素上应用一次时。

~~~
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
~~~

注：

当同一个 HTML 元素被不止一个样式定义时，会使用哪个样式呢？

权限优先级

1. 浏览器缺省设置
2. 外部样式表
3. 内部样式表（位于 head 标签内部）
4. 内联样式（在 HTML 元素内部）

!important 规则例外

当 !important 规则被应用在一个样式声明中时，该样式声明会覆盖CSS中任何其他的声明，无论它处在声明列表中的哪里。

background-position 属性改变图像在背景中的位置

为 background-position 属性提供值有很多方法。首先，可以使用一些关键字：top、bottom、left、right 和 center；其次，可以使用长度值，如 100px 或 5cm；最后也可以使用百分数值。不同类型的值对于背景图像的放置稍有差异。

## Text文本格式

## 文本的对齐方式

文本排列属性是用来设置文本的水平对齐方式。

文本可居中或对齐到左或右,两端对齐.

当text-align设置为"justify"，每一行被展开为宽度相等，左，右外边距是对齐（如杂志和报纸）。

## 文本修饰

text-decoration 属性用来设置或删除文本的装饰。

**a {text-decoration:none;}*

h1 {text-decoration:overline;}
h2 {text-decoration:line-through;}
h3 {text-decoration:underline;}

## 文本间隔

~~~css
p
{
word-spacing:30px;
}
~~~

# 字体

这个属性有三个值：

- 正常 - 正常显示文本
- 斜体 - 以斜体字显示的文字
- 倾斜的文字 - 文字向一边倾斜（和斜体非常类似，但不太支持）

~~~css
p.normal {font-style:normal;}
p.italic {font-style:italic;}
p.oblique {font-style:oblique;}
~~~

## 链接样式

a:link {color:#FF0000;}   /* 未访问链接*/
a:visited {color:#00FF00;} /* visited link */
a:hover {color:#FF00FF;} /* mouse over link */
a:active {color:#0000FF;} /* selected link */

~~~css
a:link {color:#FF0000;}      /* 未访问链接*/
a:visited {color:#00FF00;}  /* visited link */
a:hover {color:#FF00FF;}  /* mouse over link */
a:active {color:#0000FF;}  /* selected link */
~~~

# CSS 盒



![image-20200403224853564](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200403224853564.png)

- **Margin（外边距）** - 清除边框区域。Margin没有背景颜色，它是完全透明

CSS Margin属性接受任何长度单位、百分数值甚至负值。

- CSS Margin属性接受任何长度单位、百分数值甚至负值。
- **Border（边框）** - 边框周围的填充和内容。边框是受到盒子的背景颜色影响

border-style 值:

border-style属性可以有1-4个值：

none: 默认无边框

dotted: 定义一个点线框

dashed: 定义一个虚线框

solid: 定义实线边界

double: 定义两个边界。 两个边界的宽度和border-width的值相同

groove: 定义3D沟槽边界。效果取决于边界的颜色值

ridge: 定义3D脊边界。效果取决于边界的颜色值

inset:定义一个3D的嵌入边框。效果取决于边界的颜色值

outset: 定义一个3D突出边框。 效果取决于边界的颜色值



边框-简写属性

~~~html
border:5px solid red;  边框宽度5 实线 红色
~~~



- **Padding（内边距）** - 清除内容周围的区域。会受到框中填充的背景颜色影响

~~~css
padding-top:25px;
padding-bottom:25px;
padding-right:50px;
padding-left:50px;
~~~

**padding:25px 50px 75px 100px;**

- 上填充为25px
- 右填充为50px
- 下填充为75px
- 左填充为100px

- **Content（内容）** - 盒子的内容，显示文本和图像

## CSS 分组 和 嵌套 选择器

分组选择器：

~~~css
h1,h2,p
{
color:green;
} 表示这三个标签颜色都是这个
~~~

## 嵌套选择器

~~~html
<div class="marked">
<p>This paragraph has not blue text.</p>
</div>
.marked p
{
	color:white;
}可以这样选择
~~~

# CSS Display(显示) 与 Visibility（可见性）

## 隐藏元素 - display:none或visibility:hidden

隐藏一个元素可以通过把display属性设置为"none"，或把visibility属性设置为"hidden"。但是请注意，这两种方法会产生不同的结果。

visibility:hidden可以隐藏某个元素，但隐藏的元素仍需占用与未隐藏之前一样的空间。也就是说，该元素虽然被隐藏了，但仍然会影响布局。

display:none可以隐藏某个元素，且隐藏的元素不会占用任何空间。也就是说，该元素不但被隐藏了，而且该元素原本占用的空间也会从页面布局中消失。



display:inline  display:block

分别是将元素更改为内联元素和块元素

## CSS Positioning(定位)

## Fixed 定位

元素的位置相对于浏览器窗口是固定位置。

即使窗口是滚动的它也不会移动：

## Static 定位

HTML元素的默认值，即没有定位，元素出现在正常的流中。

静态定位的元素不会受到top, bottom, left, right影响。

## Relative 定位

可以移动的相对定位元素的内容和

相对定位元素的定位是相对其正常位置。

实例相互重叠的元素，它原本所占的空间不会改变

## Absolute 定位

绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于<html>:

## 使用Padding设置垂直居中对齐

CSS 中一个简单的设置垂直居中对齐的方式就是头部顶部使用 padding:

.center {    padding: 70px 0;    border: 3px solid green; }

# CSS 组合选择符

CSS组合选择符包括各种简单选择符的组合方式。

在 CSS3 中包含了四种组合方式:

- 后代选取器(以空格分隔)
- 子元素选择器(以大于号分隔）
- 相邻兄弟选择器（以加号分隔）
- 普通兄弟选择器（以波浪号分隔）

## 后代选取器

后代选取器匹配所有指定元素的后代元素。

## 子元素选择器

与后代选择器相比，子元素选择器（Child selectors）只能选择作为某元素子元素的元素。

# CSS 属性选择器

# CSS3 边框

- border-radius
- box-shadow
- border-image（

border-radius属性就是被用于创建圆角的：

## CSS3 border-radius - 指定每个圆角

如果你在 border-radius 属性中只指定一个值，那么将生成 4 个 圆角。

但是，如果你要在四个角上一一指定，可以使用以下规则：

- **四个值:** 第一个值为左上角，第二个值为右上角，第三个值为右下角，第四个值为左下角。
- **三个值:** 第一个值为左上角, 第二个值为右上角和左下角，第三个值为右下角
- **两个值:** 第一个值为左上角与右下角，第二个值为右上角与左下角
- **一个值：** 四个圆角值相同

CSS3中的box-shadow属性被用来添加阴影:

~~~css
div
{
box-shadow: 10px 10px 5px #888888;
}
~~~

## CSS3 box-shadow属性

CSS3 中 CSS3 box-shadow 属性适用于盒子阴影