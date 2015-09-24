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




