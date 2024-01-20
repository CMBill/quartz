---
title: Javascript WebAPI
tags:
  - JavaScript
  - 前端
---

## DOM
文档对象模型，用来呈现以及与任意 HTML 和 XML 交互的功能（操作网页内容）。

### DOM 树
将 HTML 文档以树状结构直观表现出来，直观地体现了标签与标签之间的关系。

### DOM 对象
浏览器根据 HTML 标签生成的 **JS 对象**，与所有标签对应。`document` 是最大的对象，网页的所有内容都在其中。

## 获取 DOM 元素
### 利用 CSS 选择器

1. 选择匹配的第一个元素
```javascript
document.querySelector('css选择器')
```

- **参数**：包含一个或多个有效的 CSS 选择器的字符串。
- **返回值**：匹配的**第一个元素**，一个 `HTMLElement` 对象。
- 获取后可以直接对属性做修改。

如：
```html
<body>
    <p id="nav">导航栏</p>
    <div class="box">This is a box.</div>
    
    <script>
        const box1 = document.querySelector('div')  // 通过标签
        const box2 = document.querySelector('.box')  // 通过类名
        const nav = document.querySelector('#nav')  //通过 id
        nav.style.color = 'red' //修改 nav 颜色为 red
        </script>
</body>
```

2. 选择匹配的多个元素
```javascript
document.querySelectorAll('css选择器')
```

- **参数**：包含一个或多个有效的 CSS 选择器的字符串。
- **返回值**：匹配的所有对象构成的 `NodeList` 对象集合。

其返回值是一个**伪数组**，有长度、索引号，但是没有[[JavaScript#数组|数组方法]]。修改属性应使用遍历的方法。

```html
<body>
    <ul class="list">
        <li>List1</li>
        <li>List2</li>
        <li>List3</li>
    </ul>

    <script>
        const lis = document.querySelectorAll('.list li')
        for (let i = 0; i < lis.length; i++) {
            lis[i].style.color = 'red'
        }
    </script>
</body>
```

### 其他获取方法
```javascript
document.getElementByID('')
document.getElementsByTagName('')
document.getElementsByClassName('')
```

## 操作元素
### 操作元素内容
#### `innerText` 属性
获取标签内的文本，不解析标签

```html
<body>
    <div class="box">This is a box.</div>
    <script>
        const box = document.querySelector('.box')
        box.innerText = '<strong>啊对对对</strong>'
    </script>
</body>
```

如上的代码会将标签内的文本更换为 `&lt;strong&gt;啊对对对&lt;/strong&gt;`，即显示赋给的内容，不会使 `<b></b>` 解析为标签。

#### `innerHTML` 属性
解析标签

```html
<body>
    <div class="box">This is a box.</div>
    <script>
        const box = document.querySelector('.box')
        box.innerHTML = '<strong>啊对对对</strong>'
    </script>
</body>
```

便会将对应的代码修改为 `<strong>啊对对对</strong>`。

### 操作元素属性
#### 操作常用属性
获取到的 `HTML` 标签是一个 JS 对象，标签的属性即是对应对象的属性。
```javascript
const img = document.querySelector('img')
// 存在对应的属性即为修改，不存在即为添加
img.src = '/path/to/the/img'
img.title = 'title of the image'
```

#### 操作样式属性
##### 修改元素的 `style` 属性
修改 `对象.style.对应属性`。

> [!Tips]
> 通过以下规则，CSS 属性名称被转换为 JavaScript 标识符：
> - 如果属性是由一个单词组成的，则保持原样：如 `height`（也保持小写）。
> - 如果属性是由若干个单词组成的，由横线分隔，则横线被移除，并转化为_小驼峰_形式：如 `background-attachment` 转换为 `backgroundAttachment`。
> - 作为 JavaScript 保留关键字的 `float` 属性被转化为 `cssFloat`。
>
> 通过 `style` 属性设置的样式优先级与内联样式声明相同。

##### 操作类名
```javascript
元素.className = 'class name'  // 修改元素对应标签的 class
```

此操作会将原有的 `name` 替换掉

##### 通过 `classList`
通过 `classList` 属性来修改元素的类名，此属性可以返回一个元素的 `class` 属性（类名）的 [`DOMTokenList`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMTokenList) 集合

方法：
- `add()`：添加
- `remove()`：删除
- `replace(oldToken, newToken)`：将 `oldToken` 替换为 `newToken`，如果前者不存在，则返回 `false`
- `toggle()`：切换，如果标记存在则删除，如果不存在则添加

#### 操作表单元素
常用的操作：
```javascript
const inputForm = document.querySelector('input')
uname = inputForm.value // 值
inputForm.type = 'password'
```

> [!Tips]
> 对于添加即有效果（如 `checked`、`disabled`）的属性，只能传入布尔值来确定是否生效

#### 自定义属性
自定义属性在标签上一律以 `data-` 开头，在 DOM 对象中存储在 `dataset` 对象里，属性名即为标签上 `data-` 后面的部分。
```javascript
Element.dataset.自定义对象名
```

## 定时器函数
### 间歇函数
```javascript
setInterval(函数名, 间隔时间 ms)
clearInterval(定时器 id)
```

`setInterval` 参数：
- **函数名**：只写函数名，不加小括号
- **间隔时间**：单位是 ms，第一次是先过间隔时间再执行

返回值是此定时器的 id 号（数字型），用于 `clearInterval` 中关闭定时器。`clearInterval` 可以放在 `setInterval` 执行的函数内，用于控制特定时间后关闭定时器。

```html
<body>
    <button class="btn" disabled>先看看 5</button>
    <script>
        const btn = document.querySelector('.btn')
        let i = 5
        let id = setInterval(function () {
            i--
            btn.innerHTML = `先看看 ${i}`
            if (i === 0) {
                clearInterval(id)
                btn.disabled = false
            }
        }, 1000)
        </script>
</body>
```

## 事件
### 事件监听
```javascript
元素对象.addEventListener('事件类型', 函数名)
```

> [!Tips]
> - 参数中函数可以传入匿名函数，也可以传入函数名（**不加括号**）
> - 无法获取此函数的返回值，如果需要获取某个值，可以在函数内部修改全局变量来实现，或者使用使用回调函数。
> - 相比于使用 on 来添加事件（如下），这一方法可以为同一个元素添加多个事件，而使用 on 来添加，后添加的事件会将前面的时间覆盖。
>     ```javascript
>     元素对象.on事件 = function () {}
>     ```

### 事件类型
参见：[事件参考|MDN](https://developer.mozilla.org/zh-CN/docs/Web/Events)


