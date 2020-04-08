# 1.css概述

## 基础语法：

slector {

​	property：value

}

注：

- 属性之间用分号隔开

- 大于一个单词用双引号

# 2.选择器

### 选择器分组

你可以对选择器进行分组，这样，被分组的选择器就可以分享相同的声明。用逗号将需要分组的选择器分开。在下面的例子中，我们对所有的标题元素进行了分组。所有的标题元素都是绿色的。

```
h1,h2,h3,h4,h5,h6 {
  color: green;
  }
```

### 继承

子元素默认继承父元素规则，根据 CSS，子元素从父元素继承属性。

但是元素的私有css属性优先级更高

### 派生选择器

**通过依据元素在其位置的上下文关系来定义样式，你可以使标记更加简洁。**

比方说，你希望列表中的 strong 元素变为斜体字，而不是通常的粗体字，可以这样定义一个派生选择器：

```
li strong {
    font-style: italic;
    font-weight: normal;
  }
```

### CSS 元素选择器

最常见的 CSS 选择器是元素选择器。换句话说，文档的元素就是最基本的选择器

```
html {color:black;}
h1 {color:blue;}
h2 {color:silver;}
```

### 通配符选择器

CSS2 引入了一种新的简单选择器 - 通配选择器（universal selector），显示为一个星号（*）。该选择器可以与任何元素匹配，就像是一个通配符。

例如，下面的规则可以使文档中的每个元素都为红色：

```
* {color:red;}
```

这个声明等价于列出了文档中所有元素的一个分组选择器。利用通配选择器，只需敲一次键（仅一个星号）就能使文档中所有元素的 color 属性值指定为 red。

### 结合元素选择器

类选择器可以结合元素选择器来使用。

例如，您可能希望只有段落显示为红色文本：

```
p.important {color:red;}
```

选择器现在会匹配 class 属性包含 important 的所有 p 元素，但是其他任何类型的元素都不匹配，不论是否有此 class 属性。选择器 p.important 解释为：“其 class 属性值为 important 的所有段落”。 因为 h1 元素不是段落，这个规则的选择器与之不匹配，因此 h1 元素不会变成红色文本。

如果你确实希望为 h1 元素指定不同的样式，可以使用选择器 h1.important：

```
p.important {color:red;}
h1.important {color:blue;}
```

### CSS 多类选择器

在上一节中，我们处理了 class 值中包含一个词的情况。在 HTML 中，一个 class 值中可能包含一个词列表，各个词之间用空格分隔。例如，如果希望将一个特定的元素同时标记为重要（important）和警告（warning），就可以写作：

```
<p class="important warning">
This paragraph is a very important warning.
</p>
```

这两个词的顺序无关紧要，写成 warning important 也可以。

我们假设 class 为 important 的所有元素都是粗体，而 class 为 warning 的所有元素为斜体，class 中同时包含 important 和 warning 的所有元素还有一个银色的背景 。就可以写作：

```
.important {font-weight:bold;}
.warning {font-style:italic;}
.important.warning {background:silver;}
```

### CSS 属性选择器详解

**CSS 2 引入了属性选择器。**

**属性选择器可以根据元素的属性及属性值来选择元素。**

## 简单属性选择

如果希望选择有某个属性的元素，而不论属性值是什么，可以使用简单属性选择器。

### 例子 1

如果您希望把包含标题（title）的所有元素变为红色，可以写作：

```
*[title] {color:red;}
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_selector_attribute_att)



### 例子 2

与上面类似，可以只对有 href 属性的锚（a 元素）应用样式：

```
a[href] {color:red;}
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_selector_attribute_att_2)



### 例子 3

还可以根据多个属性进行选择，只需将属性选择器链接在一起即可。

例如，为了将同时有 href 和 title 属性的 HTML 超链接的文本设置为红色，可以这样写：

```
a[href][title] {color:red;}
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_selector_attribute_att_3)



### 例子 4

可以采用一些创造性的方法使用这个特性。

例如，可以对所有带有 alt 属性的图像应用样式，从而突出显示这些有效的图像：

```
img[alt] {border: 5px solid red;}
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_selector_attribute_att_4)



**提示：**上面这个特例更适合用来诊断而不是设计，即用来确定图像是否确实有效。

### CSS 后代选择器

**后代选择器（descendant selector）又称为包含选择器。**

**后代选择器可以选择作为某元素后代的元素。**

## 根据上下文选择元素

我们可以定义后代选择器来创建一些规则，使这些规则在某些文档结构中起作用，而在另外一些结构中不起作用。

举例来说，如果您希望只对 h1 元素中的 em 元素应用样式，可以这样写：

```
h1 em {color:red;}
```

上面这个规则会把作为 h1 元素后代的 em 元素的文本变为 红色。其他 em 文本（如段落或块引用中的 em）则不会被这个规则选中：

```
<h1>This is a <em>important</em> heading</h1>
<p>This is a <em>important</em> paragraph.</p>
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_selector_descendant_1)

### 注：

有关后代选择器有一个易被忽视的方面，即两个元素之间的层次间隔可以是无限的。

例如，如果写作 ul em，这个语法就会选择从 ul 元素继承的所有 em 元素，而不论 em 的嵌套层次多深。

因此，ul em 将会选择以下标记中的所有 em 元素：

### CSS 子元素选择器

**与后代选择器相比，子元素选择器（Child selectors）只能选择作为某元素子元素的元素。**

## 选择子元素

如果您不希望选择任意的后代元素，而是希望缩小范围，只选择某个元素的子元素，请使用子元素选择器（Child selector）。

例如，如果您希望选择只作为 h1 元素子元素的 strong 元素，可以这样写：

```
h1 > strong {color:red;}
```

这个规则会把第一个 h1 下面的两个 strong 元素变为红色，但是第二个 h1 中的 strong 不受影响：

```
<h1>This is <strong>very</strong> <strong>very</strong> important.</h1>
<h1>This is <em>really <strong>very</strong></em> important.</h1>
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_selector_child)

## 结合后代选择器和子选择器

请看下面这个选择器：

```
table.company td > p
```

上面的选择器会选择作为 td 元素子元素的所有 p 元素，这个 td 元素本身从 table 元素继承，该 table 元素有一个包含 company 的 class 属性。

## CSS 相邻兄弟选择器

**相邻兄弟选择器（Adjacent sibling selector）可选择紧接在另一元素后的元素，且二者有相同父元素。**

# 3.css样式

## 3.1背景

### 背景属性

![image-20200408121328821](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408121328821.png)

### 背景属性值

#### 背景色

可以使用 [background-color 属性](https://www.w3school.com.cn/cssref/pr_background-color.asp)为元素设置背景色。这个属性接受任何合法的颜色值。

这条规则把元素的背景设置为灰色：

```
p {background-color: gray;}
```

如果您希望背景色从元素中的文本向外少有延伸，只需增加一些内边距：

```
p {background-color: gray; 
			padding: 20px;
			}
```

如需查看本例的效果，可以[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_background-color)！

#### 背景图像

要把图像放入背景，需要使用 [background-image 属性](https://www.w3school.com.cn/cssref/pr_background-image.asp)。background-image 属性的默认值是 none，表示背景上没有放置任何图像。

如果需要设置一个背景图像，必须为这个属性设置一个 URL 值：

```
body {background-image: url(/i/eg_bg_04.gif);}
```

大多数背景都应用到 body 元素，不过并不仅限于此。

下面例子为一个段落应用了一个背景，而不会对文档的其他部分应用背景：

```
p.flower {background-image: url(/i/eg_bg_03.gif);}
```

您甚至可以为行内元素设置背景图像，下面的例子为一个链接设置了背景图像：

```
a.radio {background-image: url(/i/eg_bg_07.gif);}
```

如需查看上述例子的效果，可以[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_background-image_2)！



理论上讲，甚至可以向 textareas 和 select 等替换元素的背景应用图像，不过并不是所有用户代理都能很好地处理这种情况。

另外还要补充一点，background-image 也不能继承。事实上，所有背景属性都不能继承。

#### 背景定位

可以利用 [background-position 属性](https://www.w3school.com.cn/cssref/pr_background-position.asp)改变图像在背景中的位置。

下面的例子在 body 元素中将一个背景图像居中放置：

```
body
  { 
    background-image:url('/i/eg_bg_03.gif');
    background-repeat:no-repeat; 表示图片是否重复显示  共有四个值
    background-position:center;
  }
```

为 background-position 属性提供值有很多方法。首先，可以使用一些关键字：top、bottom、left、right 和 center。通常，这些关键字会成对出现，不过也不总是这样。还可以使用长度值，如 100px 或 5cm，最后也可以使用百分数值。不同类型的值对于背景图像的放置稍有差异。

##### 百分数值 长度值px

百分数值的表现方式更为复杂。假设你希望用百分数值将图像在其元素中居中，这很容易：

```
body
  { 
    background-image:url('/i/eg_bg_03.gif');
    background-repeat:no-repeat;
    background-position:50% 50%;
  }
```

这会导致图像适当放置，其中心与其元素的中心对齐。**换句话说，百分数值同时应用于元素和图像。**也就是说，图像中描述为 50% 50% 的点（中心点）与元素中描述为 50% 50% 的点（中心点）对齐。

#### 背景关联

如果文档比较长，那么当文档向下滚动时，背景图像也会随之滚动。当文档滚动到超过图像的位置时，图像就会消失。

您可以通过 [background-attachment 属性](https://www.w3school.com.cn/cssref/pr_background-attachment.asp)防止这种滚动。通过这个属性，可以声明图像相对于可视区是固定的（fixed），因此不会受到滚动的影响：

```
body 
  {
  background-image:url(/i/eg_bg_02.gif);
  background-repeat:no-repeat;
  background-attachment:fixed
  }
```

如需查看上例的效果，可以[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_background-attachment)。

background-attachment 属性的默认值是 scroll，也就是说，在默认的情况下，背景会随文档滚动。

![image-20200408122958662](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408122958662.png)

size 调整背景图片大小

### 注

- 背景是不可以继承的

## 3.2文本

可以继承

![image-20200408143129413](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408143129413.png)

[text-transform 属性](https://www.w3school.com.cn/cssref/pr_text_text-transform.asp)处理文本的大小写。这个属性有 4 个值：

- none
- uppercase
- lowercase
- capitalize

### 文本装饰

接下来，我们讨论 [text-decoration 属性](https://www.w3school.com.cn/cssref/pr_text_text-decoration.asp)，这是一个很有意思的属性，它提供了很多非常有趣的行为。

text-decoration 有 5 个值：

- none
- underline
- overline
- line-through
- blink

不出所料，underline 会对元素加下划线，就像 HTML 中的 U 元素一样。overline 的作用恰好相反，会在文本的顶端画一个上划线。值 line-through 则在文本中间画一个贯穿线，等价于 HTML 中的 S 和 strike 元素。blink 会让文本闪烁，类似于 Netscape 支持的颇招非议的 blink 标记

### 处理空白符

[white-space 属性](https://www.w3school.com.cn/cssref/pr_text_white-space.asp)会影响到用户代理对源文档中的空格、换行和 tab 字符的处理。

通过使用该属性，可以影响浏览器处理字之间和文本行之间的空白符的方式。

![image-20200408143950755](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408143950755.png)

### css3文本效果

text-shadow：想文本添加阴影  后面有4个属性值 前2个定位第三个透明度最后一个颜色

word-wrap：规定文本的换行规则 这个需要和宽度一起设置

## 3.3字体

**CSS 字体属性定义文本的字体系列、大小、加粗、风格（如斜体）和变形（如小型大写字母）。**

## 字体属性

![image-20200408144304972](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408144304972.png)

## 指定字体系列

使用 [font-family 属性](https://www.w3school.com.cn/cssref/pr_font_font-family.asp) 定义文本的字体系列。

除了各种特定的字体系列外，CSS 定义了 5 种通用字体系列：

- Serif 字体
- Sans-serif 字体
- Monospace 字体
- Cursive 字体
- Fantasy 字体

### 使用通用字体系列

如果你希望文档使用一种 sans-serif 字体，但是你并不关心是哪一种字体，以下就是一个合适的声明：

```
body {font-family: sans-serif;}
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_font_family_generic)

## 字体风格

[font-style 属性](https://www.w3school.com.cn/cssref/pr_font_font-style.asp)最常用于规定斜体文本。

该属性有三个值：

- normal - 文本正常显示
- italic - 文本斜体显示
- oblique - 文本倾斜显示

### 实例

```
p.normal {font-style:normal;}
p.italic {font-style:italic;}
p.oblique {font-style:oblique;}
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_font-style)

## 字体加粗

[font-weight 属性](https://www.w3school.com.cn/cssref/pr_font_weight.asp)设置文本的粗细。

使用 bold 关键字可以将文本设置为粗体。

## 字体大小

[font-size 属性](https://www.w3school.com.cn/cssref/pr_font_font-size.asp)设置文本的大小。

有能力管理文本的大小在 web 设计领域很重要。但是，您不应当通过调整文本大小使段落看上去像标题，或者使标题看上去像段落。

请始终使用正确的 HTML 标题，比如使用 <h1> - <h6> 来标记标题，使用 <p> 来标记段落。

font-size 值可以是绝对或相对值。

绝对值：

- 将文本设置为指定的大小
- 不允许用户在所有浏览器中改变文本大小（不利于可用性）
- 绝对大小在确定了输出的物理尺寸时很有用

相对大小：

- 相对于周围的元素来设置大小
- 允许用户在浏览器改变文本大小

**注意：**如果您没有规定字体大小，普通文本（比如段落）的默认大小是 16 像素 (16px=1em)。

## css链接

## 设置链接的样式

能够设置链接样式的 CSS 属性有很多种（例如 color, font-family, background 等等）。

链接的特殊性在于能够根据它们所处的状态来设置它们的样式。

链接的四种状态：

- a:link - 普通的、未被访问的链接
- a:visited - 用户已访问的链接
- a:hover - 鼠标指针位于链接的上方
- a:active - 链接被点击的时刻

### 实例

```
a:link {color:#FF0000;}		/* 未被访问的链接 */
a:visited {color:#00FF00;}	/* 已被访问的链接 */
a:hover {color:#FF00FF;}	/* 鼠标指针移动到链接上 */
a:active {color:#0000FF;}	/* 正在被点击的链接 */
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=css_link)

## 3.4列表

### 属性

![image-20200408144840544](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408144840544.png)

### 列表项图像

有时，常规的标志是不够的。你可能想对各标志使用一个图像，这可以利用 [list-style-image](https://www.w3school.com.cn/cssref/pr_list-style-image.asp) 属性做到：

```
ul li {list-style-image : url(xxx.gif)}
```

只需要简单地使用一个 url() 值，就可以使用图像作为标志。

## 3.5表格

### 属性

![image-20200408145209804](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408145209804.png)

### 表格边框

如需在 CSS 中设置表格边框，请使用 border 属性。

下面的例子为 table、th 以及 td 设置了蓝色边框：

```
table, th, td
  {
  border: 1px solid blue;边框厚度 实线 颜色
  }
  td
  {
  text-align:right;
  }
```

text-align 和 vertical-align 属性设置表格中文本的对齐方式。

text-align 属性设置水平对齐方式，比如左对齐、右对齐或者居中：

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_table_border)

### 表格内边距

如需控制表格中内容与边框的距离，请为 td 和 th 元素设置 padding 属性：

```
td
  {
  padding:15px;
  }
```

[亲自试一试](https://www.w3school.com.cn/tiy/t.asp?f=csse_table_padding)

## 3.6轮廓

![image-20200408153151464](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408153151464.png)

# 3.7定位

CSS 有三种基本的定位机制：普通流、浮动和绝对定位。

除非专门指定，否则所有框都在普通流中定位。也就是说，普通流中的元素的位置由元素在 (X)HTML 中的位置决定。

块级框从上到下一个接一个地排列，框之间的垂直距离是由框的垂直外边距计算出来。

行内框在一行中水平布置。可以使用水平内边距、边框和外边距调整它们的间距。但是，垂直内边距、边框和外边距不影响行内框的高度。由一行形成的水平框称为*行框（Line Box）*，行框的高度总是足以容纳它包含的所有行内框。不过，设置行高可以增加这个框的高度。

### 属性

![image-20200408153840757](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408153840757.png)

### CSS position 属性

通过使用 [position 属性](https://www.w3school.com.cn/cssref/pr_class_position.asp)，我们可以选择 4 种不同类型的定位，这会影响元素框生成的方式。

position 属性值的含义：

- static

  元素框正常生成。块级元素生成一个矩形框，作为文档流的一部分，行内元素则会创建一个或多个行框，置于其父元素中。

- relative

  相对定位是一个非常容易掌握的概念。如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置垂直或水平位置，让这个元素“相对于”它的起点进行移动。

  ```
  #box_relative {
    position: relative;
    left: 30px;
    top: 20px;
  }
  ```

  如下图所示：

  ![CSS 相对定位实例](https://www.w3school.com.cn/i/ct_css_positioning_relative_example.gif)

  注意，在使用相对定位时，无论是否进行移动，元素仍然占据原来的空间。因此，移动元素会导致它覆盖其它框。

- absolute

  元素框从文档流完全删除，并相对于其包含块定位。包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。

- fixed

  元素框的表现类似于将 position 设置为 absolute，不过其包含块是视窗本身。其相对于当前视窗固定

**提示：**相对定位实际上被看作普通流定位模型的一部分，因为元素的位置相对于它在普通流中的位置。

## 浮动

**浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。**浮动元素会生成一个块级框，而不论它本身是何种元素。

**由于浮动框不在文档的普通流中，所以文档的普通流中的块框表现得就像浮动框不存在一样。**

不继承

## CSS 浮动

请看下图，当把框 1 向右浮动时，它脱离文档流并且向右移动，直到它的右边缘碰到包含框的右边缘：

![CSS 浮动实例 - 向右浮动的元素](https://www.w3school.com.cn/i/ct_css_positioning_floating_right_example.gif)

再请看下图，当框 1 向左浮动时，它脱离文档流并且向左移动，直到它的左边缘碰到包含框的左边缘。因为它不再处于文档流中，所以它不占据空间，实际上覆盖住了框 2，使框 2 从视图中消失。

如果把所有三个框都向左移动，那么框 1 向左浮动直到碰到包含框，另外两个框向左浮动直到碰到前一个浮动框。

![CSS 浮动实例 - 向左浮动的元素](https://www.w3school.com.cn/i/ct_css_positioning_floating_left_example.gif)

如下图所示，如果包含框太窄，无法容纳水平排列的三个浮动元素，那么其它浮动块向下移动，直到有足够的空间。如果浮动元素的高度不同，那么当它们向下移动时可能被其它浮动元素“卡住”：

![CSS 浮动实例 2 - 向左浮动的元素 ](https://www.w3school.com.cn/i/ct_css_positioning_floating_left_example_2.gif)

## 属性

float 左右 none inherit

要想阻止行框围绕浮动框，需要对该框应用 [clear 属性](https://www.w3school.com.cn/cssref/pr_class_clear.asp)。clear 属性的值可以是 left、right、both 或 none，它表示框的哪些边不应该挨着浮动框。

## 3.8盒子模型

### CSS 框模型概述

![CSS 框模型](https://www.w3school.com.cn/i/ct_boxmodel.gif)

元素框的最内部分是实际的内容，直接包围内容的是内边距。内边距呈现了元素的背景。内边距的边缘是边框。边框以外是外边距，外边距默认是透明的，因此不会遮挡其后的任何元素。

**提示：**背景应用于由内容和内边距、边框组成的区域。

内边距、边框和外边距都是可选的，默认值是零。但是，许多元素将由用户代理样式表设置外边距和内边距。可以通过将元素的 margin 和 padding 设置为零来覆盖这些浏览器样式。这可以分别进行，也可以使用通用选择器对所有元素进行设置：

```
* {
  margin: 0;
  padding: 0;
}
```

在 CSS 中，width 和 height 指的是内容区域的宽度和高度。增加内边距、边框和外边距不会影响内容区域的尺寸，但是会增加元素框的总尺寸。

**提示：**内边距、边框和外边距可以应用于一个元素的所有边，也可以应用于单独的边。

**提示：**外边距可以是负值，而且在很多情况下都要使用负值的外边距。

### CSS padding 属性

CSS padding 属性定义元素的内边距。padding 属性接受长度值或百分比值，但不允许使用负值。

例如，如果您希望所有 h1 元素的各边都有 10 像素的内边距，只需要这样：

```
h1 {padding: 10px;}
```

您还可以按照上、右、下、左的顺序分别设置各边的内边距，各边均可以使用不同的单位或百分比值：

```
h1 {padding: 10px 0.25em 2ex 20%;}
```

![image-20200408163712046](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408163712046.png)

### CSS 边框

![image-20200408163817571](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408163817571.png)

#### 边框的样式

边的边框样式，可以使用下面的单边边框样式属性：

- [border-top-style](https://www.w3school.com.cn/cssref/pr_border-top_style.asp)
- [border-right-style](https://www.w3school.com.cn/cssref/pr_border-right_style.asp)
- [border-bottom-style](https://www.w3school.com.cn/cssref/pr_border-bottom_style.asp)
- [border-left-style](https://www.w3school.com.cn/cssref/pr_border-left_style.asp)

因此这两种方法是等价的：

```
p {border-style: solid solid solid none;}
p {border-style: solid; border-left-style: none;}
```

**注意：**如果要使用第二种方法，必须把单边属性放在简写属性之后。因为如果把单边属性放在 border-style 之前，简写属性的值就会覆盖单边值 none。

边框默认是透明的

### CSS 外边距

- [CSS 边框](https://www.w3school.com.cn/css/css_border.asp)
- [CSS 外边距合并](https://www.w3school.com.cn/css/css_margin_collapsing.asp)

**围绕在元素边框的空白区域是外边距。设置外边距会在元素外创建额外的“空白”。**

**设置外边距的最简单的方法就是使用 margin 属性，这个属性接受任何长度单位、百分数值甚至负值。**

下面的例子为 h1 元素的四个边分别定义了不同的外边距，所使用的长度单位是像素 (px)：

```
h1 {margin : 10px 0px 15px 5px;}
```

与内边距的设置相同，这些值的顺序是从上外边距 (top) 开始围着元素顺时针旋转的：

```
margin: top right bottom left
```

### CSS 外边距合并

外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。

**注释：**只有普通文档流中块框的垂直外边距才会发生外边距合并。行内框、浮动框或绝对定位之间的外边距不会合并。

## 3.9动画

![image-20200408165319609](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408165319609.png)

### 属性transform

上图为其值

### 2D转换

#### translate()

translate(x，y)方法，根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动。

transform: translate(50px,100px);

#### rotate() 方法

rotate()方法，在一个给定度数顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。

transform: rotate(30deg);

#### scale() 方法

scale()方法，该元素增加或减少的大小，取决于宽度（X轴）和高度（Y轴）的参数：

transform: scale(2,3); /* 标准语法 */

scale（2,3）转变宽度为原来的大小的2倍，和其原始大小3倍的高度。

#### matrix() 方法

matrix()方法和2D变换方法合并成一个。

matrix 方法有六个参数，包含旋转，缩放，移动（平移）和倾斜功能

transform:matrix(0.866,0.5,-0.5,0.866,0,0);

### 2D转换方法

![image-20200408170054324](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408170054324.png)

### 3D转换

#### rotateX() 方法

rotateX()方法，围绕其在一个给定度数X轴旋转的元素

transform: rotateX(120deg);

#### rotateY() 方法

rotateY()方法，围绕其在一个给定度数Y轴旋转的元素。

transform: rotateY(130deg);

![image-20200408175841385](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408175841385.png)

## 转换属性

![image-20200408175658074](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408175658074.png)

# css3

## 边框

用 CSS3，你可以创建圆角边框，添加阴影框，并作为边界的形象而不使用设计程序，如 Photoshop。

在本章中，您将了解以下的边框属性：

- border-radius
- box-shadow
- border-image

## border-radius

用于添加圆角，使用 CSS3 border-radius 属性，你可以给任何元素制作 "圆角"。

div
{
border:2px solid;
border-radius:25px;
}

![image-20200408170949434](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408170949434.png)

## box-shadow 

属性被用来添加阴影

div
{
box-shadow: 10px 10px 5px #888888;
}

后面的值为 left top 模糊程度 颜色

## background-image属性

CSS3中可以通过background-image属性添加背景图片。

不同的背景图像和图像用逗号隔开，所有的图片中显示在最顶端的为第一张。

\#example1 {     

background-image: url(img_flwr.gif), url(paper.gif);     background-position: right bottom, left top;     

background-repeat: no-repeat, repeat;  

}

![image-20200408172512026](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408172512026.png)

## CSS3 渐变（Gradients）

CSS3 渐变（gradients）可以让你在两个或多个指定的颜色之间显示平稳的过渡。

- **线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向**
- **径向渐变（Radial Gradients）- 由它们的中心定义**

**线性渐变 - 从上到下（默认情况下）**

下面的实例演示了从顶部开始的线性渐变。起点是红色，慢慢过渡到蓝色：

#### 实例

从上到下的线性渐变：

\#grad {    background-image: linear-gradient(#e66465, #9198e5); }

从左到右的线性渐变：

\#grad {  

height: 200px;  

background-image: linear-gradient(to right, red , yellow); 

}

使用to来表示渐变方向

to bottom right到对角

#### 使用角度

background-image: linear-gradient(-90deg, red, yellow);

![image-20200408173330603](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408173330603.png)

## CSS3 文本效果

## CSS3 文本效果

CSS3中包含几个新的文本特征。

在本章中您将了解以下文本属性：

- text-shadow
- box-shadow
- text-overflow
- word-wrap
- word-break

### text-shadow属性适用于文本阴影

h1 {    text-shadow: 5px 5px 5px #FF0000; }

###  CSS3 box-shadow 属性适用于盒子阴影

示例同上

## CSS3 过渡

配合2d、3d配合使用

transition 相当于那个属性有动画效果时在这注册一下执行时间

### 实例

**简单的鼠标悬浮过渡效果:**

~~~css
div {
    width: 100px;
    height: 100px;
    background: red;
    -webkit-transition: width 2s, height 2s, -webkit-transform 2s; /* For Safari 3.1 to 6.0 */
    transition: width 2s, height 2s, transform 2s;
}

div:hover {
    width: 200px;
    height: 200px;
    -webkit-transform: rotate(180deg); /* Chrome, Safari, Opera */
    transform: rotate(180deg);
}
div{
  width: 200px;
  height: 200px;
  background-color: #f00;
  transition: all 2s;
}

div:hover{
  background-color: #00f;
  transform: translateX(500px) translateY(500px) scale(0.8) rotate(360deg);
}
~~~

过度属性

![image-20200408181112069](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408181112069.png)

  transition: width 2s, height 2s, transform 2s;  

 -webkit-transition: width 2s; /* Safari */ 

}

~~~css
div
{
	width:100px;
	height:100px;
	background:red;
	transition-property:width;
	transition-duration:1s;
	transition-timing-function:linear;
	transition-delay:2s;
	/* Safari */
	-webkit-transition-property:width;
	-webkit-transition-duration:1s;
	-webkit-transition-timing-function:linear;
	-webkit-transition-delay:2s;
}

div:hover
{
	width:200px;
}
~~~

css3多列

![image-20200408181534666](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408181534666.png)

~~~html
 
<style> 
.newspaper
{
	column-count:3;
	column-gap:40px;
	column-rule-style:dotted;

	/* Firefox */
	-moz-column-count:3;
	-moz-column-gap:40px;
	-moz-column-rule-style:dotted;

	/* Safari and Chrome */
	-webkit-column-count:3;
	-webkit-column-gap:40px;
	-webkit-column-rule-style:dotted;
}
</style>
</head>
<body>

<p><b>注意:</b> Internet Explorer 9及更早 IE 版本浏览器不支持 column-count 属性。</p>

<div class="newspaper">
当我年轻的时候，我梦想改变这个世界；当我成熟以后，我发现我不能够改变这个世界，我将目光缩短了些，决定只改变我的国家；当我进入暮年以后，我发现我不能够改变我们的国家，我的最后愿望仅仅是改变一下我的家庭，但是，这也不可能。当我现在躺在床上，行将就木时，我突然意识到：如果一开始我仅仅去改变我自己，然后，我可能改变我的家庭；在家人的帮助和鼓励下，我可能为国家做一些事情；然后，谁知道呢?我甚至可能改变这个世界。
</div>

</body>
</html>
~~~

## CSS3 框大小

CSS3 `box-sizing` 属性可以设置 width 和 height 属性中包含了 padding(内边距) 和 border(边框)。

#### 不使用 CSS3 box-sizing 属性

默认情况下，元素的宽度与高度计算方式如下：

**width(宽) + padding(内边距) + border(边框) = 元素实际宽度**

**height(高) + padding(内边距) + border(边框) = 元素实际高度**

#### 使用 CSS3 box-sizing 属性

CSS3 `box-sizing` 属性在一个元素的 width 和 height 中包含 padding(内边距) 和 border(边框)。

如果在元素上设置了 `box-sizing: border-box;` 则 padding(内边距) 和 border(边框) 也包含在 width 和 height 中:

## CSS3 弹性盒子(Flex Box)

弹性盒子是 CSS3 的一种新的布局模式。

CSS3 弹性盒（ Flexible Box 或 flexbox），是一种当页面需要适应不同的屏幕大小以及设备类型时确保元素拥有恰当的行为的布局方式。

引入弹性盒布局模型的目的是提供一种更加有效的方式来对一个容器中的子元素进行排列、对齐和分配空白空间。

#### CSS3 弹性盒子内容

弹性盒子由弹性容器(Flex container)和弹性子元素(Flex item)组即其容器内的子容器

弹性容器通过设置 display 属性的值为 flex 或 inline-flex将其定义为弹性容器。

弹性容器内包含了一个或多个弹性子元素。

#### 注

 弹性容器外及弹性子元素内是正常渲染的。弹性盒子只定义了弹性子元素如何在弹性容器内布局。

弹性子元素通常在弹性盒子内一行显示。默认情况每个容器只有一行。

## 属性

![image-20200408184123785](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200408184123785.png)

### flex-direction

`flex-direction` 属性指定了弹性子元素在父容器中的位置。

语法

```
flex-direction: row | row-reverse | column | column-reverse
```

`flex-direction`的值有:

- row：横向从左到右排列（左对齐），默认的排列方式。
- row-reverse：反转横向排列（右对齐，从后往前排，最后一项排在最前面。
- column：纵向排列。
- column-reverse：反转纵向排列，从后往前排，最后一项排在最上面。

### justify-content 属性

内容对齐（justify-content）属性应用在弹性容器上，把弹性项沿着弹性容器的主轴线（main axis）对齐。

justify-content 语法如下：

```
justify-content: flex-start | flex-end | center | space-between | space-around
```

各个值解析:

- flex-start：

  弹性项目向行头紧挨着填充。这个是默认值。第一个弹性项的main-start外边距边线被放置在该行的main-start边线，而后续弹性项依次平齐摆放。

- flex-end：

  弹性项目向行尾紧挨着填充。第一个弹性项的main-end外边距边线被放置在该行的main-end边线，而后续弹性项依次平齐摆放。

- center：

  弹性项目居中紧挨着填充。（如果剩余的自由空间是负的，则弹性项目将在两个方向上同时溢出）。

- space-between：

  弹性项目平均分布在该行上。如果剩余空间为负或者只有一个弹性项，则该值等同于flex-start。否则，第1个弹性项的外边距和行的main-start边线对齐，而最后1个弹性项的外边距和行的main-end边线对齐，然后剩余的弹性项分布在该行上，相邻项目的间隔相等。

- space-around：

  弹性项目平均分布在该行上，两边留有一半的间隔空间。如果剩余空间为负或者只有一个弹性项，则该值等同于center。否则，弹性项目沿该行分布，且彼此间隔相等（比如是20px），同时首尾两边和弹性容器之间留有一半的间隔（1/2*20px=10px）。

## align-items 属性

`align-items` 设置或检索**弹性盒子元素**在侧轴（纵轴）方向上的对齐方式。

### 语法

```
align-items: flex-start | flex-end | center | baseline | stretch
```

各个值解析:

- flex-start：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
- flex-end：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
- center：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
- baseline：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
- stretch：如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。

## flex-wrap 属性

**flex-wrap** 属性用于指定弹性盒子的子元素换行方式。

### 语法

```
flex-wrap: nowrap|wrap|wrap-reverse|initial|inherit;
```

各个值解析:

- **nowrap** - 默认， 弹性容器为单行。该情况下弹性子项可能会溢出容器。
- **wrap** - 弹性容器为多行。该情况下弹性子项溢出的部分会被放置到新行，子项内部会发生断行
- **wrap-reverse** -反转 wrap 排列。

## align-content 属性

`align-content` 属性用于修改 `flex-wrap` 属性的行为。类似于 `align-items`, 但它不是设置弹性子元素的对齐，而是设置各个行的对齐。

### 语法

```
align-content: flex-start | flex-end | center | space-between | space-around | stretch
```

各个值解析:

- `stretch` - 默认。各行将会伸展以占用剩余的空间。
- `flex-start` - 各行向弹性盒容器的起始位置堆叠。
- `flex-end` - 各行向弹性盒容器的结束位置堆叠。
- `center` -各行向弹性盒容器的中间位置堆叠。
- `space-between` -各行在弹性盒容器中平均分布。
- `space-around` - 各行在弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半。

### 完美的居中

以下实例将完美解决我们平时碰到的居中问题。

使用弹性盒子，居中变的很简单，只想要设置 `margin: auto;` 可以使得弹性子元素在两上轴方向上完全居中: