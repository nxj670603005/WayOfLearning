## 简单的秒杀场景设计
### 前端
1. 按钮置灰，限制按钮点击频率，调用地址加密
2. URL动态化，通过MD5之类的加密算法加密随机的字符串去做url，然后通过前端代码获取url后台校验才能通过。
### 集群
1. 单机的Redis大概能顶得住3-4W的QPS，高了的话就得配置Redis集群了
2. 秒杀服务集群，通过部署多台服务器减少压力，通过nginx负载均衡，也可以用其实现单个用户频繁请求（恶意请求）拦截
### 限流
1. 前端限流：这个很简单，一般秒杀不会让你一直点的，一般都是点击一下或者两下然后几秒之后才可以继续点击，这也是保护服务器的一种手段。
2. 后端限流：秒杀的时候肯定是涉及到后续的订单生成和支付等操作，但是都只是成功的幸运儿才会走到那一步，那一旦100个产品卖光了，return了一个false，前端直接秒杀结束，然后你后端也关闭后续无效请求的介入了。
3. 限流组件
### 超卖问题
1. Lua脚本是类似Redis事务，有一定的原子性，不会被其他命令插队，可以完成一些Redis事务性的操作。
2. 把判断库存扣减库存的操作都写在一个脚本丢给Redis去做，那到0了后面的都Return False了是吧，一个失败了你修改一个开关，直接挡住所有的请求
### 削峰填谷
在秒杀数量较多的情况下，如一万、十万个商品，可以通过消息队列一点点消费去修改数据库，减少数据库压力
