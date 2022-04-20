---
title: 提问webpack
thumbnail: https://w.wallhaven.cc/full/x8/wallhaven-x82p2l.jpg
tags: []
id: '315'
categories:
  - - 前端
  - - 技术博客
date: 2022-03-31 17:43:58
---

1.  why webpack?

**全局变量与依赖的问题。**

```
<script src="module-a.js"></script>
<script src="module-b.js"></script>
最开始es5并不支持模块化，我们往往需要自执行函数的闭包来进行隔离
```

**版本的问题**

例如部分浏览器不支持es6 例如import export 就需要进行转换为一个map对象，键为路径，值为可执行的函数

这里不得不提到vite，因为它基于esmodule，支持之中语法，可以做到esbuild冷启动，按需加载，我在想如果不支持esmodule，vite会怎么写？

除此之外less等也需要转化为css，最后通过style-loader嵌入到html中

**开发效率的问题**

希望能进行热加载 即使刷新

**压缩打包**

这样可以使代码的更小，我看了webpack的一些方法，比如删除空格和未使用的函数或变量，这里我感觉到了eslint的魅力，在编译的时候就已经在为最后的打包做准备了

2\. why bundle.js?!

bundle.js 能直接运行在浏览器中的原因在于输出的文件中通过 `__webpack_require__` 函数定义了一个可以在浏览器中执行的加载函数来模拟 Node.js 中的 require 语句。

原来一个个独立的模块文件被合并到了一个单独的 bundle.js 的原因在于浏览器不能像 Node.js 那样快速地去本地加载一个个模块文件，而必须通过网络请求去加载还未得到的文件。 如果模块数量很多，加载时间会很长，因此把所有模块都存放在了数组中，执行一次网络加载。

3.how bundle.js

图片： =》 base64

css： style-laoder 插入页面

es6等=》 map对象

更细：import 与 import（）

`import`经过`webpack`打包以后变成一些`Map`对象，`key`为模块路径，`value`为模块的可执行函数；  
代码加载到浏览器以后从入口模块开始执行，其中执行的过程中，最重要的就是`webpack`定义的`__webpack_require__`函数，负责实际的模块加载并执行这些模块内容，返回执行结果，其实就是读取`Map`对象，然后执行相应的函数；  
当然其中的异步方法（import('xxModule')）比较特殊一些，它会单独打成一个包，采用动态加载的方式，具体过程：当用户触发其加载的动作时，会动态的在`head`标签中创建一个`script`标签，然后发送一个`http`请求，加载模块，模块加载完成以后自动执行其中的代码，主要的工作有两个，更改缓存中模块的状态，另一个就是执行模块代码

4.how hot-reload ？

![](http://chang-rui.net/wp-content/uploads/2022/03/image-1024x625.png)

实现方式大同小异，但对于vite的，不需要重新进行打包整个模块，所以速度很快，