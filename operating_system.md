##  操作系统

1. 与进程的区别:  
(1)地址空间:进程内的一个执行单元;进程至少有一个线程;它们共享进程的地址空间;而进程有自己独立的地址空间。  
(2)资源拥有:进程是资源分配和拥有的单位,同一个进程内的线程共享进程的资源。  
(3)线程是处理器调度的基本单位,但进程不是。  

2. 什么是可重入锁
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
 
3. 对线程安全的理解