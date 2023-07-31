# 一.介绍

**CSS** (Cascading Style Sheets，层叠样式表），是一种用来为结构化文档（如 HTML 文档或 XML 应用）添加样式（字体、间距和颜色等）的计算机语言，**CSS** 文件扩展名为 **.css**。

**CSS3** 现在已被大部分现代浏览器支持，而下一版的 **CSS4** 仍在开发中。

# 二.CSS 注释

```css
/*这是个注释*/
p {
    text-align:center;
    /*这是另一个注释*/
    color:black;
    font-family:arial;
}
```

# 三.选择器

## 1.常用选择器

要给HTML元素设置CSS样式，可以使用id、class选择器

- id：id选择器为**特定id**的HTML元素指定样式，以 "#" 来定义。ID属性不要以数字开头，数字开头的ID在 Mozilla/Firefox 浏览器中不起作用。
- class：class 选择器用于描述**一组**元素的样式，class 选择器有别于id选择器，class可以在多个元素中使用。 在 CSS 中，类选择器以一个点 `.` 号表示。

## 2.分组选择器

样式表中有很多具有相同样式的元素，为了尽量减少代码，你可以使用分组选择，每个选择器用逗号分隔。

```css
h1,h2,p {
    color:green;
}

// 选择#aaa的所有h1、h2后代
#aaa h1,#aaa h2 {}
```

## 3.嵌套选择器

- **p{ }**: 为所有 **p** 元素指定一个样式。
- **.marked{ }**: 为所有 **class="marked"** 的元素指定一个样式。
- **.marked p{ }**: 为所有 **class="marked"** 元素内的 **p** 元素指定一个样式。
- **p.marked{ }**: 为所有 **class="marked"** 的 **p** 元素指定一个样式。

## 4.组合选择符

- 后代选择器(以`空格`分隔)：后代选择器用于选取某元素的后代元素。
- 子元素选择器(以大于 **>** 号分隔）：子元素择器主要用来选择某个元素的第一级子元素。
- 相邻兄弟选择器（以加号 **+** 分隔）：相邻兄弟选择器（Adjacent sibling selector）可选择紧接在另一元素后的元素，且二者有相同父元素。
- 后续兄弟选择器（以波浪号 **～** 分隔）：后续兄弟选择器选取所有指定元素之后的相邻兄弟元素。

## 5.属性选择器

### 1.属性选择器

**具有特定属性的HTML元素样式不仅仅是class和id**

```css
<style>
  [title] {
  color:blue;
  }
</style>

<h1 title="Hello world">Hello world</h1>
```

### 2.**属性和值选择器**

```css
[title=runoob] {
    border:5px solid green;
}
```

### 3.**属性和值的选择器 - 多值**

- **attribute 属性中包含 value**

[attribute~=value]属性中**包含**独立的单词value，使用`~=`分隔属性和值

```css
[title~=hello] { color:blue; }

<h1 title="hello world">Hello world</h1>
<p title="student hello">Hello CSS students!</p>
```

[attribute*=value] 属性中做字符串拆分，只要能拆出来 value 这个词

```css
[title*=flower] { color:blue; }

<h1 title="ffffflowerrrrrr" />Hello world</h1>
```

- **attribute 属性以 value 开头**

[attribute|=value] 属性中必须是完整且唯一的单词，，或者以`-`分隔开

```css
[lang|=en] {
	color:blue;
}

<p lang="en">Hello!</p>
<p lang="en-us">Hi!</p>
<p lang="en-gb">Ello!</p>
```

attribute^=value] 属性的前几个字母是 value 就可以

```css
[lang^=en]    -->  <p lang="ennn">
```

- **attribute 属性以 value 结尾**

```css
a[src$=".pdf"]
```

### 4.表单选择器

```css
input[type="text"]
{
    width:150px;
    display:block;
    margin-bottom:10px;
    background-color:yellow;
}
input[type="button"]
{
    width:120px;
    margin-left:35px;
    display:block;
}
```

# 四.CSS 伪类(Pseudo-classes)

伪类的语法：

```css
selector:pseudo-class {property:value;}
```

CSS类也可以使用伪类：

```css
selector.class:pseudo-class {property:value;}
```

## 1.anchor伪类

在支持 CSS 的浏览器中，链接的不同状态都可以以不同的方式显示

```css
a:link {color:#FF0000;} /* 未访问的链接 */
a:visited {color:#00FF00;} /* 已访问的链接 */
a:hover {color:#FF00FF;} /* 鼠标划过链接 */
a:active {color:#0000FF;} /* 已选中的链接 */
```

## 2.伪类和CSS类

伪类可以与 CSS 类配合使用

```css
a.red:visited {color:#FF0000;}

<a class="red" href="css-syntax.html">CSS 语法</a>
```

## 3.lang 伪类

lang 伪类使你有能力为不同的语言定义特殊的规则

# 四.CSS使用方式

1. 内联样式：在HTML元素中使用"style" **属性**

   ```css
   <h1 style="text-align:center;">居中对齐的标题</h1>
   ```

2. 内部样式表：在HTML文档头部 `<head>`区域使用`<style>`**元素** 来包含CSS

   ```css
   <head>
     <style type="text/css">
     	body {background-color:yellow;}
     	p {color:blue;}
     </style>
   </head>
   ```

3. 外部引用：使用外部 CSS **文件**

   ```css
   <head>
   	<link rel="stylesheet" type="text/css" href="mystyle.css">
   </head>
   ```

# 五.多重样式优先级

如果某些属性在不同的样式表中被同样的选择器定义，那么属性值将从更具体的样式表中被继承过来。 

例如，外部样式表拥有针对 h3 选择器的三个属性：

```css
# 外部样式表
h3{
    color:red;
    text-align:left;
    font-size:8pt;
}

# 内部样式表
h3{
    text-align:right;
    font-size:20pt;
}
```

假如同时拥有内部样式表与外部样式表链接，那么 h3 得到的样式是：

```css
color:red;
text-align:right;
font-size:20pt;
```

引用方式优先级：**（内联样式）Inline style > （内部样式）Internal style sheet >（外部样式）External style sheet > 浏览器默认样式**

选择器优先级：内联样式表的权值最高 > ID 选择器的权值 > Class 类选择器的权值 > HTML 标签选择器的权值

# 六.CSS 盒子模型(Box Model)

所有HTML元素可以看作盒子，在CSS中，"box model"这一术语是用来设计和布局时使用。

CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。

盒模型允许我们在其它元素和周围元素边框之间的空间放置元素。

![box-model](assist/box-model.gif)

- **Margin(外边距)** ：清除边框外的区域，外边距是透明的。
- **Border(边框)** ：围绕在内边距和内容外的边框。
- **Padding(内边距)** ：清除内容周围的区域，内边距是透明的。当元素的 padding（填充）内边距被清除时，所释放的区域将会受到元素背景颜色的填充。
- **Content(内容)** ：盒子的内容，显示文本和图像。

# 七.CSS 轮廓（outline）

轮廓（outline）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。

![box_outline](assist/box_outline.gif)

- outline（css2）：在一个声明中设置所有的轮廓属性
- outline-color（css2）：设置轮廓的颜色
- outline-style（css2）：设置轮廓的样式
- outline-width（css2）：设置轮廓的宽度

# 八.CSS Position(定位)

position 属性的五个值：

- static：HTML 元素的默认值，即没有定位，遵循正常的文档流对象。静态定位的元素不会受到 top, bottom, left, right影响。

- relative：相对定位元素的定位是相对其正常位置。移动相对定位元素，但它原本所占的空间不会改变。相对定位元素经常被用来作为绝对定位元素的容器块。

- fixed：元素的位置相对于浏览器窗口是固定位置。即使窗口是滚动的它也不会移动。

- absolute：绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于`<html>`。absolute 定位使元素的位置与文档流无关，因此不占据空间。absolute 定位的元素和其他元素重叠。

- sticky：sticky 英文字面意思是粘，粘贴，所以可以把它称之为粘性定位。基于用户的滚动位置来定位。

- 粘性定位的元素是依赖于用户的滚动，在 **position:relative** 与 **position:fixed** 定位之间切换。

  它的行为就像 **position:relative;** 而当页面滚动超出目标区域时，它的表现就像 **position:fixed;**，它会固定在目标位置。

  元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。

  这个特定阈值指的是 top, right, bottom 或 left 之一，换言之，指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。

# 九.CSS 布局-Overflow

overflow 属性可以控制内容溢出元素框时在对应的元素区间内添加滚动条。

# 十.浮动Float

CSS 的 Float（浮动），会使元素向左或向右移动，其周围的元素也会重新排列。

元素的水平方向浮动，意味着元素只能左右移动而不能上下移动。

一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。

浮动元素之后的元素将围绕它。浮动元素之前的元素将不会受到影响。

# 十一.伪类

伪类选择元素基于的是当前元素处于的状态，或者说元素当前所具有的特性，而不是元素的id、class、属性等静态的标志。由于状态是动态变化的，所以一个元素达到一个特定状态时，它可能得到一个伪类的样式；当状态改变时，它又会失去这个样式。由此可以看出，它的功能和class有些类似，但它是基于文档之外的抽象，所以叫伪类。

# 十二.伪元素

伪元素是对元素中的特定内容进行操作，它所操作的层次比伪类更深了一层，也因此它的动态性比伪类要低得多。实际上，设计伪元素的目的就是去选取诸如元素内容第一个字（母）、第一行，选取某些内容前面或后面这种普通的选择器无法完成的工作。它控制的内容实际上和元素是相同的，但是它本身只是基于元素的抽象，并不存在于文档中，所以叫伪元素。

# 十三.CSS媒体类型

一些 CSS 属性只设计了某些媒体。例如 voice-family 属性是专为听觉用户代理。其他一些属性可用于不同的媒体类型。例如， font-size 属性可用于屏幕和印刷媒体，但有不同的值。屏幕和纸上的文件不同，通常需要一个更大的字体，sans-serif 字体比较适合在屏幕上阅读，而 serif 字体更容易在纸上阅读。

## 1.@media规则

@media 规则允许在相同样式表为不同媒体设置不同的样式。
在下面的例子告诉我们浏览器屏幕上显示一个 14 像素的 Verdana 字体样式。但是如果页面打印，将是 10 个像素的 Times 字体。请注意，font-weight 在屏幕上和纸上设置为粗体。

```css
@media screen
{
    p.test {font-family:verdana,sans-serif;font-size:14px;}
}
@media print
{
    p.test {font-family:times,serif;font-size:10px;}
}
@media screen,print
{
    p.test {font-weight:bold;}
}
```























