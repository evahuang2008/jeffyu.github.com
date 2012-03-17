---
date: '2009-08-11 18:21:00'
layout: post
slug: publishing-web-service-in-jboss-esb
status: publish
title: Publishing web service in JBoss ESB
wordpress_id: '247'
categories:
- ESB
- Java
- Web Service
tags:
- JBossESB
---

As of this writing, [JBoss ESB 4.6](http://www.jboss.org/jbossesb) has two ways of publishing web service for ESB service.
1. Using JSR 181 annotation to do the web service publish and use SOAPProcessor action to connect it in ESB.
2. Providing the in,out, fault xsd schema to generate the wsdl dynamically and publish the web service.
These two ways are not exclusive, it is for different usage:
1. The first one is using JBossWS to publish the annotated Java service, and then using the SOAPProcessor to be a thin wrapper for the existed web service.
2. The second one, which we called EBWS(Endpoint Web Service), is asking developers to provide the in,out,fault xsd if it is required, And then uses these xsds, plus the service info (like service name, category etc) that were defined in the jboss-esb.xml to generate the wsdl and publish the web service.

The JBoss ESB distribution has both quick start examples for these two scenarios. We will examine them in order shortly, quickstart/webservice_producer sample is using the first approach that we've described, while the quickstart/publish_as_webservice is the EBWS as we said.

web service producer using SOAPProcessor

We will examine the first approach, below are the steps that is required to publish a web service in ESB.

1.**Add the impl class with jsr 181 annotation**
Lets see the GoodbyeWorldWS.java class, this is the class that is supposed to expose as web service.

[java]
@WebService(name = "GoodbyeWorldWS", targetNamespace="http://webservice_producer/goodbyeworld")
public class GoodbyeWorldWS {
@WebMethod
public String sayGoodbye(@WebParam(name="message") String message) {


   Message esbMessage = SOAPProcessor.getMessage();
   if(esbMessage != null) {
       System.out.println("**** SOAPRequest perhaps mediated by ESB:n" + esbMessage.getBody().get());
   }
   System.out.println("Web Service Parameter - message=" + message);
   return "... Ah Goodbye then!!!! - " + message;
}
....
}
[/java]


You can see that we are using the jsr181 annotation to expose it as web service. Noted that we are using the SOAPProcessor class to get the incoming soap message just for demonstration, you don't have to use it in this class's implementation.



2.**Add web.xml to deploy it in servlet container**
In the $webservice_producer/war/resources/WEB-INF/web.xml, it looks like

[xml]
<servlet-name>GoodbyeWorldWS</servlet-name>
   <servlet-class>org.jboss.soa.esb.samples.quickstart.webserviceproducer.webservice.GoodbyeWorldWS</servlet-class>
</servlet>

<servlet-mapping>
   <servlet-name>GoodbyeWorldWS</servlet-name>
   <url-pattern>/GoodbyeWorldWS</url-pattern>
</servlet-mapping>
[/xml]


Typically, we can build a war file that includes both web.xml and the GoodbyeWorldWS.class, and it should be enough to be published as a web service through JBoss WS. since we are trying to access the web service through our ESB, so we need to define an extra file (jboss-esb.xml) in our case.



3.**Add SOAPProcessor in the jboss-esb.xml**
In the jboss-esb.xml service section, we need to use the SOAPProcessor as following:

[xml]
<action name="JBossWSAdapter" class="org.jboss.soa.esb.actions.soap.SOAPProcessor">
    <property name="jbossws-endpoint" value="GoodbyeWorldWS"/>
</action>
[/xml]


Here the "jbossws-endpoint" property should be referred to published web service servlet name.
*Tip: There's one optional property "rewrite-endpoint-url" which is not used in this sample. This property is to support load balance on HTTP endpoints.



4.**pack them in esb and war archive**
The last step for us it to pack them and then deploy. The war file will include all needed classes and web.xml to publish web service. The esb file will include all needed esb files, like jboss-esb.xml etc. You can bundle the war file into esb archive, which is the way that sample uses.

Until now, we've described all of important steps. Next, we will deploy this esb archive into ESB server, you can see the wsdl file at: http://localhost:8080/contract/ (This is offered by ESB), or you can see the one from http://localhost:8080/jbossws/services, that is offered by JBoss WS.

5.**Add the client to do the test**
So, we've completed our server side work. In the example, we defined three gateway for this web service, for the simplicity, we will just look at the one uses JBR gateway to do the test in our client. Here is the client code:

[java]
private void sendMessageToJBRListener(String protocol, int port, String message) throws Throwable {
   String locatorURI = protocol + "://localhost:" + port;
   InvokerLocator locator = new InvokerLocator(locatorURI);
   System.out.println("Calling JBoss Remoting Listener using locator URI: " + locatorURI);


   Client remotingClient = null;
   try {
       remotingClient = new Client(locator);
       remotingClient.connect();

       // Deliver the message to the listener...
       Object response = remotingClient.invoke(message);
       System.out.println("JBR Class: " + response.getClass().getName());
       System.out.println("Response from JBoss Remoting Listener '" + locatorURI + "' was '" + response + "'.");
   } finally {
       if(remotingClient != null) {
           remotingClient.disconnect();
       }
   }
}
[/java]


We are using the following soap message in our client as input.

[xml]
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:good="http://webservice_producer/goodbyeworld">
<soapenv:Header/>
<soapenv:Body>
<good:sayGoodbye>
    <message&gt;Goodbye!!
 </good:sayGoodbye>
</soapenv:Body>
</soapenv:Envelope>
[/xml]


Run the "ant deploy" to deploy the server into ESB server; Run the 'ant runtest', you would get following result:

[xml]
saygoodbye_over_http:
[echo] Invoking a JBossWS Endpoint over HTTP (via JBoss ESB).
[java] Calling JBoss Remoting Listener using locator URI: http://localhost:8765
[java] JBR Class: java.lang.String
[java] Response from JBoss Remoting Listener 'http://localhost:8765' was '<env:Envelope xmlns:env='http://schemas.xmlsoap.org/soap/envelope/'><env:Header></env:Header><env:Body><ns2:sayGoodbyeResponse xmlns:ns2="http://webservice_producer/goodbyeworld"><return>... Ah Goodbye then!!!! - Goodbye!!</return></ns2:sayGoodbyeResponse></env:Body></env:Envelope>'.
[/xml]


ESB End Point Web Service



Now, we will see the End Point Web Service, the corresponding example is publish_as_webservice in the JBoss ESB distribution. Lets also see it step by step.

1.**The Web Service server class**
firstly, take a look at the server impl class.

[java]
public class ESBWSListenerAction extends AbstractActionLifecycle
{
protected ConfigTree _config;


public ESBWSListenerAction(ConfigTree config)
{
   _config = config;
}

public Message displayMessage(Message message) throws Exception
{
.......
}
[/java]


Is it just an ordinary ESB action? right, it is. This is totally different from the first one that we saw earlier, we do not have annotation, we used the ESB's Message Object as input/output parameter.



* Note: In this approach, you can view it as Dispatch/Provider way that we used to have in JAX-WS, it means you deal with the raw soap message directly, the server doesn't help you do the unmarshall work, this is also a very big difference from the first approach.

2. ** define request, response, fault xsd**
In this example, we just define the in and out xsd. it is as following:
request.xsd

[xml]
<xs:schema version="1.0" targetNamespace="http://www.jboss.org/sayHi" xmlns:x1="http://www.jboss.org/sayHi"  xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified">
<xs:element name="sayHi" type="x1:sayHi"/>
<xs:complexType name="sayHi">
<xs:sequence>
 <xs:element name="arg0" type="xs:string" minOccurs="1"/>
</xs:sequence>
</xs:complexType>
</xs:schema>
[/xml]


Response.xsd

[xml]
<xs:schema version="1.0" targetNamespace="http://www.jboss.org/sayHi" xmlns:x1="http://www.jboss.org/sayHi"  xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified">
<xs:element name="sayHiResponse" type="x1:sayHiResponse"/>
<xs:complexType name="sayHiResponse">
<xs:sequence>
 <xs:element name="arg0" type="xs:string" minOccurs="0"/>
</xs:sequence>
</xs:complexType>
</xs:schema>
[/xml]


We won't show the fault.xsd for the simplicity.



3.** Add xsd file in the jboss-esb.xml**
After we've defined the xsd file, we will add it in the jboss-esb.xml like following.

[xml]
<actions  inXsd="/request.xsd" outXsd="/response.xsd" faultXsd="/fault.xsd">
              <action name="action" class="org.jboss.soa.esb.samples.quickstart.publishAsWebservice.ESBWSListenerAction" process="displayMessage"/>
       </actions>
[/xml]


*Tip: Here it use the 'service name' + hard code name, like 'Binding' for binding, 'Op' for operation name in the generated wsdl. Refer to ESBServiceEndpointInfo class for its detail.



4.**build it as an esb artifact and deploy**
The last step is to build them as an esb archive and deploy it into the ESB server, as same as the first approach, you can see its wsdl file through either http://localhost:8080/contract or http://localhost:8080/jbossws/services.

The client is as same as the first one(apart from the soap message and url), so I won't show it again.

Summary

You see two approaches to help you publish web service in JBoss ESB. At first glance, you might think EBWS(second approach here) is simple as you don't need to build the war file etc. But I would say the first approach is more common in the real use case.

[Acknowledgement]
I'd like to thank my colleague [Jim Ma](http://maerqiang.blogspot.com/) for help me explain these two approaches on publishing web service.

[Reference]
1. [JBoss ESB website](http://www.jboss.org/jbossesb).
2. [JBoss ESB Webservice Producer.](http://www.mastertheboss.com/en/soa-a-esb/137-jboss-esb-webservice-producer.html)
