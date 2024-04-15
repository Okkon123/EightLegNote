# 常见集合框架
1. Collection
	1. List
	2. Set
	3. Queue
2. Map
	1. HashMap
	2. TreeMap
![[Pasted image 20240401133810.png]]
# List
## ArrayList 和 LinkedList区别
1. 数据结构
2. 用途不同
3. 是否支持随机访问
4. 内存占用

## ArrayList扩容机制
![[Pasted image 20240401134752.png]]
## ArrayList序列化
不直接序列化数组，逐个序列化元素。

## 快速失败 && 安全失败
快速失败：迭代器遍历对象时，另外一个线程对集合对象修改，会抛出Concurrent Modification
安全失败：遍历时深拷贝原先内容，再遍历。

## 实现ArrayList线程安全的方法
1. 使用Vector代替ArrayList
2. 使用Collections.synchronizedList包装ArrayList，操作包装后的list
3. 使用CopyOnWriteArrayList代替ArrayList
4. 使用ArrayList时，应用程序通过同步机制去控制ArrayList的读写。
## CopyOnWriteArrayList
![[Pasted image 20240401135738.png]]
# Map

## HashMap 数据结构
![[Pasted image 20240401140349.png]]
## 为什么不用二叉树/平衡树
二叉树：最坏情况退化为链表
平衡二叉树：插入删除效率低，维护成本大

## 红黑树如何保持平衡
1. 左旋
2. 右旋
3. 染色

## HashMap的put流程
![[Pasted image 20240401141005.jpg]]

## HashMap怎么查找元素
![[Pasted image 20240401141034.png]]
## HashMap的哈希/扰动函数如何和设计
HashMap 的哈希函数是先拿到 key 的 hashcode，是一个 32 位的 int 类型的数值，然后让 hashcode 的高 16 位和低 16 位进行异或操作。

## 为什么哈希/扰动函数能降低hash碰撞
自己的高半区和低半区做异或，就是为了混合原始哈希码的高位和低位，以此来加大低位的随机性。

## 为什么HashMap的容量是2的倍数
快速定位元素下标

## 初始化HashMap容量不为2的倍数
HashMap会想上寻找离2最近的2的倍数。

## 常见哈希函数的构造方法
1. 除留取余法
2. 直接定址法
3. 数字分析法
4. 平方取中法
5. 折叠法

## 解决哈希冲突的方法
1. 链地址法
2. 开放定址法
3. 再哈希法
4. 建立公共溢出区

## 为什么HashMap 链表转红黑树的阈值为8
红黑树节点大小更大。
红黑树回转链表的阈值是6。
## 扩容在什么时候？为什么扩容因子是0.75
扩容：存储键值对数量超过阈值(容量 * 加载因子)
对空间成本和时间成本考虑选择了0.75。

## 扩容机制
1. 超过阈值扩容
2. jdk1.8 原来元素要么在原来索引，要么在原索引+原来容量

## jdk1.8 对HashMap的优化
1. 数据结构
2. 链表插入方式(1.8尾插)
3. 扩容rehash
4. 扩容时机
5. 散列函数

## HashMap是线程安全的吗
不是
1. 多线程下扩容死循环
2. 多线程put可能造成元素的丢失
3. get和put并发时，可能导致get为null

## 如何解决HashMap线程不安全问题
1. HashTable 直接在方法上加synchronized
2. Collections.synchronizedMap 
3. ConcurrentHashMap

## ConcurrentHashMap实现

## HashMap节点是有序的吗
无序的

## LinkedHashMap如何实现有序的
LinkedHashMap维护了一个双向链表，可以实现按插入的顺序或访问顺序排序。

## TreeMap如何实现有序
TreeMap按照Comparator的顺序进行排序。

# Set
## HashSet底层实现
基于HashMap实现

HashSet和ArrayList区别
1. ArrayList基于动态数组实现，HashSet基于HashMap实现
2. ArrayList允许重复元素和null值，可以有相同元素
3. ArrayList保证元素的插入顺序

## HashSet怎么判断元素重复，重复了是否put

![[Pasted image 20240401152335.jpg]]
HashSet 通过元素的哈希值来判断元素是否重复，如果重复了，会覆盖原来的值。