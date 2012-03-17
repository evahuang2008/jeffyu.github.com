---
date: '2007-07-14 09:52:11'
layout: post
slug: cxfcxf%e4%b8%adcollection-parameter%e6%a8%a1%e5%bc%8f%e7%9a%84%e5%ba%94%e7%94%a8
status: publish
title: '[CXF]CXF中Collection Parameter模式的应用'
wordpress_id: '23'
categories:
- Chinese
- SOA
- Web Service
tags:
- CXF
- Design Patterns
---

在CXF当中,ErrorVisitor就是一个典型的[Collection Parameter](http://c2.com/cgi/wiki?CollectingParameter)模式的应用.
其实,Collection Parameter模式很简单,就是有个类,负责到各个对象去收集结果.比如Struts中的ActionErrors类.
我刚开始看到ErrorVisitor的时候,我以为是跟Visitor模式有关系,其实是没关系的.如果有可能,我希望能改个名字,比如叫:ErrorCollector. 

参考资料:
--------------------
[http://c2.com/cgi/wiki?CollectingParameter](http://c2.com/cgi/wiki?CollectingParameter)


