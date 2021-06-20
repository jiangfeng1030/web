# CSS总结

**CSS**是级联样式表（Cascading Style Sheets）的缩写。HTML 用于撰写页面的内容，而 CSS 将决定这些内容该如何在屏幕上呈现。

## CSS语法

一条CSS样式规则由两个主要的部分构成：选择器，以`{}`包裹的一条或多条声明:

![CSS-syntax](http://10.1.74.238/web/brief-css/img/86e63894cd2a6e2f.jpg)

这条规则表明，页面中所有的一级标题都显示为蓝色，字体大小为12像数。
说明：

- 选择器是您需要改变样式的对象（上图的规则就一级标题生效）。

- 每条声明由一个属性和一个值组成。（无论是一条或多条声明，都需要用`{}`包裹，且声明用`;`分割）

- 属性（property）是您希望设置的样式属性（style attribute）。每个属性有一个值。属性和值被冒号分开。

  ## 选择器

  一个页面上的元素众多，选择器就用于在页面中找到/选择需要应用这个样式的对象。
  除我们前示的元素选择器外，还有`id`和`class`选择器。其中`class`选择器使用非常普遍。

  **id 选择器**

  ```css
  /* 注意：id选择器前有 # 号。 */
  #sky{
    color: blue;
  }
  ```

  这条规则表明，找到页面上`id`为`sky`的那个元素让它呈现蓝色，如下所示的页面，**蓝色的天空**这几个字就将会是蓝色的。

  ```html
  <p id="sky">蓝色的天空</p>
  <p id="forest">绿色的森林</p>
  ```

**class 选择器**

```css
/* 注意：class选择器前有 . 号。 */
.center{
  text-align: center;
}
.large{
  font-size: 30px;
}
.red{
  color: red;
}
```

以上代码定义了三条规则，分别应用于页面上对应的元素，如只要页面上某元素的`class`为`red`，那么就让它呈现红色。
如下所示的页面：

```html
<p class="center">我会居中显示的</p>
<p class="red">我是红色的</p>
<p class="center large red">我又红又大还居中</p>
<p class="red">我也可以是红的</p>
```

## CSS如何生效

我们一般有三种方法：外部样式表，内部样式表，内联样式

### 外部样式表

新建如下内容的一个 HTML文件（后缀为.html)：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <!-- 注意下面这个语句，将导入外部的 mycss.css 样式表文件 -->
  <link rel="stylesheet" type="text/css" href="mycss.css">
  <title>页面标题</title>
</head>
<body>
  <h1>我是有样式的</h1>
  <hr>
  <p class="haha">还是有点丑：)</p>
</body>
</html>
```

在同一目录新建一个样式表文件mycss.css（注意后缀名为css）如下：

```css
body {
  background-color: linen;
  text-align: center;
}
h1 {
  color: red;
}
.haha {
  margin-top: 100px;
  color: chocolate;
  font-size: 50px;
}
```

在浏览器中打开这个 HTML 文件看看效果。

### 内部样式表

我们也可以将样式放在 HTML 文件中，这称为内部样式表。如：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <!-- 注意下面这个语句，将导入外部的 mycss.css 样式表文件 -->
  <link rel="stylesheet" type="text/css" href="mycss.css">
  <title>页面标题</title>
  <style>
    body {
      background-color: linen;
      text-align: center;
    }
    h1 {
      color: red;
    }
    .haha {
      margin-top: 100px;
      color: chocolate;
      font-size: 50px;
    }
  </style>
</head>
<body>
  <h1>我是有样式的</h1>
  <hr>
  <p class="haha">还是有点丑：)</p>
</body>
</html>
```

该例子与上述例子一样的效果，但注意在`<head>`元素中引入了`<style>`标签，放入了样式。

### 内联样式

所谓内联样式，就是直接把样式规则直接写到要应用的元素中，如：

```html
<h3 style="color:green;">I am a heading</h3>
```

### 级联的优先级

前面我们学习了三种使用样式的方式，如果某元素如`<p>`在外部、内部及内联样式中都被设置`color:red;`、`color:green;`、`color:blue;`，那么到底是什么颜色，也即到底哪个有效呢？
这就涉及样式的优先级问题，从高到低分别是：

1. 内联样式
2. 内部样式表或外部样式表
3. 浏览器缺省样式

## 颜色, 尺寸, 对齐

### 颜色

颜色在网页中的重要性不言而喻。
我们可以采用颜色名称也可以使用颜色RGB16进制值，来设定前景或背景的颜色。如：

```html
<!-- 颜色名称 -->
<h3 style="background-color:Tomato;">Tomato</h3>
<h3 style="background-color:Orange;">Orange</h3>
<h3 style="background-color:DodgerBlue;">DodgerBlue</h3>
<h3 style="background-color:MediumSeaGreen;">MediumSeaGreen</h3>
<h3 style="background-color:Gray;">Gray</h3>
<h3 style="background-color:SlateBlue;">SlateBlue</h3>
<h3 style="background-color:Violet;">Violet</h3>
<h3 style="background-color:LightGray;">LightGray</h3>
<hr>
<!-- 颜色值，3个字节分别代表RGB（Red，Green，Blue）的0～255的值 -->
<h3 style="background-color:#ff0000;">#ff0000</h3>
<h3 style="background-color:#0000ff;">#0000ff</h3>
<h3 style="background-color:#3cb371;">#3cb371</h3>
<h3 style="background-color:#ee82ee;">#ee82ee</h3>
<h3 style="background-color:#ffa500;">#ffa500</h3>
<h3 style="background-color:#6a5acd;">#6a5acd</h3>
<!-- 文本颜色 -->
<h3 style="color:Tomato;">Hello World</h3>
<p style="color:DodgerBlue;">Lorem ipsum dolor sit, amet consectetur adipisicing elit.</p>
<p style="color:MediumSeaGreen;">Ad facilis est ducimus rem consectetur, corporis omnis, eveniet esse dolor molestiae numquam odio corrupti, sed obcaecati praesentium accusamus? Tempora, dolor a?</p>
```

### 尺寸

我们可以用 `height` 和 `width` 设定元素内容占据的尺寸。常见的尺寸单位有：像数 `px`，百分比 `%`等。
新建如下 HTML 文件：

```html
<html>
  <head>
    <link rel="stylesheet" href="./mycss.css">
  </head>
  <body>
    <div class="example-1">
      这个元素高 200 pixels，占据全部宽度
    </div>
    <div class="example-2">
      这个元素宽200像素,高300像素
    </div>
  </body>
</html>
```

再建对应的 CSS 文件如下：

```css
.example-1 {
  width: 100%;
  height: 200px;
  background-color: powderblue;
  text-align: center;
}
.example-2 {
  height: 100px;
  width: 500px;
  background-color: rgb(73, 138, 60);
  text-align: right;
}
```

### 对齐

对于**元素中的文本**，我们可以简单的设置`text-align`属性为`left, center, right`即可（显然缺省的是左对齐），上例中已有相关的应用。
对于元素本身如何对齐，我们后面再学习。

## 盒子模型

盒子模型指的是一个 HTML 元素可以看作一个盒子。从内到外，这个盒子是由**内容 content, 内边距 padding, 边框 border, 外边距 margin**构成的，如下图所示：

![box](http://10.1.74.238/web/brief-css/img/bd78f5d3be0673d6.jpg)

**说明：**

- Content 盒子的内容，如文本、图片等
- Padding 填充，也叫内边距，即内容和边框之间的区域
- Border  边框，默认不显示
- Margin  外边距，边框以外与其它元素的区域

新建如下 HTML 文件：

```html
<html>
  <head>
    <link rel="stylesheet" href="./mycss.css">
  </head>
  <body>
    <div class="box1">我是内容一，外面红色的是我的边框。注意边框的内外都有25px的距离。</div>
    <div class="box2">我是内容二，外面蓝色的是我的边框。注意与上面元素的外边距，发生了叠加，不是50px而是25px。</div>
```

再建对应的 CSS 文件如下：

```css
.box1 {
  height: 200px;
  width: 200px;
  background-color:#615200;
  color: aliceblue;
  border: 10px solid red;
  padding: 25px;
  margin: 25px;
}
.box2 {
  height: 300px;
  width: 300px;
  background-color:#004d61;
  color: aliceblue;
  border: 10px solid blue;
  padding: 25px;
  margin: 25px;
}
```

打开浏览器看看效果。

![border](http://10.1.74.238/web/brief-css/img/4bc1c350e350a023.jpg)

留意上图，你会发现一个元素真正占据的宽度应该是：
左外边距 + 左边框宽度 + 左内边距 + 内容宽度 + 右内边距 + 右边框宽度 + 右外边距

因此，我们在用`width`属性设置元素的宽度时，实际上只设置了其内容的宽度。

## 边框与边距

### 边框

试一试如下的代码：

```html
<p class="example-1">I have black borders on all sides.</p>
<p class="example-2">I have a blue bottom border.</p>
<p class="example-3">I have rounded grey borders.</p>
<p class="example-4">I have a purple left border.</p>

```

```css
.example-1 {
  border: 1px dotted black; /* 上下左右都相同 */
}
.example-2 {
  border-bottom: 1px solid blue; /* 只设置底部边框 */
}
.example-3 {
  border: 1px solid grey;
  border-radius: 15px; /* 边框圆角 */
}
.example-4 {
  border-left: 5px solid purple;
}
```

### 边距

下面样式说明了内边距的设置：

```css
padding: 20px; /* 上下左右都相同 */
padding-top: 20px;
padding-bottom: 100px;
padding-right: 50px;
padding-left: 80px;
padding: 25px 50px 75px 100px; /* 简写形式，按上，右，下，左顺序设置 */
padding: 25px 10px; /* 简写形式，上下为25px，左右为10px */
```

外边距与此类似。

## 定位

`position`属性用于对元素进行定位。该属性有以下一些值：

- static    静态
- relative  相对
- fixed     固定
- absolute  绝对

设置了元素的`position`属性后，我们才能使用`top, bottom, left, right`属性，否则定位无效。

### static

设置为静态定位`position: static;`，这是元素的默认定位方式，也即你设置与否，元素都将按正常的页面布局进行。
即：按照元素在 HTML出现的先后顺序从上到下，从左到右进行元素的安排。

### relative

设置为相对定位`position: relative;`，这将把元素相对于他的静态（正常）位置进行偏移
试试如下的代码：

```html
<!-- HTML -->
<div class="example-relative">我偏移了正常显示的位置。去掉我的样式对比看看？</div>
<!-- CSS -->
.example-relative {
  position: relative;
  left: 60px;
  top: 40px;
  background-color: rgb(173, 241, 241);
}
```

### fixed

设置为固定定位`position: fixed;`，这将使得元素固定不动（即使你上下左右拖动浏览器的滚动条）。
此时元素固定的位置仍由`top, bottom, left, right`属性确定，但相对的是视口（viewport，就是浏览器的屏幕可见区域）
如下的代码将会在浏览器右下角固定放置一个按钮元素：

```html
<!-- HTML -->
<div class="broad">占位区域。请将浏览器窗口改变大小，看看右下角的按钮发生了什么？</div>
<div class="example-fixed">这个按钮是固定的</div>
<!-- CSS -->
.example-fixed {
  position: fixed;
  bottom: 40px;
  right: 10px;
  padding: 6px 24px;
  border-radius: 4px;
  color: #fff;
  background-color: #9d0f0f;
  cursor: pointer;
  box-shadow: 0 3px 3px 0 rgba(0,0,0,0.3), 0 1px 5px 0 rgba(0,0,0,0.12), 0 3px 1px -2px rgba(0,0,0,0.2);
}
.broad {
  height: 5000px;
  width: 5000px;
  padding: 20px;
  background-color: darkkhaki;
}
```

### absolute

设置为绝对定位`position: absolute;`，将使元素相对于其**最近设置了定位属性（非static）的父元素**进行偏移。
如果该元素的所有父元素都没有设置定位属性，那么就相对于`<body>`这个父元素。

试试如下的代码：

```html
<!-- HTML -->
<div class="example-relative">这是父元素，有 relative 定位属性
  <div class="example-absolute">
    这是子元素，有 absolute 定位属性
  </div>
</div>
<!-- CSS -->
.example-relative {
  position: relative;
  width: 400px;
  height: 200px;
  border: 3px solid rgb(87, 33, 173);
}
.example-absolute {
  position: absolute;
  top: 80px;
  right: 5px;
  width: 200px;
  height: 100px;
  border: 3px solid rgb(218, 73, 16);
}
```

## 溢出

当元素内容超过其指定的区域时，我们通过溢出`overflow`属性来处理这些溢出的部分。
溢出属性有一下几个值：

- visible 默认值，溢出部分不被裁剪，在区域外面显示
- hidden  裁剪溢出部分且不可见
- scroll  裁剪溢出部分，但提供上下和左右滚动条供显示
- auto    裁剪溢出部分，视情况提供滚动条

以上内容较好理解，请自行进行验证。
关于滚动，我们还可以单独对上下或左右方向进行，如下代码所示：

```html
<!-- HTML -->
<div class="example-overflow-scroll-y">You can use the overflow property when you want to have better control of the
    layout. The overflow property specifies what happens if content overflows an element's box.
</div>
<!-- CSS -->
.example-overflow-scroll-y {
  width: 200px;
  height: 100px;
  background-color: #eee;
  overflow-y: scroll;
}
```

## 浮动

在一个区域或容器内，我们可以设置`float`属性让某元素水平方向上向左或右进行移动，其周围的元素也会重新排列。
我们常用这种样式来使图像和文本进行合理布局，如我们希望有以下的效果：

![float1](http://10.1.74.238/web/brief-css/img/827b45ec5fec3e35.jpg)

让图片向右浮动即可，代码如下：

```html
<html>
<head>
  <style>
    .example-float-right {
      float: right;
    }
  </style>
</head>
<body>
  <img src="https://mdbootstrap.com/img/Photos/Others/placeholder1.jpg" class="example-float-right" alt="">
  <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quidem, architecto officiis, repellendus
  corporis obcaecati, et commodi quam vitae vel laudantium omnis incidunt repellat qui eveniet fugiat totam
  modi nam vero!</p>
</body>
```

一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。
浮动元素之后的元素将围绕它。

##  不透明度

我们可以用`opacity`对任何元素（不过常用于图片）设置不透明度。
值在`[0.0～`1.0]之间，值越低，透明度越高，如下图所示：

![opacity](http://10.1.74.238/web/brief-css/img/4922d14e36a0f88a.jpg)

试试如下代码：

```html
<html>
<head>
  <style>
    img {
      width: 25%;
      border-radius: 10px;
      float: left;
      margin: 10px;
    }
    .opacity-2 {
      opacity: 0.2;
    }
    .opacity-5 {
      opacity: 0.5;
    }
    .opacity-10 {
      opacity: 1;
    }
  </style>
</head>
<body>
  <img class="opacity-2" src="https://mdbootstrap.com/img/Photos/Horizontal/Nature/4-col/img%20(87).jpg">
  <img class="opacity-5" src="https://mdbootstrap.com/img/Photos/Horizontal/Nature/4-col/img%20(87).jpg">
  <img class="opacity-10" src="https://mdbootstrap.com/img/Photos/Horizontal/Nature/4-col/img%20(87).jpg">
</body>
</html>
```

## 组合选择器

前面我们学习了 CSS有三种选择器：元素、id 和 class 。但我们也可以进行组合，以得到简洁精确的选择。
下面我们介绍两种组合选择器。

### 后代选择器

以空格作为分隔，如：`.haha p` 代表在`div`元素内有`.haha`这种类的所有元素。
参见如下代码：

```html
<html>
<head>
  <style>
    .haha p {
      background-color: yellow;
    }
  </style>
</head>
<body>
  <div class="haha">
    <p>Paragraph 1 in the div .haha.</p>
    <p>Paragraph 2 in the div .haha>.</p>
    <span>
        <p>Paragraph 3 in the div .haha.</p>
    </span>
  </div>
  <p>Paragraph 4. Not in a div .haha.</p>
  <p>Paragraph 5. Not in a div .haha.</p>
</body>
</html>
```

段落1、2、3都将有黄色的背景，而段落4、5没有。

### 子选择器

也称为直接后代选择器，以`>`作为分隔，如：`.haha > p` 代表在有`.haha`类的元素内的直接`<p>`元素。
参见如下代码：

```html
<html>
<head>
  <style>
    .haha > p {
      background-color: yellow;
    }
  </style>
</head>
<body>
  <div class="haha">
    <p>Paragraph 1 in the div .haha.</p>
    <p>Paragraph 2 in the div .haha.</p>
    <span>
        <p>Paragraph 3 in the div .haha - it is descendant but not immediate child.</p>
    </span> <!-- not Child but Descendant -->
  </div>
  <p>Paragraph 4. Not in a div .haha.</p>
  <p>Paragraph 5. Not in a div .haha.</p>
</body>
</html>
```

虽然段落3在`.haha`类中，但它的直接父元素是`span`，不是`.haha`的直接后代，所以不能选择。只有段落1、2有黄色背景。

## 伪类和伪元素

伪类（pseudo-class）或伪元素（pseudo-element）用于定义元素的某种特定的状态或位置等。
比如我们可能有这样的需求：

- 鼠标移到某元素上变换背景颜色
- 超链接访问前后访问后样式不同
- 离开必须填写的输入框时出现红色的外框进行警示
- 保证段落的第一行加粗，其它正常
- ...

使用伪类/伪元素的语法如下：

```css
/* 选择器后使用 : 号，再跟上某个伪类/伪元素 */
selector:pseudo-class/pseudo-element {
  property:value;
}
```

以下是常用的伪类/伪元素的简单使用：

```css
a:link {color:#FF0000;}     /* 未访问的链接 */
a:visited {color:#00FF00;}  /* 已访问的链接 */
a:hover {color:#FF00FF;}    /* 鼠标划过链接 */
/* 鼠标移到段落则改变背景颜色 */
p:hover {background-color: rgb(226, 43, 144);}
p:first-line{color:blue;}   /* 段落的第一行显示蓝色 */
p:first-letter{font-size: xx-large;}   /* 段落的第一个字超大 */

h1:before { content:url(smiley.gif); } /* 在每个一级标题前插入该图片 */
h1:after { content:url(smiley.gif); } /* 在每个一级标题后插入该图片 */
```