---
title: CSS篇-隐藏属性
date: 2023-02-17 10:25:09
tags: CSS
---

# `display:none;`
* 元素不存在，不占空间位置，reflow（页面重排）
* 子元素不继承，因为子元素不会被渲染（株连性）
* 无法获取焦点（无论是否设置tab），无法响应事件
* 不影响表单提交，表单提交依然会将 `<input name='user' style="display:none; />"` 的值提交上去
* 不支持transition
* CSS中的counter会忽略设置`display:none;`元素


# `visibility:hidden;`
* 元素不存在，但占空间位置，repaint（重绘）
* 被子元素继承，修改子元素 `visibility:visible;` 可取消隐藏
* 无法获取焦点
* 不影响表单提交

# `opacity:0;`
* 透明度为0，占据空间位置
* 被子元素继承，但无法通过修改子元素 `opacity:1;` 取消隐藏

# `width:0;`
* 宽度为0，不占空间位置

# `visibility` 布局应用
* 页面加载，display会触发回流和重排，页面发生抖动，visibility将元素空间位置渲染好，只等显示即可
* 动画， `display:none` 立即显示，不支持transition，无法延时展示动画，

