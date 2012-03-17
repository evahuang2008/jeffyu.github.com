---
date: '2009-08-08 21:14:00'
layout: post
slug: jbpm-4-0-restful-service-introduction
status: publish
title: jBPM 4.0 restful service introduction.
wordpress_id: '243'
categories:
- BPM
- Java
- JBoss
- REST
tags:
- jBPM
- RESTEasy
---

We all knew that we've had a completely re-write console that is using GWT in jBPM 4.0.  But we might not know that we've also introduced a set of jbpm restful services. Specifically, it is including following resources: Process Management, Task Management, User Management, Process Engine service etc. These resources are exchanged by using json as data format. The jBPM console ([http://localhost:8080/jbpm-console](http://localhost:8080/jbpm-console)) operates jbpm services through this restful services.

Assume that you've installed the jBPM 4.0, started the server, you can see all available services at [http://localhost:8080/gwt-console-server/rs/server/resources](http://localhost:8080/gwt-console-server/rs/server/resources) url. This page basically lists the most important information for the services, like the Method (could be GET, POST etc), the url, consume and produce data format etc.

Now, lets look at how many components are consist of this restful service. In the jBPM server, we can find following three packages.

[xml]$JBoss/server/default/lib/gwt-console-rpc.jar
$JBoss/server/default/lib/gwt-console-server-integration.jar
$JBoss/server/default/deploy/jbpm/gwt-console-server.war
[/xml]

These three libraries is the backbone of our restful services.
1. gwt-console-rpc.jar: this jar includes all the domain classes that server used to expose. In other word, this jar define all of data format that we are going to expose to the client.
2. gwt-console-server-integration: This package includes all of abstracted SPIs(Service Provider Interface), like TaskManagement etc. jBPM integration layer uses this to implement these SPIs.
3. gwt-console-server.war: This artifact extends the rpc and server-integration modules(the artifacts in the default/deploy folder will see all libaries in the default/lib folder) , also leverages the RESTEasy lib to expose all of service to be restful. (here we are using the RESTEasy's jaxb-json provider to expose all the domain model into json data format.)

* Tip: we've put all of jBPM related API into the jbpm.jar itself (you can find it under the $JBoss/server/default/lib/jbpm.jar). For the jBPM integration point, we are getting the ProcessEngine API from the JNDI at "java:/ProcessEngine".

Now you saw these services. Next I will write a simple test to use this service to show you how you can leverage it.

For its simplicity, I won't do it in the html, that is what jBPM console did, here I will write a test client, and then use the [Gson library](http://code.google.com/p/google-gson/) to convert the json into our domain model(in our gwt-console-rpc).

[java]
public class RestfulServiceTest extends TestCase {

  public void testDeploymentRestfulService() throws Exception {
      URL url = new URL("http://localhost:8080/gwt-console-server/rs/engine/deployments");
      HttpURLConnection connection = (HttpURLConnection)url.openConnection();
      connection.setRequestMethod("GET");

      BufferedReader reader = new BufferedReader(new
                InputStreamReader(connection.getInputStream()));

      StringBuffer buffer = new StringBuffer();
      String line = reader.readLine();
      while (line != null)
      {
       buffer.append(line);
       line = reader.readLine();
      }

      System.out.println(buffer.toString());

      Gson gson = new Gson();
      DeploymentRefWrapper result = gson.fromJson(buffer.toString(), DeploymentRefWrapper.class);

      for (DeploymentRef deploymentRef : result.getDeployments()) {
          System.out.println("deployment name is: " + deploymentRef.getName());
      }

      connection.disconnect();
  }

}
[/java]


Before you run the above code, you need to make sure that you've started the jBPM 4.0, and deployed a bar file into the server. Otherwise you would see nothing, as there were no data on the server. (you can refer to [my previous blogs](http://jeff.familyyu.net/search/label/jBPM) if you don't know how to start and deploy bar artifact into server).



* Note: You need to add the gson lib in your classpath.

Run the test code, you would get following result.

    
    {"deployments":[{"id":"1","suspended":false,"name":"helloworld.bar","timestamp":1249805642238,"definitions":["helloworld-1"],"resourceNames":["review.ftl","META-INF/","META-INF/MANIFEST.MF","helloworld.jpdl.xml","helloworld.png"]}]}
    
    deployment name is: helloworld.bar


First one is the whole data in json format.

[Reference]
1. [BPM Console Reference](http://www.jboss.org/community/wiki/BPMConsoleReference)
