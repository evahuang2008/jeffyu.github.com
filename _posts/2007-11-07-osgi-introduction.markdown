---
date: '2007-11-07 02:28:00'
layout: post
slug: osgi-introduction
status: publish
title: OSGI introduction
wordpress_id: '162'
categories:
- Java
- OSGi
- Thoughts
---

Today, I am totally concentrating on the OSGI stuff, firstly, what OSGI tries to resolve or provide.  
1. Better separation of application logic into modules, with runtime enforcement of module boundaries.  
2. The ability to deploy multiple versions of a module (or library) concurrently. (Which is a big problem for today's classloader).  
3. The ability to dynamically discover and use services provided by other modules in the system  
4. The ability to dynamically install, update and uninstall modules in a running system  
  
Like BEA guy in the presentation[Ref 4] said, OSGI is more like a SOA stuff, see the service registry concept, it is very similar to the UDDI... well, since OSGI is still in developing in the JEE world, there are some issues right now. (excerpt from the BEA guy's presentation).  
  
1. configuration, dependency ordering. (for example, will start this bundle if others bundles are started).  
2. security? (I am not familiar with this stuff, but it is saying it is not reflecting on the OSGI, it is on Java itself).  
  
....  
  
Well, the most exiting thing about the OSGI is, by introducing the OSGI, we will build the micro-kernel system. such as, every system will has its own kernel, and all others related services are built on this, as a bundle(from OSGI spec) form. This is how operating system did. It has a kernel, and other software all are build on this kernel... I would say it would definitely change how we used to build enterprise system.  
  
  
References:  
1. [http://neilbartlett.name/blog/osgi-articles/](http://neilbartlett.name/blog/osgi-articles/)  
2. [Spring OSGI Reference Guide](http://static.springframework.org/osgi/docs/1.0-m3/reference/html_single/)  
3. [BEA OSGI presentation](http://www.parleys.com/display/PARLEYS/OSGi,+the+good+the+bad+the+ugly)  
4. [OSGI Best Practice](http://felix.apache.org/site/presentations.data/best-practices-apachecon-20060628.pdf)
