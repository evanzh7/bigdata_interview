1. StringBuffer,StringBuilder的区别是啥
	
	StringBuffer是线程安全的，而StringBuilder是非线程安全的。  
2. 什么是线程安全

	线程安全是编程中的术语，指某个函数、函数库在并发环境中被调用时，能够正确地处理多个线程之间的共享变量，使程序功能正确完成。即在多线程场景下，不发生有序性、原子性以及可见性问题。

3. 如何保证线程安全

	Java中主要通过加锁来实现线程安全。通常使用synchronized和Lock

4. 什么是锁？死锁？

	死锁是指两个或两个以上的进程在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象，若无外力作用，它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁，这些永远在互相等待的进程称为死锁进程。
死锁的发生必须具备以下四个必要条件：互斥条件、请求和保持条件、不剥夺条件、环路等待条件
死锁的解决办法就是破坏以上四种必备条件中的一个或者多个。

5. synchronized的实现原理是什么？

	[深入理解多线程（一）——Synchronized的实现原理](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650120537&idx=1&sn=f56201217c0ca6fde45ee12965b56296&chksm=f36bbc78c41c356ee363367addcdc0b311afb2f9df86a7ee20d21348b3332fd64f273d6028ca&scene=21#wechat_redirect)  
	[深入理解多线程（四）—— Moniter的实现原理 ](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650120784&idx=1&sn=3436c978f0d7ab3bb672d03689518902&chksm=f36bbf71c41c36672a3a6a7edebe0b913f2f5cf33d75d594d228f086ec7bdb9e253ab0beeae4&scene=21#wechat_redirect)  
	[再有人问你synchronized是什么，就把这篇文章发给他](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121805&idx=1&sn=8aea8c329a018c82a7ebfe80ec604226&chksm=f36bbb6cc41c327acc23d3d7cdf0b785e318d8e970d564ba9ce8b28a1ae6b41499d351497af3&scene=21#wechat_redirect)  

6. 有了synchronized，还要volatile干什么？

	volatile通常被比喻成”轻量级的synchronized“，volatile可以保证可见性和有序性，实现原理是通过内存屏障实现的。
volatile有一个重要的作用，是synchronized不具备的，那就是禁止指令重排序。这一特点在双重校验锁实现单例的时候有用到，虽然使用了synchronized关键字，但是如果不用volatile修饰单例对象，就会存在问题。  
[深入理解Java中的volatile关键字 ](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121842&idx=1&sn=e1972797ac2a7ad945d7424fc081cb49&chksm=f36bbb53c41c32455c9d77f849812f5eedb0ff4cc2ef808870ae0f005adfde384d2fc957b628&scene=21#wechat_redirect)

7. synchronized的锁优化是怎么回事？（锁粗化，锁消除，自旋锁，偏向锁，轻量锁）

	[深入理解多线程（五）—— Java虚拟机的锁优化技术
](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121186&idx=1&sn=248d37be27d3bbeb103464b2a96a0ae4&chksm=f36bbec3c41c37d59277ac8539a616b65ec44637f341325056e98323e8780e09c6e4f7cc7a85&scene=21#wechat_redirect)

8. 知道JMM吗？（原子性，可见性，有序性）

	Java内存模型（Java Memory Model ,JMM）是一种符合内存模型规范的，屏蔽了各种硬件和操作系统的访问差异的，保证了Java程序在各种平台下对内存的访问都能保证效果一致的机制及规范。  
	[再有人问你Java内存模型是什么，就把这篇文章发给他。](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121599&idx=1&sn=42b2cfabfb3057ac6c09026a8b9656cd&chksm=f36bb85ec41c31489e461a53e78f2959f0224c87c312724f420265b70e67e4efdae2331155aa&scene=21#wechat_redirect)

8. java并发包了解吗

	java.util.concurrent包(J.U.C)中包含的是java并发编程中有用的一些工具类，包括几个部分：  
1、locks部分：包含在java.util.concurrent.locks包中，提供显式锁(互斥锁和速写锁)相关功能；  
2、atomic部分：包含在java.util.concurrent.atomic包中，提供原子变量类相关的功能，是构建非阻塞算法的基础；  
3、executor部分：散落在java.util.concurrent包中，提供线程池相关的功能；  
4、collections部分：散落在java.util.concurrent包中，提供并发容器相关功能；  
5、tools部分：散落在java.util.concurrent包中，提供同步工具类，如信号量、闭锁、栅栏等功能；

9. 什么是fail-fast？什么是fail-safe？

	我们通常说的Java中的fail-fast机制，默认指的是Java集合的一种错误检测机制。当多个线程对部分集合进行结构上的改变的操作时，有可能会产生fail-fast机制，这个时候就会抛出ConcurrentModificationException。
ConcurrentModificationException，当方法检测到对象的并发修改，但不允许这种修改时就抛出该异常。
为了避免触发fail-fast机制，导致异常，我们可以使用Java中提供的一些采用了fail-safe机制的集合类。
这样的集合容器在遍历时不是直接在集合内容上访问的，而是先复制原有集合内容，在拷贝的集合上进行遍历。
java.util.concurrent包下的容器都是fail-safe的，可以在多线程下并发使用，并发修改。同时也可以在foreach中进行add/remove 。  
[一不小心就踩坑的fail-fast是个什么鬼？](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650123769&idx=2&sn=87d070e0a1a5e66a87eed4e22a99aa63&chksm=f36bb0d8c41c39ce80af4ff385a75f762a7f73850589517cb1ba28a42e9eb09eeb3bd81d4201&scene=21#wechat_redirect)

10. 什么是CopyOnWrite

	Copy-On-Write简称COW，是一种用于程序设计中的优化策略。其基本思路是，从一开始大家都在共享同一个内容，当某个人想要修改这个内容的时候，才会真正把内容Copy出去形成一个新的内容然后再改，这是一种延时懒惰策略。
CopyOnWrite容器即写时复制的容器。通俗的理解是当我们往一个容器添加元素的时候，不直接往当前容器添加，而是先将当前容器进行Copy，复制出一个新的容器，然后新的容器里添加元素，添加完元素之后，再将原容器的引用指向新的容器。

11. AQS，CAS是什么

	AQS(AbstractQueuedSynchronizer)，即队列同步器。它是构建锁或者其他同步组件的基础框架（如ReentrantLock、ReentrantReadWriteLock、Semaphore等），JUC并发包的作者（Doug Lea）期望它能够成为实现大部分同步需求的基础。它是JUC并发包中的核心基础组件。
CAS(Compare and Swap)是项乐观锁技术，当多个线程尝试使用CAS同时更新同一个变量时，只有其中一个线程能更新变量的值，而其它线程都失败，失败的线程并不会被挂起，而是被告知这次竞争中失败，并可以再次尝试。
CAS 操作包含三个操作数 —— 内存位置（V）、预期原值（A）和新值(B)。如果内存位置的值与预期原值相匹配，那么处理器会自动将该位置值更新为新值。否则，处理器不做任何操作。无论哪种情况，它都会在 CAS 指令之前返回该位置的值。（在 CAS 的一些特殊情况下将仅返回 CAS 是否成功，而不提取当前值。）CAS 有效地说明了“我认为位置 V 应该包含值 A；如果包含该值，则将 B 放到这个位置；否则，不要更改该位置，只告诉我这个位置现在的值即可。”这其实和乐观锁的冲突检查+数据更新的原理是一样的。  
[乐观锁的一种实现方式——CAS](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121285&idx=1&sn=7cf9b5badd6d38b57ccfbfed63d3aad1&chksm=f36bb964c41c307218914cab6c1592f649281460e4ec1f85627c1311441c8a43ee1854440552&scene=21#wechat_redirect)

12. CAS都知道，那乐观锁一定知道了

	乐观锁（ Optimistic Locking ） 相对悲观锁而言，乐观锁假设认为数据一般情况下不会造成冲突，所以在数据进行提交更新的时候，才会正式对数据的冲突与否进行检测，如果发现冲突了，则让返回用户错误的信息，让用户决定如何去做。
相对于悲观锁，在对数据库进行处理的时候，乐观锁并不会使用数据库提供的锁机制。一般的实现乐观锁的方式就是记录数据版本。
实现数据版本有两种方式，第一种是使用版本号，第二种是使用时间戳。  
[深入理解乐观锁与悲观锁](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650123857&idx=1&sn=d5624d62d50cb94963db57fbf4b16e03&chksm=f36bb370c41c3a66c026e2e81eb9fa747782b02300a3e741183dc776b6c355acb9789ca69612&scene=21#wechat_redirect)

13. 乐观锁，悲观锁的区别是什么

	同上

14. 数据库如何实现悲观锁和乐观锁  

	同上

15. 数据库锁有了解吗？行级锁？表级锁？共享锁？排它锁？gap锁？next-key lock?

	[MySQL中的行级锁,表级锁,页级锁](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=402330276&idx=1&sn=aa35ce5bdcfa659f4ee2f7890a46f479&chksm=79650f854e128693eb8b8aa78023fb21cfc73c7862ac5666b552c989404684fd440377f7a2dd&scene=21#wechat_redirect)  
[MySQL中的共享锁与排他锁](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=402351172&idx=2&sn=a7b4ae968095d718643bb1875c16dffd&chksm=796579654e12f0733a022f89d77bd148212f1705f2102866ba4d4f87003fda5ca9fd2c7b201b&scene=21#wechat_redirect)

16. 数据库锁和隔离级别有什么关系

	很多DBMS定义了多个不同的“事务隔离等级”来控制锁的程度和并发能力。
ANSI/ISO SQL定义的标准隔离级别有四种，从高到底依次为：  
可序列化(Serializable)、  
可重复读(Repeatable reads)、  
提交读(Read committed)、  
未提交读(Read uncommitted)。
[深入分析事务的隔离级别](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650123822&idx=2&sn=839363e712e2d0069ee3c673cd3686e6&chksm=f36bb30fc41c3a1924f1b3a587da7b9db6af2f1614459cf770f749a24f817d1687e34746251c&scene=21#wechat_redirect)

17. 数据库锁和索引有什么关系

	在MySQL中，行级锁并不是直接锁记录，而是锁索引。索引分为主键索引和非主键索引两种，如果一条sql语句操作了主键索引，MySQL就会锁定这条主键索引；如果一条语句操作了非主键索引，MySQL会先锁定该非主键索引，再锁定相关的主键索引。

18. 什么是聚簇索引？非聚簇索引，最左前缀是什么?B+树索引？联合索引?回表？

	主键索引的叶子节点存的是整行数据。在InnoDB中，主键索引也被称为聚簇索引（clustered index）  
	非主键索引的叶子节点的内容是主键的值，在InnoDB中，非主键索引也被称为非聚簇索引（secondary index）  
	当我们创建一个联合索引的时候，如(key1,key2,key3)，相当于创建了（key1）、(key1,key2)和(key1,key2,key3)三个索引，这就是最左匹配原则。
在 InnoDB 里，索引B+ Tree的叶子节点存储了整行数据的是主键索引。而索引B+ Tree的叶子节点存储了主键的值的是非主键索引。因为主键索引树的叶子节点直接就是我们要查询的整行数据了。而非主键索引的叶子节点是主键的值，查到主键的值以后，还需要再通过主键的值再进行一次查询，这个过程叫做回表。
[我以为我对Mysql索引很了解，直到我遇到了阿里的面试官](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650124338&idx=1&sn=ac152b7bdf4b1ad16827b7851f6170ff&chksm=f36bad13c41c2405aae50eb6c8a1832bc668274e14182e1ca29c4a59c845060aac149dc0967e&scene=21#wechat_redirect)
1. hashmap的底层实现，如何处理冲突，采用链表存储同一个hash值的元素，对于什么操作会有影响。

	底层实现是数组，数组中的对象是Entry类对象。  
	当存在冲突时，将具有相同hashcode的对象挂载在相同槽内，组成链。采用头插法，新插入对象放在链头，最先加入的对象放在链尾。  
	**hashcode()**  
	**indexFor()**  
	**put()**  
	**get()**  
	**addEntry()**  
	**loadfactor**  
	loadfactor=元素个数/表长  
	**hash算法**  

	```java
	int indexFor(int h, int length){
		return h&(length - 1)	
	}
	```
	**resize**  
	数组默认大小是16，负载因子默认未0.75  

2. 为何重写hashcode 和 equals方法  
	重写equals方法必然重写hashcode方法，这是java规范。  
	hashcode返回值是一个整数，代表两个对象是否相等。  


3. 异常种类有哪些
	
	![java中常见异常如下图所示](img/exception_1.jpg)  
	Throwable是所有异常的根，java.lang.Throwable  
	Error是错误，java.lang.Error  
	Exception是异常，java.lang.Exception  
	一般分为Checked异常和Runtime异常，所有RuntimeException类及其子类的实例被称为Runtime异常，不属于该范畴的异常则被称为CheckedException。


4. [java 排序算法代码实现](http://www.cnblogs.com/wolf-sun/p/4312475.html)，复杂度、稳定性

5. 浅拷贝 vs 深拷贝

	**浅拷贝**是指拷贝对象时仅仅拷贝对象本身（包括对象中的基本变量），而不拷贝对象包含的引用指向的对象。  
	**深拷贝**不仅拷贝对象本身，而且拷贝对象包含的引用指向的所有对象。  
	若不对clone()方法进行改写，则调用此方法得到的对象即为浅拷贝。  
	[详细解释浅拷贝与深拷贝](http://www.cnblogs.com/shuaiwhu/archive/2010/12/14/2065088.html)  
	当然我们还有一种深拷贝方法，就是将对象串行化。缺点耗时。

6. 怎么判断一个对象该被回收  
	计数法  
	根搜索法

7. hashMap 和 hashtable区别
8. hashtable原理
9. hashtable是怎么实现线程安全的
8. java的代理是怎么实现的
9. 抽象类和接口的区别
10. 接口和实现类的区别
10. java四种引用
11. 集合类介绍，各种集合类之间的区别
12. 继承和组合区别
13. lmbda表达式
14. java 8 新特性
15. java基础数据类型 
	- 整形 byte	short	int		long  
	- 浮点型	float	double  
	- 逻辑型 boolean  
	- 字符型	char  
16. java中的数据存储  

	- 寄存器：最快的存储区，编译器分配，程序无法控制
	- 栈：存放基础数据类型的变量数据 和 对象的引用  
	- 堆：new出来的对象存放位置
	- 静态域：静态成员变量存放位置  
	- 常量池：字符串变凉&基本数据类型变量 public static final  
	- 非rRAM存储：硬盘等永久存储空间
20. 内存溢出 和 内存泄漏
21. 内存敲代码优化，我们都用stringbuffer来代替+号，来减少建立的对象。那么问题来了，除了这个你还用过什么碼代码技巧来节省内存 
22. 方法走完，引用消失，堆内存未必消失，好多人在做报表导出的时候，就会在for循环里不断的创建对象，很容易造成堆溢出，请问这种大文件导出怎么破？  
  建议不要在for里创建对象，可以在外面搞一个对象，for循环里对一个对象修改数据即可。
23. java支持多线程，每个线程有自己的java虚拟机栈和本地方法栈。✔️
24. 新建的实例在堆内存，实例变量也是在堆内存。✔️
25. 入栈和出栈  
	入栈的时候，就是执行一个方法的时候，为这个方法创建一个栈帧入栈。  
	出栈的时候，就是方法执行完毕了。  
26. 加载父类->初始化父类->加载子类  
27. 如果我有一个静态的成员变量int，那我多线程更改是否会有线程安全问题，为什么？
	静态成员变量，它在内存里， 只有一份，就是属于类的。你多个线程并发修改，一定会有并发问题，可能导致数据出错。 
28. 类加载是按需加载，可以一次性加载全部的类吗？
	如果是默认的类加载机制，那么是你得代码运行过程中，遇到什么类加载什么类。  
	如果你要自己加载类，那么需要写自己的类加载器。  
29. 多线程的实现方式有哪些？
    继承 Thread 类、实现Runnable 接口，最后调用 的是 start() 方法来启动线程。  
    start() 跟 run() 方法的区别和联系?  
    直接调用 start() 方法，此时线程处于一个就绪（可运行）的状态，但是并没有真正	的运行。而是得到CPU 的时间片后，开始执行 run() 方法，run() 方法里面的是我们	的线程体。
	我们直接 运行 run() 方法，它其实就是一个普通的方法调用，在主线程中执行，是不会开启多线程的。
30. 死锁   
	**产生死锁的原因主要是**：  
（1） 因为系统资源不足。  
（2） 进程运行推进的顺序不合适。  
（3） 资源分配不当等。   
    **产生死锁的四个必要条件**：  
（1）互斥条件：一个资源每次只能被一个进程使用。  
（2）占有且等待：一个进程因请求资源而阻塞时，对已获得的资源保持不放。   
（3）不可强行占有:进程已获得的资源，在末使用完之前，不能强行剥夺。  
（4）循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。   
这四个条件是死锁的必要条件，只要系统发生死锁，这些条件必然成立，而只要上述条件之
一不满足，就不会发生死锁。 
 
	**处理死锁的基本方法**（银行家算法）：

	- 死锁预防：通过设置某些限制条件，去破坏死锁的四个条件中的一个或几个条件，来预防发生死锁。但由于所施加的限制条件往往太严格，因而导致系统资源利用率和系统吞吐量降低。
	- 死锁避免：允许前三个必要条件，但通过明智的选择，确保永远不会到达死锁点，因此死锁避免比死锁预防允许更多的并发。
	- 死锁检测：不须实现采取任何限制性措施，而是允许系统在运行过程发生死锁，但可通过系统设置的检测机构及时检测出死锁的发生，并精确地确定于死锁相关的进程和资源，然后采取适当的措施，从系统中将已发生的死锁清除掉。
	- 死锁解除：与死锁检测相配套的一种措施。当检测到系统中已发生死锁，需将进程从死锁状态中解脱出来。常用方法：撤销或挂起一些进程，以便回收一些资源，再将这些资源分配给已处于阻塞状态的进程。死锁检测盒解除有可能使系统获得较好的资源利用率和吞吐量，但在实现上难度也最大。

	**处理死锁的基本算法**    
	1. 如果request<=need，转向步骤2；否则认为出错，因为请求资源大于需要资源。
	2. 如果request<=available，转向步骤3,；否则尚无足够资源，进程p阻塞；
	3. 系统尝试为把资源分配给进程P，并修改available、allocation和need的数值。
	4. 系统执行安全性算法，检查此次分配后系统是否处于安全状态，若安全，才正式将资源分配给进程P，否则将本次试探性分配作废，让进程P等待。  
	安全状态：系统能按照某种进程顺序，为每个进程分配资源，直至满足每个进程对资源的最大需求，使每个进程都可顺利完成。
	
31. 线程池  
    newSingleThreadExecutor、  
    newFixedThreadPool、  
    newCachedThreadPool、  
    newScheduledThreadPool  
线程池底层都是通过 ThreadPoolExecutor 来实现的

	```java
	public ThreadPoolExecutor
	( 
	int corePoolSize,                          
	int maximumPoolSize,                         
	long keepAliveTime,                           
	TimeUnit unit,             
	BlockingQueue <Runnable> workQueue,                     
	ThreadFactory  threadFactory,              
	RejectedExecutionHandler handler)
	```
	几个参数的意思分别为：

	- corePoolSize： 线程池里最小线程数
	- maximumPoolSize：线程池里最大线程数量，超过最大线程时候会使用 RejectedExecutionHandler
	- keepAliveTime：线程最大的存活时间，超过这个时间就会被回收
	- unit：线程最大的存活时间的单位
	- workQueue：缓存需要执行的异步任务的队列
	- threadFactory：新建线程工厂
	- handler：拒绝策略，表示当workQueue已满，且池中的线程数达到maximumPoolSize时，线程池拒绝添加新任务时采取的策略。DiscardPolicy：抛弃当前任务，DiscardOldestPolicy：扔掉最旧的，CallerRunsPolicy：由向线程池提交任务的线程来执行该任务，AbortPolicy：抛出 RejectedExecutionException 异常。
32. 这几种线程池在哪些情况下使用什么类型的
33. 如何判断两个对象是否相等
2. java StringBuffer  StringBuilder区别
5. java 集合类
6. java垃圾回收，类加载机制
7. HashMap实现原理及扩容机制
8. jvm运行时内存使用区域划分



