# 基础篇

## Java 基础
### 面向对象的特征
1. 封装：把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。
2. 继承：可以使用现有类的所有功能，并在无需重新编写原来的类的情况下对这些功能进行扩展。
3. 多态：允许将子类类型的指针赋值给父类类型的指针。实现多态，有二种方式，覆盖，重载。
### [集合](src/baseSet.md)
### [JVM内存区域](src/jvm.md)
### final, finally, finalize 的区别
1. final：声明一个类或方法不可被修改、继承
2. finally：配合try catch使用，finally中的语句一定会被执行
3. finalize：object类中的方法，垃圾回收时候使用，用于回收资源，如关闭文件流
### int 和 Integer 有什么区别
1. int 是 Java 提供的 8 种原始数据类型之一，默认值为0
2. Java 为每个原始类型提供了封装类，Integer 是 Java 为 int 提供的封装类。，默认值为null
### 重载和重写的区别
1. 重载：同一个类中，参数类型或个数不同的同名方法，叫做重载
2. 重写：子类重写父类的同名方法的具体实现，叫做重写
### [抽象类和接口有什么区别](src/classAndInterface.md)
### 说说反射的用途及实现
用于获取类运行时的状态信息，如用于获取类运行日志，获取错误信息等
### 说说自定义注解的场景及实现
### HTTP 请求的 GET 与 POST 方式的区别
1. 根据 HTTP 规范，GET 用于信息获取，而且应该是安全的和幂等的。
2. 根据 HTTP 规范，POST 表示可能修改变服务器上的资源的请求。
3. GET请求有长度限制，一般为1024字节（因为是通过URL提交数据，浏览器限制，不同浏览器限制不同），而POST没有限制
### session 与 cookie 区别
session是服务器的用户信息，而cookie是用户浏览器存储的用户信息，一般浏览器cookie是有大小限制的，单个cookie 保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。
### session 分布式处理
1. 在支持 Session 复制的 Web 服务器上，通过修改 Web 服务器的配置，可以实现将 Session 同步到其它 Web 服务器上，达到每个 Web 服务器上都保存一致的 Session，如Tomcat可以通过配置来实现多个项目之间的session共享。
2. 优点：代码上不需要做支持和修改。
3. 缺点：需要依赖支持的 Web 服务器，一旦更换成不支持的 Web 服务器就不能使用了，在数据量很大的情况下不仅占用网络资源，而且会导致延迟。
4. 适用场景：只适用于Web服务器比较少且 Session 数据量少的情况。
5. 可用方案：开源方案 tomcat-redis-session-manager，暂不支持 Tomcat8。
### JDBC 流程
1. 向 DriverManager 类注册驱动数据库驱动程序
2. 调用 DriverManager.getConnection 方法， 通过 JDBC URL，用户名，密码取得数据库连接的 Connection 对象。
3. 获取 Connection 后， 便可以通过 createStatement 创建 Statement 用以执行 SQL 语句。
4. 有时候会得到查询结果，比如 select，得到查询结果，查询（SELECT）的结果存放于结果集（ResultSet）中。
5. 关闭数据库语句，关闭数据库连接。
### MVC 设计思想
1. MVC设计思想可以把用户端和服务端整个交互流程分为，M（model）数据层，用于存储用户数据，V（view）视图层，用于显示和用户的交互信息，C（controller）控制器，用于处理用户请求
2. MVC流程，用户发出请求，核心控制器接受到请求，从数据层读取数据进行对应的处理，处理好数据之后返回，然后返回结果到视图层
### equals 与 == 的区别
equals是对象值之间的比较，==是对象引用地址之前的比较
### 死锁
产生死锁的四个必要条件：
1. 互斥条件：一个资源每次只能被一个进程使用。
2. 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
3. 不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺。
4. 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。
### 什么是进程，什么是线程？
1. 进程：是并发执行的程序在执行过程中分配和管理资源的基本单位，是一个动态概念，竞争计算机系统资源的基本单位。
2. 线程：是进程的一个执行单元，是进程内科调度实体。比进程更小的独立运行的基本单位。线程也被称为轻量级进程。
3. 一个程序至少一个进程，一个进程至少一个线程。

## Java 集合
### List 和 Set 区别
list元素有放入顺序，允许重复元素出现，set元素无放入顺序，不允许重复元素（注意：元素虽然无放入顺序，但是元素在 set 中的位置是有该元素的 HashCode 决定的，其位置其实是固定的）
### List 和 Map 区别
list是数组结构的，元素有放入顺序，map则是键值对结构的，无放入顺序 ，数组+链表结构
### ArrayList 与 LinkedList 区别
1. ArrayList是无序数组，查询的时间复杂度是O（1），插入删除的时间复杂度是O(n)，因为需要重新计算下标，除非是尾插
2. linkedlist是链表形式的，查询的时间复杂度是O（n），插入删除的时间复杂度是O(1)
### ArrayList 与 Vector 区别
1. ArrayList：不是线程安全的，扩容为1.5n
2. Vector：是线程安全的，里面加了synchronized锁，扩容为2n
### HashMap 和 HashTable 的区别
1. HashMap：初始大小为16，扩容为0.75的时候，扩容大小为2n，不是线程安全的，键值对可以为null，在单一线程下使用，效率较高
2. HashTable：初始大小为11，扩容为0.75的时候，扩容大小为2n+1，里面有synchronized结构，是线程安全的，效率较低
### HashSet 和 HashMap 区别
1. HashMap：实现了 Map 接口，储存键值对，使用键对象来计算 hashcode 值
2. HashSet：实现了 Set 接口，仅仅存储对象，使用 add() 方法将元素放入 set 中，HashSet 使用成员对象来计算 hashcode 值，对于两个对象来说 hashcode 可能相同，所以 equals() 方法用来判断对象的相等性，如果两个对象不同的话，那么返回 false
### HashMap 和 ConcurrentHashMap 的区别
HashMap不是线程安全的，ConcurrentHashMap采用了分段锁结构，默认为16，两者都继承了AbstractMap
### HashMap 的工作原理及代码实现
HashMap 基于 hashing 原理，我们通过 put() 和 get() 方法储存和获取对象。当我们将键值对传递给 put() 方法时，它调用键对象的 hashCode() 方法来计算 hashcode，让后找到 bucket 位置来储存值对象。当获取对象时，通过键对象的 equals() 方法找到正确的键值对，然后返回值对象。HashMap 使用链表来解决碰撞问题，当发生碰撞了，对象将会储存在链表的下一个节点中。 HashMap 在每个链表节点中储存键值对对象。
### ConcurrentHashMap 的工作原理及代码实现

## Java 线程
### 创建线程的方式及实现
1. 继承Thread类
2. 实现Runnable接口
3. 线程池
### sleep() 、join（）、yield（）有什么区别
1. sleep()
    - sleep() 方法需要指定等待的时间，它可以让当前正在执行的线程在指定的时间内暂停执行，进入阻塞状态，该方法既可以让其他同优先级或者高优先级的线程得到执行的机会，也可以让低优先级的线程得到执行机会。但是 sleep() 方法不会释放“锁标志”，也就是说如果有 synchronized 同步块，其他线程仍然不能访问共享数据。
2. wait()
    - wait() 方法需要和 notify() 及 notifyAll() 两个方法一起介绍，这三个方法用于协调多个线程对共享数据的存取，所以必须在 synchronized 语句块内使用，也就是说，调用 wait()，notify() 和 notifyAll() 的任务在调用这些方法前必须拥有对象的锁。注意，它们都是 Object 类的方法，而不是 Thread 类的方法。
    - wait() 方法与 sleep() 方法的不同之处在于，wait() 方法会释放对象的“锁标志”。当调用某一对象的 wait() 方法后，会使当前线程暂停执行，并将当前线程放入对象等待池中，直到调用了 notify() 方法后，将从对象等待池中移出任意一个线程并放入锁标志等待池中，只有锁标志等待池中的线程可以获取锁标志，它们随时准备争夺锁的拥有权。当调用了某个对象的 notifyAll() 方法，会将对象等待池中的所有线程都移动到该对象的锁标志等待池。
    - 除了使用 notify() 和 notifyAll() 方法，还可以使用带毫秒参数的 wait(long timeout) 方法，效果是在延迟 timeout 毫秒后，被暂停的线程将被恢复到锁标志等待池。
    - 此外，wait()，notify() 及 notifyAll() 只能在 synchronized 语句中使用，但是如果使用的是 ReenTrantLock 实现同步，该如何达到这三个方法的效果呢？解决方法是使用 ReenTrantLock.newCondition() 获取一个 Condition 类对象，然后 Condition 的 await()，signal() 以及 signalAll() 分别对应上面的三个方法。
3. yield()
    - yield() 方法和 sleep() 方法类似，也不会释放“锁标志”，区别在于，它没有参数，即 yield() 方法只是使当前线程重新回到可执行状态，所以执行 yield() 的线程有可能在进入到可执行状态后马上又被执行，另外 yield() 方法只能使同优先级或者高优先级的线程得到执行机会，这也和 sleep() 方法不同。
4. join()
    - join() 方法会使当前线程等待调用 join() 方法的线程结束后才能继续执行
### 线程的拒绝策略
1. ThreadPoolExecutor.AbortPolicy:丢弃任务并抛出RejectedExecutionException异常。
2. ThreadPoolExecutor.DiscardPolicy：丢弃任务，但是不抛出异常。
3. ThreadPoolExecutor.DiscardOldestPolicy：丢弃队列最前面的任务，然后重新提交被拒绝的任务
4. ThreadPoolExecutor.CallerRunsPolicy：由调用线程（提交任务的线程）处理该任务
### 说说 CountDownLatch 原理
1. 闭锁，CountDownLatch 内部维护了一个整数 n，n（要大于等于0）在 当前线程 初始化 CountDownLatch 方法指定。当前线程调用 CountDownLatch 的 await() 方法阻塞当前线程，等待其他调用 CountDownLatch 对象的 CountDown() 方法的线程执行完毕。 其他线程调用该 CountDownLatch 的 CountDown() 方法，该方法会把 n-1，直到所有线程执行完成，n 等于 0，当前线程 就恢复执行。
2. 具体实现：countDownLatch.await(); 等待 countDownLatch.countDown(); 开始
### 说说 CyclicBarrier 原理
1. 栅栏，CyclicBarrier 是一个同步辅助类,允许一组线程互相等待,直到到达某个公共屏障点(CommonBarrierPoint)。因为该 barrier 在释放等待线程后可以重用,所以称它为循环的 barrier。
2. 具体方法：CyclicBarrier.await();
### 说说 Semaphore 原理
1. 信号量，Semaphore 直译为信号。实际上 Semaphore 可以看做是一个信号的集合。不同的线程能够从 Semaphore 中获取若干个信号量。当 Semaphore 对象持有的信号量不足时，尝试从 Semaphore 中获取信号的线程将会阻塞。直到其他线程将信号量释放以后，阻塞的线程会被唤醒，重新尝试获取信号量。
2. 具体方法：semaphore.acquire(); 开始 semaphore.release(); 释放
### 说说 Exchanger 原理
### 说说 CountDownLatch 与 CyclicBarrier 区别
### ThreadLocal 原理分析
### 讲讲线程池的实现原理
### 线程池的几种方式与使用场景
1. newCachedThreadPool ：缓存线程池，如果线程池长度超过处理需要，可回收空闲线程，若无可回收，则新建线程。
2. newFixedThreadPool ： 定长线程池，可控制线程最大并发数，超出的线程会在队列中等待。
3. newScheduledThreadPool ： 计划线程池，支持定时及周期性任务执行。
4. newSingleThreadExecutor ：单线程线程池，用唯一的线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行
### 线程的生命周期

## Java 锁机制
### 说说线程安全问题
1. 最简单的方式，使用 Synchronization 关键字
2. 使用 java.util.concurrent.atomic 包中的原子类，例如 AtomicInteger
3. 使用 java.util.concurrent.locks 包中的锁
4. 使用线程安全的集合 ConcurrentHashMap
5. 使用 volatile 关键字，保证变量可见性（直接从内存读，而不是从线程 cache 读）
### volatile 实现原理
1. 在 JVM 底层 volatile 是采用“内存屏障”来实现的
2. 缓存一致性协议（MESI协议）它确保每个缓存中使用的共享变量的副本是一致的。其核心思想如下：当某个 CPU 在写数据时，如果发现操作的变量是共享变量，则会通知其他 CPU 告知该变量的缓存行是无效的，因此其他 CPU 在读取该变量时，发现其无效会重新从主存中加载数据
### synchronize 实现原理
同步代码块是使用 monitorenter 和 monitorexit 指令实现的，同步方法（在这看不出来需要看 JVM 底层实现）依靠的是方法修饰符上的 ACC_SYNCHRONIZED 实现。
### synchronized 与 lock 的区别
### CAS 乐观锁
compare and swap 比较替换，比较原值和预期值有无区别，如果一致则修改，但可能引起ABA问题
### ABA 问题
一个值经过多次修改，如10→20→10，你比较值一致，但是实际经过了多次修改，可以采用版本号来区分，版本号是一直递增的
### 乐观锁的业务场景及实现方式

# 核心篇

## 数据存储
### 58 到家 MySQL 军规升级版（如何优化 MySQL）
### [MySQL 索引使用的注意事项](src/index.md)
### 说说反模式设计
### 说说分库与分表设计
### 分库与分表带来的分布式困境与应对之策
### [SQL优化](src/sqlOptimization.md)
### MySQL 遇到的死锁问题
### 存储引擎的 InnoDB 与 MyiSAM
### 数据库索引的原理
### 为什么要用 B-Tree
### 聚集索引与非聚集索引的区别
### limit 20000 加载很慢怎么解决
### 选择合适的分布式主键方案
### 选择合适的数据存储方案
### ObjectId 规则
### 聊聊 MongoDB 使用场景
### 倒排索引
### 聊聊 ElasticSearch 使用场景
### [测试resultType和resultMap](https://www.cnblogs.com/nxjblog/p/13040019.html)



## 缓存使用
### Redis 有哪些类型
String、list、hash、set、zset
### Redis 内部结构
### Redis 内存淘汰机制
### 聊聊 Redis 使用场景
### Redis 持久化机制
1. RDB内存快照，5分钟一次
2. AOF日志文件，秒级的
### Redis 集群方案与实现
1. 主从集群配置，即配置master和slave
2. 哨兵配置
### Redis 为什么是单线程的
### 缓存雪崩
大量缓存在同一时间失效，解决方法：可以在过期时间上增加一个随机值；缓存预热
### 缓存穿透
布隆过滤器，不在过滤器中的元素直接返回，有误判值（可以设置错误率），已经在过滤器的值一般都会匹配上，误判值一般是不在过滤器内的值，匹配成功放过去了，不过问题不大，Redis中也有自带布隆过滤器，用bf.add和bf.exist操作
### 缓存击穿
    - 热点数据失效，导致大量请求打到数据库，
    - 解决方案：
    1. 缓存预热，设置设置热点数据永远不过期
    2. 使用互斥锁(mutex key)。对缓存查询加锁，如果KEY不存在，就加锁，然后查DB入缓存，然后解锁；其他进程如果发现有锁就等待，然后等解锁后返回数据或者进入DB查询
### 缓存崩溃
### 缓存降级
### 使用缓存的合理性问题

## 消息队列
### 消息队列的使用场景
### 消息的重发补偿解决思路
### 消息的幂等性解决思路
### 消息的堆积解决思路
### 自己如何实现消息队列
### 如何保证消息的有序性

# 框架篇
## Spring
### BeanFactory 和 ApplicationContext 有什么区别
### Spring Bean 的生命周期
•Spring Bean 的生命周期简单易懂。在一个 bean 实例被初始化时，需要执行一系列的初始化操作以达到可用的状态。同样的，当一个 bean 不在被调用时需要进行相关的析构操作，并从 bean 容器中移除。
•Spring bean factory 负责管理在 spring 容器中被创建的 bean 的生命周期。Bean 的生命周期由两组回调（call back）方法组成。◦初始化之后调用的回调方法。
◦销毁之前调用的回调方法。
•Spring 框架提供了以下四种方式来管理 bean 的生命周期事件：◦InitializingBean 和 DisposableBean 回调接口
◦针对特殊行为的其他 Aware 接口
◦Bean 配置文件中的 Custom init() 方法和 destroy() 方法
◦@PostConstruct 和 @PreDestroy 注解方式
### Spring IOC 如何实现
•Spring 中的 org.springframework.beans 包和 org.springframework.context 包构成了 Spring 框架 IoC 容器的基础。
•BeanFactory 接口提供了一个先进的配置机制，使得任何类型的对象的配置成为可能。ApplicationContext 接口对 BeanFactory（是一个子接口）进行了扩展，在 BeanFactory 的基础上添加了其他功能，比如与 Spring 的 AOP 更容易集成，也提供了处理 message resource 的机制（用于国际化）、事件传播以及应用层的特别配置，比如针对 Web 应用的 WebApplicationContext。
•org.springframework.beans.factory.BeanFactory 是 Spring IoC 容器的具体实现，用来包装和管理前面提到的各种 bean。BeanFactory 接口是 Spring IoC 容器的核心接口。
### 说说 Spring AOP
面向切面编程，在我们的应用中，经常需要做一些事情，但是这些事情与核心业务无关，比如，要记录所有 update 方法的执行时间时间，操作人等等信息，记录到日志，
通过 Spring 的 AOP 技术，就可以在不修改 update 的代码的情况下完成该需求。
### Spring AOP 实现原理
Spring AOP 中的动态代理主要有两种方式，JDK 动态代理 和 CGLIB 动态代理。JDK 动态代理通过反射来接收被代理的类，并且要求被代理的类必须实现一个接口。JDK 动态代理的核心是 InvocationHandler 接口和 Proxy 类。

如果目标类没有实现接口，那么 Spring AOP 会选择使用 CGLIB 来动态代理目标类。CGLIB（Code Generation Library），是一个代码生成的类库，可以在运行时动态的生成某个类的子类，注意，CGLIB 是通过继承的方式做的动态代理，因此如果某个类被标记为 final，那么它是无法使用 CGLIB 做动态代理的。
### 动态代理（CGLIB 与 JDK）
### Spring 事务实现方式
编码方式：
所谓编程式事务指的是通过编码方式实现事务，即类似于 JDBC 编程实现事务管理。

声明式事务管理
