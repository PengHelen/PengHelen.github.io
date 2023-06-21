---
title: for...in和for...of区别
date: 2023-02-24 13:46:30
tags: JS
---

# `for...in`
> for ... in是为遍历对象属性而构建的，不建议与数组一起使用

* Array,String,Object均可用

# `for...of`
> `for...of`语句在可迭代对象上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句

### 可用范围
* Array
* String
* arguments
* Map
* Set
* TypedArray

### `for...of` 对象不可用，会报错 `obj is not iterable`

# 区别
迭代方式不同

`for...in` 以任意顺序迭代对象的可枚举属性

迭代的是**下标**

`for...of` 遍历可迭代对象定义要迭代的数据

迭代的是**元素**


# 参考文献
[MDN for...in](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in)

[MDN for...of](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...of)

