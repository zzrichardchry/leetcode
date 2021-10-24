# 简介

Deque是一个双端队列接口，继承自Queue接口，Deque的实现类是LinkedList、ArrayDeque、LinkedBlockingDeque，其中LinkedList是最常用的。

**Deque的三种用途：**

* 普通队列（一端进另一端出）：

  ```java
  Queue queue = new LinkedList()//或者Deque deque = new LinkedList()
  ```

* 双端队列（两端都可以进出）：

  ```java
  Deque deque = new LinkedList()
  ```

* 堆栈：

  ```java
  Deque deque = new LinkedList()
  ```

  Java堆栈类stack已经过时，Java官方推荐使用Deque替代Stack使用。Deque堆栈操作方法：push()、pop()、peek().

Deque是一个线性collection，支持在两端插入和移除元素。名称deque是“double ended queue（双端队列）”的缩写，通常读为“deck”。大多数Deque实现对于它们能够包含的元素没有固定限制，但此接口既支持有容量限制的双端队列，也支持没有固定大小限制的双端队列。

此接口定义在双端队列两端访问元素的方法。提供插入、移除和检查元素的方法。每种方法都存在两种形式：一种形式在操作失败时抛出异常，另一种形式返回一个特殊值（null或false，具体取决于操作）。插入操作的后一种形式是专门为有容量限制的Deque实现设计的；在大多数实现中，插入操作不能失败。

# 用法

| 修饰符和返回值 | 方法名                        | 描述                                            |
| -------------- | ----------------------------- | ----------------------------------------------- |
| **添加功能**   |                               |                                                 |
| void           | push(E)                       | 向一个队列头部插入一个元素，失败时抛出异常。    |
| void           | addFirst(E)                   | 向一个队列头部插入一个元素，失败时抛出异常。    |
| void           | addLast(E)                    | 向一个队列尾部插入一个元素，失败时抛出异常。    |
| boolean        | offerFirst(E)                 | 向一个队列头部插入一个元素，失败时返回false。   |
| boolean        | offerLast(E)                  | 向一个队列尾部插入一个元素，失败时返回false。   |
| **获取功能**   |                               |                                                 |
| E              | getFirst()                    | 获取队列头部元素，队列为空时抛出异常。          |
| E              | getLast()                     | 获取队列尾部元素，队列为空时抛出异常。          |
| E              | peekFirst()                   | 获取队列尾部元素，队列为空时返回null。          |
| E              | peekLast()                    | 获取队列头部元素，队列为空时返回null。          |
| **删除功能**   |                               |                                                 |
| boolean        | removeFirstOccurrence(Object) | 删除第一次出现的指定元素，不存在时返回false。   |
| boolean        | removeLastOccurrence(Object)  | 删除最后一次出现的指定元素，不存在时返回false。 |
| **弹出功能**   |                               |                                                 |
| E              | pop()                         | 弹出队列头部元素，队列为空时抛出异常。          |
| E              | removeFirst()                 | 弹出队列头部元素，队列为空时抛出异常。          |
| E              | removeLast()                  | 弹出队列尾部元素，队列为空时抛出异常。          |
| E              | pollFirst()                   | 弹出队列头部元素，队列为空时返回null。          |
| E              | pollLast()                    | 弹出队列尾部元素，队列为空时返回null。          |
| **迭代器**     |                               |                                                 |
| Iterator<E>    | desendingIterator()           | 返回队列反向迭代器。                            |

可以看出Deque在Queue的方法上新添了对队列头尾元素的操作,add,remove,get形式的方法会在有界队列满员和空队列时抛出异常,offer,poll,peek形式的方法则会返回false或null.

此外方法表中需要注意push = addFirst, pop = removeFirst, 只是使用了不同的方法名体现队列表示栈结构时的特点.

**作为堆栈使用：**

双端队列也可用作 LIFO（后进先出）堆栈。应优先使用此接口而不是遗留 Stack 类。在将双端队列用作堆栈时，元素被推入双端队列的开头并从双端队列开头弹出。堆栈方法完全等效于 Deque 方法，如下表所示：

| 堆栈方法 | 等效Deque方法 |
| -------- | ------------- |
| push(e)  | addFirst(e)   |
| pop()    | removeFirst() |
| peek()   | peekFirst()   |

