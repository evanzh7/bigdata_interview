## 分布式事务

19. 分布式锁有了解吗  

	目前比较常用的有以下几种方案：  
	- 基于数据库实现分布式锁 
	- 基于缓存（redis，memcached，tair）实现分布式锁 
	- 基于Zookeeper实现分布式锁  
	[分布式锁的几种实现方式~](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121038&idx=1&sn=a30023d2db37047a9912e338681bc6f7&chksm=f36bbe6fc41c3779b1eb003a7f420b443dc90e62575e9533fd770701d77fc9178865a7a115ca&scene=21#wechat_redirect)

20. Redis怎么实现分布式锁

	多个进程执行以下Redis命令：
SETNX lock.foo
如果 SETNX 返回1，说明该进程获得锁，SETNX将键 lock.foo 的值设置为锁的超时时间（当前时间 + 锁的有效时间）。 如果 SETNX 返回0，说明其他进程已经获得了锁，进程不能进入临界区。进程可以在一个循环中不断地尝试 SETNX 操作，以获得锁。

21. 为什么要用Redis

	分布式缓存，提升性能
	
22. Redis和memcache的区别是什么

	- 存储方式：Memcache把数据全部存在内存之中，断电后会挂掉，数据不能超 过内存大小。Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启时可以再次加载进行使用。（RDB快照和AOF日志两 种持久化方式）。
	- Redis支持数据的备份，及master-slave模式的数据备份。
	- 数据支持类型：Redis在数据支持上要比Memcache多得多。
	- 使用底层模型不同：新版本的Redis直接自己构建了VM机制，因为一般的系统调用系统函数的话，会浪费一定的时间去移动和请求。

23. Zookeeper怎么实现分布式锁

	基于zookeeper临时有序节点可以实现的分布式锁。
大致思想即为：每个客户端对某个方法加锁时，在zookeeper上的与该方法对应的指定节点的目录下，生成一个唯一的瞬时有序节点。 判断是否获取锁的方式很简单，只需要判断有序节点中序号最小的一个。 当释放锁的时候，只需将这个瞬时节点删除即可。同时，其可以避免服务宕机导致的锁无法释放，而产生的死锁问题。

24. 什么是ZooKeeper

	Zookeeper是一个开放源码的分布式服务协调组件，是Google Chubby的开源实现。是一个高性能的分布式数据一致性解决方案。他将那些复杂的、容易出错的分布式一致性服务封装起来，构成一个高效可靠的原语集，并提供一系列简单易用的接口给用户使用。  
	[Zookeeper介绍（二）——Zookeeper概述](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=402477716&idx=1&sn=da9fa5b6fda0745e507e1cb9d9e3e9bf&chksm=79634fb54e14c6a3e93a1888efbe7afafb18cfa6172485b8db3e385b20868fca4fe4e9fac21f&scene=21#wechat_redirect)

25. 什么是CAP 

	CAP理论：一个分布式系统最多只能同时满足一致性（Consistency）、可用性（Availability）和分区容错性（Partition tolerance）这三项中的两项。  
	[分布式系统的CAP理论](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121696&idx=1&sn=d8043efa332f3f76b96f7067754f2f01&chksm=f36bb8c1c41c31d7ca5f6bd02246bdb68ea49dd178c0b007fc0ff2f11d1a625113b5cccdc908&scene=21#wechat_redirect)

26. 什么是BASE？和CAP什么区别

	BASE理论是对CAP理论的延伸，核心思想是即使无法做到强一致性（Strong Consistency，CAP的一致性就是强一致性），但应用可以采用适合的方式达到最终一致性（Eventual Consitency）。
BASE是指基本可用（Basically Available）、软状态（ Soft State）、最终一致性（ Eventual Consistency）。  
[分布式系统的BASE理论](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121746&idx=1&sn=47ac282cd6fef6d48043e516bca8b717&chksm=f36bbb33c41c32258ecf6b19f7918dd4361d087cd2f66851eee360a66dba4bbb161422fbb1a4&scene=21#wechat_redirect)  
对于涉及到钱财这样不能有一丝让步的场景，C必须保证。网络发生故障宁可停止服务，这是保证CP，舍弃A。比如前几年支付宝光缆被挖断的事件，在网络出现故障的时候，支付宝就在可用性和数据一致性之间选择了数据一致性，用户感受到的是支付宝系统长时间宕机，但是其实背后是无数的工程师在恢复数据，保证数数据的一致性。
对于其他场景，比较普遍的做法是选择可用性和分区容错性，舍弃强一致性，退而求其次使用最终一致性来保证数据的安全。



27. 分布式系统怎么保证数据一致性

	 分布式事务

28. 啥事分布式事务？分布式事务方案

	分布式事务是指会涉及到操作多个数据库的事务。其实就是将对同一库事务的概念扩大到了对多个库的事务。目的是为了保证分布式系统中的数据一致性。分布式事务处理的关键是必须有一种方法可以知道事务在任何地方所做的所有动作，提交或回滚事务的决定必须产生统一的结果（全部提交或全部回滚）
	[关于分布式事务、两阶段提交协议、三阶提交协议](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=402387528&idx=2&sn=f89ded5a927db3cdec0d006e1a261573&chksm=7965ef694e12667fb8130fcf5a9b589f25fd1ad926f7622312afb3f020509996d33b697a40da&scene=21#wechat_redirect)
	[分布式事务解决方案——柔性事务与服务模式](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121657&idx=1&sn=350ad9766061378885a6d7218cee5ae5&chksm=f36bb898c41c318e2c120eb97b69a6ff4204f6fa4463f3be2c9fc3aa25a815178533190696a1&scene=21#wechat_redirect)
	

29. 手写一个线程安全的单例吧

	[单例模式的七种写法](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=402230646&idx=1&sn=16b7dda4dd46de380ebeb850bbcbd63b&chksm=796790574e1019414eae8dc53832670cf2fd00e59a9e626d1e0a835ade0c5c0b0ea9ea8aaf40&scene=21#wechat_redirect)
	[为什么我墙裂建议大家使用枚举来实现单例](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121482&idx=1&sn=e5b86797244d8879bbe9a69fb72641b5&chksm=f36bb82bc41c313d739f485383d3a868a79020c995ee86daef026a589f4782916c42a8d3f6c7&scene=21#wechat_redirect)

30. 不用synchronized和lock能实现线程安全的单例吗

	借助CAS（AtomicReference）实现单例模式：  
	
	```java
	public class Singleton {
    private static final AtomicReference<Singleton> INSTANCE = new AtomicReference<Singleton>(); 

    private Singleton() {}

    public static Singleton getInstance() {
        for (;;) {
            Singleton singleton = INSTANCE.get();
            if (null != singleton) {
                return singleton;
            }

            singleton = new Singleton();
            if (INSTANCE.compareAndSet(null, singleton)) {
                return singleton;
            }
        }
    }
}
	```
用CAS的好处在于不需要使用传统的锁机制来保证线程安全,CAS是一种基于忙等待的算法,依赖底层硬件的实现,相对于锁它没有线程切换和阻塞的额外消耗,可以支持较大的并行度。 CAS的一个重要缺点在于如果忙等待一直执行不成功(一直在死循环中),会对CPU造成较大的执行开销。   
[不使用synchronized和lock，如何实现一个线程安全的单例？](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650120516&idx=1&sn=31c136d35c99dfad3538465e6f068691&chksm=f36bbc65c41c3573b1c04198c1da29e3aabc47d25de047da21e083df93992def6e5ffed6d463&scene=21#wechat_redirect)  
[不使用synchronized和lock，如何实现一个线程安全的单例？（二）](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650120519&idx=1&sn=ea51a643553f12fbd56af4a2d835331b&chksm=f36bbc66c41c3570d3ae3413bbe02b92afb230bf609a405f9b2066ac397983865cef6ba4b93e&scene=21#wechat_redirect)  

31. 解释下什么是Paxos算法吧

	Paxos一种基于消息传递且具有高度容错特性的一致性算法。Paxos算法号称是最难理解的算法！！！