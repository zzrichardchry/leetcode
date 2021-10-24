# 基本定义

可变参数：适用于参数个数不确定，类型确定的情况，java将会把可变参数当作数组处理。

**注意：**可变参数必须位于最后一项。当可变参数个数多于一个时，必将有一个不是最后一项，所以只支持有一个可变参数。因为参数个数不确定，所以当其后边还有相同类型的参数时，java无法区分传入的参数属于前一个个遍参数还是后边的参数，所以只能让可变参数位于最后一位。

# 可变参数特点：

1. **只能出现在参数列表的最后。**
2. ... 位于变量类型和变量名之间，前后有无空格都可以。
3. 调用可变参数的方法时，编译器为该可变参数隐含创建一个数组，在方法体中以数组的形式访问可变参数。

```java
public class Varable {
  public static void main(String[] args) {
    System.out.println(add(2,3));
    System.out.println(add(2,3,5));
  }
  
  public static int add(int x, int ...args) {
    int sum = x;
    for(int i==0; i<args.length; i++) {
      sum+=agrs[i];
    }
    return sum;
  }
}
```

# 注意事项

1. 可变参数方法与数组参数方法重载时(会报错)

   ```java
   //带数组的方法
   public void hello(String[] params) {
     System.out.println("执行带数组参数的方法，长度为：" + params.length);
   }
   //带可变参数的方法
   public void hello(String... params) {
     System.out.println("执行带数组参数的方法，长度为：" + params.length);
   }
   //发生编译错误：Duplicate method hello(String[])
   //因为第一个和第二个方法都是同一个方法，第二个String可变参数本质上就是String[] params
   ```

2. 可变参数与无参数方法重载时

   ```java
   //带可变参数的方法
   public  static void hello(String... params) {
     System.out.println("执行带可变参数的方法，参数个数为：" + params.length);
   }
   //不带参数的方法
   public static void hello() {
     System.out.println("执行不带参数的方法");
   }
   
   public static void main(String[] args) {
     hello(); //不会报错
   }
   ```

3. 可变参数的类型和前面非可变参数类型一样的时候重载(会报错)

   ```java
   //带可变参数的方法
   public static void hello(String... params) {
     System.out.println("执行带可变参数的方法，参数个数为：" + params.length);
   }
   //带固定参数和可变参数
   public void hello(String param1, String... params) {
     System.out.println("执行带可变参数和固定参数的方法，参数个数为：" + params.length);
   }
   
   //调用方法时会出现错误
   hello("1","2","3");
   //发生编译错误：The method hello(String[]) is ambiguous
   //因为hello("1","2","3")和上面两个方法都匹配，所以不知道使用哪个方法。
   ```

4. 可变参数方法与可变参数方法重载时(会报错)

   ```java
   static void f(float i, Character... args) {
     System.out.println("first");
   }
   static void f(Character... args) {
     System.out.println("second");
   }
   
   //当使用下面代码时没有问题
   f(1,;'2');
   //当使用下面代码的时候会报错
   f('1','2');
   //发生编译错误：The method f(float, character[]) is ambiguous
   //因为此时这个调用f('1','2');会和上面两个方法都匹配，就不知道使用哪个方法了。
   ```

基本类型由低级到高级分别为 (byte, short, char) --> int --> long --> float --> double，第几变量可以直接转化为高级变量。