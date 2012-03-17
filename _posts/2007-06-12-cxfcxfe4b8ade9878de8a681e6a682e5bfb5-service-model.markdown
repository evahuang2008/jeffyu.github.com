---
date: '2007-06-12 17:25:19'
layout: post
slug: cxfcxf%e4%b8%ad%e9%87%8d%e8%a6%81%e6%a6%82%e5%bf%b5-service-model
status: publish
title: '[CXF]CXF中重要概念: Service Model'
wordpress_id: '30'
categories:
- Chinese
- SOA
- Web Service
tags:
- CXF
---

推荐我同事[willem](http://willem.bokeland.com/)写的几篇关于CXF的文章,里面阐述了一个很重要的概念ServiceModel.(而且我觉得他写得很清晰.;-) )[
](http://willem.bokeland.com/blog/794/6089/2007/06/05/199825)



	
  * [我眼中的CXF之Service Model](http://willem.bokeland.com/blog/794/6089/2007/06/05/199825)

	
  * [何为CXF](http://willem.bokeland.com/blog/794/6089/2007/05/20/192870)

	
  * [JAX-WS](http://willem.bokeland.com/blog/794/3110/2006/10/22/75588)


这里,为什么会存在一个Service Model呢,主要是因为它可以有很多个front-end,比如说 JAX-WS,simple(POJO类型的), JS etc,所以基于这种可变的,我们需要抽象出一个稳定的,这样,CXF内部runtime的程序打交道都是跟Service Model,它不需要去管前端是有JAX-WS or POJO的..  其实,我到是觉得可以把Service Model看做是meta data 管理器,因为如果你想要所有的元数据,比如说wsdl的信息啊等等的,你都可以从这取到.


