---
title: JavaScript 进阶
tags:
  - JavaScript
  - 前端
category: 
---

## 作用域
规定了变量能被访问的范围。

### 局部作用域
#### 函数作用域
函数内部声明的变量只能在内部被访问。

#### 块作用域
被 `{}` 包裹的代码称为代码块，内部声明的变量外部**有可能**无法被访问。

### 全局作用域
最外层声明的变量。

### 作用域链
本质上是底层的变量查找机制。

- 优先查找当前函数作用域中的变量
- 若无，则依次逐级查找父级作用域知道全局作用域

## 垃圾回收机制
Garbage Collection（GC），JS 中内存的分配和回收都是自动完成的，内存在不使用的时候会被垃圾回收器自动回收。

### 内存的生命周期
1. 内存分配
2. 内存使用
3. 内存回收

- 全局变量一般不会回收
- 局部变量一般会自动回收

## 闭包
一个函数对周围状态的引用捆绑在一起，内层函数中访问到其外层函数的作用域。即内层函数+外层函数的变量