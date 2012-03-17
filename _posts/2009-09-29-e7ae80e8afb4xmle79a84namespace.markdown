---
date: '2009-09-29 04:56:00'
layout: post
slug: '%e7%ae%80%e8%af%b4xml%e7%9a%84namespace'
status: publish
title: 简说XML的Namespace.
wordpress_id: '257'
categories:
- Chinese
- Java
tags:
- XML
---

这是一个简单的XML 101的贴子,写下以帮助自己记忆. ;-)

XML的namespace属性类似java中的packagename,是为了使得唯一性.在xml schema, wsdl or bpel中,我们一般会看到如下的定义

    
    <definitions name="echoWsdl"        targetNamespace="http://www.jboss.org/jeffyu/bpel/wsdl"        xmlns:tns="http://www.jboss.org/jeffyu/bpel/wsdl"        xmlns:plnk="http://docs.oasis-open.org/wsbpel/2.0/plnktype"        xmlns="http://schemas.xmlsoap.org/wsdl/"        xmlns:xsd="http://www.w3.org/2001/XMLSchema"        xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/">


这里面,就要涉及到我们所要谈的default namespace 和 targetNamespace.
先看普通的定义,比如:

    
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"


这样定义后,我们就可以在wsdl文件中写 xsd:string来引用XMLSchema所定义的数据类型,用java理解,可以理解是引入了某个package.

接着我们来看default namespace.

    
    xmlns="http://schemas.xmlsoap.org/wsdl/"


这里,我们可以看到它不像我们上个例子那样定义前缀,那么它就是这个xsd/wsdl/bpel文件中的默认namespace,(注意默认的namespace只适用于没有前缀的element,对attribute不起作用),一个xsd/wsdl文件中只能有一个默认的namespace.

最后,我们再来看targetNamespace.

    
    targetNamespace="http://www.jboss.org/jeffyu/bpel/wsdl"


定义targetNamespace的目的是对在这个xsd/wsdl中自己定义的element(s)归到这个namespace里,也就是说,如果外部的文件要调用这里面的element,那么就需要用这个targetNamespace来调用.所以这也是,当你定义了一个xsd,你要写一个相对应于这个xsd的xml,就需要这个xsd里面的targetNamespace来做校验,看xml是否符合xsd的定义.

[Reference]
1. http://www.coderanch.com/t/148016/Web-Services-Certification-SCDJWS/certification/Differences-between-targetNamespace-default-namespace
2. http://www.oracle.com/technology/pub/articles/srivastava_namespaces.html
