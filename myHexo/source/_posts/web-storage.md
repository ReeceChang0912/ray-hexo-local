---
title: Web Storage
thumbnail: https://w.wallhaven.cc/full/5d/wallhaven-5d3297.jpg
tags: []
id: '330'
categories:
  - - 前端
  - - 技术博客
date: 2022-04-08 16:29:16
---

这里的内容极其容易弄混，先弄出一个结构图

*   cookie
*   session
*   web storage ： session storage local storage

cookie 欢迎指出错误 我的结论机遇我的实验：

**cookie** 服务端首次创建，然后存在客户端 之后每次请求响应客户端都会携带cookie 服务端通过set-cookie可以改变cookie。 在客户端首次拿到cookie之后，客户端也可以修改。

问题1: 客户端可以创建cookie吗？

我的答案：不能。

![](http://chang-rui.net/wp-content/uploads/2022/04/image-4.png)

![](http://chang-rui.net/wp-content/uploads/2022/04/image-5.png)

在我们服务端创建完成后就可以

![](http://chang-rui.net/wp-content/uploads/2022/04/image-6.png)

**为什么出现 cookie** ？

假设我们拥有两个界面，一个登陆，一个主页，那么我们登陆之后跳转到主页，怎么知道登陆的状态呢？很显然，我们可以重新再像数据库发一次请求，来询问登陆状态。但是，这就显得多余。如果我们利用cookie，把path配置为主域名，我们就可移栽这两个页面访问到登陆时所储存的cookie，当主页重新发起请求时，cookie在请求体里面一起发到服务器，这样我们不用请求数据库就可以知道登陆状态。cookie的失效时间由expire字段实现，在页面之间的传递有path规则决定。

**为什么出现session？**

因为cookie一般只有4kb，太小了，并且是字符串，而且用户可见，不是很安全，那么我们的session就应运而生了。

其存储在服务端，较安全，而且可以存更大一些的数据。

**WebStorage**

这两个都可以存比较大的数据，例如5mb

local Storage 与session storage ：举一个生动的例子，你用浏览器开了一个界面，然后又新开了同一个界面，或者是你跳到了一个同源的页面，在任意一个界面中，改变了local storage中的数据，是会共享的，这是他的范围，如果跳到一个外链，也是不存在的。

![](http://chang-rui.net/wp-content/uploads/2022/04/image-9.png)

Test中进行修改

![](http://chang-rui.net/wp-content/uploads/2022/04/image-10.png)

原页面同步了

然后你关闭之后，下次在打开，他还是存在的，这是他的存在时间。而对于session Storage而言呢，你在单独的页面修改数据是不会共享的，比如你跳到了同源的页面，数据是在的，但是不能共享，然后就是你关闭了界面，跳到新的外部界面，数据是不存在的。

![](http://chang-rui.net/wp-content/uploads/2022/04/image-7.png)

![](http://chang-rui.net/wp-content/uploads/2022/04/image-8.png)

我们可以看到，注释时候，仍然是存在在localStorage中的，除非你手动removeItem才会消失

值得注意的是local Storage存入对象时应该先转化为json字符串！

具体代码可以参考我的github仓库 ：[project\_on\_mac/my\_basic at master · ReeceChang0912/project\_on\_mac (github.com)](https://github.com/ReeceChang0912/project_on_mac/tree/master/my_basic)