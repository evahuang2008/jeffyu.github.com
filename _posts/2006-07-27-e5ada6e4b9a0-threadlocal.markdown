---
date: '2006-07-27 10:11:48'
layout: post
slug: '%e5%ad%a6%e4%b9%a0-threadlocal'
status: publish
title: 学习 ThreadLocal
wordpress_id: '28'
categories:
- Java
---

ThreadLocal, 我到目前还没正式用过这个东西,因为他更多的是被应用于基础架构的编写,在我理解看来, ThreadLocal就是存放Context的地方,这个地方只能是当前的Thread才能访问,他的生命周期是到这个Thread完毕.  
文章[1]中的一段说明,我觉得说的很清楚:  
  
So what's the difference between a thread-local variable and a normal variable?
When a thread accesses a thread-local variable it has its own independently
initialized copy of the variable. Each thread holds an implicit reference to its
copy as long as the thread is alive. So when the thread goes away, all of its
thread-local instances are subject to gc.  
You typically use an anonymous
inner class to provide an initial value (if any) using an appropriate
constructor and return the newly constructed object.  
  
You can use this `ThreadLocal` in several situations:  


  1. **To keep state with a thread (user-id, transaction-id,
logging-id)**
  2. **To cache objects which you need frequently**但是,同时你也要注意Context的cleanup,要不然,他就会变成evil.[2]  
  
今天在TSS链接了一篇关于ThreadLocal的Blog: [3]  
  
总之,什么时候用ThreadLocal呢？需要一些Thread-safe的全局变量,但是用他的时候,记得最后清空,要不然会导致memory-leak.
  
  
Update: 最近刚看到Uncle Bob的一篇关于Threadlocal的文章[4]  
  
[1]:[http://www.bloggingaboutjava.org/cms/wordpress/2005/12/threadlocal-is-your-friend/](http://www.bloggingaboutjava.org/cms/wordpress/2005/12/threadlocal-is-your-friend/))  
[2]:[http://blog.arendsen.net/index.php/2005/02/16/threadlocals-are-evil/](http://blog.arendsen.net/index.php/2005/02/16/threadlocals-are-evil/)  
[3]:[http://crazybob.org/2006/07/hard-core-java-threadlocal.html](http://crazybob.org/2006/07/hard-core-java-threadlocal.html)  
[4]:[http://blog.objectmentor.com/articles/2007/09/04/thread-local-a-convenient-abomination](http://blog.objectmentor.com/articles/2007/09/04/thread-local-a-convenient-abomination)  

