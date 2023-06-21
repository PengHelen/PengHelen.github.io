---
title: import与export
date: 2021-12-27 10:42:07
tags: JS
---

## 一、import

#### 静态 import

初始化加载依赖项的最优选择，在加载时就被编译
导入的模块运行在严格模式下
在浏览器中，import 语句只能在声明了 type="module" 的 script 的标签中使用

```
import xxx from 'ppp'
import * as xxx from 'ppp'
import {xxx,yyy} from 'ppp'
import {xxx as aaa,yyy as bbb} from 'ppp'
import 'ppp';//整个模块仅为副作，运行模块中的全局代码, 但实际上不导入任何值
```

#### 动态 import

按需加载模块
不依赖 type="module" 的 script 标签
关键字 import 可以像调用函数一样来动态的导入模块。以这种方式调用，将返回一个 promise，也支持 await 关键字

## 二、export

导出的模块处于严格模式

#### 命名导出（每个模块包含任意数量）

```
export {myFunction,myVariable}
```

#### 默认导出（每个模块包含一个）

```
export let name1,name2,...,nameN;//var const均适用
export let name1=...,name2=...,...,nameN=...;//var const均适用
export function functionName(){...};
export class className{...}
```
