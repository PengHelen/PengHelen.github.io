---
title: reduce用法集锦
date: 2023-02-24 10:08:00
tags: JS
---

# `reduce`求和，参数含义

```
const arr = [1, 2, 3, 4, 5]
let previousValue = 0
const sum = arr.reduce(function(init, item, index, arr){
  console.log('params', init, item, index, arr,previousValue)
  return init + item;
}, previousValue);

// 简化2
const sum2 = arr.reduce((init, item, index, arr)=>{
  console.log('params', init, item, index, arr,previousValue)
  return init + item;
}, previousValue);

// 求和-简化3
const sum3 = arr.reduce((init, item, index, arr)=>init + item);
console.log('arr:', arr, 'sum:2', sum)
```
以上，`init`表示当前循环的初始值，`item`当前元素，`index`当前下标，`arr`原数组（reduce的数组）
`previousValue`第一次循环开始的初始值
若无初始值，第一次循环开始取第一个元素

# 统计元素出现次数
使用对象key唯一性统计，第一次循环初始值为 `{}` 
```
let names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice', 'Bob', 'Bob']
let countNames = names.reduce((allNames, item) => {
  console.log('namessssss', allNames, item)
  if (item in allNames) {
  allNames[item]++
  } else {
    allNames[item] = 1
  }
  return allNames;
}, {})
console.log('countnamed', countNames)
```

# 数组去重
数组 `indexOf()` 方法查找元素是否在初始数组中，存在忽略，不存在，追加在初始数组中
第一次初始值为 `[]`

```
let names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice', 'Bob', 'Bob']
let onlyOne = names.reduce((allNames, item) => {
  if (allNames.indexOf(item) === -1) {// 可考虑inclues
  allNames.push(item)
  }
  return allNames;
}, [])
console.log('onlyOne', onlyOne)
```

# 对象数组按属性分类

```
 const objArr = [
  {title: 'aa',num: 12}, 
  {title: 'bb',num: 32}, 
  {title: 'cc', num: 41}, 
  {title: 'aa', num: 5}, 
  {title: 'cc',num: 0}
]
// 同title放一组
let groups = objArr.reduce((init, item) => {
  let key = item.title
  console.log('key', item, key)
  if (!init[key]) {
    init[key] = []
  }
  init[key].push(item)
  return init;
}, {})
console.log('groups', groups)
```
一定要返回`init`，否则无法进行下一次循环
当`init[key]`不存在时，需要初始化当前`key`下标的数组即`[]`
当前`init[key]`初始化之后，当前元素应加入当前数组

# 对象数组按属性求和

```
// 使用以上objArr的num属性
let objSum = objArr.reduce((init, item) => init + item.num, 0)
console.log('objSum', objSum)
```

# 多维数组偏平化（转化为一维数组）
```
const multiArr = [[0, 1], 0, 1, , 2, [2, 4], [3, 90, 8, [30, 29, 1, [7, 4, 5]]]]
const arr = function (tempArr) {
  return tempArr.reduce(function (init, item, index) {
    return init.concat(Array.isArray(item) ? arr(item) : item)
  },[])
}
console.log('arr', arr(multiArr))
// 简化
const arr2 = (tempArr) => tempArr.reduce((init, item) => init.concat(Array.isArray(item) ? arr(item) : item), [])
console.log('arrr2', arr2(multiArr))
```

### 当前使用知识点
* （匿名）函数表达式
* 箭头函数
* 数组判定方
* 递归
* reduce()

### 注意事项
* 函数表达式，调用时需加括号，无论是否需要参数
* 函数作用域在函数内，函数运行结束后，函数内变量销毁（普通函数，不讨论闭包），注此例中 `init` 的变化
* 箭头函数，有 `{}` （多条语句）需要手动加 `return` 语句；无 `{}` （只有一条语句），则返回当前语句运算结果
* 递归是反复调用同一个方法，直到满足出口条件（此例出口是 `item` 不是数组）
*  `reduce` 的第一次循环初始值，简洁示意 `reduce(() => code, firstInit)` 
*  `reduce` 的返回值是下一次循环的初始值，最后一个返回值（即循环结束，退出循环）是 `reduce` 的数组最终返回值

# 求数组最大/小值

```
const arr = [0, -1, 0, 1, , 2, 2, 4, 3, 90, 8, 30, 29, 1, 7, 4, 5]
var max = arr.reduce((init, item) => Math.max(init, item));
console.log('max', max)
var max2 = arr.reduce((init, item) => init > item ? init : item)
console.log('max2', max2)
```
最小值，同理，使用 `Math.min()`

# 其他
### 数组转对象
### 数组转数组-数组中每个元素的平方（map()）
### 数组转字符串（split()）

# 参考文献
[CSDN博客](https://blog.csdn.net/qq_38970408/article/details/121018660)

[博客园](https://www.cnblogs.com/amujoe/p/11376940.html)

[MDN reduce](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)






