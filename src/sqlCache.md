## 先拿Mybatis举例
1. 一级缓存（默认开启）
    - 也称本地缓存，sqlSession级别的缓存。一级缓存是一直开启的；与数据库同一次回话期间查询到的数据会放在本地缓存中。
    - 同一个sqlsession会话中，如果查询SQL以及参数相同则会走一级缓存查询，如果需要获取相同的数据，直接从缓存中拿，不会再查数据库。
    - 一级缓存失效的四种情况：
    1. sqlSession不同
    2. sqlSession相同，查询条件不同。因为缓存条件不同，缓存中还没有数据
    3. sqlSession相同，在两次相同查询条件中间执行过增删改操作。（因为中间的增删改可能对缓存中数据进行修改，所以不能用）
    4. sqlSession相同，手动清空了一级缓存
2. 二级缓存
    - 全局缓存；基于namespace级别（比如一个mapper文件）的缓存。一个namespace对应一个二级缓存。
    - 一个会话，查询一条数据，这个数据会被放在当前会话的一级缓存中，如果会话被关闭了而且开启了二级缓存，一级缓存中的数据会被保存带二级缓存。新的会话查询信息就会参照二级缓存。
    - 开启步骤
    1. 开启全局缓存配置。<settings><setting name="cacheEnabled" value="true"/></settings>，也可注解开启
    2. 因为是namespace级别，需要搭配每个xxxMapper.xml中配置二级缓存<cache></cache>
    - 不同namespace的二级缓存可能存在脏读，脏写的情况，应该避免使用，而是去使用Redis等缓存中间件
3. 缓存首先一进来去查二级缓存，二级缓存没有去找一级缓存，一级缓存没有去找数据库。二级缓存----->一级缓存-------->数据库。
