---
title: JAVA基础笔记
date: 2024-02-10 22:31:09
tags: Java
---
# 基础知识点上

JDK，8以前，JVM，基础库，javac，javadoc，jdb等等都是混在一起。
JDK9以后增加了94个模块+jlink生成比较小的jre。

字节码解释过程
![](https://oss.javaguide.cn/github/javaguide/java/basis/java-code-to-machine-code-with-jit.png)
JIT通过 对热点代码HotSpot 惰性评估方式，保存热点代码的方式提高执行效率。

---

JDK9 引入了AOT
新的编译模式，在程序执行前编译成字节码，静态编译。可以避免jit预热，加快java程序启动速度。
减少内存和增强java程序的安全性。适合云原生场景。
更进一步，GraalVM 。
缺点，不支持反射，动态代理，动态加载，JNI。像Spring，GCLIB都没法用了。

---

OpenJdk,https://github.com/openjdk/jdk
JDK8u221 之前只要不升级可以无限期免费。OpenJDK 是完全免费的。

---

Java vs C++
java没指针，java单继承，但是可以多继承接口。
java有gc，C++需要自己释放。
C++还能重载操作符

---

《Clean Code》这本书明确指出：
代码的注释不是越详细越好。实际上好的代码本身就是注释，我们要尽量规范和美化自己的代码来减少不必要的注释。若编程语言足够有表达力，就不需要注释，尽量通过代码来阐述。

标识符，关键字，true，false，null字面值
自增    ++a先自增再赋值， a++先赋值后自增

位移运算 <<,>>, >>> 快速幂算法就用到，还有快速求奇偶数。HashMap hash方法也用到。
<< 左移，高位丢弃，低位补零
>> 右移带符号，高位补符号，低位丢弃，正高位数补0，负高位数补1.
>>> 无符号又移，忽略符号位，空位都以0补齐。
double，float二进制中表现特殊，不能进行移位操作，只有int，long才能移位
如果移位超过占位数，会先求余再进行移位操作。

```
/ ^：按位异或
// >>>:无符号右移，忽略符号位，空位都以0补齐
return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
```

continue，跳一次循环，break跳出循环体继续执行。return结束方法。

java基本类型，byte short，int，long。 float，double，char，boolean.

包装类型vs基本类型
- 包装类型可以用泛型，基本类型占用空间小，包装类型不复制是null，基本类型有默认值
- 基本类型用 ==判断，包装类型用equals()方法。
- 基本类型如果是局部变量，放到栈中，如果是成员变量存放到堆中。包装类型都存放到堆中。

基本类型的包装类型基本都用到了缓存机制来提升性能。比如默认创建[-128,127]的相应缓存数据
如果超出对应范围仍然会去创建新的对象，缓存的范围区间的大小只是在性能和资源之间的权衡。
两种浮点数类型的包装类 Float,Double 并没有实现缓存机制。

所有整型包装类对象之间值的比较，全部使用 equals 方法比较。 
![](https://oss.javaguide.cn/github/javaguide/up-1ae0425ce8646adfb768b5374951eeb820d.png)

自动装箱与拆箱
Integer i = 10;  //装箱
int n = i;   //拆箱
从字节码中，我们发现装箱其实就是调用了 包装类的valueOf()方法，拆箱其实就是调用了 xxxValue()方法。
Integer i = 10 等价于 Integer i = Integer.valueOf(10)
int n = i 等价于 int n = i.intValue();
注意：如果频繁拆装箱的话，也会严重影响系统的性能。我们应该尽量避免不必要的拆装箱操作。

浮点数精度丢失
这个和计算机保存浮点数的机制有很大关系。我们知道计算机是二进制的，而且计算机在表示一个数字时，宽度是有限的，无限循环的小数存储在计算机时，只能被截断，所以就会导致小数精度发生损失的情况。这也就是解释了为什么浮点数没有办法用二进制精确表示。
[计算机系统基础（四）浮点数](http://kaito-kidd.com/2018/08/08/computer-system-float-point/)
BigDecimal 可以实现对浮点数的运算，不会造成精度丢失。通常情况下，大部分需要浮点数精确运算结果的业务场景（比如涉及到钱的场景）都是通过 BigDecimal 来做的。
[BigDecimal 详解](https://javaguide.cn/java/basis/bigdecimal.html#bigdecimal-%E7%AD%89%E5%80%BC%E6%AF%94%E8%BE%83%E9%97%AE%E9%A2%98)

超过long可以用，BigInteger。

变量，成员变量，局部变量。语法形式，存储方式，生存时间，默认值。

字符型常量，字符串常量。char，String
方法返回值。

重载，重写。

Java5支持定义可变长参数，允许在调用方法时传入不定长度的参数
public static void method1(String... args) 
可变参数只能作为函数的最后一个参数，但其前面可以有也可以没有任何其他参数
public static void method2(String arg1, String... args) {

上END

---

# 基础中

### 面向对象
### Object
hashCode,获取哈希码，散列码。
Java 中的任何类都包含有 hashCode() 函数，Object 的 hashCode() 方法是本地方法，也就是用 C 语言或 C++ 实现的。
散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）
Java 启蒙书《Head First Java》:为什么要有 hashCode？
> 当你把对象加入 HashSet 时，HashSet 会先计算对象的 hashCode 值来判断对象加入的位置，同时也会与其他已经加入的对象的 hashCode 值作比较，如果没有相符的 hashCode，HashSet 会假设对象没有重复出现。但是如果发现有相同 hashCode 值的对象，这时会调用 equals() 方法来检查 hashCode 相等的对象是否真的相同。如果两者相同，HashSet 就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。这样我们就大大减少了 equals 的次数，相应就大大提高了执行速度。

这是因为两个对象的hashCode 值相等并不代表两个对象就相等。

- 如果两个对象的hashCode 值相等，那这两个对象不一定相等（哈希碰撞）。
- 如果两个对象的hashCode 值相等并且equals()方法也返回 true，我们才认为这两个对象相等。
- 如果两个对象的hashCode 值不相等，我们就可以直接认为这两个对象不相等。

为什么重写 equals() 时必须重写 hashCode() 方法？因为两个相等的对象的 hashCode 值必须是相等。也就是说如果 equals 方法判断两个对象是相等的，那这两个对象的 hashCode 值也要相等。如果重写 equals() 时没有重写 hashCode() 方法的话就可能会导致 equals 方法判断是相等的两个对象，hashCode 值却不相等。


### String
String、StringBuffer、StringBuilder 的区别
- 可变性，String不可变。另外两个继承自 AbstractStringBuilder。提供了append
- 线程安全
String 线程安全，可以理解为常量。
StringBuffer 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的
StringBuilder 并没有对方法进行加同步锁，所以是非线程安全的。
- 性能
每次对 String 类型进行改变的时候，都会生成一个新的 String 对象，然后将指针指向新的 String 对象。StringBuffer 每次都会对 StringBuffer 对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用 StringBuilder 相比使用 StringBuffer 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

对于三者使用的总结：
操作少量的数据: 适用 String
单线程操作字符串缓冲区下操作大量数据: 适用 StringBuilder
多线程操作字符串缓冲区下操作大量数据: 适用 StringBuffer

String 真正不可变有下面几点原因：
1. 保存字符串的数组被 final 修饰且为私有的，并且String 类没有提供/暴露修改这个字符串的方法。
2. String 类被 final 修饰导致其不能被继承，进而避免了子类破坏 String 不可变。

Java 9 之后，String、StringBuilder 与 StringBuffer 的实现改用 byte 数组存储字符串。

Java 语言本身并不支持运算符重载，“+”和“+=”是专门为 String 类重载过的运算符，也是 Java 中仅有的两个重载过的运算符。
字符串对象通过“+”的字符串拼接方式，实际上是通过 StringBuilder 调用 append() 方法实现的，拼接完成之后调用 toString() 得到一个 String 对象 。
不过，在循环内使用“+”进行字符串的拼接的话，存在比较明显的缺陷：编译器不会创建单个 StringBuilder 以复用，会导致创建过多的 StringBuilder 对象。

StringBuilder 对象是在循环内部被创建的，这意味着每循环一次就会创建一个 StringBuilder 对象。
如果直接使用 StringBuilder 对象进行字符串拼接的话，就不会存在这个问题了。

使用 “+” 进行字符串拼接会产生大量的临时对象的问题在 JDK9 中得到了解决。
String 中的 equals 方法是被重写过的，比较的是 String 字符串的值是否相等。 Object 的 equals 方法是比较的对象的内存地址。

字符串常量池 是 JVM 为了提升性能和减少内存消耗针对字符串（String 类）专门开辟的一块区域，主要目的是为了避免字符串的重复创建。
```
// 在堆中创建字符串对象”ab“
// 将字符串对象”ab“的引用保存在字符串常量池中
String aa = "ab";
// 直接返回字符串常量池中字符串对象”ab“的引用
String bb = "ab";
System.out.println(aa==bb);// true
```
String.intern() 是一个 native（本地）方法，其作用是将指定的字符串对象的引用保存在字符串常量池中，可以简单分为两种情况：

在编译过程中，Javac 编译器（下文中统称为编译器）会进行一个叫做 常量折叠(Constant Folding) 的代码优化。《深入理解 Java 虚拟机》中是也有介绍到：
常量折叠会把常量表达式的值求出来作为常量嵌在最终生成的代码中，这是 Javac 编译器会对源代码做的极少量优化措施之一(代码优化几乎都在即时编译器中进行)。对于 String str3 = "str" + "ing"; 编译器会给你优化成 String str3 = "string"; 。
我们在平时写代码的时候，尽量避免多个字符串对象拼接，因为这样会重新创建对象。如果需要改变字符串的话，可以使用 StringBuilder 或者 StringBuffer。

不过，字符串使用 final 关键字声明之后，可以让编译器当做常量来处理。

---

# 基础下

### 异常

Exception 和Error有共同祖先，但是Error没法catch。
Unchecked Exception 即 不受检查异常 ，Java 代码在编译过程中 ，我们即使不处理不受检查异常也可以正常通过编译。
RuntimeException 及其子类都统称为非受检查异常
- NullPointerException(空指针错误)
- IllegalArgumentException(参数错误比如方法入参类型错误)
- NumberFormatException（字符串转换为数字格式错误，IllegalArgumentException的子类）
...

不要在 finally 语句块中使用 return! 当 try 语句和 finally 语句中都有 return 语句时，try 语句块中的 return 语句会被忽略。

finally的代码也有可能不执行
finally 之前虚拟机被终止运行的话，finally 中的代码就不会被执行。
程序所在的线程死亡。
关闭 CPU。 

### 泛型

### 反射

### 注解

### SPI

### 序列化，反序列化

### I/O

### 语法糖




# 集合

![](https://oss.javaguide.cn/github/javaguide/java/collection/java-collection-hierarchy.png)

HashMap通过 jdk1.8以前，数组+链表组成。拉链法解决解决哈希冲突。1.8以后在链表长度大于阈值，默认。的时候转化为红黑树。

LinkedHashMap继承自HashMap，增加了一条双向链表。

Hash算法
散列算法，从任意文件中创造小的数字的指纹的方法。
MD5系列，SHA系列。
MD5和SHA1已经被破解，推荐用SHA2-256
（彩虹表）
哈希碰撞

Hash冲突，两个或者更多的输入值被哈希函数映射到同一hash值。
解决方法，
1. 链地址法（separate chaining） 常见处理方法，将哈希表每一个位置看做一个桶当新的元素哈希值冲突时，我们可以将它添加到同一哈希值的其他元素的链表中。例如，Java的HashMap就是用链表和红黑树（链表长度大于一定阈值时转为红黑树）解决冲突的
2. 开放地址法 
3. 再哈希法 Rehashing 
4. 公共溢出法



---
几个目标，
1. 彻底搞懂反射
2. 泛型的一些用法