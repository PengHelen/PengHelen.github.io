---
title: svg入门基础
date: 2023-05-24 19:23:51
tags: web
---

# 一、SVG
### 1.简介
Scalable Vector Graphics  
可缩放矢量图形  
XML语言，严格区分大小写

- 优点
实现了DOM接口

- 缺点
加载慢

### 2.svg文件基本属性
- 后来居上，越后面的元素越可见（类似层级叠加）
- HTML是XHTML且声明 `application/xhtml+xml` ，svg可嵌入到XML源码
- HTML5通过 `object/iframe` 引用svg文件

``` 
<object data="image.svg" type="image/svg+xml" />
<iframe src="image.svg"></iframe>
```

- 可通过JS创建并注入到HTML中
- gzip压缩后，svg扩展名为 `.svgz`（仍有服务器压缩、浏览器兼容问题）

# 二、基本形状和属性
### 1.矩形
```
<rect x="60" y="10" rx="10" ry="10" width="30" height="30"/>
```

x,y为矩形的坐标值
rx,ry控制矩形的圆角，没有设置默认为0
width,height为矩形的宽、高

### 2.圆形
```
<circle cx="25" cy="75" r="20"/>
```

r为圆的半径
cx,cy为圆心坐标

### 3.椭圆
```
<ellipse cx="75" cy="75" rx="20" ry="5"/>
```

rx,ry为椭圆的x,y半径
cx,cy为椭圆中心的坐标值

### 4.线条
```
<line x1="10" x2="50" y1="110" y2="150" stroke="black" stroke-width="5"/>
```

x1,y1为起点坐标
x2,y2为终点坐标

### 5.折线
```
<polyline points="60, 110 65, 120 70, 115 75, 130 80, 125 85, 140 90, 135 95, 150 100, 145"/>
```

points点集数列，每个数字用空白、逗号、终止命令符或者换行符分隔开

### 6.多边形
```
<polygon points="50, 160 55, 180 70, 180 60, 190 65, 205 50, 195 35, 205 40, 190 30, 180 45, 180"/>
```
pionts同以上，路径绘制完后闭合图形，polygon的路径在最后一个点处自动回到第一个点

### 7.路径
```
<path d="M20,230 Q40,205 50,230 T90,230" fill="none" stroke="blue" stroke-width="5"/>
```
[mdn参考](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Paths)

# 三、svg的CSS样式
### 1.def
```
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <style><![CDATA[
       #MyRect {
         stroke: black;
         fill: red;
       }
    ]]></style>
  </defs>
  <rect x="10" height="180" y="10" width="180" id="MyRect"/>
</svg>
```

### 2.外部样式表
```
<?xml version="1.0" standalone="no"?>
<?xml-stylesheet type="text/css" href="style.css"?>

<svg width="200" height="150" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <rect height="10" width="10" id="MyRect"/>
</svg>

<!-- style.css -->
#MyRect {
  fill: red;
  stroke: black;
}
```

### 3.渐变（线性，径向）
```
<!-- 线性 -->
<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <linearGradient id="Gradient1">
        <stop class="stop1" offset="0%"/>
        <stop class="stop2" offset="50%"/>
        <stop class="stop3" offset="100%"/>
      </linearGradient>
      <style type="text/css"><![CDATA[
        #rect1 { fill: url(#Gradient1); }
        .stop1 { stop-color: red; }
        .stop2 { stop-color: black; stop-opacity: 0; }
        .stop3 { stop-color: blue; }
      ]]></style>
  </defs>
  <rect id="rect1" x="10" y="10" rx="15" ry="15" width="100" height="100"/>
</svg>

<?xml version="1.0" standalone="no"?>
<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <radialGradient id="RadialGradient1">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
  </defs>
  <rect x="10" y="10" rx="15" ry="15" width="100" height="100" fill="url(#RadialGradient1)"/>
</svg>
```

### 4.其他
- patterns 图案
- text 文本
- g 元素集合
- 基础变形
  平移 `transform="translate(30,40)"`  
  旋转 `transform="rotate(45)"`  
  斜切 skewX(),skewY()
  缩放 scale()  
  矩阵变换 matrix(a, b, c, d, e, f)
- svg可嵌套
- 剪切 clipPath
- 遮罩 mask
- 透明度 `opacity=".5"` 
- 光栅图像 image
- 滤镜 filter

# 四、工具
[snap.svg](http://snapsvg.io/docs/)
[元素参考](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element)
[属性参考](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute)
[文档对象模型](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model#svg_%E6%8E%A5%E5%8F%A3)



