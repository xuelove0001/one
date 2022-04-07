List类：

subList() 方法可以轻松地从更大的列表中创建切片

retainAll() 方法实际上是一个 “集合交集” 操作它保留了同时在 copy 和 sub 中的所有元素。

removeAll() 方法也是基于 equals() 方法运行的

==链表 LinkedList==

​		LinkedList 也像 ArrayList 一样实现了基本的 List 接口，但它在 List 中间执行 插入和删除操作时比 ArrayList 更高效。然而, 它在随机访问操作效率方面却要逊色一 些。

​		==LinkedList 还添加了一些方法，使其可以被用作栈、队列或双端队列（deque）==。 在这些方法中，有些彼此之间可能只是名称有些差异，或者只存在些许差异，以使得这 些名字在特定用法的上下文环境中更加适用（特别是在 Queue 中）。例如：

​	 • getFirst() 和 element() 是相同的，它们都返回列表的头部（第一个元素）而并 不删除它，如果 List 为空，则抛出 NoSuchElementException 异常。peek() 方法与这两个方法只是稍有差异，它在列表为空时返回 null 。

​	 • removeFirst() 和 remove() 也是相同的，它们删除并返回列表的头部元素，并 在列表为空时抛出 NoSuchElementException 异常。poll() 稍有差异，它在列 表为空时返回 null 。

​	• addFirst() 在列表的开头插入一个元素。

​	• offer() 与 add() 和 addLast() 相同。它们都在列表的尾部（末尾）添加一个元 素。

​	• removeLast() 删除并返回列表的最后一个元素。

==Queue==:

​		如果查看 Queue 接口就会发现，它在 LinkedList 的基础上添加了 element() ，offer() ，peek() ，poll() 和 remove() 方法，以使其可以成为一个 Queue 的实现。

==堆栈 Stack==

​		堆栈是 “后进先出”（LIFO）集合。它有时被称为叠加栈（pushdown stack），因为 最后 “压入”（push）栈的元素，第一个被 “弹出”（pop）栈。经常用来类比栈的事物是 带有弹簧支架的自助餐厅托盘。最后装入的托盘总是最先拿出来使用的。

==集合 Set==（Set 就是一个 Collection只是行为不同。）

​	**Set 不保存重复的元素**。Set 最常见的用途是测试归属性可以很轻松地询问某个对象是否 在一个 Set 中。因此通常会选择 HashSet 实 现，该实现针对快速查找进行了优化。

​	