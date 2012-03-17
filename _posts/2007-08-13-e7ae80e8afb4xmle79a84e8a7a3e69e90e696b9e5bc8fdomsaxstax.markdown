---
date: '2007-08-13 06:56:25'
layout: post
slug: '%e7%ae%80%e8%af%b4xml%e7%9a%84%e8%a7%a3%e6%9e%90%e6%96%b9%e5%bc%8fdomsaxstax'
status: publish
title: 简说XML的解析方式(DOM,SAX,StAX)
wordpress_id: '14'
categories:
- Java
---

一般来说,解析XML文件存在着两种方式,一种是event-based API，比如说象SAX,XNI. 第二种是tree-based API,比如说DOM,JDOM,DOM4j等等. 一般来说,读取配置文件时,我们一般比较喜欢应用tree-based API这种方式,就是把xml文件读入,变成DOM形式的一棵树,然后进行查找，获取自己说想要的东西. 但是,这种方式有个缺点,那就是如果你这个XML文件很大的话,你需要占用很大的内存.  
所以对于很大的一个xml文件,又不需要进行随机查找的时候,比较适合采用event-based API,那就是说他解析xml文件,如果是START_ELEMENT，那么他就调用startElement()的回调方法..他遍历过了就过了，不能再回去.   
在event-based API中又存在两种方式: 一个是PUSH的方式,就比如说是SAX. 另外一种是PULL的方式,比如StAX.   
怎么来理解PUSH和PULL的区别呢. 先假设有这么三个角色: application, xmlFile, xmlParser. 那么,如果我们采用PUSH的方式,步骤为:  
 1. 创建一个xmlParser.  
 2. 把我们的application处理xml的注册到xmlParser.  
 3. xmlParser遍历xmlFile,然后来调用application.  
这里面,用的是Observer的模式,就是接收到event的时候,去调用event的callback函数, 这里面有个很不好的地方就是,你application反而是被Parser控制了.  
于是,就出现了PULL方式的解析.  
 1. 创建一个xmlParser  
 2. xmlParser打开一个xmlFile  
 3. application调用这个xmlParser, 来获取xmlParser打开xmlFile所得到的一系列event.  
这里,用到了Iterator的模式. 最主要的一点是: 这个时候application控制了xmlParser.  
StAX有两种API,一种是cursor-based,一种是iterator-based. 这两种详细的比较参考: [http://java.sun.com/webservices/docs/1.6/tutorial/doc/SJSXP3.html#wp102139](http://java.sun.com/webservices/docs/1.6/tutorial/doc/SJSXP3.html#wp102139)  
  
这里,SAX和StAX的另外一点区别是: SAX只能读xml文件. StAX不但能读xml文件,而且还能写xml文件.  
  
参考资料:  
[An Introduction to StAX](http://www.xml.com/pub/a/2003/09/17/stax.html?page=1)  
[Having Good SAX with Java](http://www.topxml.com/java/articles/sax_xml/default.asp)  

