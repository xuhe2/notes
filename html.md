* 在自结束的标签最好选择使用`/`加入结尾处

# 标题(heading)

HTML 标题（Heading）是通过 <h1> - <h6> 等标签进行定义的。

```html
<h1>This is a heading</h1>
<h2>This is a heading</h2>
<h3>This is a heading</h3>
```



# HTML 段落

HTML 段落是通过 <p> 标签进行定义的。

```html
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
```



## 换行

如果您希望在不产生一个新段落的情况下进行换行（新行），请使用 <br /> 标签：

```html
<p>This is<br />a para<br />graph with line breaks</p>
```





# HTML 链接

HTML 链接是通过 <a> 标签进行定义的。

```html
<a href="http://www.w3school.com.cn">This is a link</a>
```



## `target`属性

* 打开一个新的界面加载链接

```html
<a href="http://www.w3school.com.cn/" target="_blank">Visit W3School!</a>
```







# HTML 图像

HTML 图像是通过 <img> 标签进行定义的。

## 实例

```html
<img src="w3school.jpg" width="104" height="142" />
```



## 当图片不能正常显示的时候,使用替换文本属性

* 当图片不能正常显示的时候,显示一串文字提示错误

```html
<img src="boat.gif" alt="Big Boat">
```



## 替换界面的`背景图片`

```html
<body background="/i/eg_background.jpg">
```



## 把图片放在文字中

```html
<p>图像 <img src="/i/eg_cute.gif" align="bottom"> 在文本中</p>

<p>图像 <img src ="/i/eg_cute.gif" align="middle"> 在文本中</p>

<p>图像 <img src ="/i/eg_cute.gif" align="top"> 在文本中</p>
```





# HTML 元素

HTML 元素指的是从开始标签（start tag）到结束标签（end tag）的所有代码。

| 开始标签                | 元素内容            | 结束标签 |
| :---------------------- | :------------------ | :------- |
| <p>                     | This is a paragraph | </p>     |
| <a href="default.htm" > | This is a link      | </a>     |
| <br />                  |                     |          |

**注释：**开始标签常被称为开放标签（opening tag），结束标签常称为闭合标签（closing tag）。

# HTML 属性

HTML 标签可以拥有*属性*。属性提供了有关 HTML 元素的*更多的信息*。

属性总是以名称/值对的形式出现，比如：*name="value"*。

属性总是在 HTML 元素的*开始标签*中规定。



<h1> 定义标题的开始。

<h1 align="center"> 拥有关于对齐方式的附加信息。



```html
<body> 定义 HTML 文档的主体。

<body bgcolor="yellow"> 拥有关于背景颜色的附加信息。
```



# HTML 水平线

<hr /> 标签在 HTML 页面中创建水平线。

hr 元素可用于分隔内容。

# HTML 注释

可以将注释插入 HTML 代码中，这样可以提高其可读性，使代码更易被人理解。浏览器会忽略注释，也不会显示它们。

注释是这样写的：

## 实例

```
<!-- This is a comment -->
```



# HTML样式`style`

## 背景颜色

* 淘汰了`bgcolor`的使用

```html
<html>

<body style="background-color:yellow">
<h2 style="background-color:red">This is a heading</h2>
<p style="background-color:green">This is a paragraph.</p>
</body>

</html>
```



## 字体颜色样式

font-family、color 以及 font-size 属性分别定义元素中文本的字体系列、颜色和字体尺寸：

```html
<html>

<body>
<h1 style="font-family:verdana">A heading</h1>
<p style="font-family:arial;color:red;font-size:20px;">A paragraph.</p>
</body>

</html>
```



## 位置对齐

text-align 属性规定了元素中文本的水平对齐方式：

```html
<html>

<body>
<h1 style="text-align:center">This is a heading</h1>
<p>The heading above is aligned to the center of this page.</p>
</body>

</html>
```



# 引用

# 单句的引用

HTML *<q>* 元素定义*短的引用*。

浏览器通常会为 <q> 元素包围*引号*。

```html
<p>WWF 的目标是：<q>构建人与自然和谐共存的世界。</q></p>
```



## 块引用

* 注意,浏览器可能会对这个做缩进的处理

```html
<blockquote>
这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。
</blockquote>
```



# 标记缩写

HTML *<abbr>* 元素定义*缩写*或首字母缩略语。

对缩写进行标记能够为浏览器、翻译系统以及搜索引擎提供有用的信息。

### 实例

```html
<p><abbr title="World Health Organization">WHO</abbr> 成立于 1948 年。</p>
```



# 删除文字和插入文字的效果

```html
<del>二十</del> <ins>十二</ins>
```



# 定义

* 使用`dfn`
* 会变成`斜体`的字体

```html
<p><dfn title="World Health Organization">WHO</dfn> 成立于 1948 年。</p>
```





# HTML表格

表格由 <table> 标签来定义。每个表格均有若干行（由 <tr> 标签定义），每行被分割为若干单元格（由 <td> 标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。

```html
<table border="1">
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>row 2, cell 1</td>
<td>row 2, cell 2</td>
</tr>
</table>
```



## 边框属性

如果不定义边框属性，表格将不显示边框。有时这很有用，但是大多数时候，我们希望显示边框。

使用边框属性来显示一个带有边框的表格：

```html
<table border="1">
<tr>
<td>Row 1, cell 1</td>
<td>Row 1, cell 2</td>
</tr>
</table>
```



* 设置出边框实线,并且设置边框颜色

```html
<table style="border: 10px solid forestgreen">
```





## 列表头(table heading)

表格的表头使用 <th> 标签进行定义。

大多数浏览器会把表头显示为粗体居中的文本：

```html
<table border="1">
<tr>
<th>Heading</th>
<th>Another Heading</th>
</tr>
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>row 2, cell 1</td>
<td>row 2, cell 2</td>
</tr>
</table>
```



# HTML列表



## 无序列表(unordered list)

* 每个列表的元素使用小圆点标记.

无序列表始于 <ul> 标签。每个列表项始于 <li>。

```html
<ul>
<li>Coffee</li>
<li>Milk</li>
</ul>
```



### 无序列表的样式(type)

* 点状

```html
<ul type="disc">
```



* 圆圈

```html
<ul type="circle">
```



* 正方形

```html
<ul type="square">
```



## 有序列表(ordered list)

同样，有序列表也是一列项目，列表项目使用`数字`进行标记。

有序列表始于 <ol> 标签。每个列表项始于 <li> 标签。

```html
<ol>
<li>Coffee</li>
<li>Milk</li>
</ol>
```



## 有序列表的样式(type)

* 数字

> 这个是默认的



* 大写字母

```html
<ol type="A">
```



* 小写字母

```html
<ol type="a">
```



* 大写罗马字母

```html
<ol type="I">
```





* 小写罗马字母列表

```html
<ol type="i">
```





## 自定义列表

`<dl>` 表示定义列表，`<dt>` 表示术语标题，`<dd>` 表示术语的定义

```html
<dl>
<dt>Coffee</dt>
<dd>Black hot drink</dd>
<dt>Milk</dt>
<dd>White cold drink</dd>
</dl>
```



# HTML块

大多数 HTML 元素被定义为块级元素或内联元素。

编者注：“块级元素”译为 block level element，“内联元素”译为 inline element。

块级元素在浏览器显示时，通常会以新行来开始（和结束）

| 标签     | 描述                                       |
| :------- | :----------------------------------------- |
| `<div>`  | 定义文档中的分区或节（division/section）。 |
| `<span>` | 定义 span，用来组合文档中的行内元素。      |



# HTML类

对 HTML 进行分类（设置类），使我们能够为元素的类定义 CSS 样式。

* 这样就不用每次都敲一遍重复的代码
* 声明的时候,前面加上`.`

```html
<!DOCTYPE html>
<html>
<head>
<style>
.cities {
    background-color:black;
    color:white;
    margin:20px;
    padding:20px;
} 
</style>
</head>

<body>

<div class="cities">
<h2>London</h2>
<p>
London is the capital city of England. 
It is the most populous city in the United Kingdom, 
with a metropolitan area of over 13 million inhabitants.
</p>
</div> 

</body>
</html>
```

* HTML <div> 元素是*块级元素*。它能够用作其他 HTML 元素的容器。

  设置 <div> 元素的类，使我们能够为相同的 <div> 元素设置相同的类



# HTML`id`

* 注意,`ID`的值应该是唯一的
* `ID`是特定的样式声明,并且使用`JS`可以访问ID指向的对象.

* 声明的时候前面加上`#`,后续我们在访问这个元素的时候也要在`ID`前面加上`#`.

> id 的语法是：写一个井号 (#)，后跟一个 id 名称。然后，在花括号 {} 中定义 CSS 属性

```html
<!DOCTYPE html>
<html>
<head>
<style>
#myHeader {
  background-color: lightblue;
  color: black;
  padding: 40px;
  text-align: center;
}
</style>
</head>
<body>

<h1 id="myHeader">My Header</h1>

</body>
</html>
```



## 用过`ID`来实现跳转HTML书签

> 通过使用`href`实现

* 跳到当前界面的一个部分

```html
<a href="#C4">跳转到第四章</a>
```

* 跳到别的HTML文件的一个部分

```html
<a href="html_demo.html#C4">Jump to Chapter 4</a>
```





# HTML内联框架

> 使用`iframe`实现,可以从一个小部分访问别的界面

```html
<iframe src="URL"></iframe>
```

* 设置宽高

```html
<iframe src="demo_iframe.htm" width="200" height="200"></iframe>
```



# HTML头部(`<head>`)

> 注意以下的操作都在`<head>`中进行.
>
> 以下标签都可以添加到 head 部分：<title>、<base>、<link>、<meta>、<script> 以及 <style>

* 设置网页的标题

```html
<title>Title</title>
```



* 通过设置`<base>`让全部的`<a>`链接都在新的界面打开(注意,它是`自结束`的)

```html
<base target="_blank" />
```



* 描述网页的内容`<meta>`

```html
<meta name="author"
content="w3school.com.cn">

<meta name="revised"
content="David Yang,8/1/07">
 
<meta name="generator"
content="Dreamweaver 8.0en">
```



* 网页重定向

```html
<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
<meta http-equiv="Refresh" content="5;url=http://www.w3school.com.cn" />
```



* 定义文档和外部资源的关系

```html
<!-- 在HTML中，rel的全称是"Relationship"，用于指定链接元素与被链接资源之间的关系。 -->
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" type="text/css" href="styles.css">
  <link rel="icon" type="image/png" href="favicon.png">
</head>
<body>
  <p>这是一个示例网页。</p>
</body>
</html>
```



# HTML布局



## 使用`<div>`来切分



```html
<body>

<div id="header">
<h1>City Gallery</h1>
</div>

<div id="nav">
London<br>
Paris<br>
Tokyo<br>
</div>

<div id="section">
<h1>London</h1>
<p>
London is the capital city of England. It is the most populous city in the United Kingdom,
with a metropolitan area of over 13 million inhabitants.
</p>
<p>
Standing on the River Thames, London has been a major settlement for two millennia,
its history going back to its founding by the Romans, who named it Londinium.
</p>
</div>

<div id="footer">
Copyright W3School.com.cn
</div>

</body>
```

* 这些`ID`格式可以在`<head>`中实现.

| header  | 定义文档或节的页眉             |
| ------- | ------------------------------ |
| nav     | 定义导航链接的容器             |
| section | 定义文档中的节                 |
| article | 定义独立的自包含文章           |
| aside   | 定义内容之外的内容（比如侧栏） |
| footer  | 定义文档或节的页脚             |
| details | 定义额外的细节                 |
| summary | 定义 details 元素的标题        |



## 可以使用`details`来折叠信息

```html
<!DOCTYPE html>
<html lang="zh">
<head>
  <title>title</title>
  <meta charset="UTF-8"/>
  <style>
    /* 定义一个样式，使<summary>元素前面有个箭头 */
    summary::before {
      padding-right: 5px;
    }
  </style>
</head>
<body>
  <!-- <details> 元素用于创建可展开和折叠的详细内容块。 -->
  <details>
    <summary>点击我展开详细内容</summary>
    <p>这里是详细内容，可以在用户点击上面的标题后展开。</p>
  </details>
</body>
</html>
```





# HTML响应式设计(RWB)

> 什么是响应式设计?
>
> - RWD 指的是响应式 Web 设计（Responsive Web Design）
> - RWD 能够以可变尺寸传递网页
> - RWD 对于平板和移动设备是必需的

* 使用直接构建的方式

```html
/* 以下是 CSS 选择器，它匹配所有使用 class="city" 的 HTML 元素。 */
.city {
  /* 设置浮动为左，使元素在其容器内左浮动。 */
  float: left;

  /* 设置元素与周围元素的外边距为 5 像素。 */
  margin: 5px;

  /* 设置元素内部内容与边框之间的填充为 15 像素。 */
  padding: 15px;

  /* 设置元素的宽度为 300 像素。 */
  width: 300px;

  /* 设置元素的高度为 300 像素。 */
  height: 300px;

  /* 设置元素的边框为 1 像素宽、黑色实线边框。 */
  border: 1px solid black;
}
```



* 使用CSS的框架实现

> 待写



# HTML关键字的表示

> 在HTML代码中,有一部分的关键字是不能直接表示的,我们需要使用别的方法表示

* 访问官方的字符实体表来查询
* 一些特殊的`符号`和`表情(emoj)`也可以使用这样表示