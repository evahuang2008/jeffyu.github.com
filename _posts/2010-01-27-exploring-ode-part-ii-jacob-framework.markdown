---
date: '2010-01-27 18:50:00'
layout: post
slug: exploring-ode-part-ii-jacob-framework
status: publish
title: 'Exploring ODE Part II: JACOB Framework'
wordpress_id: '270'
categories:
- BPM
- Java
tags:
- BPEL
- ODE
- RiftSaw
---

In this blog entry, we will look at the ODE's jacob framework, which is of a library taking care of concurrency processing. ODE use this lib underlying to solve the concurrency problem, ODE has [a very good wiki](http://ode.apache.org/jacob.html) explains about this framework, but here I would like to highlight some concepts and introduce a simple example in the end.

Firstly, I am reusing the wiki page's example. Say we have a following process.

[xml]
1.invoke
2.receive
3.wait
4.invoke
[/xml]

and we have 2 parallel execution of the process, without Jacob framework the execution would be:

[xml]
1. Invoke1
2. Receive1
3. Wait1
4. Invoke1
5. Invoke2
6. Receive2
7. Wait2
8. Invoke2
[/xml]

so the above is totally sequentially, no concurrency at all. With the jacob framework, we might see following execution order.

[xml]
1. Invoke1
5. Invoke2
2. Receive1
3. Wait1
6. Receive2
7. Wait2
4. Invoke1
8. Invoke2
[/xml]

From a client standpoint, we've achieved concurrency of execution even with one thread.

Now, we will see following concepts in jacob:

1. JacobRunnable, JacobObject
In the wiki page, the JacobRunnable, JacobObject is described as a simple closure. Just like above example shows, here we abstract the action like 'Invoke, Receive' etc as a JacobRunnable object. Personally I also see JacobRunnable as a command pattern, which implements the run method.

2. Channel
Once we have had the JacobRunnable object, how do we connect JacobObject and ChannelListener? Here is where Channel comes to play, we can see that JacobRunnable as one end of the channel, and ChannelListener as the other end of the channel. The Channel implementation is used JDK's dynamic proxy, you can see it from **ChannelFactory**.

For every JacobRunnable or ChannelListener, it will take a Channel class in. It is not very useful if have the JacobRunnable without means to communicate.

3. ChannelListener
In the wiki page, it is referred as MLs (MethodList), but I'd prefer to call it as Listener. With introduction of Channel object, we are able to pass the Channel object into our next activity or child activity, but we need to have a listener mechanism for the parent activity so that once the child activity finished, it is able to get notified and continues the flow.

4. @ChannelType annotion
In the Jacob, we are using the '@ChannelType' annotation to generate the Channel and ChannelListener interfaces in the compile time.

5. JacobVPU, ExecutionQueueImpl
As wiki page said, here are the responsibilities of JacboVPU and ExecutionQueueImpl.
1) JacobVPU is the place of Jacob processing.
2) ExecutionQueueImpl is the container for all artifacts (mostly channels and reactions) managed by JacobVPU.
3) JacobVPU is also responsible for persisting its internal state, like serialize or de-serialize the object.
4) Continuations (and hence JacobRunnables) don't "stay" in the VPU queues. They just get popped, executed and that's it.

Now, I will introduce an example that works with Jacob API to accomplish the above example. we are having three JacobObjects(Continuation), they are INVOKE, RECEIVE, WAIT. But for the simplicity purpose, I will just have INVOKE and RECEIVE. Also we will add a channel for their communication, I called it Demo, here is the code for Demo Channel.

[java]
@ChannelType
public interface Demo {
public void onSuccess(String successInfo);
public void onFailure(String errorString);
}
[/java]

as you read from the code, we are having two methods, one for successful case, the other is for failure. use either the maven tool or buildr, you would see the generated classes for this interface, they are DemoChannel and DemoChannelListener.

Next, we will see actions.

[java]
static class INVOKE extends JacobRunnable {
private DemoChannel _channel;

public INVOKE(DemoChannel channel) {
_channel = channel;
}

@Override
public void run() {
System.out.println("INVOKE Activity");

DemoChannel demoChannel2 = newChannel(DemoChannel.class, "demo2");
instance(new RECIEVE(demoChannel2));
object(new DemoChannelListener(demoChannel2) {
public void onSuccess(String successInfo) {
 System.out.println(successInfo);
 _channel.onSuccess("INVOKE Done...");
}

public void onFailure(String errorString) {
 System.out.println(errorString);
}
});

}
}

static class RECIEVE extends JacobRunnable {
private DemoChannel _demoChannel;

public RECIEVE(DemoChannel demoChannel) {
_demoChannel = demoChannel;
}

@Override
public void run() {
System.out.println("Receive Activity");
_demoChannel.onSuccess("RECEIVE success...");
}
}
[/java]

For this example, I will add another action to start our process, it is called Process.

[xml]
static class Process extends JacobRunnable {

@Override
public void run() {
DemoChannel channel = newChannel(DemoChannel.class, "demo");
instance(new INVOKE(channel));
object(new DemoChannelListener(channel) {
public void onSuccess(String successInfo) {
 System.out.println(successInfo);
 System.out.println("Process Done");
}

public void onFailure(String errorString) {
 System.out.println(errorString);
}
});
}

}
[/xml]

We will talk from Process class, basically, we've created a DemoChannel, and then we use 'instance(...)' method to add the 'activity/JacobRunnable' into the queue, use the 'object(....)' to define a listener for that channel.
In the INVOKE class, we've created a child activity that is called RECEIVE. Which puts RECEIVE class as part of INVOKE class. I know this is a bad example, it would be much better if I use a composite activity, like While or Sequence, but you know I am just being lazy. ;)

At last, we will use following code to execute this example:

[java]
public static void main(String[] args) throws Exception {
ExecutionQueueImpl soup = new ExecutionQueueImpl(null);
JacobVPU vpu = new JacobVPU(soup, new Process());

while(vpu.execute()) {
}

}
[/java]

Run this method, you would get following output.

[xml]
INVOKE Activity
Receive Activity
RECEIVE success...
INVOKE Done...
Process Done
[/xml]

If you want to look at the code by yourself, it lies in the [ode-jacob](http://svn.apache.org/repos/asf/ode/trunk/jacob/) module, it extends the [ode-jacob-ap](http://svn.apache.org/repos/asf/ode/trunk/jacob-ap/) module. Below are some classes that you'd look into. CommSend, CommRecv. Jacob wraps the JacobRunnable as CommSend, wraps the ChannelListener as CommRecv. And then uses the CommGroup to do the match.ExecutionQueueImpl is the container for Continuation, ExecutionObject, Channel etc. In the ExecutionQueueImpl class, you would find couple static classes, like ChannelFrame, MessageFrame... these classes are mostly used for serialized and de-serialized the object.
