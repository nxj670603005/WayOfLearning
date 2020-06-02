## 微服务架构介绍
1. 微服务架构是一种服务间松耦合的、每个服务之间高度自治并且使用轻量级协议进行通信的可持续集成部署的分布式架构体系。
2. 微服务架构中最核心的部分是服务治理，服务治理最基础的组件是注册中心。Dubbo和Spring Cloud是我们熟知的微服务架构的解决方案。
## 注册中心:
1. dubbo(Zookeeper):支持Zookeeper、Redis、Multicast和Simple。
2. Spring Cloud(Eureka):支持Zookeeper、Consul和Eureka。
## Zookeeper与Eureka:
1. Zookeeper设计原则是CP，即强一致性和分区容错性。他保证数据的强一致性，但舍弃可用性，如果出现网络问题可能会影响Zookeeper的选举，导致Zookeeper注册中心的不可用。
2. Eureka设计原则是AP，即可用性和分区容错性。他保证注册中心的可用性，但舍弃了数据一致性，各节点上的数据有可能是不一致的（会最终一致）。
## 顺序一致性
1. 假设有一个Zookeeper集群（N>=3，N为奇数），那么只有一个Leader（通过FastLeaderElection选主策略选取），所有的写操作（客户端请求Leader或Follower的写操作）都由Leader统一处理，Follower虽然对外提供读写，但写操作会提交到Leader，由Leader和Follower共同保证同一个Follower请求的顺序性，Leader会为每个请求生成一个zxid（高32位是epoch，用来标识leader选举周期，每次一个leader被选出来，都会有一个新的epoch，标识当前属于哪个leader的统治时期，低32位用于递增计数）
2. 针对同一个Follower A提交的写请求request1、request2，某些Follower虽然可能不能在请求提交成功后立即看到（也就是强一致性），但经过自身与Leader之间的同步后，这些Follower在看到这两个请求时，一定是先看到request1，然后再看到request2，两个请求之间不会乱序，即顺序一致性
3. 不管这多个客户端的请求顺序如何交叠，都可以，但是必须按照请求到达的顺序执行，即顺序一致性
4. 相应的也要看是针对一个客户端达到顺序一致性还是针对所有客户端都达到顺序一致性，实现也是不同的
## Eureka的可用性
Eureka Client 会定时的连接Eureka Server，获取注册表里的信息进行缓存到本地，如果微服务发现不可用了Eureka Client 就不会更新，就会影响微服务的调用，所以要一个有高可用的Eureka Server 集群，Eureka Server 可以通过运行多个实例来相互注册的方式实现高可用部署。从而保证里数据的一致性。
## Zookeeper的缺陷
1. 本身不是为高可用性设计，master撑不住高流量容易导致系统crash。当然，对网络隔离的敏感也导致Zookeeper的脆弱。（典型的zookeeper的tps大概是一万多，无法覆盖系统内部每天动辄几十亿次的调用。因此每次请求都去zookeeper获取业务系统master信息是不可能的。因此zookeeper的client必须自己缓存业务系统的master地址。因此zookeeper提供的‘强一致性’实际上是不可用的。如果我们需要强一致性，还需要其他机制来进行保障：比如用自动化脚本把业务系统的old master给kill掉，但是那会有很多陷阱）
2. 一致性同步协议（ZAB）的复杂性，选举过程或许缓慢，结合上一点，动辄需要重新选举master导致耗时过长。（zookeeper的选举流程通常耗时30到120秒，期间zookeeper由于没有master，都是不可用的。对于网络里面偶尔出现的，比如半秒一秒的网络隔离，zookeeper会由于选举过程，而把不可用时间放大几十倍。）
3. 难以避免数据的不一致。（在是否要kill current master这个问题上，程序是无法完全自动决定的，因为网络隔离的时候zookeeper已经不可用了，自动脚本没有全局信息，不管怎么做都可能是错的，什么都不做也可能是错的。当网络故障的时候，只有运维人员才有全局信息，程序是无法接电话得知其他机房的情况的）
4. metadata对namenode的频繁访问导致大量disk I/O，限制应用的速度。而且，用SSD代替HDD也有自身缺陷，在此就不赘述。
5. zookeeper无法进行有效的权限控制，权限控制非常薄弱

