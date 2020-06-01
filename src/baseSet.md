## Collection
### List
1. LinkedList
    - LinkedList 是链表的操作
    - get() 获取第几个元素，依次遍历，复杂度O(n)
    - add(E) 添加到末尾，复杂度O(1)
    - add(index, E) 添加第几个元素后，需要先查找到第几个元素，直接指针指向操作，复杂度O(n)
    - remove（）删除元素，直接指针指向操作，复杂度O(1)
2. ArrayList
    - ArrayList 是线性表（数组）
    - get() 直接读取第几个下标，复杂度 O(1)
    - add(E) 添加元素，直接在后面添加，复杂度O（1）
    - add(index, E) 添加元素，在第几个元素后面插入，后面的元素需要向后移动，复杂度O（n）
    - remove（）删除元素，后面的元素需要逐个移动，复杂度O（n）
3. Vector
### Set
1. 特点：
    - 不允许元素重复
    - 不会记录元素的添加先后顺序
    - Set只包含从Collection继承的方法，不过Set无法记住添加的顺序，不允许包含重复的元素。当试图添加两个相同元素进Set集合，添加操作失败，add()方法返回false
    - set接口定义了一种规范，也就是该容器不记录元素的添加顺序，也不允许元素重复。
2. HashSet
    - 底层数据结构是哈希表(是一个元素为链表的数组)
3. TreeSet
    - 底层数据结构是红黑树(是一个自平衡的二叉树)
    - 保证元素的排序方式
4. LinkedHashSet
    - 底层数据结构由哈希表和链表组成。
## Map
1. Hashtable
    - Hashtable 是一个散列表，它存储的内容是键值对(key-value)映射。
    - 继承于Dictionary，实现了Map、Cloneable、java.io.Serializable接口。
    - 函数都是同步的，这意味着它是线程安全的。它的key、value都不可以为null。
2. HashMap
    - 由数组和链表组合构成的数据结构
    - 数组里面每个地方都存了Key-Value这样的实例，在Java7叫Entry在Java8中叫Node
    - 因为他本身所有的位置都为null，在put插入的时候会根据key的hash去计算一个index值
    - 扩容机制：一共分为两步，第一步扩容：创建一个新的Entry空数组，长度是原数组的2倍。第二步，ReHash：遍历原Entry数组，把所有的Entry重新Hash到新数组。
3. WeakHashMap
4. ConcurrentHashMap
5. TreeMap
    - 底层是红黑树来实现的
