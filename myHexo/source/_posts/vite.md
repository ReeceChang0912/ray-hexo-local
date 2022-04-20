---
title: Vite+
tags: []
id: '318'
categories:
  - - 前端
  - - 技术博客
date: 2022-04-01 18:59:41
thumbnail:https://w.wallhaven.cc/full/5w/wallhaven-5w5wj8.jpg
---

去年的四月中旬，我快速的粗略的学习了一下TypeScript，都说ts与vue3，vite等新技术是未来的新趋势，我这学期做项目的时候，也可以的往ts这方面去靠，尝试一些新的特性，react-native都已经支持了ts，我在利用expo创建了一个基于ts的项目之后，虽然基本能看懂与ts有关的东西，但感觉在react-native方面的生态还是不够。所以我今早复习了一遍ts与es6的一些基本知识，下午尝试了vite创建vue3与ts结合的项目。然后我就开始思考他们什么时候能够变成开发主流。带着这个问题，我找寻了vue的社区，没找到答案，最终在知乎上看到了一篇博文：

> Vue3生态发展现状和展望「尤雨溪」

在youtube上有视频，会议是2021年10月20日举行的，到今天也过了快半年了吧，但是解释道为什么还没那么普及的原因：

![](http://chang-rui.net/wp-content/uploads/2022/04/image.png)

从这个会议来看，还是很有必要要添加自己的技能包的。

接下来主要讲几点vue3+ts给我的新体验：

1.  script set up. 这个东西使得写vue3更加爽了，不用return，不用setup（），引入ref直接使用
2.  volar插件 提供了一些很友好的功能，例如把css temple script 切分为三个小窗口更方便找

![](http://chang-rui.net/wp-content/uploads/2022/04/image-2.png)

很多范型的东西我虽然理解基本概念，但还是看的很懵逼，唯有多看多练8⃣️。

此外由vite延伸出去认识了很多库，封装好vue，react的库，觉得开发更加简洁，例如nuxt，preact等等，真的很轻巧。我在想到时候去工作了，当年的era框架会不会也在渐进，开发到vite系列了。

\------------------------分割线 2022/04/06

今天对react进行了复习 尝试结合vite与编写react代码，有以下不同

![](http://chang-rui.net/wp-content/uploads/2022/04/image-3.png)

主要是在哪里声明类型有一些讲究，还使用了一个泛型类

然后回顾了一些基础知识，如组件之间的通信，setState等，思考了以下的几个问题。

1 setState 异步还是同步的问题，这个问题在我们的开发过程中很容易出现

首先当其上下文是setTimeout，addEventListener这些原生事件的时候，答案是同步的？写到这，我突然有了一个问题？addEventListener是dom二级事件，那么dom一级事件呢？应该是不可以的。简单的可以理解为被 React 控制的函数里面就会表现出“异步”，反之表现为同步

2 那么如何在异步的setState中拿到同步的数据？

很简单 第一个参数使用函数的形式，便是同步的效果

或者第二个参数中，也可以拿到执行后的结果

3 为什么要异步？

因为改变state会调用rendor，但是这是很大的资源消耗，我们可以放到一个栈中，合并后再批量修改。

4 如何实现？

来自简书：

在 React 的 setState 函数实现中，会根据 isBatchingUpdates(默认是 false) 变量判断是否直接更新 this.state 还是放到队列中稍后更新。然后有一个 batchedUpdate 函数，可以修改 isBatchingUpdates 为 true，当 React 调用事件处理函数之前，或者生命周期函数之前就会调用 batchedUpdate 函数，这样的话，setState 就不会同步更新 this.state，而是放到更新队列里面后续更新