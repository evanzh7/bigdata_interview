## 1. 算法题

1. 单向链表存在环结构，如何快速判断存在环结构

	一块一慢两个指针

2. 单向链表，存在一个特定的节点，如何快速删除该节点

3. 编程题 1,11,21,1211,111221,312211,13112221...
	数列规律，后面的数字是对前一个数字的描述，第二个数字11表示1个1，描述的是第一个数字。21表示2个1，1211表示1个2，1个1。  

4. 字符串逆序 	
5. 快速排序

	快速排序运用了分治的思想、递归的思想。将数组分成两部分，两部分分别排序
	
	```python
	def quick_sort(arr,start=0,end=None):
    if end is None:
        end = len(arr)-1
    if end<=start:
        return(arr)
    i,j = start,end
    ref = arr[start]
    while j>i:
        if arr[j]>= ref:
            j = j - 1
        else:
            # 此处使用一行语句交换3个元素的值
            arr[i],arr[j],arr[i+1] = arr[j],arr[i+1],arr[i]
            i = i + 1
    quick_sort(arr,start=start,end = i-1)
    quick_sort(arr,start=i+1,end = end)
    return(arr)

	print(quick_sort([1,1,3,3,2,2,6,6,6,5,5,7]))
	
	result:  
	[1, 1, 2, 2, 2, 3, 5, 5, 6, 6, 6, 7]
	```
	
6. 二分查找
	
	题目形式：手写一下二分查找算法。给定一个有序数组 arr 和一个目标元素 target ，返回该 target 在 arr 中的索引，若不存在，返回-1。  
	题目难度：简单。  
	思想：二分查找有两个游标，每次游标都朝着减半的位置移动。但是二叉查找有个限制，就是待查找的数组必须是有序的。
	
	```python
	def binary_search(arr,target):
	    star,end = 0,len(arr)-1
	    while True:
	        if end - start <= 1:
	            if target == arr[start]:
	                return(start)
	            elif target == arr[end]:
	                return(end)
	            else:
	                return(-1)
	         mid = (start + end)//2
	         if arr[mid]>=target:
	             end = mid
	         else:
	             start = mid
	demo:
	print(binary_search([1,4,7,8,9,12],9))
	print(binary_search([1,4,7,8,9,12],3))
	result:
	4
	-1
	```
	
6. 爬楼梯

	题目形式：有一个楼梯，总共有10级台阶，每次只能走一级或者两级台阶，全部走完，有多少种走法？  
	题目难度：简单。  
	爬楼梯问题可以用递归来解决，但是如果考虑到时间复杂度，最好用动态规划的思想来处理，这是一个动态规划算法的教科书级别的案例。  
	[关于爬楼梯算法分析](关于爬楼梯算法分析)
	
	```python
	def climb_stairs(n):
    if n==1:
        return 1
    if n==2:
        return 2
    a,b = 1,2
    i = 3
    while i<=n:
        a,b = b,a+b
        i +=1
    return b

	print(climb_stairs(10))
	result:89
	```

6. 两数之和

	题目形式：寻找列表中满足两数之和等于目标值的元素的下标。例如：arr = [2,7,4,9]，target = 6  则返回 [0,2]，若不存在，返回空列表[]。

	题目难度：简单。  
	两数之和问题考察候选人对哈希表可以用空间换取时间这个特性的理解。
	
	```python
	def sum_of_two(arr,target):
    dic = {}
    for i,x in enumerate(arr):
        j = dic.get(target-x,-1)
        if j != -1:
            return((j,i))
        else:
            dic[x] = i
    return([])

	arr = [2,7,4,9]
	target = 6
	print(sum_of_two(arr,target))
	result:(0, 2)
	```

6. 最大回撤
6. 合并两个有序数组
6. 最大连续子数组和
6. 最长不重复子串
6. 全排列
6. 三数之和