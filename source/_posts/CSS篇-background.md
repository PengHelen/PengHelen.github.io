---
title: CSS篇-background
date: 2023-05-16 10:36:42
tags: CSS
---

# 1.所有值
以下属性的一个或多个值，可以按任意顺序放置
- backbround-attachment
- background-clip
- background-origin
- background-color
- background-image
- background-position
- background-repeat
- background-size

# 2.属性值
### background-attachment(固定/滚动)
- scroll
- fixed
- local
- local,scroll
- scroll,local

### background-clip/background-origin(背景图片宽高)
- border-box
- padding-box
- content-box
- text // 仅background-clip有

组合设置背景图片元素仅在透明字体上显示
```
background-clip:text;
-webkit-background-clip:text;
color:transparent;
```

当 `background-attachment:fixed`, `background-origin`无效

### background-color
- red;/#bbff00;/rgb(255,255,128);/hsla(50,33%,25%,0.75);
- currentColor // 关键字，代表color属性的计算值
- transparent 

### background-image
一个元素设置一个或多个背景图像
- none
- url('xxx.png'),url('xxx.jpeg');
- linear-gradient(to bottom, rgba(255,255,0,0.5), rgba(0,0,255,0.5)),url('xxx.png');

### background-position(背景图片位置)
- top/right/bottom/left
- center
- 25% 75%/1cm 2cm/10ch 8em
- 0 0,center; // 多张图片
- bottom 10px right 20px

### background-repeat
- repeat-x;/repeat-y;/repeat;
- space  
// 图像会尽可能得重复，不会裁剪，第一个和最后一个会被固定在元素的边上，同时空白会均匀地分布在图像之间
- round
- no-repeat
- space repeat // 水平 垂直

### background-size
- contain // 背景图全展示出来
- cover // 背景图布满元素
- x%
- 20px 10px // width height
- auto // 默认值
- auto,auto; // 多个背景

