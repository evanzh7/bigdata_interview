记录it公司面试过程中的问题  
- [美团](meituan.md)
- [京东](jingdong.md)

1. 单向链表存在环结构，如何快速判断存在环结构

一块一慢两个指针

2. 单向链表，存在一个特定的节点，如何快速删除该节点

3. hashmap的底层实现，如何处理冲突，采用链表存储同一个hash值的元素，对于什么操作会有影响。

4. 数据库索引的数据结构，叶子节点存储什么？非叶子节点存储什么？
	
	<http://tech.meituan.com/mysql-index.html>
	<http://blog.codinglabs.org/articles/theory-of-mysql-index.html>

5. sprig aop如何实现

6. 数据库 如何在学生成绩表中查询成绩排名第五第学生成绩信息

	oracle:
	```sql
	select * from(
	select * from scrore order by score desc
	}where rownum =5
	```
	mysql 
7. post get put 区别
8. 表单信息传到服务器加密问题
	HTTPS 对称加密 非对称加密 tls/ssl rsa
9. session cookie。http是无协议的，客户第二次访问，服务器如何分辩此用户之前访问过服务器，用户的信息是如何保存的。
10. 编程题 1,11,21,1211,111221,312211,12112221...
	数列规律，后面的数字是对前一个数字的描述，第二个数字11表示1个1，描述的是第一个数字。21表示2个1，1211表示1个2，1个1。
11. HTTP HTTPS 前台数据加密传输后台

1. 为何重写hashcode 和 equals方法

	
2. spring 事务如何实现


3. 分布式数据库如何保证一致性


4. 异常种类有哪些
	
	![java中常见异常如下图所示](img/exception_1.jpg)  
	Throwable是所有异常的根，java.lang.Throwable
	Error是错误，java.lang.Error
	Exception是异常，java.lang.Exception
	一般分为Checked异常和Runtime异常，所有RuntimeException类及其子类的实例被称为Runtime异常，不属于该范畴的异常则被称为CheckedException。


5. spring事务遇到什么异常的时候不回回滚  
	Spring的事务管理默认只对出现运行期异常(java.lang.RuntimeException及其子类)进行回滚。	




[java 排序算法代码实现](http://www.cnblogs.com/wolf-sun/p/4312475.html)

