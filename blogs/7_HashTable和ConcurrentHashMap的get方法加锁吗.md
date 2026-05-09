# HashTable和ConcurrentHashMap的get方法加锁吗



> 为什么 Hashtable 的 get 操作需要加锁，但 ConcurrentHashMap 的 get 操作却能在不加锁的情况下保证线程安全？这篇博客从底层原理出发，帮助你理解它们在线程安全与性能之间的取舍。



## HashTable 的 `get()` 加锁

实际上，**HashTable 的所有方法都加锁**，因为它的所有方法都被 synchronized 修饰。

在线程执行任何一个方法时，都会锁住整个 HashTable 对象。即使某个线程执行 `get()` 方法，其他线程也不能执行任何方法，连 `get()` 也不能执行。



## ConcurrentHashMap 的 `get()` 不加锁

`get()` 即使不加锁，也能保证线程安全。粗略地说，**它用到 `volatile` 保证「内存可见性」**。



想要讲清楚为什么不加锁，需要先了解 ConcurrentHashMap 的 Node 节点：

Node 节点在 JDK 7 是 HashEntry；在 JDK8 是数组中的元素节点（链表、红黑树中的每个节点，都被称为 Node）。



Node 中有一些关键字段，例如 `val`、`next`，它们被 `volatile` 修饰。

`volatile` 保证了「**内存可见性**」。如果有线程执行了 `put()`，修改的结果立刻对其他线程可见，也就是说，**`volatile` 保证读到的 `val` 和 `next` 是最新的**，`get()` 可以读到最新的数据。从而保证了线程安全。

