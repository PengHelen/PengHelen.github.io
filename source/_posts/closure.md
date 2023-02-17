---
layout:
  - layout
title: closure
date: 2023-02-07 15:40:01
tags: JS
---

# 特征
* 外部函数不存在，闭包仍然可以访问外部函数的变量
* 闭包不能访问其外部函数的args形参???

# 优点
* 允许将变量添加到执行上下文
* 闭包中可存储外部函数变量，方便以后使用
* 可以数据封装
* 可用于维护模块代码

# 缺点
* 闭包中的变量不会被垃圾回收
* 太多的闭包会降低网页运行效率，实际是由于内存中的代码重复造成

# 手动回收闭包中的变量
```
function test() {
  var count = 0;
  return function() {
    count++;
  };
}
var x = test();
x = "";
// 或以下写法
function foo () {
  var x = test();
  x();
}
foo();
```
