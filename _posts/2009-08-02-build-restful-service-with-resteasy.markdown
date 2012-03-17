---
date: '2009-08-02 21:44:00'
layout: post
slug: build-restful-service-with-resteasy
status: publish
title: Build restful service with RESTEasy
wordpress_id: '242'
categories:
- Java
- REST
tags:
- RESTEasy
---

Haven't used JAX-RS to build RESTful service for a while, these days I look at the BPM console project, and one thing is that its service are all rest services. So I tried to build a restful service with [RESTEasy](http://jboss.org/resteasy/) library to see how it goes. Hope this blog entry could help people who are also trying to build Restful service with RESTEasy. I am using the RESTEasy 1.1.GA version in our example.

If you are still working on the REST topic, then take a look at [this resource](http://jeff.familyyu.net/2008/08/rest-articles-link.html), also I strongly recommend that you have a read on 《Restful webservice》if possible. I will build a restful-blog project as our helloworld, and will look into it from three aspects: build, deployment and unit test.

Build the Project

1.**create a project and add the resteasy lib**

Firstly, lets create the project, I am using the m2eclipse plugin to create a maven blank project. Open up the pom.xml, add the resteay-jaxrs, resteasy-jaxb-provider libs in our pom.xml, in order to download the resteasy-jaxrs, you need to add the jboss maven repo in the repository.
The repository and the dependency would be like:

[xml]
<repositories>
  <repository>
   <id>JBossMavenRepo</id>
   <name>JBoss Maven2 repo</name>
   <url>http://repository.jboss.org/maven2</url>
   <releases>
    true</enabled>
   </releases>
   <snapshots>
    false</enabled>
   </snapshots>
  </repository>
 </repositories>

 <dependencies>
  <dependency>
   <groupId>junit</groupId>
   <artifactId>junit</artifactId>
   <version>4.4</version>
   <scope>test</scope>
  </dependency>
  <dependency>
   <groupId>org.jboss.resteasy</groupId>
   <artifactId>resteasy-jaxrs</artifactId>
   <version>1.1.GA</version>
  </dependency>
  <dependency>
   <groupId>org.jboss.resteasy</groupId>
   <artifactId>resteasy-jaxb-provider</artifactId>
   <version>1.1.GA</version>
  </dependency>
[/xml]

Run: mvn eclipse:eclipse, it should generate all the eclipse needed workspace files.

2. **Build the Resource service**
Here, I created the UserService interface, which takes care of users CRUD operation, and UserServiceImpl to implement UserService. I am a guy that like to keep the API and implementation separated as much as possible. (Because I found people would typically created a resource class directly in building restful service. like they would name it as UserResource class directly, don't have UserService interface. I still prefer to have interface as the contract.) As the JAX-RS 1.0 spec supports that put the annotation on its interface, so it is ok for us to keep API and impl separated.

Lets look at the UserService firstly.

[java]
public interface UserService {

 @GET
 @Path("{id}")
 @Produces({"application/xml"})
 public User getUser(@PathParam("id") long id);

 @POST
 @Consumes("application/xml")
 public Response addUser(User user);

}
[/java]

JAX-RS spec introduced a set of annotations to help us to expose the java bean as RESTful service.

@Path: This annotation defines which url that we are trying to expose our service to.
@GET:  We know that we have five operations in HTTP, they are GET, PUT, POST, DELETE and HEAD. This annotation is mapped to HTTP's GET, it means you need to use the GET method to access the url to get this resource.
@POST: Mapped to the HTTP's POST.
@Produces: This annotation defines which media type that this method(every method is a resource here) produced.
@Consumes:This annotation is opposed to the @Produces, this one specifies what kind of media type (format) is expected for this method(resource)
@PathParam: This means we will extract the id value from the url path. Other params are: QueryParam, CookieParam, HeaderParam, FormParam etc.

The 'Response' object is a JAX-RS spec defined return type. Client is able to get this object from the HTTP's Response object.

Now, let's look at User Object itself,

[java]
@XmlRootElement(name="user")
public class User {

 @XmlAttribute
 public long getId() {
  return id;
 }
 @XmlElement
 public String getUsername() {
  return username;
 }
 @XmlElement
 public String getEmail() {
  return email;
 }
.....
}
[/java]

Here, I omitted the class memeber and its setter methods. You can see that our domain object has the JAXB specific annotation.

Let's step back and look at what we are trying to do in the UserService, we want client to send a xml file over HTTP to add a User, so we need to have a data binding lib that convert the xml to Java Object, thats the reason that we introduced the JAXB annotation.

Our User Object corresponding xml would be like following:

[xml]
<user id="1">
 <username>TestUser</username>
 <email>testuser@test.com</email>
</user>
[/xml]

Now, let's look at the UserServiceImpl class.

[java]
@Path("/user")
public class UserServiceImpl implements UserService{

   private Map userDB = new ConcurrentHashMap();
   private AtomicLong idCounter = new AtomicLong();

 public UserServiceImpl() {
  User user = new User();
  user.setId(100);
  user.setUsername("jeff.yuchang");
  user.setEmail("jeff.yuchang@jboss.org");
  userDB.put(Long.valueOf(100), user);
 }

 public Response addUser(User user) {
  user.setId(idCounter.getAndIncrement());
  userDB.put(user.getId(), user);
  System.out.println("User was created, its id " + user.getId());
  return Response.created(URI.create("/user/" + user.getId())).build();
 }

 public User getUser(long id) {
  final User user = userDB.get(Long.valueOf(id));
  if (null == user) {
   throw new WebApplicationException(Response.Status.NOT_FOUND);
  }
  return user;
 }
[/java]

This is a very simple implementation, you would understand it easily.
Note: Here we got one thing to note is that we've used the '@Path' in our impl, we didn't include this in our UserService interface, the reason that I am doing so is because I didn't make it work when I deployed it into the Servlet container.
Until now, we've built a very simple resource, next is to deploy it under container, and then we can check it through browser or HttpClient code etc.

Deploy it into Servlet Container

In order to deploy our restful resource into Servlet container, we still need to add one class, which needs to extends the 'Application' object that defined in the JAX-RS. we can simply view the Application as a registry that allows us to register our resource into system.

[java]
public class BlogApplication extends Application {

   private Set<Object> singletons = new HashSet<Object>();
   private Set<Class<?>> empty = new HashSet<Class<?>>();

   public BlogApplication() {
    singletons.add(new UserServiceImpl());
   }

 @Override
 public Set<Class<?>> getClasses() {
  return empty;
 }

    @Override
    public Set<Object> getSingletons() {
       return singletons;
    }

}
[/java]

Once we've finished the Application class, we need to add the web.xml and then use the maven-war plugin file to build a war.

The web.xml is as following:

[xml]
<web-app>
    <display-name>restful-blog</display-name>

    <context-param>
      <param-name>javax.ws.rs.core.Application</param-name>
      <param-value>org.jboss.resteasy.blog.BlogApplication</param-value>
   </context-param>

    <listener>
        <listener-class>org.jboss.resteasy.plugins.server.servlet.ResteasyBootstrap</listener-class>
    </listener>

    <servlet>
        <servlet-name>Resteasy</servlet-name>
        <servlet-class>org.jboss.resteasy.plugins.server.servlet.HttpServletDispatcher</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>Resteasy</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
</web-app>
[/xml]

Also, add the maven-war-plugin into your pom.xml, like

[xml]
<plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-war-plugin</artifactId>
          <version>2.0</version>
          <configuration>
            <webappDirectory>src/webapp</webappDirectory>
          </configuration>
       </plugin>
[/xml]

Now, run the mvn clean install, you would see the restful-blog-1.0-SNAPSHOT.war in the target folder.

Copy it into the $Tomcat/webapps, start the tomcat, and then access the following url: http://localhost:8080/restful-blog-1.0-SNAPSHOT/user/100, you should see the following xml file.

[xml]
<user id="100">
<email>jeff.yuchang@jboss.org</email>
<username>jeff.yuchang</username>
</user>
[/xml]

OK, now we've successfully built and deployed a restful service. If you are a TDD(Test Driven Development) person like me, I guess you would like to use the embedded servlet container in your unit test.

Unit Test (Embedded servlet container)

RESTEasy has a out-of-box integration with [Tiny Java Web Server](http://tjws.sourceforge.net/) as the embedded servlet container. We are using the http client as our client in our unit tests.

1.**Adding tjws-webserver and servlet 2.5**
We need to add the twjs webserver-1.3.3.jar and the servlet-2.5.jar in our pom.xml

[xml]
 <dependency>
   <groupId>tjws</groupId>
   <artifactId>webserver</artifactId>
   <version>1.3.3</version>
   <scope>test</scope>
  </dependency>
  <dependency>
   <groupId>org.apache.geronimo.specs</groupId>
   <artifactId>geronimo-servlet_2.5_spec</artifactId>
   <version>1.2</version>
   <scope>test</scope>
  </dependency>
[/xml]

2.**Write a Base test to start the webserver**
I write a following base test, which takes care of starting and stopping servlet server.

[java]
public class BaseTest extends Assert{

 protected static TJWSEmbeddedJaxrsServer server;

 protected static ResteasyDeployment deployment;

 protected static int port = 8081;

 @BeforeClass
 public static void initialize() throws Exception{
  server = new TJWSEmbeddedJaxrsServer();
  deployment = new ResteasyDeployment();
  server.setDeployment(deployment);
  server.setPort(port);
  server.start();
 }

 public void addPerRequestResource(Class<?> clazz) {
  deployment.getRegistry().addPerRequestResource(clazz);
 }

 @AfterClass
 public static void destroy() throws Exception{
  if (server != null) {
   server.stop();
  }
 }
[/java]

3.**Write unit test by using http client**
And now, comes our unit test class.

[java]
public class UserServiceTest extends BaseTest {

 @Before
 public void setUp() throws Exception {
    this.addPerRequestResource(UserServiceImpl.class);
 }

 @Test
 public void testGetUser() throws Exception {
  URL url = new URL("http://localhost:8081/user/100");
  HttpURLConnection connection = (HttpURLConnection)url.openConnection();
  connection.setRequestMethod("GET");

     BufferedReader reader = new BufferedReader(new
               InputStreamReader(connection.getInputStream()));
     String line = reader.readLine();
        while (line != null)
        {
         System.out.println(line);
         line = reader.readLine();
        }

  connection.disconnect();
 }

 @Test
 public void testCreateUser() throws Exception {
  URL url = new URL("http://localhost:8081/user");
  HttpURLConnection connection = (HttpURLConnection)url.openConnection();
  connection.setRequestMethod("POST");
  connection.setRequestProperty("Content-Type", "application/xml");
  connection.setDoOutput(true);
  connection.setInstanceFollowRedirects(false);

  StringBuffer sbuffer = new StringBuffer();
  sbuffer.append("<user id="0">");
  sbuffer.append("   <username>Test User</username>");
  sbuffer.append("   <email>test.user@test.com</email>");
  sbuffer.append("</user>");

  OutputStream os = connection.getOutputStream();
  os.write(sbuffer.toString().getBytes());
  os.flush();

     assertEquals(HttpURLConnection.HTTP_CREATED, connection.getResponseCode());
  connection.disconnect();
 }

}
[/java]

You should be able to run test cases either in IDE or simply do it by running maven surefire plugin. You could obtain [the whole project as a tall bar from here](http://people.apache.org/~jeffyu/articles/artifacts/restful-blog.tar).

[References]
1. [RESTEasy user guide](http://jboss.org/file-access/default/members/resteasy/freezone/docs/1.1.GA/userguide/html_single/index.html).
2. [JAX RS 1.0 spec](http://jcp.org/en/jsr/detail?id=311).
