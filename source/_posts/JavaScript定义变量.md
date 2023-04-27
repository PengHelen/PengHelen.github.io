---
title: JavaScript定义变量
date: 2021-12-23 14:22:39
tags: JS
---

## 一、声明变量

**1.** 优先执行：在执行任何代码之前进行处理
**2.** 不可配置性：声明变量所在上下文环境的不可配置属性，非声明变量是可配置的
**3.** 作用域在当前执行上下文：作用域限制函数内或全局作用域

**注：** 建议先声明变量再使用，在 ES5 严格模式下，分配值给未声明变量将引发错误

---

声明变量的方法：
ES5：var 和 function
ES6：var、function、let、const、import、class

---

#### 优先执行

**变量提升：** 变量在任意代码执行之前处理，意味着变量可以在声明之前使用，这种行为叫做“hosting”
始终在作用域顶部声明变量（全局/函数代码的顶部）
变量提升影响变量声明，不影响其值的初始化

#### 不可配置性

```
var a=1;
b=2;
delete this.a;//在严格模式下抛出typeError，其他情况下执行失败，但无提示
delete this.b;
console.info(a,b);//抛出refrenceerror（引用错误，b已被删除）
```

#### 声明多个变量

**隐式声明全局变量**
在非严格模式下，直接赋值给未声明的变量中，则执行赋值后，该变量会被隐式地创建为全局变量（它将成为全局对象的属性）

```
var a=b='A';
//等效于
b='A';
var a='A';
//连等操作是从右向左执行的，相当于b = 'A'、let a = b，很明显b没有声明就直接赋值了，所以会隐式创建为一个全局变量
var a=(b='A');
console.info(a,b);//'A','A'
//并且赋值号返回右侧变量的值

var x=y,y='A';
console.info(x+y);//undefinedA
//当"x = y"执行时，y 已经存在，所以不抛出ReferenceError，并且它的值是'undefined'

var x=0;
function f(){
  var x=y=1;//此处x为函数内局部变量，执行函数f之后隐式创建全局变量y并赋值1
}
f();//不执行函数f，获取x的值全局声明的x，y则是未定义
console.info(x,y);//0,1 //此处获取的全局的x,y
```

## 二、var 定义变量

var 声明的变量作用域是它当前的**执行上下文**，作用域是函数内或全局
多次用 var 声明变量，变量不会丢失其值

## 三、let 定义变量

let 声明的变量作用域被限制在块级中的变量、语句或者表达式
在同一个函数或块作用域中重复声明同一个变量会引起 SyntaxError（语法错误）
**注：** 在 switch 语句中只有一个块，多次 let 声明同一个变量则报错；在 case 子句中的块会创建一个新的块作用域的词法环境，就不会产生上诉重复声明的错误

#### var 与 let 不同

初始化：
let 定义被执行时（编译时）才初始化
var 在作用域最顶部初始化且值为 undefined
作用域：
let 被限制在块级中的变量、语句或者表达式
var 只能是全局或者整个函数块的

#### 暂存死区

“暂时性死区”（temporal dead zone，简称 TDZ）

暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量（摘自 ES6 入门-->阮一峰）

(let,const)在变量初始化之前访问变量导致 ReferenceError，该变量处在一个自顶部到初始化处理的“暂存死区”中
使用 typeof 检测暂存死区中的变量，抛出异常 RefeferenceError

```
function test(){
   var foo = 33;
   if (foo) {
      let foo = (foo + 55); // ReferenceError
      //先计算foo+55，但是foo存在暂时性死区中（foo在if块中声明foo之前使用，作用域是从内到外……就近）
   }
}
test();

function go(n) {
  // n here is defined!
  console.info(n); // Object {a: [1,2,3]}

  for (let n of n.a) { // ReferenceError，n.a被解析为位于指令本身("let n")中的“ n”对象的属性“ a”。
    console.info(n);
  }
}
go({a: [1, 2, 3]});

let x = 1;
{
  var x = 2; // SyntaxError for re-declaration
}
//var会将变量提升至块的顶部, 这会导致隐式地重复声明变量
//等效-->
let x=1;
var x;//重复
{
  x=2;
}
```

## 四、cosnt 定义变量

与 let 声明变量类似
const 定义块级常量，声明必须赋值
创建一个值的只读引用，变量标识符不能重新分配
在引用内容是对象的情况下，可以改变对象的内容（例如，其参数）
一个常量不能和它所在作用域内的其他变量或函数拥有相同的名称

```
const MY_FAV=7;
if (MY_FAV === 7) {
  // 没问题，并且创建了一个块作用域变量 MY_FAV
  // (works equally well with let to declare a block scoped non const variable)
  let MY_FAV = 20;
  console.info('my favorite number is ' + MY_FAV);//20
  // 这被提升到全局上下文并引发错误
  var MY_FAV = 20;//SyntaxError for re-declaration 语法错误，重复声明
}
console.info('my favorite number is ' + MY_FAV);//全局,7

const MY_OBJECT={'key':'value'}
MY_OBJECT={'OTHER_KEY':'value'};//Uncaught TypeError: Assignment to constant variable 分配常量值错误
MY_OBJECT.key='otherValue';

const MY_ARRAY = [];
// 可以向数组填充数据
MY_ARRAY.push('A'); // ["A"]
// 但是，将一个新数组赋给变量会引发错误
MY_ARRAY = ['B'];// Uncaught TypeError: Assignment to constant variable.
```

将对象冻结，使用 Object.freeze()，不让对象的引用值改变

## 五、块级作用域与函数声明

ES5 规定，函数只能在顶层作用域和函数作用域之中声明，不能在块级作用域声明
浏览器没有遵守这个规定，为了兼容以前的旧代码，还是支持在块级作用域之中声明函数
ES6 规定，块级作用域之中，函数声明语句的行为类似于 let，在块级作用域之外不可引用
ES6 的块级作用域必须有大括号，如果没有大括号，JavaScript 引擎就认为不存在块级作用域。

#### 对 ES6 的浏览器

- 允许在块级作用域内声明函数
- 函数声明类似于 var，即会提升到全局作用域或函数作用域的头部
- 同时，函数声明还会提升到所在的块级作用域的头部

严格模式下，函数只能声明在当前作用域的顶层。
