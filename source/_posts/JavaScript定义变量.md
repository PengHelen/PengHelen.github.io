---
title: JavaScript定义变量
date: 2021-12-23 14:22:39
categories:
  - work
---

## 一、声明变量

**1.** 优先执行(var)：在执行任何代码之前进行处理
**2.** 不可配置性：声明变量所在上下文环境的不可配置属性，非声明变量是可配置的
**3.** 作用域在当前执行上下文(var)：作用域限制函数内或全局作用域

**注：** 未声明变量将很可能导致意想不到的结果，建议始终声明变量
在 ES5 严格模式下，分配值给未声明变量将引发错误

#### 优先执行(var)

**变量提升：** 变量在任意代码执行之前处理，意味着变量可以在声明之前使用，这种行为叫做“hosting”
始终在作用域顶部声明变量（全局/函数代码的顶部）
变量提升影响变量声明，不影响其值的初始化

#### 不可配置性

```
var a=1;
b=2;
delete this.a;//在严格模式下抛出typeError，其他情况下执行失败，但无提示
delete this.b;
console.log(a,b);//抛出refrenceerror（引用错误，b已被删除）
```

#### 声明多个变量

**隐式声明全局变量**
在非严格模式下，直接赋值给未声明的变量中，则执行赋值后，该变量会被隐式地创建为全局变量（它将成为全局对象的属性）

```
var a=b='A';
//等效于
var a,b;
b='A';
a='A';
//涉及到赋值符号是右结合计算规则，也就是说依次从右边赋值到左边;
var a=(b='A');
console.log(a,b);//'A','A'
//并且赋值号返回右侧变量的值

var x=y,y='A';
console.log(x+y);//undefinedA
//当"x = y"执行时，y 已经存在，所以不抛出ReferenceError，并且它的值是'undefined'

var x=0;
function f(){
  var x=y=1;//此处x为函数内局部变量，执行函数f之后隐式创建全局变量y并赋值1
}
f();//不执行函数f，获取x的值全局声明的x，y则是未定义
console.log(x,y);//0,1 //此处获取的全局的x,y
```

## 二、var 定义变量

var 声明的变量作用域是它当前的**执行上下文**，可以是嵌套函数，或在任何函数外
多次用 var 声明变量，变量不会丢失其值

## 三、闭包（未完-待更新）
嵌套函数可访问声明于它们外部作用域的变量
函数被引用包围（一个函数和对其周围状态（lexical environment，词法环境）的引用捆绑在一起的组合就是闭包）
闭包让在一个内层函数中访问到其外层函数的作用域
在 JavaScript 中，每当创建一个函数，闭包就会在函数创建的同时被创建出来。

#### 缺点
处理速度和内存消耗方面对脚本性能具有负面影响
创建新的对象或者类时，每个对象的创建，方法都会被重新赋值



## 四、let 定义变量

let 声明的变量作用域被限制在块级中的变量、语句或者表达式
不会在全局声明时（在最顶部的范围）创建 window 对象的属性，而在编译时才初始化
在同一个函数或块作用域中重复声明同一个变量会引起 SyntaxError
**注：** 在 switch 语句中只有一个块，多次 let 声明同一个变量则报错；在 case 子句中的块会创建一个新的块作用域的词法环境，就不会产生上诉重复声明的错误。

#### var 与 let 不同

初始化：
let 定义被执行时（编译时）才初始化
var 在函数顶部或代码顶部初始化且值为 undefined
作用域：
let 被限制在块级中的变量、语句或者表达式
var 只能是全局或者整个函数块的

#### 暂存死区

(let,const)在变量初始化之前访问变量导致 ReferenceError,该变量处在一个自顶部到初始化处理的“暂存死区”中
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
  console.log(n); // Object {a: [1,2,3]}

  for (let n of n.a) { // ReferenceError，n.a被解析为位于指令本身("let n")中的“ n”对象的属性“ a”。
    console.log(n);
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

## 五、cosnt 定义变量

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
  console.log('my favorite number is ' + MY_FAV);//20
  // 这被提升到全局上下文并引发错误
  var MY_FAV = 20;//SyntaxError for re-declaration 语法错误，重复声明
}
console.log('my favorite number is ' + MY_FAV);//全局,7

const MY_OBJECT={'key':'value'}
MY_OBJECT={'OTHER_KEY':'value'};//Uncaught TypeError: Assignment to constant variable 分配常量值错误
MY_OBJECT.key='otherValue';// Object.freeze() 不让对象的引用值改变

const MY_ARRAY = [];
// 可以向数组填充数据
MY_ARRAY.push('A'); // ["A"]
// 但是，将一个新数组赋给变量会引发错误
MY_ARRAY = ['B'];// Uncaught TypeError: Assignment to constant variable.
```
