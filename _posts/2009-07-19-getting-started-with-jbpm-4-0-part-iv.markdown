---
date: '2009-07-19 17:45:00'
layout: post
slug: getting-started-with-jbpm-4-0-part-iv
status: publish
title: Getting Started with jBPM 4.0 (Part IV)
wordpress_id: '236'
categories:
- BPM
- Java
- JBoss
tags:
- jBPM
---

As said in [part III](http://jeffyuchang.blogspot.com/2009/07/getting-started-with-jbpm-40-part-iii.html), we will revise our example, to create the task form, and then use the jbpm console to take or complete the task.

Firstly, because there was a minor issue related to this feature, which was reported [here in the jBPM jira](https://jira.jboss.org/jira/browse/JBPM-2423), we will use the 'form' attribute in the jpdl file.

1.Add the task form template
Here, we will create a freemarker template file, named review.ftl. the files content is as following:

[xml]
<html>
<body>
<h2>Please review the request
<form action="${form.action}" method="POST" enctype="multipart/form-data">
<#list outcome.values as transition>
<input type="submit" name="outcome" value="${transition}">
</#list>
</form>
</body>
</html>
[/xml]

2.Add the form attribute in task node
As we said earlier, due to the [JBPM-2423 issue](https://jira.jboss.org/jira/browse/JBPM-2423) in jBPM 4.0 GA, we need to update our jpdl to associate our task form template. the updated section is as following.

    
    <task assignee="alex" g="277,235,92,52" name="review" <span style="color: #ff0000;">form="review.ftl"</span>>
    <transition g="-73,-25" name="approved" to="audit"/>
    </task>


3.  Update the build.xml, to include the .ftl file in .bar archive
The last step would be to update our build.xml, to include the ftl template file, and also include the png file for the diagram show usage in our jbpm console.
The updated bar package built script is:

[xml]
<target name="bar" depends="init">
<jar destfile="${basedir}/target/helloworld.bar">
  <fileset dir="${basedir}/src/main/resources">
        <include name="*.jpdl.xml" />
        <include name="*.ftl" />
       <include name="*.png" />
</fileset>
   </jar>
</target>
[/xml]

That is it, now you can re-deploy it into the jBPM server, [like we said in the part3](http://jeffyuchang.blogspot.com/2009/07/getting-started-with-jbpm-40-part-iii.html).

Task Form in jBPM console
well, after we started the process instance, let's see the diagram and the task form in its console UI.

On the process instance tab, click the 'diagram' button in the instance details page, you would see page as following picture.
[![](http://jeff.familyyu.net/wp-content/uploads/2011/01/diagram1.gif?w=300)](http://jeff.familyyu.net/wp-content/uploads/2011/01/diagram1.gif)

Go to the task list -> Personal tasks, you would see there is a task, the name is called "review", select the task and click the 'view' button, it would pop up the task form interface as following picture.
[![](http://jeff.familyyu.net/wp-content/uploads/2011/01/taskform.gif?w=300)](http://jeff.familyyu.net/wp-content/uploads/2011/01/taskform.gif)

Once you click the 'approved' button, the task is completed, and the whole process goes to the 'audit' state as we've defined in the jpdl file.

So, that is all for the task form example. If you want to know more about the template, like syntax, you can refer to the [freemarker webiste](http://freemarker.sourceforge.net/).

One thing interesting is that there is a console-server, which is the jbpm console talk to, the console server is responsible for exposing the jBPM service as a RESTful services. You can go to "http://localhost:8080/gwt-console-server/rs/server/resources" to see all available resources. we won't go detail in this entry, this is an interesting topic that we will cover in the future blog entry.

Summary

Until now, this 《Getting Started with jBPM 4.0》series is finished, you can download the [jbpm-helloworld example as a tar ball from here](http://people.apache.org/%7Ejeffyu/articles/artifacts/jbpm-helloworld.tar). Its aim is to help you get started, if you want to know more about jBPM 4.0, the [userguide](http://docs.jboss.com/jbpm/v4.0/userguide/html_single/) and [dev guide](http://docs.jboss.com/jbpm/v4.0/devguide/html_single/) are very good documents, and you also shouldn't miss [the jbpm user forum](http://www.jboss.org/index.html?module=bb&op=viewforum&f=217).
