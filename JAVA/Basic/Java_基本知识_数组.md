# 数组变量

数组的声明方法

```java
dataType[] arrayRefVar; //首选的方法
dataType arrayRefVar[]; //效果相同，但是不是首选方法。 
```

数组的创建方法

```java
arrayRefVar = new dataType[arraySize];
```

将数组的声明和创建何在一条语句中完成就是：

```java
dataType[] arrayRefVar = new dataType[arraySize]; //这样就在同一个语句中完成了声明以及创建
dataType[] arrayRefVar = {value0, value1, ..., valuek};
```

数组的元素是通过索引访问的。数组索引从0开始，所以索引值是从0到arrayRefVar.length-1

