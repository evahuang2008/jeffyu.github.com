---
date: '2006-09-03 16:35:18'
layout: post
slug: jeff%e8%af%b4%e6%a8%a1%e5%bc%8f-vistor-%e6%a8%a1%e5%bc%8f
status: publish
title: Jeff说模式 - Vistor 模式
wordpress_id: '37'
categories:
- Chinese
- Java
tags:
- Design Patterns
---

今天下午翻阅了数本资料,终于把Vistor这个模式整理出了一条比较清晰的思路,因为毕竟在实际的做应用程序的时候,很少用到vistor模式,所以一直在我的脑海里是处于半桶水的状态. 

[意图]
Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.
表示一个作用于某个对象结构中的各元素的操作,它使你可以在不改变各元素的类的前提下定义作用于这些元素的新操作.

我觉得这个模式主要是在这样的情景情况下应用的.

有几个比较稳定的类结构,比如说: 存在 Engineer, Senior Engineer, Project Manager, Account Manager 这么几个不同的类,那么他们可能有些共同的待遇问题,就比如说每次的加薪,这个加薪的算法是每个类他有自己的算法. 理论上来说,这个加薪的算法应该是放在Engineer, Senior Engineer, Project Manager自己类里面的. 但是问题在于,他们之间的共同待遇问题不仅仅就一个,他们有很多,而且在未来里,比如说因为公司的福利待遇好,又要增加某些他们共有的东西,但是呢,算法是根据各个类来做决定的,就比如说Project Manager的待遇肯定要比Engineer的待遇好...

就这个问题,我们看到了不变和变的部分, 不变的是各个职位; 变的是他们之间共有的待遇算法. 所以,我们必须抽取出变的部分,封装起来,把它独立放在一个地方.

这也正是Vistor模式最适合应用的场景.
Uncle Bob这么描述, 我们可以把这样的问题看作是一个矩阵(或者坐标), X轴是职位, Y轴是共有的待遇. 如果Y轴经常变,我们就需要用Vistor模式,如果是X轴经常变,那么我们就应该把待遇的算法直接放入到职位类当中. (我很喜欢这个总结. ;-) ).

[效果] - 优缺点:
1. 更容易增加新的操作. (也就是更容易添加新的福利,待遇算法)
2. 集中相关的操作,分离无关的操作. (也就是把共有的福利算法集中在一起)
3. 累积状态.
4. 破坏封装. ( 因为现在在外面的福利算法这个类可以改变职位类当中的某些属性,这样就说明了职位类这个类封装的不好,因为好的类的封装只能是通过这个类本身来改变自己的数据.)
5. 增加新的ConcreteElement很难. (也就是增加新的职位难,因为你新增加一个职位,你需要相应的去改变这个职位的福利算法).

具体的实现和参考资料:
[
http://www.dofactory.com/Patterns/PatternVisitor.aspx ](http://www.dofactory.com/Patterns/PatternVisitor.aspx)
[http://www.exciton.cs.rice.edu/JavaResources/DesignPatterns/VisitorPattern.htm ](http://www.exciton.cs.rice.edu/JavaResources/DesignPatterns/VisitorPattern.htm)
[http://www.javaworld.com/javaworld/javatips/jw-javatip98.html](http://www.javaworld.com/javaworld/javatips/jw-javatip98.html)
<Agile Software Development Principles, Patterns and Practices>
<Design Patterns>
<Refactoring to Patterns>


