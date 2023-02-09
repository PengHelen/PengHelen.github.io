---
layout:
  - layout
title: CSS篇-auto关键词
date: 2023-01-06 11:09:07
tags:
---

---

> 根据auto在CSS常用属性的实际表现来探究auto的作用

auto是自适应，自动的意思

# 1.width:auto;
width默认值（即不设置width值时）是auto
当使用`width:auto;`时，元素的宽被限制在父元素内，元素内容的宽度会自动减去元素的margin，padding和border，即元素内容自动充满元素剩余空间

## width:auto; VS width:100%;
`width:auto;`表示：父元素内容宽度=子元素margin+padding+border+content(元素内容宽度，即元素的剩余空间)

`width:100%;`表示：父元素内容宽度=子元素content(即子元素内容宽度等于父元素宽度)

**注意：适用标准浏览器的盒子模型，不适用IE盒子模型**

# 2.height:auto;
height默认值是auto
`height:auto;`，元素高度等于元素内容高度，此时即使设置`height:100%;`元素高度也还是元素的内容高度

# 3.margin:auto;
margin的默认值是0，表示元素没有margin
当使用`margin:auto;`，除去元素的content内容的宽高、padding、border，剩余空间都由margin来填充

如下代码，元素宽高确定，巧用`margin:auto;`，达到水平垂直居中效果

```
<div class="wrapper">
  <div class="item">I am centered.</div>
</div>
.wrapper {
    position: relative;
}
.item {
    width: 200px;
    height: 100px;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;
}
```

如下代码，元素宽确定，巧用`margin:0 auto;`，让元素水平居中

```
<div class="wrapper">
  <div class="item">I am centered.</div>
</div>
.item {
    width: 200px;
    margin: auto;
}
```

**margin-inline和margin-block属性是实验中属性，暂不研究**

# 4.background-size:auto;
background-size默认值是auto，以背景图片的比例缩放背景图片

# 5.top/right/bottom/left:auto;
top/right/bottom/left的默认值是auto

**MDN** 
**left:auto**

**对于绝对定位元素，元素将忽略此属性而以right属性为准，如果此时设置width: auto，将基于内容需要的宽度设置宽度；如果right也为auto的话，元素的水平位置就是它假如作为静态 (即 static) 元素时该在的位置**

**对于相对定位元素，元素相对正常位置的偏移量将基于right属性；如果right也为auto的话，元素将不会有偏移**

# 6.z-index:auto;
z-index默认值是auto
盒子不会创建一个新的本地堆叠上下文  
在当前堆叠上下文中生成的盒子的堆叠层级和父级盒子相同

# 7.overflow:auto;
overflow默认值是visible，内容不能被裁减并且可能渲染到边距盒（padding）的外部

**MDN：`overflow:auto;`**
**取决于用户代理。如果内容适应边距（padding）盒，它看起来与 visible 相同，但是仍然建立了一个新的块级格式化上下文；如果内容溢出，则浏览器提供滚动条**

# 8.cursor:auto;
cursor默认值是auto，浏览器根据当前内容决定指针样式

# 9.table-layout:auto;
table-layout默认值是auto，表格及单元格的宽度取决于其包含的内容

# 10.flex:auto;
flex默认值是`0 1 auto`，flex是flex-grow，flex-shrink，flex-basis的合并简写属性
当使用`flex:auto;`，等同于`flex:1 1 auto;`

### flex+margin-left:auto;可使元素右对齐
```
<div class="wrapper">
  <div class="item">Item1</div>
  <div class="item item-2">Item2</div>
</div>
.wrapper {
  display: flex;
}
.item-2 {
  margin-left: auto;
}
```

### flex+margin:auto;可使元素水平垂直居中
```
<div class="wrapper">
  <div class="item">Item1</div>
</div>
.wrapper {
  display: flex;
  height: 400px;
  background-color: blue;
}
.item {
  width: 200px;
  height: 100px;
  margin: auto auto;
  background-color: red;
}
```

**grid可参考flex，暂不研究**

---

---

# 参考文献：  
英文版：https://ishadeed.com/article/auto-css/  

中文翻译版：https://blog.csdn.net/qq449245884/article/details/105963479/   
https://css-tricks.com/how-auto-margins-work-in-flexbox/  

---
