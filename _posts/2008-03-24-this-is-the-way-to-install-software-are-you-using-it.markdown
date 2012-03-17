---
date: '2008-03-24 00:35:00'
layout: post
slug: this-is-the-way-to-install-software-are-you-using-it
status: publish
title: This is the way to install software, are you using it?
wordpress_id: '189'
categories:
- Maven
- OS
- Thoughts
tags:
- Fedora
- Maven
- Ubuntu
---

I know it is a bit later to write an entry about this installing way, you know, I am always a bit later than it should be. ;(. anyway, it is better than never.:)

If you read my blog, you might know I am using the Ubuntu these days, and I am comfortable with the "apt-get" utility (actually, it is from the Debian distro) to install the software that I want, I think this way is far better than the old way, which needs you download the software into your local disk and install it. In Ubuntu, if you need to install a software, lets say it called "eva", you just simply run the command: sudo apt-get install eva. and then it will download and install from the internet. It doesn't need you to find the eva in the internet.

Today, I am trying to use the fedora distro, and I found there is an similar utility called "yum", which is "apt-get" in Ubuntu. Suddenly, I think of the "features" module in the [Apache Servicemix](http://servicemix.apache.org) [ Kernel](http://servicemix.apache.org/SMX4KNL/index.html), it uses the similar way to install the feature, such as NMR feature. Actually, I can't say it is belong to the servicemix functionality, it stems from the OSGi, which has an OBR (OSGi Bundle Repository).

Software is quite different from other commodities, it is very nature for us to see a software with a version, but it is not common for us to have a version with other commodities. The stuff with version also means it changes a lot and very frequent. it means you need to update the software from time to time to make it up-to-date, for the security or functionality sake.  The other aspect of software is dependency, the softwares are connected, most of time they are not isolated. So here comes the "dependency" issue for the software library.

[Apache Maven](http://maven.apache.org) is famous on resolving the "dependency" issue, it introduces the "pom.xml" file, which you can declare the repository and the library that you used in your project.

So back to the "apt-get" utility or "yum" utility in linux distro, it typically has a config file which contains the repository url, take ubuntu for example, it is in the "/etc/apt/sources.list". You can add/update the repository url, which contains the packages or softwares. if you need to install/upgrade/remove a software, simply running below commands:

    
     apt-get install/upgrade/remove "softwareName"


but this should be happening that your computer are connected..
