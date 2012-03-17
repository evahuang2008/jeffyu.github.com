---
date: '2007-11-14 03:50:00'
layout: post
slug: packaging-osgi-bundle
status: publish
title: Packaging OSGi bundle.
wordpress_id: '168'
categories:
- Maven
- OSGi
---

It is tedious for you to write the Import-Package, Export-Package directly in the MENIFEAST.MF file... Here is a [felix maven plugin](http://felix.apache.org/site/maven-bundle-plugin-bnd.html) that helps you make life easier.  
  
Today, talked with [Guillaume](http://gnodet.blogspot.com/) , it makes me know clear and more about the packaging OSGi bundle options.  
  
1.<Export-Package>. (It is detailed explained in the Reference 1).  
2.< Private-Package>: it will actually "merge" (copied) the jars and include in the bundle you are creating all the packages referenced.  
3. < Import-Package> If you want to import something as optional, use the syntax as: javax.jmdns*;resolution:=optional,  
4. <Spring-Context> This option is for spring-OSGi, it specified where spring config file need to load, and some other spring-osgi attributes, such as: create-asynchronously etc, take "publish-context" for example, if we specify the "publish-context := fasle", then you registered some bean in the registry, meanwhile, in the test case, you use the "waitOnContextCreation()" method, you would get a timeout error.  
  
5. If you want to test the configuration admin functionalities, you need to install below 3 bundles:  
1) org.apache.felix:org.apache.felix.configadmin  
2) org.apache.felix:org.osgi.compendium  
3) org.apache.geronimo.specs:geronimo-servlet_2.5_spec  
  
6. If you install a bundle, you get below error message:  


> Missing Constraint: Import-Package: *; version="0.0.0"

  
It means you are missing libraries dependency in the pom file.  
  
Reference:  
1. [Felix maven pulgin info](http://felix.apache.org/site/maven-bundle-plugin-bnd.html)  
2. [BND tool](http://www.aqute.biz/Code/Bnd)
