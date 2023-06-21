---
title: CSS篇-重排与重绘
date: 2023-02-17 11:34:09
tags: CSS
---

# 重排
当DOM变化影响了元素的几何因素（元素的位置和尺寸大小），表现为重新生成布局，重新排列元素

### 发生重排的情况
* 页面初始渲染，开销最大的一次重排
* 添加/删除可见的DOM元素
* 改变元素位置
* 改变元素尺寸（margin，padding，border，width，height等）
* 改变元素的内容影响元素的尺寸（字体大小，文字数量，图片大小等）
* 改变浏览器窗口尺寸（resize）
* CSS伪类（:hover）
* `display:none`
* DOM添加动画

# 重绘
由于节点的样式发生改变，表现为某些元素的外观被改变，但不改变布局

**发生重排必然触发重绘**

### 发生重绘的情况
* color改变
* `visibility:hidden;`
* border-style
* 圆角、阴影
* ouline

# 避免重排重绘
* 集中改变样式
* 使用`documentFragment`，`document.createDocumentFragment`创建一个游离于DOM树之外的节点，
在节点上操作，最后插入DOM树，只触发一次重排重回（虚拟DOM？）


