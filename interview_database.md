## 3. 数据库  

1. 数据库 如何在学生成绩表中查询成绩排名第五第学生成绩信息

	oracle:
	```sql
	select * from(
	select * from scrore order by score desc
	)where rownum =5
	```
	mysql : ?

2. 数据库索引的数据结构，叶子节点存储什么？非叶子节点存储什么？
	
	<http://tech.meituan.com/mysql-index.html>  
	
	<http://blog.codinglabs.org/articles/theory-of-mysql-index.html>
	
3. mysql数据库存储引擎：InnoDB和MyISAM  


	MyISAM:这个是默认类型,它是基于传统的ISAM类型,ISAM是Indexed Sequential Access Method (有索引的顺序访问方法) 的缩写,它是存储记录和文件的标准方法.与其他存储引擎比较,MyISAM具有检查和修复表格的大多数工具. MyISAM表格可以被压缩,而且它们支持全文搜索.它们不是事务安全的,而且也不支持外键。如果事物回滚将造成不完全回滚，不具有原子性。如果执行大量的SELECT，MyISAM是更好的选择。  
	InnoDB:这种类型是事务安全的.它与BDB类型具有相同的特性,它们还支持外键.InnoDB表格速度很快.具有比BDB还丰富的特性,因此如果需要一个事务安全的存储引擎,建议使用它.如果你的数据执行大量的INSERT或UPDATE,出于性能方面的考虑，应该使用InnoDB表,
对于支持事物的InnoDB类型的标，影响速度的主要原因是AUTOCOMMIT默认设置是打开的，而且程序没有显式调用BEGIN 开始事务，导致每插入一条都自动Commit，严重影响了速度。可以在执行sql前调用begin，多条sql形成一个事物（即使autocommit打开也可以），将大大提高性能。

	区别：
	是否支持外键  innoDB支持  
	是否需要事务	innoDB支持  
	是否需要全文搜索  MyISAM支持  
	经常使用什么样的查询模式（是否带where）    
	你的数据多大  innoDB  
	是否使用count(*)	MyISAM    
	主键查询	innoDB  
	insert	MyISAM  
	update	innoDB  

4. 分布式数据库如何保证一致性
5. sql注入原理
6. 数据库范式  
	

7. 乐观锁 vs 悲观锁
8. 数据库锁机制
9. 事务隔离机制  


10. 数据库连接池原理
11. 连接池使用什么数据结构实现，
12. B+树和二叉树查找时间复杂度
3. 异常处理机制  
5. java 垃圾处理机制 
