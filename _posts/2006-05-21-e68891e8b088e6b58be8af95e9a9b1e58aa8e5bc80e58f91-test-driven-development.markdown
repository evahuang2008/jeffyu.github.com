---
date: '2006-05-21 14:33:23'
layout: post
slug: '%e6%88%91%e8%b0%88%e6%b5%8b%e8%af%95%e9%a9%b1%e5%8a%a8%e5%bc%80%e5%8f%91-test-driven-development'
status: publish
title: 我谈测试驱动开发 (Test-Driven Development)
wordpress_id: '58'
categories:
- Java
---

    我一直感觉自己是个后知后觉的人,就说在大学的时候,有时候突然觉得一部片很好看,然后推荐给同学看,没想到他们说"啊?我们早看过了,你怎么才看?"...顿时我无语和冒汗.  
    在TDD上,我记得我是2004年7月的时候,买了一本书叫<Test-Driven Development: A pratical guide>,当时这本书好像获得了Jolt大奖,说实话,当时看这本书的时候,没什么感觉,只是觉得很简单的一本书,就讲怎么设计一个租片的例子...  
    从去年底公司开始强调Unit Test(主要是老美客户强烈要求),在这点上我很喜欢,因为我觉得Unit Test太重要了,我来到这家公司,可以说大多数的时间都在Debug,没办法啊,我所碰到的是遗留代码(legacy code),是别人写的,有时候要改个bug,我不能说先去读懂他所做的整个功能模块,然后再去改他的代码,那样太耗时了...而且很多时候就算是自己写的代码,有bug,也要用Debug,为什么呢?测试的粒度太大,整合了所有的Web tier, Business tier,虽然说Exception的信息可以给我们很多提示,但是很多时候,我还是要用debug...,但是,如果我们用Unit Test,我们的粒度小了,我们也就更能容易的发现到问题的所在了!,这是对提高写代码速度的最直接的影响,当然了,同时Unit Test对代码质量的保障起着至关重要的作用. (Uncle bob 这里有篇写为什么Unit Test和Code一样重要. http: //www.butunclebob.com/ArticleS.UncleBob.TheSensitivityProblem)  
    在写Unit Test的时候,有个问题就是,写Unit Test也耗时,而且刚开始大家会不愿意去写,当然了,更多的时候,刚开始写了,因为后来或者是业务逻辑变了,需要改Code,也需要改Unit Test,这个时候大家就不愿意去改Test Case,这样就造成了Test Case的obsolete,也就慢慢的没去维护Test了,其实解决这个问题,那么就需要引入Daily Build,Continous Integration...  
    话回到Test-Driven Development,其实TDD is not just Unit Tests([http://blog.kirkk.com/index.php?itemid=37),](http://blog.kirkk.com/index.php?itemid=37),)它更是一种Design..  
    那么,TDD到底是怎么样的一个流程呢? 我比较喜欢James Shore在他的Blog上所描述的一个流程([http://www.jamesshore.com/Blog/Red-Green-Refactor.html](http://www.jamesshore.com/Blog/Red-Green-Refactor.html)):  



* * *


  





  1. **Think:** Figure out what test will best move your code towards completion. (Take as much time as you need. This is the hardest step for beginners.)   



  2. **Red:** Write a very small amount of test code. Only a few lines... usually no more than five. Run the tests and watch the new test fail: the test bar should turn red. (This should only take about 30 seconds.)   



  3. **Green:** Write a very small amount of production code. Again, usually no more than five lines of code. Don't worry about design purity or conceptual elegance. Sometimes you can just hardcode the answer. This is okay because you'll be refactoring in a moment. Run the tests and watch them pass: the test bar will turn green. (This should only take about 30 seconds, too.)   



  4. **Refactor:** Now that your tests are passing, you can make changes without worrying about breaking anything. Pause for a moment. Take a deep breath if you need to. Then look at the code you've written, and ask yourself if you can improve it. Look for duplication and other "code smells." If you see something that doesn't look right, but you're not sure how to fix it, that's okay. Take a look at it again after you've gone through the cycle a few more times. (Take as much time as you need on this step.) After each little refactoring, run the tests and make sure they still pass.   



  5. **Repeat:** Do it again. You'll repeat this cycle dozens of times in an hour. Typically, you'll run through several cycles (three to five) very quickly, then find yourself slowing down and spending more time on refactoring. Than you'll speed up again. 20-40 cycles in an hour is not unreasonable.






* * *


  
     这之间有个小插曲,微软的MSDN有次发表了一个TDD的GuideLine,但是实际上并不是真正意义上的TDD,很多人 such as Uncle Bob,Michael Feather, James Shore等都写blog说Microsoft miss the TDD points at all,可以看看下面的这个Blog..(当时我根据链接过去的时候,Microsoft上面已经显示: this page is obsoleted and has been removed.:( ),但是有个blog上面是详细的记录下来,并且逐点的抨击...( http: //codebetter.com/blogs/scott.bellware/archive/2005/11/21/134899.aspx)  

