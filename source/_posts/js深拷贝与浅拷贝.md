---
title: js深拷贝与浅拷贝
date: 2021-12-30 16:05:39
tags: work
---

## 一、概念

深拷贝：两个对象经过拷贝后，除了拷贝下来相同的属性之外，没有任何其他关联的两个对象
浅拷贝：两个对象经过拷贝后，虽然属性相同，也是不同对象，但内部的对象指向同一个内存空间

## 二、实现方式

#### JSON 方法

`let newObj = JSON.parse(JSON.stringify(oldObj))`
缺点：无法拷贝对象里的函数、原型链的属性

#### 循环递归

```
function deepCopy(source){
  let target = Array.isArray(source)?[]:{}
  for(let k in source){
    if(typeof source[k] ==== 'object'){
      target[k]=deepCopy(source[k])
    }else{
      target[k] = source[k]
    }
  }
  return target;
}
```
