---
date: '2007-08-26 16:18:26'
layout: post
slug: '%e7%ae%80%e8%af%b4ws-addressing'
status: publish
title: 简说WS-Addressing
wordpress_id: '9'
categories:
- Web Service
---

WS-Addressing主要是做什么呢?我们先来看一个普通的,没有加入WS-A的SOAP信息:  
  
A SOAP 1.2 message, without WS-Addressing, sent over HTTP transport looks like:  
(001) POST /fabrikam/Purchasing HTTP 1.1/POST  
(002) Host: example.com  
(003) SOAPAction: http://example.com/fabrikam/SubmitPO  
(004)  
(005) <S:Envelope xmlns:S="http://www.w3.org/2003/05/soap-envelope"  
xmlns:wombat="http://wombat.org/">  
(006) <S:Header>  
(007) <wombat:MessageID>  
(008) uuid:e197db59-0982-4c9c-9702-4234d204f7f4  
(009) </wombat:MessageID>  
(010) <S:Header>  
(011) <S:Body>  
(012) ...  
(013) </S:Body>  
(014) </S:Envelope>  
Line (001) - (003) shows the HTTP transport headers. Line (005) - (014) shows the SOAP message in HTTP body.  
这里,没有WS-A的情况下,所有Transport层的信息都没有放到SOAP的Message里面.   
我们来看看WS-A存在的目的:  
SOAP does not provide a standard way to specify where a message is
going, how to return a response, or where to report an error. Those
details have historically been left up to the transport layer. For
example, when a standard SOAP request is sent over HTTP, the URI of the
HTTP request serves as the message's destination.  
Addressing at the transport level is sufficient for many existing
services, but it has been a limiting factor in the development of
others. WS-Addressing defines standard ways to route a message over
multiple transports or direct a response to a third party.  
  
简单来说呢?就是想把本来是在Transport这一层的信息写入到SOAP的信息头<Head>中.下面可以看下有了WS-A后的SOAP信息:  
A SOAP 1.2 message, with WS-Addressing, sent over HTTP transport looks like:  
(001) POST /fabrikam/Purchasing HTTP 1.1/POST  
(002) Host: example.com  
(003) SOAPAction: http://example.com/fabrikam/SubmitPO  
(004)  
(005) <S:Envelope xmlns:S="http://www.w3.org/2003/05/soap-envelope"  
xmlns:wsa="http://www.w3.org/2005/08/addressing/">  
(006) <S:Header>  
(007) <wsa:MessageID>  
(008) uuid:e197db59-0982-4c9c-9702-4234d204f7f4  
(009) </wsa:MessageID>  
(010) <wsa:To>  
(011) http://example.com/fabrikam/Purchasing  
(012) </wsa:To>  
(013) <wsa:Action>  
(014) http://example.com/fabrikam/SubmitPO  
(015) </wsa:Action>  
(016) <S:Header>  
(017) <S:Body>  
(018) ...  
(019) </S:Body>  
(020) </S:Envelope>  
  
在这个WS-Addressing规范中,主要引入了两个东西: 1. Endpoint References (EPR) 2. Message addressing properties (MAPs).  如[1]中文章所说: 可以把EPR想象成具体的某个地址,比如说某市某县某胡同的2号楼. 而把MAPs想象成地址的布局.比如有收信地址,收信人.  
  
把这些Transport的信息放入Soap信息中,有个好处就是能实现Transport-neutral,因为我们传递的是SOAP信息.  
  
参考资料:   
[1] [http://dev2dev.bea.com/pub/a/2005/01/ws_addressing_intro.html](http://dev2dev.bea.com/pub/a/2005/01/ws_addressing_intro.html)  
[2] [http://www.javapassion.com/webservices/wsaddressing.pdf](http://www.javapassion.com/webservices/wsaddressing.pdf)  

