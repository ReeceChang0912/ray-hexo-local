---
title: 系统学webpack第二天
tags: []
id: '260'
categories:
  - - 技术博客
date: 2021-09-30 11:20:25
---

前端的资源有些什么？图片，样式文件，字体，数据文件，媒体文件...

Webpack最出色的功能之一就是，除了JS，还可以通过loader来家在其他类型的文件。

这就需要我们安装相应的loader并进行配置。

1.图片资源 file-loder

图片资源的URL会被转换后放到output 当被引用是回被解析为output中的形式

2.样式资源 css-loader

样式的输出文件在执行的时候会被插入到<header>标签中的<script>

3.字体文件 file-loader url—loader（这两个loader可以接受任何类型）

通过@font-face文件引入也是一个这的学习的点

```
+ @font-face {
+   font-family: 'MyFont';
+   src:  url('./my-font.woff2') format('woff2'),
+         url('./my-font.woff') format('woff');
+   font-weight: 600;
+   font-style: normal;
+ }
```

4.数据资源 xml-loader csv-loader

可以实现一些预加载的功能

总结：wrbpack最牛的就是可以创建依赖树，动态的把需要的资源整合的一个模块里面，这样不用加在全部的asset

![](http://chang-rui.net/wp-content/uploads/2021/09/image-1024x676.png)

方便移植这里其实我不是很理解，

对于加在全部资源我可以理解，比如之前我们都是直接写绝对相对路径那样，那样就要去遍历找资源，为不是直接引用。这是我的理解，等什么时候问问强哥，记个土豆。