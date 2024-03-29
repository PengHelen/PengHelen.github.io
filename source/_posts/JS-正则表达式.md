---
title: 正则表达式
date: 2023-01-30 11:20:51
tags: JS
---

# 可选参数
例：`/a-z/gi`
```
g 全局搜索
i 不区分大小写
m 多行
s 允许 .匹配
u 使用uniocde码的模式进行匹配
y 粘性搜索，匹配从目标字符串的当前位置开始
```

# 方法

### 正则表达式方法
```
exec 返回：数组（未匹配到返回null）
/a{1,3}/.exec('caaaandy')
['aaa', index: 1, input: 'caaaandy', groups: undefined]

test 返回true或false
```

### 字符串方法

```
match 
'caaaaaandy'.match(/a{1,3}/)
['aaa', index: 1, input: 'caaaaaandy', groups: undefined]

matchAll
必须加可选参数g，否则报错String.prototype.matchAll called with a non-global RegExp argument
[...'caaaaaaandy'.match(/a{1,3}/g)]
['aaa', 'aaa', 'a']

search 返回匹配到的位置索引，或者在失败时返回 -1 

replace  
'dcaaaaaaandy'.replace(/a{1,3}/g,'HH')
'dcHHHHHHndy'

split
```

# 特殊字符

### 断言
```
// 边界类断言
^ 首
$ 尾

\b 匹配字边界的长度为零
\B 匹配非单词边界(\b的否定版)
\b在前，则regExp前要么是字符串开头，要么是空格；反之则为\B
\b在后，则regExp后要么是字符串结尾，要么是空格；反之则为\B

// 其他断言
x(x?=y) 先行断言： x 被 y 跟随时匹配 x
x(?!y) 先行否定断言： x 没有被 y 紧随时匹配 x
(?<=y)x 后行断言： x 跟随 y 的情况下匹配 x
(?<!y)x 后行否定断言： x 不跟随 y 时匹配 x
```

### 字符类
```
[xyz][a-c] 匹配包含在方括号中的任何字符
[^xyz][^a-c] 匹配【未】包含在方括号中的任何字符

. 匹配除行终止符（\n, \r, \u2028或\u2029）之外的任何单个字符；若 s ("dotAll") 标志位被设为 true（即加上可选参数s），它也会匹配换行符

\d [0-9]
\D [^0-9]

\w [A-Za-z0-9_]
\W [^A-Za-z0-9_]

\s [\f\n\r\t\v\u0020\u00a0\u1680\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]
\S [^\f\n\r\t\v\u0020\u00a0\u1680\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]

\t 水平制表符
\r 回车符
\n 换行符
\v 垂直制表符
\f 换页符
[\b] 退格键
\0 匹配一个 NUL 字符；不要在此后面加上另一个数字

（暂不考究）
\cX
\xhh
\uhhhh
\u{hhhh}或\u{hhhhh}
\p{UnicodeProperty}或\P{UnicodeProperty}
\

x|y 匹配“x”或“y”。每个由管道符 (|) 分隔的部分称为一个可选项
```

### 组和范围
```
x|y
[xyz][a-c]
[^xyz][^a-c]
(x)
\n
(?<Name>x)
(?:x)
```

### 量词
```
* 0或多次（贪婪）
+ 1+（贪婪）
? 0次或1次（非贪婪）
{n} n正整数，例：/a{2}/ 匹配“caandy”中的所有“a”，以及“caaandy”中的前两个“a”
{n,} n正整数，至少匹配n次，例：匹配“caandy”和“caaaaaaandy”中的所有 a
{n,m} n自然数，至少匹配n次，至多匹配m次
*? 
+?
??
{n}?
{n,}?
{n,m}?
```

### Unicode属性转义
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes

# 参考文献

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions

https://www.regular-expressions.info/wordboundaries.html

https://www.pineboat.in/post/regular-expressions-your-ally/