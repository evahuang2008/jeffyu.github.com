---
date: '2007-08-23 16:27:27'
layout: post
slug: cxfcxf%e5%bd%93%e4%b8%ad%e7%9a%84configuration-spring2-0%e5%8f%af%e6%89%a9%e5%b1%95xml%e9%85%8d%e7%bd%ae
status: publish
title: '[CXF]CXF当中的Configuration -- Spring2.0可扩展XML配置'
wordpress_id: '10'
categories:
- Chinese
- SOA
- Web Service
tags:
- CXF
- Design Patterns
---

还是忍不住,昨天看完了CXF中Bus后,就一直想着CXF的Configuration的实现问题.可以说,CXF中的configuration是依赖于spring2.0中所提供的可扩展XML. 

如果你使用CXF的话,如果你是通过xml文件来部署endpoint的话,那么下面的这段,你肯定不陌生:

<jaxws:endpoint
id="hello_world"
implementor="demo.hw.server.GreeterImpl"
wsdlLocation="WEB-INF/wsdl/hello_world.wsdl"
address="/hello_world">
<jaxws:features>
<bean class="org.apache.cxf.feature.LoggingFeature"/>
</jaxws:features>
</jaxws:endpoint>

在Spring当中,本来没有endpoint这样的tag,这属于我们自定义的tag. 那么在spring2.0当中,我们可以很容易的扩展他原有的标签.

到底怎么来实现Spring的可扩展XML配置呢. 可以参考以下几篇文章: (当然了,你也可以从CXF的源代码中看到大量这样的实现).

[http://www.javaeye.com/topic/102450](http://www.javaeye.com/topic/102450)
[http://www.javaeye.com/topic/30963](http://www.javaeye.com/topic/30963)
[http://www.javaeye.com/topic/30964](http://www.javaeye.com/topic/30964)
[http://www.memestorm.com/blog/spring-components-xml-configuration-on-steroids/](http://www.memestorm.com/blog/spring-components-xml-configuration-on-steroids/)


