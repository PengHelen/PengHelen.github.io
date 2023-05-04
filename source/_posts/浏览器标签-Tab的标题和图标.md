---
title: 浏览器标签/Tab的标题和图标
date: 2023-01-05 14:12:54
tags: web
---

---

## 一、图标
favicon.ico只需要放到网站根目录，并不需要添加到程序中，浏览器会直接通过域名调取这个文件

```
<!DOCTYPE html>
<html>
<head>
<link rel="shortcut icon" type="image/x-icon" href="favicon.ico" />
</head>
</html>
```

rel表示关系relationship，icon是一个网站图标的链接，type属性包含了链接资源的MIME类型

图片格式，type可接受类型：
* image/png(PNG)
* image/gif(GIF)
* image/jpg(JPEG)
* image/x-icon(ICO)
* image/svg+xml(SVG)

一个favicon图标必须满足以下要求：
* 默认名字是：favicon.ico
* 尺寸大小范围有：16x16，32x32，48x48，64x64，128x128（单位是px）
* 颜色通道值：8/24/32 bites

更新窗口图标后，浏览器仍不显示，需要清除浏览器缓存刷新网页（ctrl+f5）

参考文档：

https://github.com/audreyfeldroy/favicon-cheat-sheet 


## 二、标题
```
<html>
    <head>
        <title>文档标题</title>
    </head>
</html>
```

### 动态修改标题

```
document.title = "新标题";
document.querySelector('title').textContent = '新标题';
```

---
