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
浏览器根据 HTML 标签生成的 **[[JavaScript#对象（Object）|JS 对象]]**，与所有标签对应。`document` 是最大的对象，网页的所有内容都在其中。

## 获取 DOM 元素
### 利用 CSS 选择器

1. 选择匹配的第一个元素
```javascript
document.querySelector('css选择器')
```

- **参数**：包含一个或多个有效的 CSS 选择器的字符串。
- **返回值**：匹配的**第一个元素**，一个 `HTMLElement` 对象。
- 获取后可以直接对[[JavaScript#属性与方法|属性]]做修改。

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

此操作会将原有的 `class` 替换掉

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

### 元素的尺寸与位置
#### 尺寸
元素的宽度与高度。

##### `client` 家族
- `clientWidth`：元素内部的宽度
- `clientHeight`：元素内部的高度

包括内边距（`padding`），但**不包括**边框（`border`）、外边距（`margin`）和滚动条（如果存在）。

##### `offset` 家族
- `offsetWidth`
- `offsetHeight`

**包含**元素的边框（`border`）、水平线上的内边距（`padding`）、滚动条（`scrollbar`）（如果存在）以及 CSS 设置的宽度（`width`）的值。

#### 位置
##### `offset` 家族
- `offsetLeft`
- `offsetTop
获取自己相对于最近一级带有**定位**的祖先元素的左、上距离（只读）。

##### 获取相对于视口的位置
`Element.getBoundingClientRect()` 方法返回一个 [`DOMRect`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMRect) 对象，其提供了元素的大小及其相对于[视口](https://developer.mozilla.org/zh-CN/docs/Glossary/Viewport)（Viewport）的位置。

```JavaScript
element.getBoundingClientRect()
```

##### 整个页面滚动距离
通过获取 `html` 标签的滚动距离（`scrollTop`）来实现。

```JavaScript
window.addEventListener('scroll', function () {
    console.log(document.documentElement.scrollTop)
})
```

获取页面的 `html` 标签：
```JavaScript
document.documentElement
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

#### 常见事件
##### 鼠标事件
- `click`：点击
- `mouseenter`：经过（无[[#事件冒泡|冒泡]]效果，推荐）
- `mouseleave`：离开（无冒泡效果，推荐）
- `mouseover`：经过（有冒泡效果）
- `mouseout`：离开（有冒泡效果）

##### 表单焦点事件
- `focus`：（输入框光标）获得焦点
- `blur`：（输入框光标）失去焦点

##### 键盘与输入事件
- `keydown`：按下
- `keyup`：抬起
- `input`：文本框内有输入

#### 进阶事件
##### 页面加载事件
###### `load`
加载外部资源（图片、外联 CSS 与 JavaScript）结束时触发。

如果直接将 JavaScript 代码写在 `head` 中，执行时不会获取到下方 `<body>` 内的代码，因此无法正常执行。使用如下的代码在页面内有资源加载完毕后执行回调函数，则执行可以在 `<head>` 中的 JavaScript 代码。
```javascript
window.addEventListener('load', function () {})
```

也可以用于监听某个特定的资源（如图片）加载完毕。

###### `DOMContentLoaded`
初始的 HTML 文档被完全加载和解析完成之后被触发，是 `document` 的事件。

##### 页面滚动事件
滚动条在滚动的时候持续触发的事件 `scroll`。

```JavaScript
window.addEventListener('scroll', function () {}) //  监听整个页面的滚动
div.addEventListener('scroll', function () {}) //  监听 div 这个元素内的滚动
```


属性：
- `scrollLeft`：向**左侧**卷去的不可见部分的大小
- `scrollTop`：向**上方**卷去的不可见部分的大小

两者均是可读写的属性，可以写入值控制页面滚动的位置，也可使用 `scrollto` 的方法

```JavaScript
window.scrollTo(x, y)
```

##### 页面尺寸事件
窗口尺寸改变的时候触发的事件 `resize`。

```JavaScript
window.addEventListener('resize', function () {})
```

### 相关对象与参数
#### 事件对象
存有事件触发时相关信息的对象，在事件触发的函数里的第一个参数即是事件对象，一般用 `event`、`e` 等命名。详见 [Event | MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Event#%E5%9F%BA%E4%BA%8E_event_%E7%9A%84%E6%8E%A5%E5%8F%A3)。
```javascript
<body>
    <button class="btn">先看看</button>
    <script>
        const btn = document.querySelector('button')
        btn.addEventListener('click', function (e) {
            console.log(e)
        })
        // 或者
        function fn (e) {
            console.log(e)
        }
        btn.addEventListener('click', fn)
        </script>
</body>
```

#### 环境对象
即函数内部的特殊变量 `this`，指当前函数运行时所处的环境。

```html
<body>
    <button class="btn">先看看</button>
    <script>
        const btn = document.querySelector('.btn')
        btn.addEventListener('click', function () {
            console.log(this)
            console.log(this === btn)
        })
    </script>
</body>
```

单击按钮后，在控制台输出：
```javascript
<button class="btn">
true
```

可以看出此函数中的 `this` 即是 `btn`（谁调用即是谁（粗略规则））。

#### 回调函数
将一个函数作为**参数**来传递到另一个函数时，被**作为参数**的函数即是回调函数。

### 事件流
事件完整执行过程中的流动路径。

- 捕获：由父到子
- 冒泡：由子到父

#### 事件捕获
从 DOM 的根元素开始去执行对应的事件（由外到里）
```javascript
DOM.addEventListener(事件类型, 触发函数, 是否使用捕获机制)
```

**是否使用捕获机制**：传入 `true` 代表捕获阶段触发，默认为 `false` （即冒泡）。

#### 事件冒泡
当一个元素的事件被触发时，同样的事件会在该元素的所有祖先元素中依次被触发。即当一个元素触发事件后，会依次向上调用所有父级元素的**同名事件**（同一事件类型）。

事件冒泡是默认存在的，有的事件（[[#鼠标事件]]）没有冒泡效果，其余的可以通过方法设定。

##### 阻止冒泡
是[[#事件对象]]的一个方法，可以阻止事件流动传播，包括冒泡和捕获阶段。放置在事件触发的函数内部。

```javascript
事件对象.stopPropagation()
```

#### 解绑事件
1. 使用 `on事件` 绑定的事件（L0 事件），直接使用 `null` 覆盖。
```javascript
// 绑定
btn.onclick = function () {
    alert('啊对对对')

}
// 解绑
btn.onclick = null
```

2. `addEventListener` 绑定的事件（L2 事件），使用 `removeEventListener` 方法，匿名函数无法解绑。

```javascript
DOM.removeEventListener(事件类型, 触发函数[, 获取捕获或者冒泡阶段])
```

#### 事件委托
利用事件流的特征来解决一些开发需求的技巧，实际是利用[[#事件冒泡]]的特点，将子元素的事件委托给父元素，触发子元素后会冒泡到父元素触发事件。能减少注册次数，提高程序性能。

通过事件对象的 `target` 属性可以获得真正触发事件的对象。

```javascript
<body>
    <ul>
        <li id="li1">1</li>
        <li id="li2">2</li>
    </ul>
    <script>
        const ul = document.querySelector('ul')
        ul.addEventListener('click', function (e) {
            console.log(this) //  <ul> 此处 this 指向的是注册事件的元素
            console.log(e.target) //  <li id="li1">1</li>
            console.log(e.target.tagName) //  LI  同样的方法可获取标签的属性
        })
        const li1 = document.querySelector('#li1')
        li1.addEventListener('click', function () {
            console.log(this) // 与上方只注册父级元素的事件一致
        })
    </script>
```

#### 阻止默认行为
与[[#阻止冒泡]]类似，是事件对象的一个方法，放置于事件触发的函数内。
```javascript
e.preventDefault()
```

如
```html
<body>
    <a href="https://files.billw.cn">点击跳转</a>
    <script>
        const a = document.querySelector('a')
        a.addEventListener('click', function (e) {
            e.preventDefault()
        })
    </script>
</body>
```

`button` 按钮单击后默认会进行页面跳转，但由于单击后触发的函数内阻止了这一行为，所以点击后不会跳转。

### 移动端事件
#### 触屏事件 `touch`
- `touchstart`：手指触摸到一个 DOM 元素
- `touchmove`：在一个 DOM 元素上滑动
- `touchend`：从一个 DOM 元素上移开


## 节点
DOM 树内的每一个内容都被称为节点。

### 节点类型
- **元素节点**
    - 所有的标签都是节点，`html` 是根节点
- 属性节点
    - 所有的属性
- 文本节点
    - 所有的文本
- 其他

### 查找节点
#### 父节点
标签对象的 `parentNode` 属性，返回最近一级的父节点，若无则返回 `null`。

#### 子节点
- `childNodes`：获得所有子节点，包括文本节点、注释节点等。
- `children`：仅获得所有**元素节点**（标签），返回一个伪数组。

#### 兄弟节点
- `nextElementSibling`：下一个兄弟节点
- `previousElementSibling`：上一个兄弟节点

#### 增加节点
##### 创建节点
```JavaScript
document.createElement('标签名')
```

##### 追加节点
- 作为最后一个子元素插入到某个父元素
```JavaScript
父元素.appendChild(要插入的元素)
```

- 插入到父元素的某个子元素前面
```JavaScript
父元素.insertBefore(要插入的元素, 在哪个元素前面)
```

第二个参数可以为 `undefined`。

#### 克隆节点
```JavaScript
元素.cloneNode(布尔值)
```

若为 `true`，则表明后代节点会一同克隆（深克隆），若为 `false` 则不会，只克隆标签（不克隆文本等，浅克隆）。默认为 `false`。

#### 删除节点
```JavaScript
父元素.removeChild(要删除的元素)
```

## BOM
浏览器对象模型，`window` 对象是全局对象，也可以说是 JavaScript 中的顶级对象。大部分情况下 `window` 可以省略。

### 延时函数
```JavaScript
setTimeout(回调函数, 等待的毫秒数)
```

只执行一次，相当于延迟一段时间后执行。返回一个独特的定时器的编号，可以传递给 [`clearTimeout()`](https://developer.mozilla.org/zh-CN/docs/Web/API/clearTimeout "clearTimeout()") 来取消该定时器。

### `location` 对象
拆分并保存了 URL 的各个部分的对象。

#### 属性与方法
- `href` 属性：当前页面的地址，可以用于赋值来跳转页面。
- `search` 属性：返回地址中的参数（`?` 后的部分）。
- `hash` 属性：返回地址中的哈希（`#` 后的部分）
- `reload()` 方法：刷新当前页面，传入 `true` 强制刷新。

### `navigator` 对象
记录了浏览器的相关信息，如 `UA`。

### `history` 对象

- `back()`：后退
- `forward()`：前进
- `go()`：前进或后退几个页面，`1` 前进一个页面，`-1` 后退一个页面

### 本地存储
数据存储在用户浏览器中，容量较大。

#### 分类
##### `localStorage`
永久性地存储在本地，除非手动删除，否则会一直存在。

- 可以多页面（同一域）共享。
- 只存储**字符串**，输入数字也会被转换。

```javascript
localStorage.setItem('key', 'value')  // 存储、修改
localStorage.getItem('key')  // 获取
localStorage.removeItem('key')  // 删除
```

#### `sessionStorage`
关闭浏览器窗口即消失，其他方法与 `localStorage` 一致。

#### 存储复杂数据
本地存储只能储存字符串，复杂数据类型必须先转换为 JSON 字符串。

```JavaScript
// 转换为 JSON 字符串
JSON.stringify()
let obj = {a: 'aa', b: 'b'}
console.log(JSON.stringify(obj))  // '{"a":"aa","b":"bb"}'
// 转换回对象
JSON.parse()
```
