---
title: JavaScript 基础
tags:
  - JavaScript
  - 前端
category: 
---

## 基础语法
### 输出
- 语法一：`document.write()`：会将空格中的内容直接写到 `body` 的部分
- 语法二：`alert()`
- 语法三：`console.log()`

### 输入
`prompt()`：弹窗输入，输入值默认为字符串。

### 变量
本质上是在内存中申请的用来存放数据的一部分空间。

#### 基本数据类型和引用数据类型
- **基本数据类型**（简单类型、值类型）：在存储时存储的是值本身，例如字符串、数字等。存储在栈里
- **引用数据类型**（复杂类型）：存储的只是地址，例如使用 `new` 关键字创建的对象。存储在堆里

#### 声明
```javascript
let name = 'bill', age = 18
const pi = 3.1415 //常量
```

`let` 的声明只作用于其所在的块或子块内部，只在声明所在的位置后才能被访问。 `var` 声明的变量的作用域是整个闭合的函数，将在任何代码执行前被创建，即变量提升，但不会被赋值。

> [!Hint]
> - 能用 `const` 的情况尽量用 `const`，由于[[#基本数据类型和引用数据类型|复杂数据类型]]实际存储的是地址，若修改时存储的地址不变动，因此会改变的复杂数据类型也可以使用 `const` 声明。
> - `let` 不允许多次声明，而 `var` 可以。

#### 模板字符串
```javascript
let gender = 'male'
let age = 18
document.write(`性别：${gender}，年龄：${age}`)
```
- 字符串整体使用反引号 （`） 包裹 
- 反引号内可以保留换行符
- 变量名写在花括弧内 `${variable}`

#### 字符串类型转换
##### 隐式转换 
某些运算符执行时自动进行的类型转换 
- `+` 两侧只要存在字符串，则都会被转换为字符串。但是作为正号解析会将字符串转换为数字 `+'123'`
- 其余运算符（`- * 、/ %`）会将数据转换为数字
- `==` 比较时会将字符串转换为数字，而 `===` 不会转换，会同时比较类型和值
- `null` 数字转换后为 `0`，`undefined` 则为 `NaN`

##### 显式转换
- 转换为数字：
    - `Number()`
    - `parseInt()`：取字符串起始部分的所有数字，忽略其他字符，只取整数
    - `parseFloat()`：与 Int 相同，但可以保留小数

### 语句
#### 逻辑运算符
##### 布尔值（boolean）
即真（`true`）、假（`false`）

```javascript
Boolean() // 转换为布尔值 （true 或 false）
```

> [!hint]
> -  `0 == false` 为真；`0 === false` 为假。`''` 同，且 `0 == ''` 为真
> -  `''`、`0`、`undefined`、`null`、`false`、`NaN` 转换为布尔值之后都为 `false`，其余为 `true`

##### 逻辑中断
`&&` 和 `||` 满足一定条件后，会使右侧的运算不再执行
- `&&`：左侧为 `false` 则右侧不再执行；若均为 `true`，则返回右侧的值
- `||`：左侧为 `true` 则右侧不再执行；若均为 `true`，则返回左侧的值
- 
```javascript
console.log(11 && 22)       // 22
console.log(11 || 22)       // 11
console.log(11 && 22 || 33) // 22
```

例如函数：

```javascript
function fn (x, y) {
    x = x || 0
    y = y || 0
    retrun x + y
}
```

此函数中，若调用时没有传入参数，`x` `y` 会被视为 `undefined`，则会在第一步处理中由逻辑中断被赋为 `0`，相当于设置了默认值。

#### 三元运算符
```javascript
// 条件 ? 满足时执行的代码 : 不满足时执行的代码 
a > b ? a : b 
```

### 数组

#### 新增值
`push` 方法将一个或多个元素添加到数组的末尾，并返回新数组的长度
```javascript
let arr = [1, 2]
arr.push(7, 8, 9)
console.log(arr) // Array(5) [ 1, 2, 7, 8, 9 ]
```

`unshift` 方法将一个或多个元素添加到数组的开头，并返回新数组的长度
```javascript
let arr = [1, 2]
arr.unshift(7, 8, 9) 
console.log(arr) // Array(5) [ 7, 8, 9, 1, 2 ]
```

#### 删除值
- `pop` 方法从数组中删除最后一个值，并返回删除的元素
- `shift` 方法从数组中删除第一个值，并返回删除的元素
- 两者均不带参数
```javascript
let arr = [1, 2, 3, 4, 5]
arr.pop()
console.log(arr)  // Array(4) [ 1, 2, 3, 4 ]
arr.shift()
console.log(arr) // Array(3) [ 2, 3, 4 ]
```

`splice` 方法删除指定元素
```javascript
arr.splice(start, [deletCount])
```
`start`：起始位置（索引号） 
`deleteCount`：删除的数量，默认为到最后

#### 冒泡排序
```javascript
let arr = [4, 5, 1, 3, 2]
for (let i = 0; i < arr.length - 1; i++) {
    for (let j = 0; j < arr.length - i -1; j++) {
        if (arr[j] < arr[j + 1]) {
            let tmp = arr[j]
            arr[j] = arr[j + 1]
            arr[j + 1] = tmp
        }
    }
}
console.log(arr) // Array(5) [ 5, 4, 3, 2, 1 ]
```

`sort` 方法用来排序，默认排序是将元素转换为字符串，然后按照它们的 UTF-16 码元值升序排序。可以通过传入一个定义排序顺序的函数，其返回值应该是一个数字，其正负性表示两个元素的相对顺序。
```javascript
// sort 升序排列
arr.sort(function (a, b) {
    return a - b
})
// sort() 降序
arr.sort(function (a, b) {
    return b - a
})
```

#### `map()` 方法
创建一个新数组，这个新数组由原数组中的每个元素都调用一次提供的函数后的返回值组成。也称为映射。

```JavaScript
arr.map(callbackFn, [thisArg])
```

-  `callbackFn`：执行的函数。它的返回值作为一个元素被添加到新数组中。该函数被调用时将依次传入以下参数：
    - `element`：数组中当前正在处理的元素。
    - `index`：正在处理的元素在数组中的索引。
    - `array`：当前调用的数组自身。
- `thisArg`：执行 `callbackFn` 时用作 `this` 的值。

#### `join()` 方法
把数组中所有元素转换为一个**字符串**。

```JavaScript
arr.join('') // 传入参数是不同元素间的分隔符，空字符串则无间隔。默认为逗号
```

### 函数 
```javascript
// 定义函数
function 函数名(参数列表) {  // 形参，可以赋默认值
    函数体
}
// 调用函数
函数名(参数列表) // 实参
```

> [!hint]
> - 若形参不定义默认值，实参不传入值，则均默认为 `undefined`
> - `return` 会结束函数，其之后的行不会运行

#### 变量作用域
- 若在函数内部用 `let` 声明变量，则是局部变量 
- 若在函数内部不定义直接赋值的变量为全局变量，但不推荐

#### 匿名函数 
与具名函数相对，指没有名字的函数，无法直接使用

##### 函数表达式
```javascript
let fn = function (x, y, ...) {
    // 函数体
}

fn (x, y, ...) // 调用
```

将函数赋值给变量，通过变量名加括弧进行调用；函数表达式只能在声明之后调用

##### 立即执行函数 
可以避免来自全局变量的污染，例如调用外部 js 文件，其文件内的函数使用立即执行函数，可以防止调用时的全局变量影响内部函数。

写法一
```javascript
(function (x, y, ...) {          // 形参
    // 函数体
}) (x, y, ...)                   // 实参

res = (function(num1, num2) {
    return num1 + num2 
}) (1, 2)
console.log(res)  // 3
```

写法二
```javascript
(function (x, y, ...) {} ())     // 内部第一个圆括弧为形参，第二个圆括弧为实参
```

> [!hint]
> 注意若是以括号开头某行，则应考虑添加 `;` (本行首或上行尾)

### 对象（Object）
一种数据类型，是一种无序的数据集合

#### 声明
```javascript
let obj = {} 
let obj = new Object()  // 两种均可
```

#### 属性与方法 
对象由属性与方法组成，属性名可以使用 `""` 或 `''` 包裹，一般可以省略

```javascript
let 对象名 = {
    属性名：属性值,
    方法名：function () {} // 匿名函数
}
```

#### 操作
```javascript
let obj = {
    uname: 'Alex',
    gender: 'Male',
    age: 18,
    fn: function () { console.log('666') }
}

console.log(obj.uname) // Alex
console.log(obj['uname']) // 作用与上方相同，但是这样可以查询带属性名有''的属性

obj.age = 20
console.log(obj.age) // 20

obj.tel = '123456'
console.log(obj) // { uname: "Alex", gender: "Male", age: 20, tel: "123456" }

delete obj.gender
console.log(obj) // { uname: "Alex", age: 20, tel: "123456" }

obj.fn() // 666
```

> [!hint]
> `obj['uname']` 方括弧中的属性名必须有引号包裹，如果不使用引号包裹则会被视为变量传入
> ```javascript
> let obj = { uname: 'Alex', gender: 'Male' }
> console.log(obj[uname]) // 报错
> let n = 'uname'
> console.log(obj[n]) // Alex
> ```

#### 遍历对象
```javascript
for (let k in obj) {
    console.log(k)  // 输出属性名字符串
    console.log(obj[k]) // 输出所有属性值
}
```

#### 内置对象
内部提供的对象，可以直接调用

##### `Math` 对象
[Math - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)

#### 对象的存储方式
对象是引用数据类型，其实际存储在堆里，只在栈里存储指向堆的地址，因此直接向另一个变量赋值，实际上也是赋这个地址。

```javascript
let obj1 = { uname : 'Alex'}
let obj2 = obj1
obj2.uname = 'Bill'
console.log(obj1) // Bill
```

上方代码中，第二行的赋值操作实际上是让 `obj2` 指向了 `obj1` 的地址，因此对 `obj2` 的属性进行操作，实际上也是对 `obj1` 进行操作。

#### 实例化
使用 `new` 关键字

##### 时间对象
实例化一个[时间对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date)
```JavaScript
// 当前时间
const date = new Date()
// 指定事件
const date1 = new Date('2023-12-12 08:30:00')
```

时间对象存储的是以 1970 年 1 月 1 日 00 时 00 分 00 秒开始后过去事件的毫秒数。两个事件戳相减的差即是两个时间点之间间隔的毫秒数。

获取时间戳
```JavaScript
// 1. getTime() 方法
const date = new Date()
console.log(date.getTime())
// 2. +new Date()
console.log(+new Date())
// 3. Date.now() 方法，只能得到当前的
console.log(Date.now())
```

## JS 执行机制
**单线程**，即同一时间只能做一件事。

### 同步
前一个任务结束后再执行后一个任务，程序执行的顺序与任务的排列顺序是一致的、同步的

#### 同步任务
所有任务都在主线程上执行，形成一个**执行栈**。

### 异步
#### 异步任务
耗时的任务一般为异步任务，JS 的异步由回调函数来执行。异步任务被添加到**任务队列**（也称为消息队列）中。

### 执行机制
1. 先执行执行栈中的同步任务。
2. 异步任务放入任务队列中。
3. 执行栈中的所有同步任务执行完毕，系统按次序读取**任务队列**中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈开始执行。

## 正则
JavaScript 中正则表达式是对象。

### 语法
```JavaScript
const regObj = /表达式/  // 定义一个正则表达式对象，不加引号
regObj.test(被检查的字符串)  // 返回布尔值
regObj.exec(被检查的字符串)  // 返回一个数组或 null
被替换的字符串.replace(regObj, '替换的文本')  // 替换
```

### 元字符
具有特殊含义的字符。

#### 边界符
提示字符所处的位置

- `^`：行首（以谁开始）
- `$`：行尾（以谁结束）
```JavaScript
const reg = /^a$/  // 同时出现则表示只能由表达式规定的情况对应的字符构成
```

#### 量词
某个模式出现的次数，默认匹配为只匹配**一次**

- `*`：重复**零次**或更多次（重复零次：可以不出现）
- `+`：重复**一次**或更多次
- `?`：重复零次或一次
- `{n}`：重复 n 次
- `{n,}`：重复 n 次或更多次（>=n）
- `{n,m}`：重复 n 到 m 次（均取等）

逗号两侧不能出现空格。

#### 字符类
- `[]`：匹配字符集合，只要包含其中**任意一个字符**，返回 `true`
    - `-`：表示一个范围：`[a-zA-Z]` 不分大小写地表示字母
    - `^`：取反
- `.`：除换行符以外的任何单个字符
- 预定义字符
    - `\d`：相当于 `[0-9]`
    - `\D`：相当于 `[^0-9]`
    - `\w`：相当于 `[A-Za-z0-9_]`
    - `\W`：相当于 `[^A-Za-z0-9]`
    - `\s`：匹配空格，相当于 `[\t\r\n\v\f]`
    - `\S`：匹配非空格，相当于 `[^\t\r\n\v\f]`

#### 修饰符
约束正则执行的某些细节行为，放在表达式后方（`/` 后）

- `i`：不区分大小写（ignore）
- `g`：匹配所有满足表达式的结果（global）


