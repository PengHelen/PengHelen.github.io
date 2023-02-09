---
layout:
  - layout
title: Promise
date: 2023-01-31 10:02:41
tags:
---

# 状态
* pending 初始状态，未成功也未拒绝
* fulfilled 操作成功完成
* rejected 操作失败

# 链式调用
链式调用中的第一个 `promise` 是嵌套最深的一个，也将是第一个被弹出的
```
const myPromise = new Promise((resolve,reject)=>{
  setTimeout(()=>{
    resolve('foo');
  },500)
});
myPromise
  .then()
  .then()
  .then()
  .catch()
  .finally()
```

# 构造函数
`Promise()`

# 静态方法
* Promise.all(iterable)
* Promise.allSettled(iterable)
* Promise.any(iterable)
* Promise.race(iterable)
* Promise.reject(reason)
* Promise.resolve(value)

# 实例方法
* Promise.prototype.catch()
* Promise.prototype.then()
* Promise.prototype.finally()

# `Promise.all()` VS `Promise.allSettled()`
* Promise.all()：所有promise都成功则返回所有成功的结果；数组中出现一个rejected，返回出现rejected的promise

* Promise.allSettled()：结果允许resolved和rejected两种状态，因此返回的都是敲定结果之后的状态，返回的是由多个 `{status:'fulfilled'/'reject',value:''}` 组成的数组

```
const promise1 = Promise.resolve(31);
const promise2 = Promise.reject('23');
//(1) const promise2 = 23
const promise3 = new Promise(resolve=>setTimeout(()=>resolve(2023),50));
let allPromise = [promise1,promise2,promise3];

Promise.all(allPromise).then(res=>console.log(res))
// Promise {<rejected>: '23'}
// [[Prototype]]: Promise
// [[PromiseState]]: "rejected"
// [[PromiseResult]]: "23"
//(1) [31,23,2023] 

Promise.allSettled(allPromise).then(res=>console.log(res))
// [
//   {status: 'fulfilled', value: 31},
//   {status: 'rejected', reason: '23'},
//   {status: 'fulfilled', value: 2023},
// ]
// (1) 将以上数组中第二个元素的status修改成'fulfilled'即可

```

# `async/await` (ES2017)
异步Promise的同步写法

`async`关键字可定义一个异步函数
```
async function sayHi(){
  return 'Hi';
}
// 等同于
async function sayHi(){
  return Promise.resolve('Hi')
}
```

`await` 关键字等待一个promise敲定状态，resolved和rejected；仅能放在async声明的函数中，否则报错
```
async function display(){
  let result = await sayHi();
  console.log(result);
}
```

### 错误处理：try...catch
```
async function getUser(userId) {
    try {
       const user = await Promise.reject(new Error('Invalid User Id'));
    } catch(error) {
       console.log(error);
    }
}
```

### `promise` 与 `async/await` 区别
* `async/awai`t 是`promise`处理异步事件的同步写法，一种语法糖
* `promise` 有三种状态；`async/await` 没有状态，无论resolved还是rejected军返回一个promise
* `promise` 的错误处理可使用`.then()`和`.catch()`；async/await使用`try...catch`
* `promise`链式调用太长时会臃肿难理解，`async/await`简洁、易读
* `promise`链是异步的；`async/await`整个函数作用域都是异步的
* 多个promise时，可使用`Promise.all()`；`async/await`拆分成多个变量


# 参考文献
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise

https://dev.to/viclafouch/promise-allsettled-vs-promise-all-in-javascript-4mle

https://www.javascripttutorial.net/es-next/javascript-async-await/

https://www.geeksforgeeks.org/difference-between-promise-and-async-await-in-node-js/

https://levelup.gitconnected.com/async-await-vs-promises-4fe98d11038f

