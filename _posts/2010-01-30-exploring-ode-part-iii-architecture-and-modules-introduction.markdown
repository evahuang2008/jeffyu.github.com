---
date: '2010-01-30 01:16:00'
layout: post
slug: exploring-ode-part-iii-architecture-and-modules-introduction
status: publish
title: 'Exploring ODE Part III: architecture and modules introduction'
wordpress_id: '271'
categories:
- BPM
- Java
tags:
- ODE
- RiftSaw
---

In this blog entry, we will continue to explore the ODE source code. Typically, we should see the ODE's architecture in our first part of this series, but here I put it in the third part, as at that time, I was just trying to write a blog entry about the ODE's inner model about bpel file, didn't thought I will write this as a series.

Anyway, lets see the ODE's architecture diagram, which I copied it from the [ODE's architecture wiki page](http://ode.apache.org/architectural-overview.html).
[![](http://jeff.familyyu.net/wp-content/uploads/2011/01/odearchitecture1.png?w=300)](http://jeff.familyyu.net/wp-content/uploads/2011/01/odearchitecture1.png)
On [our first part](http://jeff.familyyu.net/2010/01/exploring-apache-ode-source-code-part-i.html), we look at the bpel compiler module, and we look at the JACOB framework on [our second part](http://jeff.familyyu.net/2010/01/exploring-apache-ode-source-code-part.html).

In this part, we will try to make an introduction to ODE's modules:

ODE core modules
1.bpel-api: It contains the api definition for ODE, some important packages are: 




	
  * org.apache.ode.bpel.iapi: this is for integration interfaces, like Axis2 module will implement it.

	
  * org.apache.ode.bpel.rapi: these interfaces are for runtime api that are implemented in the bpel-runtime module.

	
  * org.apache.ode.bpel.pmapi: this is for the process management.

	
  * org.apache.ode.bpel.evt: this is for the event.


2. bpel-runtimes: this module takes care of implementing the Bpel's Activities, like INVOKE, REPLY, WAIT by extending the JacobRunnable Object, also it is the place that includes the internal model for compiled Bpel file, and Channel definition. You would notice that it has v1 and v2 packages, thats for ODE 1.x and ODE 2.x respectively.
3. bpel-dao: this module is the API for DAO layer, currently, it doesn't include the DAO API for process store.
4. dao-jpa: currently it is the openjpa implementation for DAO.
5. dao-jpa-db: This is the DDL script for openjpa's impl.
6. dao-hibernate, dao-hibernate-db: these two are the Hibernate's impl for DAO, and its DDL scripts.
7. bpel-schemas: this is module that use xmlbeans to generate Java objects from xsd schemas, they are: deploymentDescriptor, (dd.xsd), pmapi.xsd (Process Management API), schedules.xsd, context.xsd.
8. bpel-scripts: this module is having those bpel files, it is used in bpel-compiler's test case.
9. bpel-compiler: this module is to convert the bpel file into ODE internal model for compiled bpel file.
10. il-common: this module is the common integration layer.
11. scheduler-simple: this module is the implementation of scheduler service.
12. bpel-store: this is the module takes charge of storing process from the filesystem, the artifact includes deploy.xml, .bpel, wsdl artifacts.
13. engine: this is the ode engine that uses the runtimes, dao, scheduler services.
14. bpel-ql: bpel query language.

JACOB framework module
1. jacob-ap
2. jacob

Integration modules:
1.axis2 integration: axis2, axis2-war
2.jca integration: bpel-api-jca, bpel-connector, jca-ra, jca-server
3.jbi integration: jbi
4.extension: extensions

some leftover modules are:
1. tools: this is for the bpelc, sendsoap command line.
2. utils: utils for ODE project.
3. tasks: this is tasks for buildr tool.
4. distro: this is the module for building distro.
