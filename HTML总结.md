#                            HTML总结

HTML是超文本标记语言，一种定义内容结构的标记语言，不是一门编程语言。“超文本”指连接单个网站内或多个网站间的网页的链接；链接是网络的一个基本方面。

## HTML元素

HTML使用“标记”来注明文本、图片和其他内容，以便在浏览器中显示。HTML 标记包含一些规定的"元素"如 `<head>，<title>，<body>，<header>，<footer>，<article>，<section>，<p>，<div>，<span>，<img>，<aside>，<audio>，<canvas>，<d`atalist>，<details>，<embed>，<nav>，<output>，<progress>，<video> 等等。如下所示的一个用于展示段落的元素：

![f63738cc51ebfa14](C:\Users\Administrator\Pictures\f63738cc51ebfa14.png)

1. 开始标签（Opening tag）：包含元素的名称（本例为 p），被左、右角括号所包围。表示元素从这里开始或者开始起作用 
2. 结束标签（Closing tag）：与开始标签相似，只是其在元素名之前包含了一个斜杠。这表示着元素的结尾 
3. 内容（Content）：元素的内容，本例中就是所输入的文本本身。
4. 元素（Element）：开始标签、结束标签与内容相结合，便是一个完整的元素。

## 注释

如同大部分的编程语言一样，在 HTML 中有一种可用的机制来在代码中书写注释 。

为了将一段 HTML 中的内容置为注释，你需要将其用特殊的记号`<!--`和`-->`包括起来， 比如：



```html
<p>我在注释外，可以显示！</p>
<!-- <p>我在注释内！浏览器将忽略我</p> -->
```

## 空元素

一般来说，元素都拥有**开始标签，内容，结束标签**。但有一些元素只有一个开始标签，通常用来在此元素所在位置插入/嵌入一些东西，如`<br>, <hr>, <input>, <img>, <a>`等等。我们称其为空元素，如下：



```html
<!-- 换行 -->
<p>我可以<br>换行</p> 
<!-- 水平分割线 -->
<hr>
<!-- 输入框 -->
<input>
```

## 元素的属性

元素是可以有相关属性的。属性包含元素的额外信息，这些信息不会在浏览器中显示出来。



```html
<!-- 带属性的段落输入框 -->
<p title="这是个title属性">鼠标移上来试试！</p>
<!-- 带属性的输入框 -->
<input type="text">
<input type="password">
```



一个属性必须包含如下内容：



1. 一个空格，在属性和元素名称之间。(如果已经有一个或多个属性，就与前一个属性之间有一个空格。)
2. 属性名称，后面跟着一个 = 号。
3. 一个属性值，由一对引号 "" 引起来。

## 超链接语法

```html
<a href="https://www.baidu.com/" target="_blank">百度一下</a>
```



说明：



1. `href`即为要跳转去的地址 URL（Uniform Resorce Locator)
2. `target`属性为`_blank`表示在新的页面打开超链接（默认是在当前页面打开即`_self`）
3. 超链接标签包含的内容（当前为文字"百度一下"）即为显示在页面上供用户点击的

## 锚点

锚点，也称为书签，用于标记页面的某个元素或位置。通过锚点，我们可以轻易的在长页面内实现跳转。



先使用`id`属性生成某元素的锚点，然后再使用超链接指向该锚点即可。



```html
<!-- 文档其余部分 -->
<h2 id="C4">第四章 论零号病人的重要性</h2>
<!-- 文档其余部分 -->
<a href="#C4">跳到第四章</a>
<!-- 文档其余部分 -->
...
```



**注意：**

1. 元素的`id`值必须是唯一的，也即页面不能再有其它元素的`id`值为`C4`
2. 超链接中的地址需要有`#`符号

## 图片

在页面插入一张图片如下：



```html
<img src="https://mdbootstrap.com/img/logo/mdb192x192.jpg" alt="MDB Logo" width="200" height="200">
```



说明：



1. `src`属性为要显示图片文件的位置 URL，即图片文件的路径
2. `alt`属性当获取图片出现问题时显示的文字（占位符）
3. 可为图片指定高宽度，但不建议（可能导致图片变形）

## 文件路径

为获取图片文件，我们需要指定该文件位于何处，这称为文件路径。文件路径有相对路径和绝对路径两种。



上面图片的例子即为绝对路径。下面是相对路径的例子：



|                                    |                                        |
| ---------------------------------- | -------------------------------------- |
| 例子                               | 解释                                   |
| `<img src="picture.jpg">`          | 该图片文件与当前文档在同一目录中       |
| `<img src="./images/picture.jpg">` | 该图片文件在当前目录下的`images`目录中 |
| `<img src="../picture.jpg">`       | 该图片文件在上一级目录中               |

## 无序列表

```html
<ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>
```



无序列表使用`<ul>`标签，默认使用**实心圆点**作为每项的标志，其它的标志可以是空心圆`circle`，实心方块`square`以及不出现标志。



```html
<ul type="square">
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>
```

## 有序列表

```html
<ol>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
```



有序列表使用`<ol>`标签，默认使用**数字**作为每项的标志，其它的标志可以是大写字母`A`，小写字母`a`，罗马字母`i`等。



```html
<ol type="a">
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
```

当网站需要获取我们的一些信息如：用户名、密码、选择买什么、买多少、提出意见等等时，我们就需要使用表单（form）来让用户填写或选择。



请输入如下代码进行学习：



```html
<form>
  <!-- 文本框，注意有 placeholder 提示符 -->
  用户名：<br>
  <input type="text" name="name" placeholder="请输入用户名"><br>
  <!-- 密码框 -->
  密码：<br>
  <input type="password" name="ps" placeholder="请输入密码"><br>
  年龄：<br>
  <!-- 数字输入框，注意 min 和 value 属性-->
  <input type="number" name="age" min="18" value="18"><br>
  <!-- 单选按钮, 注意 checked 属性 -->
  性别：<br>
  <input type="radio" name="gender" value="male" checked> 男<br>
  <input type="radio" name="gender" value="female"> 女<br>
  <input type="radio" name="gender" value="other"> 其它<br>
  <!-- 下拉列表，注意 selected 属性 -->
  党派：<br>
  <select name="party">
    <option value="D">民主党</option>
    <option value="R" selected>共和党</option>
    <option value="N">无党派</option>
  </select><br>
  <!-- 多选框 -->
  您有哪些交通工具：<br>
  <input type="checkbox" name="vehicle1" value="Bike"> 自行车<br>
  <input type="checkbox" name="vehicle2" value="Motocycle" checked> 摩托车<br>
  <input type="checkbox" name="vehicle3" value="Car"> 轿车<br>
  <input type="checkbox" name="vehicle4" value="Jet"> 飞机<br>
  <!-- 日期选择器 -->
  您的工作日期：<br>
  <input type="date"><br>
  <!-- 文件选择器 -->
  上传您的照片:<br>
  <input type="file" name="photo"><br>
  <!-- 文本输入区域，注意 rows 和 cols 属性 -->
  您的建议：<br>
  <textarea name="message" rows="5" cols="30">
    The cat was playing in the garden.
  </textarea><br><hr>
  <!-- 表单提交/重置按钮，将表单中的数据取消或传输给服务器端进行处理 -->
  <input type="submit" value="提 交">
  <input type="reset" value="重 置">
</form>
```



**提示：** 当提交时，表单中没有`name`属性的元素将不会提交，比如上面工作日期的选择器。有`name`属性的元素其`value`的值将提交给服务器。

## 区块元素

区块元素在浏览器显示时，通常会以**新行**来开始（和结束）。如：`<h1>, <pre>, <ul>, <table>，<`div> 等。



```html
<h2>区块元素</h2>
<div>Hello</div>
<div>World</div>
<p>单独一行</p>
```

## 内联元素

内联元素相反，他们总是一个接一个进行显示，不会新起一行。如： `<span>, <input>, <td>, <a>, <img>`等。



```html
<h3>下面的元素将在一行中显示</h3>
<span>姓名：</span>
<input name="username">
<span>哈哈哈</span>
<a href="https://google.com/">Google</a>
<img src="https://mdbootstrap.com/img/logo/mdb192x192.jpg">
```

## 预设格式

如果你想在网页中展示一首诗或一些特别格式的文本，那么请使用`pre`标签。



```html
<!-- pre标签中的内容将保持格式不变 -->
<pre>
              我如果爱你——
              绝不象攀援的凌霄花，
              借你的高枝炫耀自己；

              我如果爱你——
              绝不学痴情的鸟儿，
              为绿荫重复单调的歌曲；

              也不止像泉源，
              常年送来清凉的慰藉；

              也不止像险峰，
              增加你的高度，衬托你的威仪。

              甚至日光。
              甚至春雨。

              不，这些都还不够！
              我必须是你近旁的一株木棉，
              作为树的形象和你站在一起。

              根，紧握在地下，
              叶，相触在云里。

              每一阵风过，
              我们都互相致意，
              但没有人，
              听懂我们的言语。

              你有你的铜枝铁干，
              像刀，像剑，
              也像戟；

              我有我红硕的花朵，
              像沉重的叹息，
              又像英勇的火炬。

              我们分担寒潮、风雷、霹雳；
              我们共享雾霭、流岚、虹霓。
              仿佛永远分离，
              却又终身相依。

              这才是伟大的爱情，
              坚贞就在这里：
              爱——
              不仅爱你伟岸的身躯，
              也爱你坚持的位置，足下的土地。
</pre>
```

## 特殊字符

考虑下面的代码将显示成什么？



```html
<p>有多          远，滚                         多远！</p>
```



或者你希望在页面显示一段 HTML 的源代码，你打算用标签`<pre>`:



```html
<pre>
  <h1>这是个一级标题</h1>
  <p>这是一个段落<p>
  <a href="https://twitter.com/">眼见何事，情系何处，身处何方，心思何人</a>
<pre>
```



以上代码将得不到你想要的结果。
原因是：在 HTML 中，某些字符是预留的。
在 HTML 中不能使用小于号（<）和大于号（>），这是因为浏览器会误认为它们是标签。
如果希望正确地显示预留字符，我们必须在 HTML 源代码中使用字符实体（character entities）



```html
<p>有多&nbsp;&nbsp;&nbsp;远，滚&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;多远！</p>
<hr>
<h2>test.html</h2>
<pre>
  &lt;h1&gt;这是个一级标题&lt;/h1&gt;
  &lt;p&gt;这是一个段落&lt;p&gt;
  &lt;a href="https://twitter.com/"&gt;眼见何事，情系何处，身处何方，心思何人&lt;/a&gt;
<pre>
```