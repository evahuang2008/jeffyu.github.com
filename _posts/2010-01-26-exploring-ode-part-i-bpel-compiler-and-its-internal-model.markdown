---
date: '2010-01-26 21:32:00'
layout: post
slug: exploring-ode-part-i-bpel-compiler-and-its-internal-model
status: publish
title: 'Exploring ODE Part I: Bpel Compiler and its internal model.'
wordpress_id: '269'
categories:
- BPM
- Java
- JBoss
tags:
- BPEL
- ODE
- RiftSaw
---

In the [Apache ODE](http://ode.apache.org/), it has a bpelc, bpelc.bat script for you to compile the bpel file into ODE specific format file. We can use this tool to verify whether the bpel file's semantic is correct or not.

So in this blog entry, we will take a closer look at the architecture of this tool, (also known as [bpel-compiler](http://svn.apache.org/repos/asf/ode/trunk/bpel-compiler/) module). The [ode-tool](http://svn.apache.org/repos/asf/ode/trunk/tools/) module is just a wrapper for [bpel-compiler](http://svn.apache.org/repos/asf/ode/trunk/bpel-compiler/) module.

Firstly, lets look at the bpel object model for BPEL file, it is known as 'bom' (bpel object model, I guess) in the source file. It put all of bpel object model into this package, and its base class is BpelObject, this base class extends the sourceLocation which is for keeping detail info of original bpel file. some known subclasses are: IfActivity, PartnerLink, PartnerLinkType, SequenceActivity etc. These subclasses share one feature, their constructor parameter type is Element.

Second concept here is called ActivityGenerator, as name implied, it is taking care of generating the Activities, like IfActivity, InvokeActivity, SequenceActivity.

The other concept is called OBase, this class is a base class for compiled bpel object, the known subclasses are: OAssign, OInvoke, which both extend from OActivity, others are like: OPartnerlink, OProperty..

So in the bpel-compiler module, the work procedure is convert the bpel file into BOM, and then using AcitivityGenerator to convert them into OBase (ODE inner Object model).

If you want to look at the source code, you can start with BpelC class, the method for it is called compile(File file), in this method, you would find it uses the BpelObjectFactory to convert the xml file into BOM, and then get the correct BpelCompiler implementation to convert the BOM object to compiled object representation. (objects extends OBase class).

In the bpel-compiler module's test part, we are using the bpel files that are put in the [bpel-scripts](http://svn.apache.org/repos/asf/ode/trunk/bpel-scripts/) module, to do the unit test. If you want to learn about the bpel's activity, this is also a good resource.
