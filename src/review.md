# 基础部分：
## 面向对象的基本特征
封装、继承、多态
封装：把实例属性和方法封装成一个类，通过类调用其中的属性方法
继承：子类可以继承父类的属性和方法
多态：重写，子类可以重写父类相同名称相同、参数相同的方法；重载：同一个类中可以有名称相同、参数（类型和个数）不同的同名方法

## final, finally, finalize 的区别
final:声明一个方法或者实例不可被修改
finally：配合try catch使用，finally中的方法必定会被执行
finalize：gc中使用的方法，用于关闭资源，比如文件流等

## equals 与 == 的区别
equals：用于对象值的比较
==：用于对象引用地址的比较

## int和integer类型的区别
int为基本数据类型，integer为封装类，int默认值为0，integer默认值为null

## mvc设计思想
把整个用户交互流程分为 m（model）数据层，用于存储数据对象，v（view）视图层，用户显示数据与用户交互，c（controller）控制器，用于处理用户具体请求，
调用相关的逻辑方法，处理数据层中的数据，返回结果

# 线程部分
## 线程的实现方式
1.继承Thread类 2.实现Runnable接口 3.线程池

## 线程的几种状态
新建（New）：使用new 实例化一个线程的时候
就绪（Runnable）：使用start开始运行一个线程的时候，线程进入就绪状态，等待CPU分配资源
运行（Running）：使用run运行一个线程的时候
死亡（Dead）：当一个线程run命令执行完成，或者使用stop方法停止线程（不推荐使用，stop方法已经过时，而且有一定隐患）
阻塞（Blocked）：等待状态，使用wait命令使一个线程进入等待状态，可用notify唤醒线程，进入就绪状态；睡眠状态，使用sleep命令使线程进入一段时间的休眠状态，结束后进入就绪状态；由于某种原因导致正在运行的线程让出CPU并暂停自己的执行，即进入堵塞状态。

## 线程池
### 常用的线程池：
1.定长线程池 newFixedThreadPool
2.计划线程池 newScheduledThreadPool
3.缓存线程池 newCachedThreadPool
4.单线程线程池 newSingleThreadExecutor

### 线程池属性：
初始线程池大小（CORE_POOL_SIZE）、最大线程池大小（MAX_POOL_SIZE）、存活时间（KEEP_ALIVE_TIME）、超时时间（Time_Unit）、线程池结构（Blocking_Queue）、拒绝策略（Rejected_Execution_Handler）

### 线程池常用的同步工具类
闭锁（CountDownLatch）：允许一个或多个线程一直等待，直到其它线程完成它们的操作。
栅栏（CyclicBarrier）：允许一组线程互相等待，直到到达某个公共屏障点
信号量（Semaphore）：控制同时访问的线程个数

# 中间件部分
## Redis
### 基本数据结构
String、list、hash、set、Zset

### 选择Redis的理由
1.存储数据在内存，多路复用机制，读写速度快：读11W/s，写8.1W/s
2.数据结构较为丰富，适用于更多的场景（同向对比memcached）
3.持久化策略，RDB（内存快照）和AOF(日志文件)，数据容灾恢复，以及使Redis的存储数据不被内存大小所限制
4.可以通过Redis集群机制实现高可用性，哨兵机制，选举机制

### Redis集群
主从库配置（master slave地址）

哨兵配置，哨兵节点至少要有3个，因为至少两个节点的权重才为2，如果少于3个选举机制则不会生效

可能风险：基本由集群数据的异步复制引起的，异步复制（选举出新的master节点的时候，一部分数据还未同步）和脑裂（master节点因为网络原因挂掉，一段时间之后恢复了，但是选举已经完成，这时候就有两个master节点，部分数据还是会写入旧master节点中，然后同步数据时候丢失）





