记录it公司 java工程师 面试题

##算法题

1. 单向链表存在环结构，如何快速判断存在环结构

	一块一慢两个指针

2. 单向链表，存在一个特定的节点，如何快速删除该节点

10. 编程题 1,11,21,1211,111221,312211,12112221...
	数列规律，后面的数字是对前一个数字的描述，第二个数字11表示1个1，描述的是第一个数字。21表示2个1，1211表示1个2，1个1。
	
##java 基础  

1. hashmap的底层实现，如何处理冲突，采用链表存储同一个hash值的元素，对于什么操作会有影响。

2. 为何重写hashcode 和 equals方法

3. 异常种类有哪些
	
	![java中常见异常如下图所示](img/exception_1.jpg)  
	Throwable是所有异常的根，java.lang.Throwable
	Error是错误，java.lang.Error
	Exception是异常，java.lang.Exception
	一般分为Checked异常和Runtime异常，所有RuntimeException类及其子类的实例被称为Runtime异常，不属于该范畴的异常则被称为CheckedException。


4. [java 排序算法代码实现](http://www.cnblogs.com/wolf-sun/p/4312475.html)

5. 浅拷贝 vs 深拷贝

	**浅拷贝**是指拷贝对象时仅仅拷贝对象本身（包括对象中的基本变量），而不拷贝对象包含的引用指向的对象。  
	**深拷贝**不仅拷贝对象本身，而且拷贝对象包含的引用指向的所有对象。  
	若不对clone()方法进行改写，则调用此方法得到的对象即为浅拷贝。  
	[详细解释浅拷贝与深拷贝](http://www.cnblogs.com/shuaiwhu/archive/2010/12/14/2065088.html)  
	当然我们还有一种深拷贝方法，就是将对象串行化。缺点耗时。

##数据库  

1. 数据库 如何在学生成绩表中查询成绩排名第五第学生成绩信息

	oracle:
	```sql
	select * from(
	select * from scrore order by score desc
	}where rownum =5
	```
	mysql : ?

2. 数据库索引的数据结构，叶子节点存储什么？非叶子节点存储什么？
	
	<http://tech.meituan.com/mysql-index.html>  
	
	<http://blog.codinglabs.org/articles/theory-of-mysql-index.html>
	
3. mysql存储引擎：InnoDB和MyISAM
	MyISAM:这个是默认类型,它是基于传统的ISAM类型,ISAM是Indexed Sequential Access Method (有索引的顺序访问方法) 的缩写,它是存储记录和文件的标准方法.与其他存储引擎比较,MyISAM具有检查和修复表格的大多数工具. MyISAM表格可以被压缩,而且它们支持全文搜索.它们不是事务安全的,而且也不支持外键。如果事物回滚将造成不完全回滚，不具有原子性。如果执行大量的SELECT，MyISAM是更好的选择。  
	InnoDB:这种类型是事务安全的.它与BDB类型具有相同的特性,它们还支持外键.InnoDB表格速度很快.具有比BDB还丰富的特性,因此如果需要一个事务安全的存储引擎,建议使用它.如果你的数据执行大量的INSERT或UPDATE,出于性能方面的考虑，应该使用InnoDB表,
对于支持事物的InnoDB类型的标，影响速度的主要原因是AUTOCOMMIT默认设置是打开的，而且程序没有显式调用BEGIN 开始事务，导致每插入一条都自动Commit，严重影响了速度。可以在执行sql前调用begin，多条sql形成一个事物（即使autocommit打开也可以），将大大提高性能。

	区别：
	是否支持外键  innoDB
	是否需要事务	innoDB
	是否需要全文搜索  MyISAM
	经常食用什么样的查询模式（是否带where）  
	你的数据多大  innoDB
	是否使用count(*)	MyISAM  
	主键查询	innoDB  
	insert	MyISAM  
	update	innoDB  

4. 分布式数据库如何保证一致性


##网络
7. post get put 区别


8. 表单信息传到服务器加密问题
	HTTPS 对称加密 非对称加密 tls/ssl rsa
	
	
9. session cookie。http是无协议的，客户第二次访问，服务器如何分辩此用户之前访问过服务器，用户的信息是如何保存的。


11. HTTP HTTPS 前台数据加密传输后台


##操作系统
1. 与进程的区别:
(1)地址空间:进程内的一个执行单元;进程至少有一个线程;它们共享进程的地址空间;而进程有自己独立的地址空间;
(2)资源拥有:进程是资源分配和拥有的单位,同一个进程内的线程共享进程的资源
(3)线程是处理器调度的基本单位,但进程不是.

2. 怎么判断一个对象该被回收


3. 什么是可重入锁
	java 递归锁，可重入锁
所谓递归锁，就是在同一线程上该锁是可重入的，对于不同线程则相当于普通的互斥锁。
func A （） {  
     LOCK.lock();
     B();
    LOCK.unlock();
  }

  func B（） {
     LOCK.lock();
     LOCK.unlock();
  }
  java为每个线程分配一个锁，而不是为每次调用分配一个锁。
   java锁的可重入性机制可以解决下面这个问题
   可重入的意思是线程可以重复获得它已经持有的锁。


##java web 框架
5. sprig aop如何实现


13. spring 事务如何实现


16. spring事务遇到什么异常的时候不回回滚  
	
	Spring的事务管理默认只对出现运行期异常(java.lang.RuntimeException及其子类)进行回滚。	
	
##linux
1. 硬链接 vs 软链接  
	**硬连接**
硬连接指通过索引节点来进行连接。在Linux的文件系统中，保存在磁盘分区中的文件不管是什么类型都给它分配一个编号，称为索引节点号(Inode Index)。在Linux中，多个文件名指向同一索引节点是存在的。一般这种连接就是硬连接。硬连接的作用是允许一个文件拥有多个有效路径名，这样用户就可以建立硬连接到重要文件，以防止“误删”的功能。其原因如上所述，因为对应该目录的索引节点有一个以上的连接。只删除一个连接并不影响索引节点本身和其它的连接，只有当最后一个连接被删除后，文件的数据块及目录的连接才会被释放。也就是说，文件真正删除的条件是与之相关的所有硬连接文件均被删除。  
ln命令产生硬链接。   
```ln f1 f2``` #创建 f1的一个硬连接文件f2   

	**软连接**
另外一种连接称之为符号连接（Symbolic Link），也叫软连接。软链接文件有类似于Windows的快捷方式。它实际上是一个特殊的文件。在符号连接中，文件实际上是一个文本文件，其中包含的有另一文件的位置信息。  
``` ln -s f1 f3```       #创建f1的一个符号连接文件f3



