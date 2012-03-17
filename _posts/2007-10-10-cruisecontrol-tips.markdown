---
date: '2007-10-10 21:08:00'
layout: post
slug: cruisecontrol-tips
status: publish
title: CruiseControl Tips
wordpress_id: '158'
categories:
- Java
---

Out Of Memory Solution:  
  
1. Downloaded saxon6-5-5.zip from saxon.sourceforge.net  
2. Extracted saxon.jar from the zip file  
3. Added saxon.jar to CC lib dir  
4. Removed xalan-2.6.0.jar from CC lib dir  
5. Edited CRUISE_PATH in cruisecontrol.sh to add saxon.jar to classpath  
-----------------------------------------------------------------------------------------------------  
FAQ link:  
  
http://confluence.public.thoughtworks.org/display/CC/Frequently+Asked+Questions#FrequentlyAskedQuestions-faq4  
-----------------------------------------------------------------------------------------  
  
Q: I am running some jUnit tests, and the results don't show up in cruise control's JSP. What's going on?  
  
A: There are a couple things that the buildresults.jsp needs. First, your jUnit results need to be xml formatted. You can set this by adding  element, within your jUnit ANT task. Second, make sure that you merge your unit test results with cruise control's own xml report of the build. Do this in the  section of your config file, like this:  
  
if you had one file:  
  
&lt log ...&gt  
   &lt merge file=""/&gt  
&lt /log &gt  
  
and if you had a directory of files:  
  
&lt log ...&gt  
   &lt merge dir=""/&gt  
&lt/log &gt  
  
Cruise control may also report that you don't have any unit tests if they failed to build and never got to the point of being run in your junit task.  
  
Finally, if you are using a custom XML format and not the default Ant one, you will need to update unittests.xsl as appropriate  
------------------------------------------------------------------------------------------  
Code coverage solution  
  
We link to it directly by adding something similar to the following to buildresults.jsp:  
&lt cruisecontrol:artifactsLink &gt  
 [JCoverage Report](../jcoverage)  
&lt /cruisecontrol:artifactsLink &gt  
Er, I think that"s right. In any case, you should just be able to follow the default "Artifacts" link from the buildresults page, right? And if it helps, the line in your config.xml that publishes the jcoverage dir should be similar to the following:   
  
-----------------------------------------------------------------------------------------------------  
General CruiseControl Add Button (Tab) solution:  
  
http://sourceforge.net/mailarchive/message.php?msg_id=15825063
