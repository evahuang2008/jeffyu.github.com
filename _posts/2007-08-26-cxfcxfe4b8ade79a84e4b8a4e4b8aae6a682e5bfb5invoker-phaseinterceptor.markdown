---
date: '2007-08-26 10:48:06'
layout: post
slug: cxfcxf%e4%b8%ad%e7%9a%84%e4%b8%a4%e4%b8%aa%e6%a6%82%e5%bf%b5invoker-phaseinterceptor
status: publish
title: '[CXF]CXF中的两个概念:Invoker & PhaseInterceptor'
wordpress_id: '6'
categories:
- Chinese
- SOA
- Web Service
tags:
- CXF
- Design Patterns
---

在读CXF代码中,其中有个Invoker的概念,在CXF的WIKI上有对为什么有这个概念的解释,写得很清楚: 参考[1] 

另外,在CXF当中的Interceptor概念中,引入PhaseInterceptor,就是说从一个endpoint发送message到另外一个endpoint的时候,它所要经历的Phases,那么这些Phases是哪些呢?而且分别代码什么呢? 参考[2]

[1] [http://cwiki.apache.org/CXF20DOC/invokers.html](http://cwiki.apache.org/CXF20DOC/invokers.html)
[2] [http://cwiki.apache.org/CXF20DOC/interceptors.html](http://cwiki.apache.org/CXF20DOC/interceptors.html)


