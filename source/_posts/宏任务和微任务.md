---
title: 宏任务和微任务
date: 2023-02-08 14:33:00
tags: web
---

# `macrotasks` 宏任务
* UI rendering`<script>`
* I/O 鼠标事件 `mousemove`,`click`
* `setTimeout()`
* `setImmediate()`
* `setInterval()`
* `requestAnimationFrame()`

split the task into pieces.

`there’s the in-browser minimal delay of 4ms for many nested setTimeout calls. Even if we set 0, it’s 4ms (or a bit more)`
在浏览器中，嵌套调用`setTimeout`最小延迟为4ms，即使是`setTimeout(fn,0)`，也是4ms+

# `microtasks` 微任务
* `Promise`,`await`
* `process.nextTick()`
* `queue Microtask()`
* `MutationObserver`

# event loop 执行顺序
1.常规同步调用
2.微任务调用
3.宏任务调用

### 宏任务中：
常规同步-->所有微任务-->下一个宏任务

# examples
注意使用 `setTimeout` 时，第一个参数是函数，调用已定义的函数，无需加`()`
`setTimeout` 调用的必须是函数，`promise.resolve().then()`是表达式
```
function log1(){
  console.log(1);
}
function log2(){
  console.log(2);
}
function log3(){
  console.log(3);
}
function log4(){
  console.log(4);
}
function log5(){
  console.log(5);
}
function log6(){
  console.log(6);
}
function log7(){
  console.log(7);
}
function log8(){
  console.log(8);
}

log1();

setTimeout(log2);

Promise.resolve().then(log3);

Promise.resolve().then(setTimeout(log4));

Promise.resolve().then(log5);

setTimeout(log6);

setTimeout(()=>Promise.resolve().then(log8))

log7();

// 1 7 3 5 2 4 6 8
```

先执行匿名箭头函数，再执行箭头函数里面的内容
宏任务需要执行完内部代码（包含常规同步函数，所有微任务）才能执行下一个宏任务
```
function log1(){
  console.log(1);
}
function log2(){
  console.log(2);
}
function log3(){
  console.log(3);
}
function log4(){
  console.log(4);
}
function log5(){
  console.log(5);
}
function log6(){
  console.log(6);
}
function log7(){
  console.log(7);
}
function log8(){
  console.log(8);
}

log1();

setTimeout(()=>log2());
// 等价： setTimeout(()=>{log2()})
// 等价： setTimeout(function (){log2()})

Promise.resolve().then(()=>log3());

Promise.resolve().then(()=>setTimeout(()=>log4()));
// 等价： Promise.resolve().then(()=>{setTimeout(()=>{log4()})})
// 等价： Promise.resolve().then(function (){setTimeout(function (){log4()})}

Promise.resolve().then(()=>log5());

setTimeout(()=>log6());

setTimeout(()=>Promise.resolve().then(()=>log8()))

log7();

// 1 7 3 5 2 6 8 4
```

`promise` 链中的需要等待回复之后才能执行下一个`then`
在 `promise` 中的宏任务无需等待回复，直接添加到宏任务队列中
```
function logA() {
  console.log('A');
}
function logB() {
  console.log('B');
}
function logC() {
  console.log('C');
}
function logD() {
  console.log('D');
}
function logE() {
  console.log('E');
}
function logF() {
  console.log('F');
}
function logG() {
  console.log('G');
}
function logH() {
  console.log('H');
}
function logI() {
  console.log('I');
}
function logJ() {
  console.log('J');
}

logA();
setTimeout(logG, 0);
Promise.resolve()
  .then(logC)
  .then(setTimeout(logH))
  .then(logD)
  .then(logE)
  .then(logF);
setTimeout(logI);
setTimeout(logJ);
logB();
// A B C D E F G H I J
```

# 参考文献
[宏任务和微任务](https://javascript.info/event-loop)

[在线工具](https://www.jsv9000.app/)

[宏任务和微任务执行](https://medium.com/dkatalis/eventloop-in-nodejs-macrotasks-and-microtasks-164417e619b9)


