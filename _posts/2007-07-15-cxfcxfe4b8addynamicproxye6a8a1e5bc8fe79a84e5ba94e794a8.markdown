---
date: '2007-07-15 09:55:46'
layout: post
slug: cxfcxf%e4%b8%addynamicproxy%e6%a8%a1%e5%bc%8f%e7%9a%84%e5%ba%94%e7%94%a8
status: publish
title: '[CXF]CXF中DynamicProxy模式的应用'
wordpress_id: '19'
categories:
- Chinese
- SOA
- Web Service
tags:
- CXF
- Design Patterns
---

在讲Dynamic Proxy模式之前,可能需要理解下[Proxy模式](http://www.dofactory.com/Patterns/PatternProxy.aspx), 经典的Proxy模式里,我们一般需要建立个Proxy的类来包含真正的实现类,而Client端调用的时候,则是去调用Proxy的类,这样Proxy类里就可以控制权限等问题.
在CXF当中用的是JDK自带的Dynamic Proxy,为什么叫Dynamic Proxy呢,因为他在编译的时候,并没有那个Proxy类,而是在运行时期生成一个Proxy类.
在看CXF代码应用Dynamic Proxy之前,来看一个简单的实现. 

Interface类：
public interface HelloInterface {
public void sayHi(String name) throws Exception;
}

Impl类:
public class HelloInterfaceImpl implements HelloInterface {
public void sayHi(String name) throws Exception {
System.out.println("This is real HelloInterfaceImpl");
System.out.println("You Inovke sayHi with name : [" + name +"]");
}
}

Proxy的实现..
public class HelloInterfaceProxy implements InvocationHandler {
private Object object;
public static Object getInstance(Object o) {
return Proxy.newProxyInstance(o.getClass().getClassLoader(), o.getClass().getInterfaces(), new HelloInterfaceProxy(o));
}
private HelloInterfaceProxy(Object o) {
object = o;
}
public Object invoke(Object arg0, Method method, Object[] arg2) throws Throwable {
System.out.println("It was interceptored by the HelloInterfaceProxy class firstly");
return method.invoke(object, arg2);
}
}

Client端的调用:
HelloInterfaceImpl impl = new HelloInterfaceImpl();
HelloInterface hello = (HelloInterface)HelloInterfaceProxy.getInstance(impl);
hello.sayHi("Jeff");
运行结果:
It was interceptored by the HelloInterfaceProxy class firstly
This is real HelloInterfaceImpl
You Inovke sayHi with name : [Jeff]

在Client端的调用程序中,我们所获得的hello是一个HelloInterfaceProxy的类,并不是指到真正的HelloInterfaceImpl类.
这里,我们并没有一个真正的HelloInterfaceProxy的类,因为他是在运行时期产生的,所以我们把这个模式叫做Dynamic Proxy.

在CXF当中,实现InvocationHandler的类是: ClientProxy
Interface呢,就是SEI: 比如说是: Greeter.
真正的实现类,是GreeterImpl.
我们在客户端所获取到的Greeter实现,实际上是个GreeterProxy对象.

下面这是获取到客户端实现:
SOAPService ss = new SOAPService(wsdlURL, SERVICE_NAME);
Greeter port = ss.getSoapPort();


