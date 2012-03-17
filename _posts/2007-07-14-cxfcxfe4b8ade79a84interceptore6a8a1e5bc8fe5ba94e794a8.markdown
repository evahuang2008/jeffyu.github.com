---
date: '2007-07-14 04:55:55'
layout: post
slug: cxfcxf%e4%b8%ad%e7%9a%84interceptor%e6%a8%a1%e5%bc%8f%e5%ba%94%e7%94%a8
status: publish
title: '[CXF]CXF中的Interceptor模式应用'
wordpress_id: '21'
categories:
- Chinese
- SOA
- Web Service
tags:
- CXF
---

先来说说Interceptor模式中各个参与对象的功能和职责:
Interceptor:
* Defines an interface for integrating out-of-band services
Concrete Interceptor:
* Implements a specific out-of-band service
* Uses context object to control the concrete framework.
Dispatcher
* Allows applications to register and remove concrete interceptors.
* Dispatches registered concrete interceptor callbacks when event occur
Context Object
* Allows services to obtain information from the concrete framework
* Allows services to control certain behaviour of the concrete framework. 

看上去是很好理解的... Dispatcher负责添加和删除Interceptor, Concrete Interceptor通过Context Object获取到具体的上下文内容,去改变值,或者处理业务功能.

现在我们来看下CXF中是怎么使用Interceptor模式的.
Interceptor (对应Interceptor角色)
public interface Interceptor<T extends Message> {
void handleMessage(T message) throws Fault;
void handleFault(T message);
}
在CXF当中,还引入了一个[Phase](https://svn.apache.org/repos/asf/incubator/cxf/trunk/api/src/main/java/org/apache/cxf/phase/Phase.java)的概念.相当于说在Interceptor顺序方面加了一个比较大粒度的区别. 比如说,执行的phase顺序为:
pre-invoke, invoke, post-invoke. 具体的Phase优先级可以参考[PhaseManagerImpl](https://svn.apache.org/repos/asf/incubator/cxf/trunk/rt/core/src/main/java/org/apache/cxf/phase/PhaseManagerImpl.java)看看到底有哪些Phases.

所以说,在CXF当中,真正对应(Interceptor角色)的应该是[PhaseInterceptor](https://svn.apache.org/repos/asf/incubator/cxf/trunk/api/src/main/java/org/apache/cxf/phase/PhaseInterceptor.java)
对于每个concrete Interceptor来讲,它一定要指定自己是属于哪个Phase.
这里我们以[MessageSenderInterceptor](https://svn.apache.org/repos/asf/incubator/cxf/trunk/rt/core/src/main/java/org/apache/cxf/interceptor/MessageSenderInterceptor.java) 来作为Concrete Interceptor的例子.

[Message](https://svn.apache.org/repos/asf/incubator/cxf/trunk/api/src/main/java/org/apache/cxf/message/Message.java) (对应Context Object角色),从Message这里你可以获取到你所要的信息,可以说所有的内容都可以从Message里面直接或者间接取到.

[InterceptorChain](https://svn.apache.org/repos/asf/incubator/cxf/trunk/api/src/main/java/org/apache/cxf/interceptor/InterceptorChain.java) (对应Dispatcher角色),在InterceptorChain里,我们可以进行增加,删除一个Concrete Interceptor.同时,也负责根据Phase和ID的顺序来执行各个Interceptor,具体的你可以参考[PhaseInterceptorChain](https://svn.apache.org/repos/asf/incubator/cxf/trunk/api/src/main/java/org/apache/cxf/phase/PhaseInterceptorChain.java)的实现.
我觉得这个InterceptorChain名字起得挺好的,因为如果你看它实现的话,里面用的就是链表来实现顺序的..

虽然我们上面把各个角色都介绍完了,但是当你看CXF的代码时候,你不会看到用InterceptorChain来注册具体实现的Interceptor,那么又是谁来充当这个注册器呢.
在CXF中,还有个类,叫做[InterceptorProvider](https://svn.apache.org/repos/asf/incubator/cxf/trunk/api/src/main/java/org/apache/cxf/interceptor/InterceptorProvider.java),根据名字,我们可以看出,凡是实现这个接口的,都有可能提供Interceptor,也就是说,Interceptor的注册器.
我们来看看有哪些类实现这个接口.
BUS, Client, Service, Binding, Endpoint. 这些地方都有可能提供他们的Interceptor. 记住我们的concrete interceptor实际上就是一个小模块的逻辑处理,比如我有可能是soapBinding,那么我就需要做一些soap binding所需要的特殊逻辑,这个时候,我们就需要在binding这个扩展点加入我们所需要的interceptors来处理. 一般来说,在InterceptorProvider里面注册的时候是没有顺序的. 我们会通过PhaseChainCache来对它构造出一个PhaseInterceptorChain. 然后再来调用doIntercept(Message)方法: 比如如下的代码.(摘自ClientImpl.java)

protected PhaseInterceptorChain setupInterceptorChain(Endpoint endpoint) {

PhaseManager pm = bus.getExtension(PhaseManager.class);

List<Interceptor> i1 = bus.getOutInterceptors();
if (LOG.isLoggable(Level.FINE)) {
LOG.fine("Interceptors contributed by bus: " + i1);
}
List<Interceptor> i2 = endpoint.getOutInterceptors();
if (LOG.isLoggable(Level.FINE)) {
LOG.fine("Interceptors contributed by endpoint: " + i2);
}
List<Interceptor> i3 = getOutInterceptors();
if (LOG.isLoggable(Level.FINE)) {
LOG.fine("Interceptors contributed by client: " + i3);
}
List<Interceptor> i4 = endpoint.getBinding().getOutInterceptors();
if (LOG.isLoggable(Level.FINE)) {
LOG.fine("Interceptors contributed by binding: " + i4);
}
return outboundChainCache.get(pm.getOutPhases(), i1, i2, i3, i4);
}

PhaseInterceptorChain chain = setupInterceptorChain(endpoint);
message.setInterceptorChain(chain);
modifyChain(chain, requestContext);
chain.setFaultObserver(outFaultObserver);
// setup conduit selector
prepareConduitSelector(message);
// execute chain
chain.doIntercept(message);

说到这里, 还需要提一点的就是: 在CXF中,还引入了另外一个概念: [AbstractFeature](https://svn.apache.org/repos/asf/incubator/cxf/trunk/api/src/main/java/org/apache/cxf/feature/AbstractFeature.java), 这个我是从我同事willem的blog中知道了这个概念. 可能对于某个interceptor来说, 他要在IN, OUT, FAULTIN, FAULTOUT都需要这个interceptor,那么用feature.

* A Feature is something that is able to customize a Server, Client, or Bus, typically adding capabilities. For instance, there may be a LoggingFeature which configures one of the above to log each of their messages.
By default the initialize methods all delegate to initializeProvider(InterceptorProvider).  If you're simply adding interceptors to a Server, Client, or Bus, this allows you to add them easily.

现在我们再来理一理CXF当中的Interceptor的关系.
InterceptorProvider 有 IN/OUT 两个 Interceptor的集合.
IN/OUT Interceptor有他固定的PhaseInterceptor.
某一个具体的PhaseInterceptor有他所对应的具体Interceptors.
[ ](http://willem.bokeland.com/blog/794/6089/2007/06/30/209718)
关于CXF中的Interceptor可以参考我同事willem写的两篇文章：
[http://willem.bokeland.com/blog/794/6089/2007/06/30/209717](http://willem.bokeland.com/blog/794/6089/2007/06/30/209717)
[http://willem.bokeland.com/blog/794/6089/2007/06/30/209718](http://willem.bokeland.com/blog/794/6089/2007/06/30/209718)
------------
参考文档:
<Pattern oriented software architecture volume2>


