---
date: '2007-11-13 04:32:00'
layout: post
slug: ims-rolled-out-its-0-1-version
status: publish
title: IMS rolled out its 0.1 version
wordpress_id: '167'
categories:
- Java
- SOA
- Web Service
tags:
- CXF
- Spring
---

I created a little project at [Google Code](http://code.google.com/p/blogging/), it rolled out its 0.1 version in 5 Nov 2007.. In this release, it demonstrates below functionalities (copied from release note)..

ims-core module



	
  1. Using JAXWS + JAXB (CXF runtime) to publish web service.

	
  2. Using Spring acegi as web service authorization.

	
  3. Using ws-security (plain password) as authentication.

	
  4. Using Spring AOP transaction.

	
  5. Using DBUnit to do the dao unit test.

	
  6. Using easymock to do the service layer unit test.

	
  7. Using cxf local transport to do the web service unit test.


ims-web module



	
  1. Using CXF wsdl2java (codegen tool) to generate the stub.

	
  2. Using JAXWS customization to use the java.util.Date instead of XMLGregorianCalendar.

	
  3. Using JAXWS + JAXB (CXF runtime) to access the web service.

	
  4. Using Spring acegi web application filter and Jcaptcha as security implementation.

	
  5. Using div + css as layout design implementation.


You can download the source code from [here](http://blogging.googlecode.com/files/ims-0.1-src.zip), since its war size is about 20M, I don't provide it in the website, you need to refer to the README.txt in the source code to build it, it is quite straightforward to get it working.. (actually you just need to set up database manually, and then update the database connection config file appropriately).

I've also created some tasks for 0.2 release or future in the [issue page](http://code.google.com/p/blogging/issues/list), if you want to join this project, drop me a mail, (or add a comment here), I would add you as a commiter.
