---
title: 应用层协议--SMTP POP
tags: []
id: '211'
categories:
  - - 前端
  - - 技术博客
date: 2021-07-04 10:58:14
---

电子邮箱是互联网最伟大的应用之一.

我们现在普遍使用的是Web邮箱,例如GMail,Foxmail.outlook,apple等等很多著名的邮箱,学校会给老师学生提供教育邮箱,企业会给员工提供企业邮箱...邮箱的使用无处不在.

邮箱的构成主要有一个用户代理(user agent)与一个邮件服务器.

![](http://chang-rui.net/wp-content/uploads/2021/07/image-1.png)

如图中,当Alice要与Bob通信时,Alice先在用户代理写好邮件,然后发送到邮件服务器,邮件服务器发送给Bob的邮件服务器,当Bob方便时,Bob通过POP协议读取邮件的内容.

SMTP的一个显著缺点是其要求每个报文使用7比特ASCII码格式,如有像二进制文件的图片,那么报文必须重新进行编码,HTTP则不受这种限制.  
SMTP的端口号是２５

POP的端口号是１１０