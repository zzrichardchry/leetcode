# 定义

Vector类实现了一个动态数组，和ArrayList蕾丝，但是两者不同点有：

* Vector 是同步访问的。
* Vector包含了许多传统的方法，这些方法不属于集合框架。

Vector主要用在事先不知道数组的大小，或者是只需要一个可以改变大小的数组的情况。

### 源码

```java
public class Vector<E>
    extends AbstractList<E>
    implements List<E>, RandomAccess, Cloneable, java.io.Serializable{
  
  protected Object[] elementData;//用initillCapacity来通过Object来构造给elementData
  protected int elementCount;//Object中有效的component
  protected int capacity Increment;//当增加到超过vector本身的容量的时候自动增加的元素个数
  
  ...}
```

# 构造方法

1. 默认构造方法，大小为10。

   ```java
   Vector()
   ```
   ```java
   public Vector() {this(10);} 
   //源码
   ```

2. 指定大小进行创建。

   ```java
   Vector(int size)
   ```

   ```java
   public Vector(int initialCapacity) {this(initialCapacity, 0);}
   //源码
   ```

3. 指定创建大小以，增量用incr指定。增量表示响亮每次增加的元素数目。

   ```java
   Vector(int size,int incr)
   ```

   ```java
   public Vector(int initialCapacity, int capacityIncrement) {
           super();
           if (initialCapacity < 0)
               throw new IllegalArgumentException("Illegal Capacity: "+
                                                  initialCapacity);
           this.elementData = new Object[initialCapacity];
           this.capacityIncrement = capacityIncrement;
   }
   //源码
   ```

4. 创建一个包含集合c元素的向量。

   ```java
   Vector(Collection c)
   ```

   ```java
   public Vector(Collection<? extends E> c) {
           elementData = c.toArray();
           elementCount = elementData.length;
           // defend against c.toArray (incorrectly) not returning Object[]
           // (see e.g. https://bugs.openjdk.java.net/browse/JDK-6260652)
           if (elementData.getClass() != Object[].class)
               elementData = Arrays.copyOf(elementData, elementCount, Object[].class);
   }
   //源码
   ```

# Vector的方法

1. ```java
   void add(int index, Object element)
   ```

   在此向量的指定位置插入指定的元素。

   ```java
   private void add(E e, Object[] elementData, int s) {
           if (s == elementData.length)
               elementData = grow();
           elementData[s] = e;
           elementCount = s + 1;
   }
   ```
   
2. ```java
   boolean add(Object o)
   ```

   将指定元素添加到此向量的末尾。

3. ```java
   boolean addAll(Collection c)
   ```

   将指定Collection中的所有元素添加到此向量的末尾，按照指定collection的迭代器所返回的顺序添加这些元素。

4. ```java
   boolean addAll(int index, Collection c)
   ```

   在指定位置将指定Collection中的所有元素插入到此向量中。

5. ```java
   void addElement(Object obj)
   ```

   将指定的组件添加到此向量的末尾，将其大小增加1.

6. ```java
   int capacity()
   ```

   返回此向量当前的容量。
   
7. ```java
   void clear();
   ```

   从此向量中移除所有元素。

8. ```java
   Object clone()
   ```

   返回向量的一个副本。

9. ```java
   boolean contains(Object elem)
   ```

   如果此向量包含指定的元素，则返回true。

10. ```java
    boolean containsall(Collection c)
    ```

    如果此向量包含指定Collection中的所有元素，则返回true。

11. ```java
    void copyInto(Object[] anArray)
    ```

    将此向量的组件复制到指定的数组中。

12. ```java
    Object elementAt(int index)
    ```

    返回指定索引处的组件。

13. ```java
    Enumeration elements() 
    ```

    返回此向量的组件的枚举。

14. ```java
    void ensureCapacity(int minCapacity)
    ```

    增加此向量的容量（如果有必要），以确保其至少能够保存最小容量参数指定的组件数。

15. ```java
    boolean equals(Object o)
    ```

    比较指定对象与此向量的相等型。

16. ```java
    Object firstElement()
    ```

    返回此向量的第一个组件（位于索引0）的项。

17. ```java
    Object get(int index)
    ```

    返回向量中指定位置的元素。

18. ```java
    int hashCode()
    ```

    返回此向量的哈希码值。

19. ```java
    int indexOf(Object elem)
    ```

    返回此向量中第一次出现的指定元素的索引，如果此向量不包含该元素，则返回-1.

20. ```java
    int indexOf(Object elem, int index)
    ```

    返回此向量中第一次出现的指定元素的索引，从index正向搜索，如果未找到元素，返回-1.

21. ```java
    void insertElementAt(Object obj, int index)
    ```

    将指定对象作为向量中的组件插入到指定的index处。

22. ```java
    boolean isEmpty()
    ```

    测试此向量是否不包含组件。

23. ```java
    Object lastElement()
    ```

    返回此向量的最后一个组件。

24. ```java
    int lastIndexOf(Object elem)
    ```

    返回此向量中最后一次出现的指定元素的索引，如果不包含该元素，返回-1.

25. ```java
    int lastIndexOf(Object elem, int index)
    ```

    返回此向量中最后一次出现制定元素的索引，从index处逆向搜索，如果未找到元素，返回-1.

26. ```java
    Object remove(int index)
    ```

    移除此向量中指定位置的元素。

27. ```java
    boolean remove(Object o)
    ```

    移除此向量中指定元素的第一个匹配项，如果向量不包含该元素，则元素保持不变。

28. ```java
    boolean removeAll(Collection C)
    ```

    从此向量中移除包含在指定Collection里的所有元素。

29. ```java
    void removeAllElements()
    ```

    从此向量中移除全部组件，并将其大小设置为0.

30. ```java
    boolean removeElement(Object obj)
    ```

    从此向量中移除变量的第一个（索引最小的）匹配项。

31. ```java
    void removeElementAt(int index)
    ```

    删除指定索引处的组件。

32. ```java
    protected void removeRange(int fromIndex, int toindex)
    ```

    从此list中移除其索引位于from-index（包括）与to-index（不包括）之间的所有元素。

33. ```java
    boolean retainAll(Collection C)
    ```

    在此向量中仅保留包含在指定Collection中的元素。

34. ```java
    Object set(int index, Object element)
    ```

    用指定的元素替换此向量中指定位置处的元素。

35. ```java
    void setElementAt(Object obj, int index)
    ```

    将此向量指定index处的组件设置为指定的对象。

36. ```java
    void setSize(int newSize)
    ```

    设置此向量的大小。

37. ```java
    int size()
    ```

    返回此向量中的组件数。

38. ```java
    List subList(int fromInedx, int toIndex)
    ```

    返回List的部分视图，元素范围为从from-index(包括)到to-index(不包括)。

39. ```java
    Object[] toArray()
    ```

    返回一个数组，包含此向量中以恰当顺序存放的所有元素。

40. ```java
    Object[] toArray(Object[] a)
    ```

    返回一个数组，包含此向量中以恰当顺序存放的所有元素。返回数组的运行时类型为指定数组的类型。

41. ```java
    String toString()
    ```

    返回此向量的字符串表示形式，其中包含每个元素的String表示形式。

42. ```java
    void trimToSize()
    ```

    对此向量的容量进行微调，使其等于向量的当前大小。

