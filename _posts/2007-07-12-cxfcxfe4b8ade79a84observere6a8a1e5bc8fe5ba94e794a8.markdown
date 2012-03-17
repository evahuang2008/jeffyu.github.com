---
date: '2007-07-12 09:03:20'
layout: post
slug: cxfcxf%e4%b8%ad%e7%9a%84observer%e6%a8%a1%e5%bc%8f%e5%ba%94%e7%94%a8
status: publish
title: '[CXF]CXF中的Observer模式应用'
wordpress_id: '20'
categories:
- Chinese
- SOA
- Web Service
tags:
- CXF
- Design Patterns
---

在CXF当中,其中在Transport这一层接收信息里,采用了Observer的模式,我记得我刚前段时间刚看这段代码的时候,
老感觉跟Observer模式对不上号...现在,我明白了,原来他是一个简化版的Observer模式.
先看下典型Observer模式 



	
  * **Subject**** **

	
    * knows its observers. Any number of
Observer objects may observe a subject

	
    * provides an interface for attaching and detaching Observer objects.




	
  * **ConcreteSubject**** **

	
    * stores state of interest to
ConcreteObserver

	
    * sends a notification to its observers when its state changes




	
  * **Observer**** **

	
    * defines an updating interface for objects that should be notified of changes in a subject.




	
  * **ConcreteObserver** 

	
    * maintains a reference to a
ConcreteSubject object

	
    * stores state that should stay
consistent with the subject's

	
    * implements the Observer updating interface to keep its state consistent
with the subject's





在对号入座前,先讲讲我们解决的这个问题场景.
我们要通过Transport这一层来传送Message(消息),我们假设以HTTP传输协议来做例子.
在CXF当中,有两个概念来对Transport进行了封装.
1: Conduit 可以理解为信息发送地,发送一条信息需要经过两个步骤:
1) conduit.prepare(message);
2) conduit.close(message);
2: Destination 可以理解为目的地.

接下来,我们来看看是怎么应用Observer模式的.

Observable: (对应的是Subject)
public interface Observable {
void setMessageObserver(MessageObserver observer);
}

MessageObserver: (对应的是Observer)
public interface MessageObserver {
void onMessage(Message message);
}

Conduit/Destination (对应ConcreteSubject)
ClientImpl/ChainInitiationObserver (对应ConcreteObserver)

可以说,在CXF当中应用的Observer模式有点不一样.
1) 我们可以从Observable类中看出,他只能注册一个,以往典型的Subject是支持多于Observer注册的.
2) 我们不能在Subject中看到他调用Observer的方法.实际上呢,他是隐藏于ConcreteSubject类当中.
这里我们来看一个ConcreteSubject( ServletDestination )
protected void doMessage(MessageImpl inMessage) throws IOException {
try {
setHeaders(inMessage);
inMessage.setDestination(this);
incomingObserver.onMessage(inMessage);
} finally {
if (LOG.isLoggable(Level.FINE)) {
LOG.fine("Finished servicing http request on thread: " + Thread.currentThread());
}
}
}

当你读CXF的源代码的时候,你会发现尽管Conduit也支持Observable,但是目前代码出好像还没有具体的应用.
其实这是一个简单版本的Observer模式,而且并不是一个one-to-many,而是one-to-one的.
-----------------------
参考文档:
[http://www.dofactory.com/Patterns/PatternObserver.aspx](http://www.dofactory.com/Patterns/PatternObserver.aspx)


