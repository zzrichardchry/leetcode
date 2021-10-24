# 定义

* HashMap 是一个散列表，它存储的内容是键值对(key-value)的映射。

* HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，最多允许一条记录的键为 null，不支持线程同步。

* HashMap 是无序的，即不会记录插入的顺序。

* HashMap 继承于AbstractMap，实现了 Map、Cloneable、java.io.Serializable 接口。

* HashMap 的 key 与 value 类型可以相同也可以不同，可以是字符串（String）类型的 key 和 value，也可以是整型（Integer）的 key 和字符串（String）类型的 value。

# 基本创建方法

```java
Map<Integer, String> mapName = Map.of(1, "google", 2, "baidu");
```

| Key  | Value  |
| ---- | ------ |
| 1    | google |
| 2    | baidu  |

```java
HashMap<Integer, String> mapName = new HashMap<Integer, String>;
```

