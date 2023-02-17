---
layout:
  - layout
title: CSS层级
date: 2023-01-16 15:19:26
tags: CSS
---

# 层叠影响因素

* 资源顺序（平级）
* 优先级（等级压制）
* 重要程度（覆盖所有优先级）

# 资源顺序

当应用两条同级别的规则到一个元素的时候，写在后面的（在CSS样式表中的顺序，<s>在HTML中顺序</s>）就是实际使用的规则

# 优先级

仅当某一列的优先级权重相同时，才评估下一列；
否则，可直接忽略低等级的选择器，因为它们无法覆盖高优先级等级的选择器

例：即无论选择器中有多少个 ID，内联样式总是比其它任何优先级的权重都要高

* 内联样式(1000)
* ID(100)
* 类，伪类，属性选择器(10)
* 元素，伪元素（如::after）(1)

否定（:not()）和任意匹配（:is()）的参数，对优先级算法有贡献的参数的优先级的最大值将作为该伪类选择器的优先级

### 不影响优先级
通用选择器 \* 组合选择器(+,>,~,'') 调整优先级选择器(:where())

# 重要程度
覆盖所有上面所有优先级计算  
!important与优先级无关，但它与最终的结果直接相关

### 使用场景
* 覆盖内联样式
* 覆盖优先级高的选择器

# a标签伪类元素优先级
link-visited-hover-active   
LVHA  
趣味记法：LoVe HAte

# 参考文献

https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance

https://www.freecodecamp.org/news/what-is-css-specificity/

https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/










