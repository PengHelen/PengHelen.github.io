---
title: 类型转换
date: 2023-01-13 10:10:06
tags: JS
---

---

# 一、结果类型

* String
* Boolean
* Number


# 二、String(字符串)、Number(数值)和Boolean(布尔)转换

### 1.字符串

除`null`和`undefined`外，所有值都有`toString()`方法，结果与`String()`方法一致

**String**
```
String();''
String({});//'[object Object]'
String([]);//''
String(undefined);//'undefined'
String(null);//'null'
String(NaN);//'NaN'
String(Symbol());//'Symbol()'
String([0]);//'0'
String([0,1]);//'0,1'
String(0);//'0'
String(' ');//' ' 非空串，包含一个空格
```

**toSting()**
```
toString();//'[object Undefined]'

{}.toString();//Uncaught SyntaxError: Unexpected token '.'
({}.toString());//'[object Object]'

[].toString();//''

(undefined.toString())或undefined.toString();//Uncaught TypeError: Cannot read properties of undefined (reading 'toString')

null.toString();//Uncaught TypeError: Cannot read properties of null (reading 'toString')

NaN.toString();//'NaN'

Symbol().toString();//'Symbol()'

[0].toString();//'0'

[0,1].toString();//'0,1'

0.toString();//Uncaught SyntaxError: Invalid or unexpected token
(0.toString());//Uncaught SyntaxError: Invalid or unexpected token

' '.toString();//' '非空串，包含一个空格
```

**空串('')+特殊值** 

为了更清晰，字符串+任何值=>字符串，实验以下代码

```
''+0;//'0'
''+[];//''
''+{};//'[object Object]'
''+undefined;//'undefined'
''+null;//'null'
''+NaN;//'NaN'
''+[0];//'0'
''+[0,1];//'0,1'
''+Symbol();//Uncaught TypeError: Cannot convert a Symbol value to a string
```


### 2.数值

字符串转换成数值：引擎都会先去除字符串起始和末尾的空白，比如\n \t，去除空表后，字符串无法转换成数字时，则返回NaN

**Number,Math.floor,Math.ceil**
```
Number({});//NaN
Number(NaN);//NaN
Number(undefined);//NaN
Number('true');//NaN
Number('false');//NaN
Number('123id');//NaN
Number('id123');//NaN
Number([0,1]);//NaN
Number([0]);//0
Number();//0
Number(null);//0
Number([]);//0
Number('');//0
Number(' ');//0 非空串，包含一个空格
Number(false);//0
Number(true);//1
Number("-12.34");// -12.34
Number("\n");// 0
Number(Symbol());//Uncaught TypeError: Cannot convert a Symbol value to a number
```

**+(一元)**
```
+{};//NaN
+NaN;//NaN
+undefined;//NaN
+'true';//NaN
+'123id';//NaN
+'id123';//NaN
+[0,1];//NaN
+[0];//0
+0;//0
+null;//0
+[];//0
+'';//0
+' ';//0
+false;//0
+true;//1
```

**parseFloat/parseInt** 
```
parseInt([0,1]);//0
parseInt(0);//0
parseInt(1);//1
parseInt('123id');//123
parseInt('id123');//NaN
parseInt();//NaN
parseInt({});//NaN
parseInt([]);//NaN
parseInt(undefined);//NaN
parseInt(null);//NaN
parseInt('true');//NaN
parseInt('');//NaN
parseInt(' ');//NaN
parseInt(false);//NaN
parseInt(true);//NaN
parseInt(NaN);//NaN
parseInt('0x89id');//137
parseInt('0x89ed');//35309
```
***parseInt语法***
parseInt(string, radix);
string：要被解析的值。将参数转换为字符串 (使用 ToString抽象操作)，字符串开头的空白符将会被忽略
radix：从 2 到 36 的整数，表示进制的基数，超出这个范围，将返回 NaN；假如指定 0 或未指定，基数将会根据字符串的值进行推算（没有默认值，不是10，例0x开头会自动转成8进制）


### 3.布尔

* 字符串转布尔值：除了空串('')，其他字符串转换成布尔值都是`true`
* 数字转布尔值：除了数字0（和非数字NaN），其他数字布尔值为`true`
* 任何非基本类型值总是转换成`true`

```
Boolean();//false
Boolean('');//false
Boolean(NaN);//false
Boolean(undefined);//false
Boolean(null);//false
Boolean(false);//false
Boolean(' ');//true
Boolean('true');//true
Boolean('false');//true
Boolean('0');//true
Boolean(true);//true
Boolean({});//true
Boolean([]);//true
Boolean(Symbol());//true
```


# 三、不严格相等(==)

### 1.转换规则

`==`两边的操作数通常进行数值转换（除以下 ***特殊规则***外）

#### 参考表格
* ==或!= 特殊值的不严格相等
[JavaScript-Equality-Table](https://dorey.github.io/JavaScript-Equality-Table/)

* ==或!= 特殊值的不严格相等-图片
![截图](images/JS-Equality-Table.png)


### 2.特殊规则

* `null/undefined`只与`null`和`undefined`等，且==两边操作数不转换成数字

* NaN与任何值都不等，包括自身(==,===均适用)

* 当`==`两个操作数都是字符串时，操作数都 ***不转换*** 为数字


# 四、+（加）隐式转换

### 优先级顺序

* 1.操作数都是非基本类型，使用`[ToPrimitive]`转换成基本类型

* 2.其中一个操作数是string（字符串），另一个操作数转换成字符串进行运算

* 3.以上都不是，俩操作数都转成数值进行运算

### 规则

* 运算顺序是从左到右

* 将字面量[]转成空串''

# 五、Symbol

* 1.symbol只能显示转换，不支持隐式转换，隐式转换会报错：TypeError

* 2.symbol无法转换成数字，抛出TypeError错误


# 六、对象值

对象值转换成数字或字符串有专用内置属性`[[ToPrimitive]]`
对象值转换主要使用定义在`Object.prototype`上的`valueOf`和`toString`两种方法
`==`转换数组为数值时，数组先执行`valueOf()`，返回数组本身，再执行`toString()`，相当于执行数组的`join()`方法，将数组拼接成字符串

运算规则：
* 1).输入值本就是基本类型，不转换，直接返回；
* 2).调佣`toString()`方法，结果是基本类型，返回；
* 3).调用`valueOf()`，结果是基本类型，返回；
* 4).`toString()`和`valueOf()`都无法得到基本类型值，抛出错误`TypeError`

注：数值先调用`valueOf()`，返回值再调用`toString()`；字符串则相反先`toString()`再`valueOf()`
数组和对象的`valueOf()`方法返回对象本身，因此被忽略
大多数内置类型没有`valueOf()`方法，因此转换成数值和转换成字符串最后都是调用`toString()`


# 七、运算符(待完善...)

### `-` `*` `/` `%`
适用`Number`将两操作数转换后得到的结果

### `|` `&` `^` `~` 

### `>` `<` `>=` `<=`
`NaN` , `undefined` 与转换后的值比较都为 `false`

### `{}` 的特殊比较结果
`{}` 放在操作符第一位最好用括号分组，否则引擎认为 `{}` 是块语句声明，直接忽略，无转换
`{}` 与`0,1,undefined,NaN,null`比较，`{}`转换成`NaN`，因此与`>,<,>=,<=`比较结果均为`false`
```
({}>{});//false
({}>={});//true
({}<{});//false
({}<={});//true
({}=={});//false

({}>[]);//true [[]]同[]结果
({}>=[]);//true
({}<=[]);//false
({}<[]);//false
({}==[]);//false

({}>'1');//true '0',''(空串)同'1'一致
({}>='1');//true
({}<='1');//false
({}<'1');//false
({}=='1');//false

({}>[1]);//true
({}>=[1]);//true
({}<=[1]);//false
({}<[1]);//false
({}==[1]);//false
```

### `[]` 特殊结果
```
[]>null;//false
[]>=null;//true
[]<null;//false
[]<=null;//true
[]==null;//false
```


# 参考文献

[MDN:parseInt](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

[JavaScript Type Conversions](https://www.programiz.com/javascript/type-conversion)

[JavaScript type coercion explained](https://www.freecodecamp.org/news/js-type-coercion-explained-27ba3d9a2839/)

[JavaScript Type Conversions Explained](https://blog.openreplay.com/javascript-type-conversions-explained/)

---
