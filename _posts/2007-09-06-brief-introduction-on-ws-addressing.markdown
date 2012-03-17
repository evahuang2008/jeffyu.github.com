---
date: '2007-09-06 19:11:00'
layout: post
slug: brief-introduction-on-ws-addressing
status: publish
title: Brief introduction on WS-Addressing
wordpress_id: '147'
categories:
- SOA
---

what is WS-Addressing? Before answer this question, lets see a soap message without WS-A.  
  
A SOAP 1.2 message, without WS-Addressing, sent over HTTP transport looks like:  


  
(001) POST /fabrikam/Purchasing HTTP 1.1/POST  
(002) Host: example.com  
(003) SOAPAction: http://example.com/fabrikam/SubmitPO  
(004)   
(005)  <s:envelope s="http://www.w3.org/2003/05/soap-envelope" wombat="http://wombat.org/">  
(006) <s:header>  
(007) <wombat:messageid>  
(008) uuid:e197db59-0982-4c9c-9702-4234d204f7f4  
(009) </wombat:messageid>  
(010) <s:header>  
(011) <s:body>  
(012) ...  
(013) </s:body>  
(014) </s:envelope>  


  
Line (001) - (003) shows the HTTP transport headers. Line (005) - (014) shows the SOAP message in HTTP body.  
  
Here we can see, we didn't put any transport information in the SOAP message without the WS-A.  
  
The Intent of WS-Addressing:  
  


  
SOAP does not provide a standard way to specify where a message is going, how to return a response, or where to report an error. Those details have historically been left up to the transport layer. For example, when a standard SOAP request is sent over HTTP, the URI of the HTTP request serves as the message's destination.  
Addressing at the transport level is sufficient for many existing services, but it has been a limiting factor in the development of others. WS-Addressing defines standard ways to route a message over multiple transports or direct a response to a third party.  


  
  
Simply put, we want to put the transport information in the SOAP message Header Part. lets see below SOAP message with WS-Addressing feature.  
  
A SOAP 1.2 message, with WS-Addressing, sent over HTTP transport looks like:  


  
(001) POST /fabrikam/Purchasing HTTP 1.1/POST  
(002) Host: example.com  
(003) SOAPAction: http://example.com/fabrikam/SubmitPO  
(004)  
(005) <s:envelope s="http://www.w3.org/2003/05/soap-envelope" wsa="http://www.w3.org/2005/08/addressing/">  
(006) <s:header>  
(007) <wsa:messageid>  
(008) uuid:e197db59-0982-4c9c-9702-4234d204f7f4  
(009) </wsa:messageid>  
  
(010) <wsa:to>  
(011) http://example.com/fabrikam/Purchasing  
(012) </wsa:to>  
(013) <wsa:action>  
(014) http://example.com/fabrikam/SubmitPO  
(015) </wsa:action>  
(016) <s:header>  
(017) <s:body>  
(018) ...  
(019) </s:body>  
(020) </s:envelope>  


  
  
In the WS-Addressing specification, it has introduced two concepts:  
1. Endpoint Reference (EPR)  
2. Message Addressing Properties (MAPs)  
Like an article[1] says: we can think the EPR as the concrete address. consider the MAPs as envelop layout, such as it has receiver etc. The benefits of the WS-Addressing is that we put the transport in the SOAP message, so we are able to deal with message across multiple transports.   
  
Reference:  
[1] [http://dev2dev.bea.com/pub/a/2005/01/ws_addressing_intro.html](http://dev2dev.bea.com/pub/a/2005/01/ws_addressing_intro.html)  
[2] [http://www.javapassion.com/webservices/wsaddressing.pdf](http://www.javapassion.com/webservices/wsaddressing.pdf)  
  
You can see the chinese version of this article [here](http://jeffyuchang.spaces.live.com/blog/cns!4001C604AF3F011!480.entry).
