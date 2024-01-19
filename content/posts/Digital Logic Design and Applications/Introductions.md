---
title: 绪论 - 数字逻辑设计
tags:
  - 数字逻辑设计
category: 
---

## 数字设计与数字系统
数字设计（Digital Design）又称逻辑设计（Logic Design），其目标是构建系统，是一门工程，意味着解决问题，绝大部分是常规的设计方法。

数字系统的优越性：
- 结果再现性（Reproducibility），稳定可靠，精度更高
- 易于设计，灵活性（Flexibility）更高，功能性（Functionality）更强
- 具有可编程性（Programmability），使用 HDL（硬件描述语言）

## 数字器件
### 组合电路与时序电路
- 组合逻辑电路：当前输出只与当前输入有关
- 时序逻辑电路：还与过去的输入（即电路状态有关）

### 门电路
最基本的组合电路器件：与门（AND Gates），或门（OR Gates），非门（NOT Gates），反相器（Inverters）

### 存储电路
最基本的时序电路器件：存储器（Latches）和触发器（Flip-Flops）

### 专用集成电路 ASIC
是为一个特殊的、受限制要求的产品或应用而设计的芯片，也称为半定制集成电路

## 数字设计层次
- 物理级层次：器件物理层（Device Physics Level）和 IC 制造过程（IC Manufacturing Process Level）
- **晶体管级（Transistor Level）**
- **门电路结构级（Gates Structure Level）**
- **逻辑设计级（Logic Design Level）**
- 整体系统设计（Overall System Design）

