# 1. static 修饰符



# 2. final 修饰符



# 3. abstract 修饰符



# 4. synchronized 修饰符

## 定义

synchronized关键字声明的方法同一时间只能被一个线程访问。synchronized修饰符可以应用于四个访问修饰符

```java
//例子
public synchronized void showDetails() {...}
```

其他线程必须等待当前线程执行完该方法/代码块后才能执行该方法/代码块。

## 应用场景

**保证线程安全，解决多线程中的并发同步问题（实现的是阻塞型并发），**具体场景如下：

1. 修饰 实例方法/代码块时，（同步）保护的是同一个对象方法的调用&当前实例对象。
2. 修饰 静态方法/代码块时，（同步）保护的是静态方法的调用&class类对象。

## 原理

1. 依赖JVM实现同步。
2. 底层通过一个监视器对象(monitor)完成，wait(), notify() 等方法也依赖于monitor对象。

监视器(monitor)锁的本质依赖于底层操作系统的互斥锁(Mutex Lock)实现。

### 1. 锁的内存语义

* **内存可见性：**同步快的可见性是由“如果对一个变量执行lock操作，将会清空工作内存中此变量的值，在执行引擎使用这个变量前需要重新执行load或assign操作初始化变量的值“、

未完，没有看完https://zhuanlan.zhihu.com/p/29866981

# 5. transient 修饰符



# 6. volatile 修饰符

