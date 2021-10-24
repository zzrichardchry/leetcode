# 泛型

# 概述

泛型，即“参数化类型”。一提到参数，最熟悉的就是定义方法时有形参，然后调用此方法时传递实参。那么参数化类型怎么理解呢？

顾名思义，就是将类型由原来的具体的类型参数化，类似于方法中的变量参数，此时类型也定义成参数形式（可以称之为类型形参），然后在使用/调用时传入具体的类型（类型实参）。

泛型的本质是为了参数化类型（在不创建新的类型的情况下，通过泛型指定的不同类型来控制形参具体限制的类型）。也就是说在泛型使用过程中，

操作的数据类型被指定为一个参数，这种参数类型可以用在类、接口和方法中，分别被称为泛型类、泛型接口、泛型方法。

### 一个例子：

```java
List arrayList = new ArrayList();
arrayList.add("aaaa");
arrayList.add(100);

for(int i = 0; i< arrayList.size();i++){
    String item = (String)arrayList.get(i);
    Log.d("泛型测试","item = " + item);
}
//最终会有报错
java.lang.ClassCastException: java.lang.Integer cannot be cast to java.lang.String
```

因为有一个String类型和Integer类型，使用的时候都以String方式使用，所以出错。泛型就是解决类似这样的问题，可在**编译阶段就解决**。

```java
List<String> arrayList = new ArrayList<String>();
//这样在添加Integer到List里面编译器就会报错
```

# 特点

**泛型只在编译阶段有效。**

```java
List<String> stringArrayList = new ArrayList<String>();
List<Integer> integerArrayList = new ArrayList<Integer>();

Class classStringArrayList = stringArrayList.getClass();
Class classIntegerArrayList = integerArrayList.getClass();

if(classStringArrayList.equals(classIntegerArrayList)){
    Log.d("泛型测试","类型相同");
}
//输出：泛型测试：类型相同
```

在编译之后程序会采取去泛型化的措施。Java中的泛型，只在编译阶段有效。在编译的过程中，正确检验了泛型的结果后，会将泛型的相关信息擦出。只会在对象进入和离开方法的边界处添加类型检查和类型转换的方法。**泛型并不会进入到运行时的阶段**。

因此，**泛型知识逻辑上的多个不同类型，实际上都是相同的基本类型。**

# 泛型的使用

泛型一共有三类：泛型类、泛型接口、泛型方法。

### 泛型类

泛型类型用于类的定义中，被称为泛型类。通过泛型可以完成一组类的操作对外开放相同的接口。最典型的就是各种容器类：List、Set、Map。

常用的泛型类型变量：

* E：Element，多用于java集合框架
* K：Key
* N：Number
* T：Type
* V：Value

```java
//泛型的最基本写法
class 类名称 <泛型标识：可以随便写任意标识号，标识指定的泛型的类型>{
  private 泛型标识 /*（成员变量类型）*/ var; 
  .....
  }
}
```

```java
//在实例化泛型类时，必须指定T的具体类型
public class Generic<T>{ 
    //key这个成员变量的类型为T,T的类型由外部指定  
    private T key;

    public Generic(T key) { //泛型构造方法形参key的类型也为T，T的类型由外部指定
        this.key = key;
    }

    public T getKey(){ //泛型方法getKey的返回值类型为T，T的类型由外部指定
        return key;
    }
}
```

```java
//泛型的类型参数只能是类类型（包括自定义类），不能是简单类型
//传入的实参类型需与泛型的类型参数类型相同，即为Integer.
Generic<Integer> genericInteger = new Generic<Integer>(123456);

//传入的实参类型需与泛型的类型参数类型相同，即为String.
Generic<String> genericString = new Generic<String>("key_vlaue");
Log.d("泛型测试","key is " + genericInteger.getKey());
Log.d("泛型测试","key is " + genericString.getKey());

//输出：
//12-27 09:20:04.432 13063-13063/? D/泛型测试: key is 123456
//12-27 09:20:04.432 13063-13063/? D/泛型测试: key is key_vlaue
```

定义的泛型类，就一定要传入泛型类型实参么？并不是这样，在使用泛型的时候如果传入泛型实参，则会根据传入的泛型实参做相应的限制，此时泛型才会起到本应起到的限制作用。如果不传入泛型类型实参的话，在泛型类中使用泛型的方法或成员变量定义的类型可以为任何的类型。

```java
Generic generic = new Generic("111111");
Generic generic1 = new Generic(4444);
Generic generic2 = new Generic(55.55);
Generic generic3 = new Generic(false);

Log.d("泛型测试","key is " + generic.getKey());
Log.d("泛型测试","key is " + generic1.getKey());
Log.d("泛型测试","key is " + generic2.getKey());
Log.d("泛型测试","key is " + generic3.getKey());
//输出：
// D/泛型测试: key is 111111
// D/泛型测试: key is 4444
// D/泛型测试: key is 55.55
// D/泛型测试: key is false
```

**注意：**

* 泛型的类型参数只能是类类型，不能是简单类型。

* **不能对确切的泛型类型使用instanceof操作。**如这个操作是非法的：

  ```java
  if(ex_num instanceof Generic<Number>){ }
  ```

### 泛型接口

泛型接口与泛型类的定义及使用基本相同。

```java
//定义一个泛型接口
public interface Generator<T> {
    public T next();
}
```

当实现泛型接口的类，未传入泛型实参的时候：

```java
/**
 * 未传入泛型实参时，与泛型类的定义相同，在声明类的时候，需将泛型的声明也一起加到类中
 * 即：class FruitGenerator<T> implements Generator<T>{
 * 如果不声明泛型，如：class FruitGenerator implements Generator<T>，编译器会报错："Unknown class"
 */
class FruitGenerator<T> implements Generator<T>{
    @Override
    public T next() {
        return null;
    }
}
```

当实现泛型接口的类，传入泛型实参的时候：

```java
/**
 * 传入泛型实参时：
 * 定义一个生产器实现这个接口,虽然我们只创建了一个泛型接口Generator<T>
 * 但是我们可以为T传入无数个实参，形成无数种类型的Generator接口。
 * 在实现类实现泛型接口时，如已将泛型类型；传入实参类型，则所有使用泛型的地方都要替换成传入的实参类型
 * 即：Generator<T>，public T next();中的的T都要替换成传入的String类型。
 */
public class FruitGenerator implements Generator<String> {

    private String[] fruits = new String[]{"Apple", "Banana", "Pear"};

    @Override
    public String next() {
        Random rand = new Random();
        return fruits[rand.nextInt(3)];
    }
}
```

### 泛型通配符

首先Integer是Number的一个子类，并且Generic<Integer>和Generic<Number>是同一基本类型。在使用Generic<Number>作为形参的方法中，能否让Generic<Integer>的实例传入呢？逻辑上Generic<Integer>和Generic<Number>是有可以看成具有父子关系的泛型类型？

使用Generic<T>来举个例子：

```java
public void showKeyValue1(Generic<Number> obj) {
  Log.d("泛型测试", "key value is " + obj.getKey());
}

Generic<Integer> gInteger = new Generic<Integer>(123);
Generic<Number> gNumber = new Generic<Number>(456);
showKeyValue(gInteger);

// showKeyValue编译器会报错：
// Generic<java.lang.Integer> cannot be applied to Generic<java.lang.Number>
```

由此可见Generic<Integer>不能被当作Generic<Number>的子类。因此，一种泛型可以对应多个版本，但是不同版本的泛型类型实例是不兼容的。

可是在定义showKeyValue方法的时候，这个方法的形惨中的Generic<Number>的< >中也不能使用T来代指所有的类型。**类型通配符就是应运而生。**

```java
public void showKeyValue1(Geneirc<?> obj) {
  Log.d("泛型测试，", "Key Value is " + obj.getKey());
}
```

这个地方的 **?** 就是类型通配符。**注意：这个地方的？是类型实参！！！！不是类型形参！！！**相当于此处的？可以看成所有类型的父类，是一种真实的类型。所以当方法的类型参数不确定的时候，并且不需要使用类型的具体功能，只需要Object类中的功能，就可以使用？来表示位置类型。

# 泛型方法

泛型类，是指在实例化类的时候指明泛型的具体类型；泛型方法，是在调用方法的时候指明泛型的具体类型。

```java
/**
 * 泛型方法的基本介绍
 * @param tClass 传入的泛型实参
 * @return T 返回值为T类型
 * 说明：
 *   1）public与返回值中间<T>非常重要，可以理解为声明此方法为泛型方法。
 *   2）只有声明了<T>的方法才是泛型方法，泛型类中的使用了泛型的成员方法并不是泛型方法。
 *   3）!! <T>表明该方法将使用泛型类型T，此时才可以在方法中使用泛型类型T。!!
 *   4）与泛型类的定义一样，此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型。
*/
public <T> T genericMethod(Class<T> tClass)throws InstantiationException ,
  IllegalAccessException{
        T instance = tClass.newInstance();
        return instance;
}
Object obj = genericMethod(Class.forName("com.test.test"));
```

### 泛型方法的基本用法

```java
public class GenericTest {
  
  //这个是泛型类
  public class Generic<T> {
    private T key;
    
    public Generic(T key) {
      this.key = key;
    }
    
    //(1) 看似是泛型方法，但不是泛型方法。
    //这个并不是泛型方法，只是在方法中使用了泛型，是一个普通的成员方法。
    //返回值是在生命泛型类的时候已经声明过的泛型，所以在这个方法中才可以继续使用T这个泛型。
    public T getKey() {
      return key;
    }
    //这也不是一个泛型方法，只是使用了Generic<Number>这个泛型类做形参而已。
    public void showKeyValue1(Generic<Number> obj) {
      Log.d("泛型测试", "Key value is " + obj.getKey());
    }
    //这是一个会报错的类似(1)中的方法。
    //整个方法是有问题的，因为在类的声明中并未声明泛型E，所以在使用E作为形参和返回值类型会报错。
    //编译器报错内容："cannot resolve symbol E"
    public E setKey(E key) {
      this.key = keu;
    }
    
    //(2) 泛型方法的详细内容。
    /**
     * 真正的一个泛型方法实例：
     * 1） 在public和返回值中间的<T>必不可少。这表明了一个泛型方法，并且生命了一个泛型T。
     * 2） 这个T可以出现在泛型方法中的任意位置。
     * 3） 泛型的数量也可以为多个，如：
     *				public <T,K> K showKeyName(Generic<T> container) {...}
    */
    public <T> T showKeyName(Generic<T> container){
      System.out.println("container key:" + container.getKey());
      T test = container.getKey();
      return test;
    }
    
    //(3) 错误的泛型方法
    /**
     *1）public <T> T showKeyName(Generic<E> container) {...}
     * 此方法也会报错。虽然声明了<T>，也表明了这是一个可处理泛型类型的泛型方法。
     * 但是只声明了泛型类型T，并未声明泛型类型E，因此编译器无法识别这个E类型。
     * 编译器会报错"UnKnown class 'E'"。
     *2）public void showKey(T genericObj) {...}
     * 此方法也会报错。因为T类型并未在项目中声明过，因此编译器无法识别这个T类型。
     * 编译器会报错"UnKnown class 'T'"。
    */
  }
}
```

### 类中的泛型方法

泛型方法可以出现在任何地方和任何场景中使用。但是有一种情况是非常特殊的，当泛型方法出现在泛型类中时：

```java
public class GenericFruit {
  
	class Fruit {
    @Override
    public String toString(){
      return "fruit";
    }
  }
  class Apple extends Fruit {
    @Override
    public String toString() {
      return "apple";
    }
  }
  class Person() {
    @Override
    public String toString() {
      return "Person";
    }
  }
  
  class GenerateTest<T> {
    public void show_1(T t){
      System.out.pritln(t.toString());
    }
    
    //(1)使用泛型E的泛型方法。
    /**
     * 使用泛型E在泛型类中来声明一个泛型方法。
     * 泛型E可以为任意泛型类型，可以和T相同也可以和T不同，因为时这个方法使用的泛型。
     * 由于泛型方法被声明的时候会声明泛型<E>，因此即使在泛型类中并未声明该泛型，编译器仍可识别。
    */
    public <E> void show_2(E t) {
      System.out.println(t.toString());
    }
    //当使用和泛型类相同的T时，这个T是一个全新的类型，可以与泛型类中声明的T不是同一种类型。
    public <T> void show_3(T t) {
      System.out.println(t.toString());
    }
  }
  
  public static void main(String[] args) {
    Apple apple = new Apple();
    Person person = new Person();
    
    GenerateTest<Fruit> gereateTest = new GenerateTest<Fruit>();
    //apple是Fruit的子类，因此这个例子不会报错；
    generateTest.show_1(apple);
    //person是Person的子类，所以传入的实参类是Person，因此会报错
    //generateTest.show_1(person);
    
    //以下两种方法都可以成功，因为是泛型方法
    generateTest.show_2(apple);
    generatetest.show_2(person);
    generateTest.show_3(apple);
    generatetest.show_3(person);
  }
}
```

### 泛型方法与可变参数

```java
public <T> void printMsg(T... args) {
  for(T t: args) {
    Log.d("泛型测试","t is" + t)
  }
}
```

这个例子展示了泛型方法中，使用可变参数的基本内容。其实和非泛型的可变参数没有什么区别（把具体的类型参数替换成泛型就OK）。

### 静态方法与泛型

静态方法有一种情况需要注意，就是在类中的静态方法使用泛型：**静态方法无法访问类上定义的泛型**；如果静态方法操作的应用数据类型不确定的时候，必须要将泛型定义在方法上。

```java
public class StaticGenerator<T> {
  ...
  /**
   * 如果在类中定义使用泛型的静态方法，需要添加额外的泛型声明，以此来将这个方法定位为泛型方法。
   * 就算静态方法要使用泛型类中已经声明过的泛型也不可以。如：
   * public static void show(T t){...}
   * 会出现编译错误：StaticGenerator cannot be refrenced from static context
  */
  public static <T> void show(T t) {
    ...
  }
}
```

### 泛型方法总结

泛型方法能使方法独立于类而产生变化，以下是一个基本的指导原则：

无论何时，如果你能做到，就该尽量使用泛型方法。也就是说，如果使用泛型方法将整个类泛型化，那么就应该使用泛型方法。

static方法无法访问泛型类型的参数，所以如果static方法要使用泛型，就必须使其成为泛型方法。

# 泛型上下边界

使用泛型的时候，我们还可以为传入的泛型类型实参进行上下边界的限制。

例：类型实参只允许传入某种类型的父类或者某种类型的子类。

为泛型添加上下边界，即传入的类型实参必须是指定类型的子类行。

```java
public void showKeyValue1(Generic<? extends Number> obj) {
  Log.d("泛型测试","key value is " + obj.getKey());
}

Generic<String> generic1 = new Generic<String>("11111");
Generic<Integer> generic2 = new Generic<Integer>(2222);
Generic<Float> generic3 = new Generic<Float>(2.4f);
Generic<Double> generic4 = new Generic<Double>(2.56);

//这一行代码编译器会提示错误，因为String类型并不是Number类型的子类
//showKeyValue1(generic1);

showKeyValue1(generic2);
showKeyValue1(generic3);
showKeyValue1(generic4);
```

如果将泛型类的定义也进行修改：

```java
public class Generic<T extends Numbe>{
  private T key;
  
  public Generic(T key) {
    this.key = key;
  }
  
  public T getKey() {
    return key;
  }
}

//以下代码会报错，因为String不是Number的子类
Generic<String> generic1 = new Generic<String>("11111");
```

再举一个泛型方法的例子：

```java
//在泛型方法中添加上下边界限制的时候，必须在权限声明与返回值之间的<T>上添加上下边界。
//也就是在泛型声明的时候这样会报错：
//public <T> T showKeyName(Generic<T extends Number> container)
//编译器报错:Unexpected bound
public <T extends Number> T showKeyName(Generic<T> container) {...}
```

因此，泛型方法中的上下边界添加，必须和泛型的声明放在一起。

# 泛型数组

根据SUN的说明文档，在java中是"**不能创建一个确切的泛型类型数组**"。

也就是说这个例子是不允许的：

```java
List<String>[] ls = new ArrayList<String>[10];
```

但是**使用通配符创建泛型数组是可以的**，如这个例子：

```java
List<?>[] ls = new ArrayList<?>[10];
```

这样也是可以的：

```java
List<String>[] ls = new ArrayList[10];
```

使用SUN的文档来说明这个问题就是：

```java
List<String> [] lsa = new List<String>[10]; //Note really allowed(经过验证现在不行了)
Object o = lsa;
Object[] oa = (Object[]) o;
List<Integer> li = new ArrayList<Integer>();
li.add(new Integer(3));
oa[1] = li;// Unsound, but passes run time store check
String s = lsa[1].get(0); //Run-time error: ClassCastException
```

这种情况下，由于JVM泛型的擦除机制，运行时JVM不知道泛型信息的，所以可以给oa[1]附上一个ArrayList不出现异常。但是在取出数据的时候却要做一次类型转换，所以就会出现ClassCastException。

对泛型数组的声明进行限制，对于这样的情况，可以在编译期提示代码有类型安全问题，比没有任何提示要强很多。

下面采用通配符的方式是被允许的：数组的类型不可以是类型变量，除非采用通配符的方式，因为对于通配符的方式，最后取出数据是要做显式的类型转换的。

```java
List<?>[] lsa = new List<?>[10]; //OK, array of unbounded wildcard type.
Object o = lsa;
Object[] oa = (Object[]) o;
List<Integer> li = new ArrayList<Integer>();
li.add(new Integer(3));
oa[1] = li; //Correct
Integer i = (Integer) lsa[1].get(0); //OK
```

# 最后

本文中的例子主要是为了阐述泛型中的一些思想而简单决出。

一提到泛型，相信大家用到最多的就是集合中，其实在实际的编程过程中，自己可以使用泛型去简化开发，且能很好的保证代码质量。