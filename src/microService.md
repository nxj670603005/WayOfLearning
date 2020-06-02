## 微服务架构介绍
1. 微服务架构是一种服务间松耦合的、每个服务之间高度自治并且使用轻量级协议进行通信的可持续集成部署的分布式架构体系。
2. 微服务架构中最核心的部分是服务治理，服务治理最基础的组件是注册中心。Dubbo和Spring Cloud是我们熟知的微服务架构的解决方案。
## 注册中心:
1. dubbo(Zookeeper):支持Zookeeper、Redis、Multicast和Simple。
2. Spring Cloud(Eureka):支持Zookeeper、Consul和Eureka。
## Zookeeper与Eureka:
1. Zookeeper设计原则是CP，即强一致性和分区容错性。他保证数据的强一致性，但舍弃可用性，如果出现网络问题可能会影响Zookeeper的选举，导致Zookeeper注册中心的不可用。
2. Eureka设计原则是AP，即可用性和分区容错性。他保证注册中心的可用性，但舍弃了数据一致性，各节点上的数据有可能是不一致的（会最终一致）。
