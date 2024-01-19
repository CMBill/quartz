---
title: HTML
tags: 
  - HTML
  - 前端
---



## 元素语法
- 以 **开始标签（起始标签）** 开始，**结束标签（闭合标签）** 结束。
- 某些元素具有空内容，以开始标签的结束而结束，如 `<br>`。

### 空元素 
**不能**存在子节点（例如内嵌的元素或者文本节点）的元素。空元素只有开始标签且不能指定结束标签。

如果一个 HTML 元素的开始标签中存在尾随的 `/`（斜杠）字符，HTML 解析器会忽略该斜杠字符。因此空元素标签可以选择在末尾加一个斜杠 `/`，也可以省略斜杠 `/`。如 `<br/>`、`<hr>` 均可。

选择使用斜杠 `/` 是为了与 XML 语法保持一致，或者出于代码风格和一致性的考虑。XML、XHTML、SVG 的空元素必须使用自闭合标签。

### 注释
```HTML
<!-- 
我是 html 注释
可以多行
-->
```

### 标题
### 段落 `<p>`
### 换行 `<br>`
在不产生一个新段落的情况下进行换行

### 文本格式化
从 HTML4 开始，不赞成标签表示带样式信息，因此许多元素含义发生变化，如`<b>` 为**提醒注意**。单纯改变样式建议使用 CSS。

### 锚 `<a>`
使用 `href` 属性来描述前往的链接。

属性：
- `href`：指定链接目标的 URL。
- `target`（可选）：指定链接如何在浏览器中打开。常见的值包括 `_blank`（在新标签或窗口中打开链接）和 `_self`（在当前标签或窗口中打开链接）。
- `title`（可选）：提供链接的额外信息，通常在鼠标悬停在链接上时显示为工具提示。
- `rel`（可选）：指定与链接目标的关系，如 nofollow、noopener 等。
- `download`（可选）：将链接的 URL 视为下载资源。

`<a>` 标签内可以是文本，也可以是图片作为链接，直接在标签内使用 `<img>` 元素即可。也可以进行页面内跳转，也可以使用 `id` 属性：

```HTML
<a href="#section2">跳转到第二部分</a>
<!-- 在页面中的某个位置 -->
<a name="section2"></a>
```

### 头部 `<head>`
机器可读的区域，可以添加在头部区域的元素标签为: `<title>`,`<style>`，`<meta>`，`<link>`，`<script>`，`<noscript>` 和 `<base>`。

#### `<base>`
指定一个文档中包含的所有相对 URL 的根 URL。如果指定了多个 `<base>` 元素，只会使用第一个 `href` 和 `target` 值，其余都会被忽略。

#### 外部资源链接元素 `<link>`
规定了当前文档与外部资源的关系。该元素最常用于链接样式表，此外也可以被用来创建站点图标。如：
```HTML
<head>
    <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

#### 元数据 `meta`
通常用于指定网页的描述，关键词，文件的最后修改时间，作者等元数据。

```html
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width"/>
```

### 图像 `<img>`

### 表格 `<table>`
按照这个顺序：

1. 一个可选的标题 `<caption>` 元素
2. 零个或多个的列组 `<colgroup>` 元素，可以将不同的列分组
3. 一个可选的表头 `<thead>` 元素，定义列头的行
4. 下列任意一个：
    - 零个或多个 `<tbody>`，表示表格主体，与表头相对
    - 零个或多个 `<tr>`，表示表格的一行
5. 一个可选的 `<tfoot>` 元素，可用于在表格的底部定义摘要

而在表格内容中，使用 `th` 表示表头单元格（行或者列），其形式默认为加粗。使用 `td` 表示表格的数据单元格（table data）。

如下的代码其显示效果如下图
```html
<table>
  <caption>
    Superheros and sidekicks
  </caption>
  <colgroup>
    <col />
    <col span="2" class="batman" />
    <col span="2" class="flash" />
  </colgroup>
  <tr>
    <td> </td>
    <th scope="col">Batman</th>
    <th scope="col">Robin</th>
    <th scope="col">The Flash</th>
    <th scope="col">Kid Flash</th>
  </tr>
  <tr>
    <th scope="row">Skill</th>
    <td>Smarts</td>
    <td>Dex, acrobat</td>
    <td>Super speed</td>
    <td>Super speed</td>
  </tr>
</table>
```

![[Pasted image 20231228180519.png]]

### 区块 `<div>`、`<span>`
可以用于划分文档结构，设置文档样式等。

- `<div>`：块级元素，可以将内容分组，从而可以使用 CSS 定义内容的格式，或者划定文档布局。也可以在一段文档中划分标记出使用另一种语言书写的内容（使用 `lang` 属性）等。
- `<span>`：内联元素，适合用于对文本或其他行内元素进行样式化、标记或包裹。

### 框架 `<iframe>`
可以在同一个浏览器窗口中显示其他页面。

```html
<iframe src="demo_iframe.htm" width="200" height="200" frameborder="0"></iframe>
```

通过定义 `<fram>` 的 `name` 属性和 `<a>` 的 `target` 属性，也可以将页面中某个链接的目标页面在框架中显示，

```html
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="https://www.runoob.com" target="iframe_a" rel="noopener">RUNOOB.COM</a></p>
```

### 表单 `<form>`
表单表示文档中的一个区域，此区域包含交互控件，将用户收集到的信息发送到 Web 服务器，表单自身是**不可见**的，可见的是其中的控件。

`action` 属性定义表单数据提交的目标 URL，`method` 属性定义了提交数据的 HTTP 方法（POST 和 GET）

- POST：表单数据会包含在表单体内然后发送给服务器，用于提交敏感数据，如用户名与密码等。
- GET：默认值，会附加在 `action` 属性的 URL 中，并以 `?` 作为分隔符，一般用于不敏感信息。

`<input>` 获取的信息会以 `name=value` 的形式附加，并以 `&` 分隔。

#### 输入 `<input>`
由 `<type>` 属性定义输入控件的类型，常见的包括

| type 属性  | 类型   |
| ---------- | ------ |
| `text`     | 文本   |
| `password` | 密码   |
| `radio`    | 单选择 |
| `checkbox` | 复选   |
| `submit`   | 提交   |

具体详见：[&lt;input&gt;：输入（表单输入）元素-MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input)

## 样式 
- 内联样式：在 HTML 元素中使用 `style` 属性
- 内部样式表：在 HTML 文档头部 `<head>` 区域使用 `<style>` 元素来包含 CSS
- 外部引用：使用外部 CSS 文件

最好的方式是通过外部引用 CSS 文件。

## 脚本
使用 Javascript 使得页面具有更强的交互性。

### 脚本 `<script>`
通常用作嵌入或者引用 JavaScript 代码，既可包含脚本语句，也可通过 src 属性指向外部脚本文件。

```html
<!-- 引用外部脚本 -->
<script src="javascript.js"></script>
<!-- 使用内部脚本 -->
<script>
  alert("Hello World!");
</script>
```

### 脚本替代 `<noscript>`
定义脚本未被执行时的替代内容。

## 字符实体
用一串 `&` 开头，`;` 结尾的字符来表示特定的字符。HTML 的预留字符必须被替换为字符实体，一些在键盘上找不到的字符也可以使用字符实体来替换。

`&` 开头后直接加实体名称，或者 `&#` 开头后加实体编码均可。

一些常用的字符：
- &lt;：`&lt;`（less than）、`&#60;`
- &gt;：`&gt;`（greater than）、`&#62;`
- &nbsp;：`$nbsp;`（non-breaking space）、`&#160;`
- &amp;：`$amp;` 

详见：
- [HTML Standard](https://html.spec.whatwg.org/multipage/named-characters.html#named-character-references)
- [HTML ISO-8859-1 参考手册](https://www.runoob.com/tags/ref-entities.html)


