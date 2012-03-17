---
date: '2007-07-14 09:10:33'
layout: post
slug: cxfcxf%e4%b8%ad%e7%9a%84abstractfactory%e6%a8%a1%e5%bc%8f%e5%ba%94%e7%94%a8
status: publish
title: '[CXF]CXF中的AbstractFactory模式应用.'
wordpress_id: '22'
categories:
- Chinese
- SOA
- Web Service
tags:
- CXF
- Design Patterns
---

在CXF当中,Abstract Factory模式随处可见.这里我们就以BindingFactory为例子,来介绍CXF当中是怎么使用Abstract Factory模式的.
首先,我们来看下Abstract Factory模式:
[意图]
Provide an interface for creating families of related or dependent
objects without specifying their concrete classes.
[参与者和职责]



	
  * **AbstractFactory** 

	
    * declares an interface for operations that create abstract products




	
  * **ConcreteFactory**** **

	
    * implements the operations to create concrete product objects




	
  * **AbstractProduct**

	
    * declares an interface for a type of product object




	
  * **Product** ****

	
    * defines a product object to be created by the corresponding concrete factory

	
    * implements the AbstractProduct interface





下面我们来看CXF中的代码:
[BindingFactory](https://svn.apache.org/repos/asf/incubator/cxf/trunk/api/src/main/java/org/apache/cxf/binding/BindingFactory.java): (对应AbstractFactory角色)

public interface BindingFactory {
Binding createBinding(BindingInfo binding);
BindingInfo createBindingInfo(Service service, String namespace, Object configObject);
void addListener(Destination d, Endpoint e);
}

[SoapBindingFactory ](https://svn.apache.org/repos/asf/incubator/cxf/trunk/rt/bindings/soap/src/main/java/org/apache/cxf/binding/soap/SoapBindingFactory.java)(对应Concrete Factory角色)
Binding, BindingInfo (对应Abstract Product角色)
SoapBinding, XMLBinding, SoapBindingInfo(对应Concrete Product角色).

举第2个例子在CXF中使用这个模式的.

Databinding (对应Abstract Factory角色)
JAXBDatabinding, AegisDatabinding, SourceDataBinding (对应Concrete Factory角色)
DataReader, DataWriter (对应Abstract Product角色)
NodeDataReader, XMLStreamDataReader, NodeDataWriter... (对应Concrete Product角色)

虽然说在这里,Databinding类我们用的是interface而不是用abstract,但是从使用的意义和用途,我们仍可断定是Abstract Factory模式.

参考资料:
-------------------
[http://www.dofactory.com/Patterns/PatternAbstract.aspx](http://www.dofactory.com/Patterns/PatternAbstract.aspx)


