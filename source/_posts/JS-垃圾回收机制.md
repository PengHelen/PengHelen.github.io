---
title: JS垃圾回收机制
date: 2023-11-09 10:16:51
tags: JS
---

# 介绍
JS中自动内存管理，实现了内存的分配和闲置资源的回收

持续运行的服务进程，要及时释放内存，否则内存占用越来越高，轻则影响系统性能，重则就会导致进程崩溃

简称：GC(Garbage Collection)
是JS中使用内存管理系统的基本组成部分，靠浏览器中垃圾回收器来回收处理
垃圾回收器是浏览器中一个专门的线程

# 判断垃圾对象
内存中未被引用的变量或对象，都是垃圾

JS运行时存在一个储存作用域链的栈，栈最底层元素时全局作用域
函数/块执行结束，作用域随机被推出，被推出的作用域变得不可访问，内部所保存的变量，也不能访问，这些成为垃圾

# 变量生命周期

### 全局变量
定义在所有函数之外的变量（挂在window下的变量）
生命周期：只在页面卸载时进行销毁（持续到浏览器关闭页面）

### 局部变量
定义在函数中的变量
生命周期：函数执行后，变量占的内存被垃圾回收机制释放

# 垃圾回收办法

- 引用计数法
每一个对象内部都标记一下引用它的总个数，若引用个数为0，即为垃圾对象

循环引用：2个对象内部存在相互引用，断开对象引用后，还不是垃圾对象

- 标记清除法
从根对象（window）开始查找所有引用的对象，标记为“使用中”，没有标记的使用中对象就是垃圾对象

内存碎片化，分配速度慢，最坏的情况，每次进行分配都要遍历整个空闲链表

- 复制算法
将整个存储空间一分为二，一个存数据，一个暂时闲置

堆使用效率低下

- 标记整理算法
标记，移动活动对象位置，使活动对象聚集到堆的一端

吞吐量差，整理过程需要多次整堆遍历，速度慢

- 分代式垃圾回收
大部分对象生成后马上变成垃圾，只有少部分对象能够存活长久

新生代对象，老年代对象，新生代GC，老生代GC，晋升（存活一定次数的新生代对象转化为老年对象）

- 增量式垃圾回收（暂停性GC）
根查找阶段，标记阶段，清除阶段
降低吞吐量

- 三色标记法
白色：指的是未被标记的对象
灰色：指自身被标记，成员变量（该对象的引用对象）未被标记
黑色：指自身和成员变量皆被标记

# V8垃圾回收
新生代：复制算法+标记-整理算法（并行回收）
老生代对象：标记-清除算法+标记-整理算法
并行回收(Parallel)：垃圾回收器在主线程上执行的过程中，开启多个辅助线程，同时执行同样的回收工作

- 默认情况下，它将内存空间一分为二：
针对 32 位系统，新生代内存大小为 16MB，老生代内存大小为 700MB 
针对 64 位系统：新生代内存大小为 32MB，老生代内存大小为 1.4GB 

# 内存泄露与优化
### 概念
JS中已经分配内存地址的对象由于长时间未进行内存释放或无法清除，造成了长期占用内存，使得内存资源浪费，最终导致运行的应用响应速度变慢以及最终崩溃的情况

### 优化
- 少定义**全局变量**，或者使用全局变量后置为null
- **变量声明**用const和let替代var
- 及时清理**缓存**
- 手动清除**定时器**
- 避免使用**闭包**
- 避免**死循环**
- 从内到外**appendChild**，避免从外到内执行appendChild
- 给删除的**DOM**节点引用设置为null
