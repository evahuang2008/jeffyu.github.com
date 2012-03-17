---
date: '2009-07-24 19:38:00'
layout: post
slug: code-against-web-service
status: publish
title: code against web service.
wordpress_id: '240'
categories:
- Java
- Web Service
---

Have worked on the web service area since when I joined the IONA in 2007, specifically, from the time that I started working on the [Apache CXF project](http://cxf.apache.org/). Although I've been working on web service stuff about 3 years, I still thought it is not an easy job to code against web service. these days, some of my friends ask me about the web service, from concepts to its hello-world example. So I think it worths to do a blog entry for people to get started with web service projects.  
  
And then I remembered that [Glen](http://www.jroller.com/gmazza/) has did a ton of great blog entries about web service stack.(CXF, Metro and even Aix2 lately), and all of them are very detail, step-to-step. So here we go, we pick some of Glen's blog entries to get you started on web service.  
  
It is better that you get some concepts like the WSDL, SOAP, XSD, and read the JAXWS spec if time is allowed, just get a rough idea on it is ok, before we code against web service.  
  
Firstly, let's see the[ Creating a WSDL-first web service with Apache CXF or GlassFish Metro](http://www.jroller.com/gmazza/entry/creating_a_wsdl_first_web1) entry, it is our 'hello world' example.  
  
Want to see the SOAP Message that was transferred on the wire? you have couple options for this. One is to use tools like [Apache TCP Monitor](http://wso2.org/blog/saliya/3938) or [wireshark](http://www.jroller.com/gmazza/entry/wireshark_usage_for_cxf). Another option is to use the JAXWS handler(similar to interceptor) mechanism, which is a very important feature in the spec. See [Glen's JAX-WS handler blog entry](http://www.jroller.com/gmazza/entry/adding_jax_ws_handlers_to) to try it out.  
  
So you saw the soap message on the wire, how can we do with the binary stuff, that is what MTOM is for, you can see ["Returning PDFs from Web Services using MTOM and Apache FOP" blog entry](http://www.jroller.com/gmazza/entry/using_mtom_and_apache_fop) for its usage and detail.  
  
If you are a person who like the Test-Driven Development, then don't miss the '[creating junit test case for web service](http://www.jroller.com/gmazza/entry/writing_junit_test_cases_for)' blog entry.  
  
Security is a big concern in the enterprise development, so that is what ws-security spec for. firstly, you could read the '[Using SSL and Basic Authentication with web services (Tomcat or WebLogic)](http://www.jroller.com/gmazza/entry/setting_up_ssl_and_basic)' for its basic usage, and then go on reading the [username token profile blog entry](http://www.jroller.com/gmazza/entry/implementing_ws_security_using_usernametokens), [Implementing WS-Security with public key certificates for Metro-based web services](http://www.jroller.com/gmazza/entry/implementing_ws_security_with_pki). Also can read the ' [Using OpenSAML in JAX-WS Handlers](http://www.jroller.com/gmazza/entry/using_the_opensaml_library_in)' if you are interested in the SAML token profile in ws-security.  
  
I think that should be enough for you to get it started, you can explore more on the [Glen's website](http://www.jroller.com/gmazza/), you would find more entries about web service.
