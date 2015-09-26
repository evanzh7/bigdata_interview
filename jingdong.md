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
