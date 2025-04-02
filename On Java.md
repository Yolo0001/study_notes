## 第三章 对象无处不在

### 3.2 必须创建所有对象

#### 3.2.1数据保存在哪里

1. 寄存器 ：速度最快 数据会保存在CPU里 数量有限
2. 栈： 数据存储在随机存储器(random-access memory,RAM) 处理器通过栈指针直接操作数据 栈指针向下移动将申请一块新的内存，向上移动会释放这块内存，效率仅次于寄存器 Java系统在创建应用程序时必须明确栈上所有对象的生命周期。限制了程序的灵活性，有一些数据保存在栈上(尤其是对象引用)，对象本身却并非如此。
3. 堆：通用的内存池(使用的也是RAM)，存放所有Java对象。与栈不同，编译器不关心位于堆上的对象需要存在多久。灵活。new创建对象，Java会在堆上分配内存空间。这种可灵活性要付出代价的，分配和清理堆存储要花费更多时间。好消息是，Java的堆内存分配机制已经变得非常高效了。
4. 常量存储：直接保存在程序代码中，值不变，所以是安全的。有时候常量会与其他代码隔离开来，在某些嵌入式系统中，这些常量保存在只读存储器中(read-only memory,ROM)。
5. 非RAM存储：如果一段数据没有保存在应用程序中，那么该数据的生命周期既不依赖于应用程序是否运行，也不受应用程序的管制。其中最典型的例子之一是“序列化对象(serialized object)”，它指的是转换为字节流并可以发送至其他机器的对象。另一个是“持久化对象(persistent object)”，它指的是保存在磁盘上的对象，而这些对象即便在程序结束运行之后也依然能够保持其状态这些数据存储类型的特点在于，它们会将对象转换成其他形式以保存于其他媒介中，后在需要的时候更新转换回常规的RAM对象 。Java支持轻量级的持久化对象存储， 而JDBC以及Hibernate等库则提供了更为成熟的解决方案,即支持使用数据库存取对象信息。

#### 3.2.2 特殊情况：基本类型

对于new一个新对象不是很高效，基本类型无需使用new，而是直接创建一个“自动变量”，在栈上保存它的的值。

| 基本类型 | 大小 | 最小值           | 最大值            | 包装类    | 默认值       |
| -------- | ---- | ---------------- | ----------------- | --------- | ------------ |
| boolean  | -    | -                | -                 | Boolean   | false        |
| char     | 16位 | Unicode 0 \u0000 | 65535 \uffff      | Character | \u0000(null) |
| byte     | 8位  | -128             | +127              | Byte      | (byte)0      |
| short    | 16位 | -32768           | +32767            | Short     | (short)0     |
| int      | 32位 | -2<sup>31</sup>  | +2<sup>31</sup>-1 | Integer   | 0            |
| long     | 64位 | -2<sup>63</sup>  | +2<sup>63</sup>-1 | Long      | 0L           |
| float    | 32位 | IEEE754          | IEEE754           | Float     | 0.0f         |
| double   | 64位 | IEEE754          | IEEE754           | Double    | 0.0d         |
| void     | -    | -                | -                 | Void      |              |

自动装箱与拆箱

```Java
Character ch = 'x';
char c = ch;
```

高精度数字

BigInteger：支持任意精度的整数

BigDecimal：支持任意精度的定点数



```java
class DataOnly {
    int i;
    double d;
    boolean b;
}
```

当一个类是基本类型时，即便你没有初始化这些字段，它们也会有默认值。

局部变量没有这个特性。

### 3.6 方法、参数以及返回值

方法名和参数列表共同构成了方法的“签名”，方法的签名及该方法的唯一标识符。

static方法通过类调用，所以不需要对象

- 有时候我们需要一小块共享空间来保存某个特定的字段，而并不关心创建多少个对象，甚至有没有创建对象。
- 你需要使用一个类的某个方法，而该方法和具体的对象无关

```java
class StaticTest {
    static int i = 47;
}

StaticTest st1 = new StaticTest();
StaticTest st2 = new StaticTest();
//st1.i和st2.i都是47，两者使用的内存空间是相同的
```

```java
class Tank {
    int level;
}

public class Assignment {
    public static void main(String[] args) {
        Tank t1 = new Tank();
        Tank t2 = new Tank();
        t1.level = 9;
        t2.level = 47;
        //9 ,47
        System.out.println("1: t1.level: " + t1.level + ",t2.level" + t2.level);
        //t2的引用指向了t1的引用
        t1=t2;     
        //t1.level = t2.level;
        //47, 47
        System.out.println("2: t1.level: " + t1.level + ",t2.level" + t2.level);
        
        //27,27
        t1.level = 27;
        System.out.println("3: t1.level: " + t1.level + ",t2.level" + t2.level);
        
        
    }
}

```

## 第四章 操作符

### 4.6 关系操作符

5%(-2) = 1

(-2)%5 = -2

```java
// operators/Equivalence.java
// (c)2021 MindView LLC: see Copyright.txt
// We make no guarantees that this code is fit for any purpose.
// Visit http://OnJava8.com for more book information.

public class Equivalence {
  static void show(String desc, Integer n1, Integer n2) {
    System.out.println(desc + ":");
    System.out.printf(
      "%d==%d %b %b%n", n1, n2, n1 == n2, n1.equals(n2));
  }
  @SuppressWarnings("deprecation")
  public static void test(int value) {
    Integer i1 = value;                             // [1]
    Integer i2 = value;
    show("Automatic", i1, i2);
    // Old way, deprecated since Java 9:
    Integer r1 = new Integer(value);                // [2]
    Integer r2 = new Integer(value);
    show("new Integer()", r1, r2);
    // Preferred since Java 9:
    Integer v1 = Integer.valueOf(value);            // [3]
    Integer v2 = Integer.valueOf(value);
    show("Integer.valueOf()", v1, v2);
    // Primitives can't use equals():
    int x = value;                                  // [4]
    int y = value;
    // x.equals(y); // Doesn't compile
    System.out.println("Primitive int:");
    System.out.printf("%d==%d %b%n", x, y, x == y);
  }
  public static void main(String[] args) {
    test(127);
    test(128);
  }
}
/* Output:
Automatic:															
127==127 true true			Integer的取值范围-128~127

new Integer():
127==127 false true

Integer.valueOf():
127==127 true true

Primitive int:
127==127 true


Automatic:
128==128 false true

new Integer():
128==128 false true

Integer.valueOf():
128==128 false true

Primitive int:
128==128 true
*/
```

```java
// operators/DoubleEquivalence.java
public class DoubleEquivalence {
  static void show(String desc, Double n1, Double n2) {
    System.out.println(desc + ":");
    System.out.printf(
      "%e==%e %b %b%n", n1, n2, n1 == n2, n1.equals(n2));
  }
  @SuppressWarnings("deprecation")
  public static void test(double x1, double x2) {
    // x1.equals(x2) // Won't compile
    System.out.printf("%e==%e %b%n", x1, x2, x1 == x2);
    Double d1 = x1;
    Double d2 = x2;
    show("Automatic", d1, d2);
    Double r1 = new Double(x1);
    Double r2 = new Double(x2);
    show("new Double()", r1, r2);
    Double v1 = Double.valueOf(x1);
    Double v2 = Double.valueOf(x2);
    show("Double.valueOf()", v1, v2);
  }
  public static void main(String[] args) {
    test(0, Double.MIN_VALUE);
    System.out.println("------------------------");
    test(Double.MAX_VALUE,
      Double.MAX_VALUE - Double.MIN_VALUE * 1_000_000);
  }
}
/* Output:
0.000000e+00==4.900000e-324 false
Automatic:
0.000000e+00==4.900000e-324 false false
new Double():
0.000000e+00==4.900000e-324 false false
Double.valueOf():
0.000000e+00==4.900000e-324 false false
------------------------
1.797693e+308==1.797693e+308 true
Automatic:
1.797693e+308==1.797693e+308 false true
new Double():
1.797693e+308==1.797693e+308 false true
Double.valueOf():
1.797693e+308==1.797693e+308 false true
*/

```



```java
// operators/EqualsMethod.java
// Default equals() does not compare contents

class ValA {
  int i;
}

class ValB {
  int i;
  // Works for this example, not a complete equals():
  public boolean equals(Object o) {
    ValB rval = (ValB)o;  // Cast o to be a ValB
    return i == rval.i;
  }
}

public class EqualsMethod {
  public static void main(String[] args) {
    ValA va1 = new ValA();
    ValA va2 = new ValA();
    va1.i = va2.i = 100;
    System.out.println(va1.equals(va2));
    ValB vb1 = new ValB();
    ValB vb2 = new ValB();
    vb1.i = vb2.i = 100;
    System.out.println(vb1.equals(vb2));
  }
}
/* Output:
false
true
*/
//默认equals()方法是比较引用，要重写才能比较内容
```

### 4.7 逻辑操作符

- 不能将非布尔值当成布尔值使用
- 在使用字符串的地方使用布尔值，会将布尔值自动转换成合适的文本格式

### 4.10 移位操作符

右移 >> : 符号为正，高位插入0；符号为负，高位插入1。

无符号右移 (>>>)：无论正负，都在高位插入0。

```java
// operators/URShift.java
// Test of unsigned right shift

public class URShift {
  public static void main(String[] args) {
    int i = -1;
    System.out.println(Integer.toBinaryString(i));
    i >>>= 10;
    System.out.println(Integer.toBinaryString(i));
    long l = -1;
    System.out.println(Long.toBinaryString(l));
    l >>>= 10;
    System.out.println(Long.toBinaryString(l));
    short s = -1;
    System.out.println(Integer.toBinaryString(s));
    s >>>= 10;
    System.out.println(Integer.toBinaryString(s));
    byte b = -1;
    System.out.println(Integer.toBinaryString(b));
    b >>>= 10;
    System.out.println(Integer.toBinaryString(b));
    b = -1;
    System.out.println(Integer.toBinaryString(b));
    System.out.println(Integer.toBinaryString(b>>>10));
  }
}
/* Output:
1111 1111 1111 1111 1111 1111 1111 1111
1111 1111 1111 1111 1111 11
1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111
1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 11
s
1111 1111 1111 1111 1111 1111 1111 1111
s>>>
1111 1111 1111 1111 1111 1111 1111 1111
b
1111 1111 1111 1111 1111 1111 1111 1111
b>>>
1111 1111 1111 1111 1111 1111 1111 1111
b
1111 1111 1111 1111 1111 1111 1111 1111
(b>>>10)
1111 1111 1111 1111 1111 11
*/
//如果对byte或short值进行移位运算，得到的可能不是正确的结果。他们会先被提升为int类型，进行右移操作，然后在被赋回给原来的变量时被截断，这时仍是-1。


// operators/BitManipulation.java
// (c)2021 MindView LLC: see Copyright.txt
// We make no guarantees that this code is fit for any purpose.
// Visit http://OnJava8.com for more book information.
// Using the bitwise operators
import java.util.*;

public class BitManipulation {
  public static void main(String[] args) {
    Random rand = new Random(47);
    int i = rand.nextInt();
    int j = rand.nextInt();
    printBinaryInt("-1", -1);
    printBinaryInt("+1", +1);
    int maxpos = 2147483647;
    printBinaryInt("maxpos", maxpos);
    int maxneg = -2147483648;
    printBinaryInt("maxneg", maxneg);
    printBinaryInt("i", i);
    printBinaryInt("~i", ~i);
    printBinaryInt("-i", -i);
    printBinaryInt("j", j);
    printBinaryInt("i & j", i & j);
    printBinaryInt("i | j", i | j);
    printBinaryInt("i ^ j", i ^ j);
    printBinaryInt("i << 5", i << 5);
    printBinaryInt("i >> 5", i >> 5);
    printBinaryInt("(~i) >> 5", (~i) >> 5);
    printBinaryInt("i >>> 5", i >>> 5);
    printBinaryInt("(~i) >>> 5", (~i) >>> 5);

    long l = rand.nextLong();
    long m = rand.nextLong();
    printBinaryLong("-1L", -1L);
    printBinaryLong("+1L", +1L);
    long ll = 9223372036854775807L;
    printBinaryLong("maxpos", ll);
    long lln = -9223372036854775808L;
    printBinaryLong("maxneg", lln);
    printBinaryLong("l", l);
    printBinaryLong("~l", ~l);
    printBinaryLong("-l", -l);
    printBinaryLong("m", m);
    printBinaryLong("l & m", l & m);
    printBinaryLong("l | m", l | m);
    printBinaryLong("l ^ m", l ^ m);
    printBinaryLong("l << 5", l << 5);
    printBinaryLong("l >> 5", l >> 5);
    printBinaryLong("(~l) >> 5", (~l) >> 5);
    printBinaryLong("l >>> 5", l >>> 5);
    printBinaryLong("(~l) >>> 5", (~l) >>> 5);
  }
  static void printBinaryInt(String s, int i) {
    System.out.println(
      s + ", int: " + i + ", binary:\n   " +
      Integer.toBinaryString(i));
  }
  static void printBinaryLong(String s, long l) {
    System.out.println(
      s + ", long: " + l + ", binary:\n    " +
      Long.toBinaryString(l));
  }
}
/* Output: (First 32 Lines)
-1, int: -1, binary:
   1111 1111 1111 1111 1111 1111 1111 1111
+1, int: 1, binary:
   1
maxpos, int: 2147483647, binary:
   1111 1111 1111 1111 1111 1111 1111 111
maxneg, int: -2147483648, binary:
   1000 0000 0000 0000 0000 0000 0000 0000
i, int: -1172028779, binary:
   1011 1010 0010 0100 0100 0010 1001 0101
~i, int: 1172028778, binary:
    100 0101 1101 1011 1011 1101 0110 1010
-i, int: 1172028779, binary:
    100 0101 1101 1011 1011 1101 0110 1011
j, int: 1717241110, binary:
   110 0110 0101 1011 0000 0101 0001 0110
i & j, int: 570425364, binary:
   10 0010 0000 0000 0000 0000 0001 0100
i | j, int: -25213033, binary:
   1111 1110 0111 1111 0100 0111 1001 0111
i ^ j, int: -595638397, binary:
   1101 1100 0111 1111 0100 0111 1000 0011
i << 5, int: 1149784736, binary:
   100 0100 1000 1000 0101 0010 1010 0000
i >> 5, int: -36625900, binary:
   1111 1101 1101 0001 0010 0010 0001 0100
(~i) >> 5, int: 36625899, binary:
   10 0010 1110 1101 1101 1110 1011
i >>> 5, int: 97591828, binary:
   101 1101 0001 0010 0010 0001 0100
(~i) >>> 5, int: 36625899, binary:
   10 0010 1110 1101 1101 1110 1011
                  ...
*/
```

## 第6章 初始化和清理

### 6.4 this关键字

```java
// housekeeping/BananaPeel.java

class Banana { void peel(int i) { /* ... */ } }

public class BananaPeel {
  public static void main(String[] args) {
    Banana a = new Banana(),
           b = new Banana();
    a.peel(1);
    b.peel(2);
  }
}

//a,b是隐藏参数
//

```

this关键字只能在非静态方法中使用。当你想在方法里调用对象时，直接使用this就可以了，因为它表示对该对象的引用。

如果从类的一个方法中调用该类的另一个方法，没必要使用this，直接调用即可。

```Java
// housekeeping/Apricot.java

public class Apricot {
  void pick() { /* ... */ }
  void pit() { pick(); /* ... */ }
}

```

```Java
// housekeeping/Leaf.java
// Simple use of the "this" keyword

public class Leaf {
  int i = 0;
  Leaf increment() {
    i++;
    return this;
  }
  void print() {
    System.out.println("i = " + i);
  }
  public static void main(String[] args) {
    Leaf x = new Leaf();
    x.increment().increment().increment().print();
  }
}
/* Output:
i = 3
*/
```

```Java
// housekeeping/PassingThis.java

class Person {
  public void eat(Apple apple) {
    Apple peeled = apple.getPeeled();
    System.out.println("Yummy");
  }
}

class Peeler {
  static Apple peel(Apple apple) {
    // ... remove peel
    return apple; // Peeled
  }
}

class Apple {
  Apple getPeeled() { return Peeler.peel(this); }
}

public class PassingThis {
  public static void main(String[] args) {
    new Person().eat(new Apple());
  }
}
/* Output:
Yummy
*/
//Apple需要调用Peeler.peel()方法，这是一个外部的工具方法，用来执行出于某种原
//因必须在Apple外部进行的操作(或许是因为这个外部方法可以用于许多不同的类，这样
//你就不用编写重复的代码了) 要将自身传递给外部方法，Apple就必须使用this关键字。

```

#### 6.4.1 在构造器中调用构造器

```Java
// housekeeping/Flower.java
// Calling constructors with "this"

public class Flower {
  int petalCount = 0;
  String s = "initial value";
  Flower(int petals) {
    petalCount = petals;
    System.out.println(
      "Constructor w/ int arg only, petalCount= "
      + petalCount);
  }
  Flower(String ss) {
    System.out.println(
      "Constructor w/ String arg only, s = " + ss);
    s = ss;
  }
  Flower(String s, int petals) {
    this(petals);
    //- this(s); // Can't call two!
    this.s = s; // Another use of "this"
    System.out.println("String & int args");
  }
  Flower() {
    this("hi", 47);
    System.out.println("Zero-argument constructor");
  }
  void printPetalCount() {
    //- this(11); // Not inside non-constructor!
    System.out.println(
      "petalCount = " + petalCount + " s = "+ s);
  }
  public static void main(String[] args) {
    Flower x = new Flower();
    x.printPetalCount();
  }
}
/* Output:
Constructor w/ int arg only, petalCount= 47
String & int args
Zero-argument constructor
petalCount = 47 s = hi
*/

```

#### 6.4.2 static的含义

static方法里没有this，你不能从static方法里调用非静态方法

你可以在没有创建对象的时候，直接通过类本身调用一个静态方法。

### 6.5 清理：终结和垃圾收集

**垃圾收集算法**：其中一种算法是“ 停止-复制”（stop-and-copy）。 这意味程序首先停止（这不是后台收集方案），原因很明显。然后，将所有存活对象从一 个堆复制到另一个堆，剩下的就都是垃圾。另外，当对象被复制到新堆中时，它们紧挨着打包，因此新堆十分紧凑（并且允许我们像前面描述的那样，将新堆尾部空出来，从头开始分配存储空间）。

**“标记-清除”**算法遵循相同的逻辑，即从栈和静态存储开始。遍历所有引用以查找存活对象。每当它找到一个存活对象。就会给该对象设置一个标志——此时尚未开始收集。

只有在标记过程完成后才会进行清除。在清除过程中，没有标记的对象被释放，但不会发生复制，因此如果收集器想压缩堆里的碎片，就需要通过重新排列对象来实现。

### 6.7 构造器初始化

1. 构造器也是静态方法。第一次创建类型为Dog的对象时，或者第一次访问类Dog的静态方法或静态字段时,Java解释器会搜索类路径来定位Dog.class文件。
2. 当Dog.class被加载后（这将创建一个Class对象，后面会介绍），它的所有静态初始化工作都会执行 因此，静态初始化只在Class对象首次加载时发生一次。
3. 当使用new Dog()创建对象时，构建过程首先会在堆上为Dog对象分配足够的存储空间。
4. 这块存储空间会被淸空，然后自动将该Dog对象中的所有基本类型设置为其默认值。
5. 执行所有出现在字段定义处的初始化操作
6. 执行构造器。

```Java
// housekeeping/Mugs.java
// (c)2021 MindView LLC: see Copyright.txt
// We make no guarantees that this code is fit for any purpose.
// Visit http://OnJava8.com for more book information.
// Instance initialization

class Mug {
  Mug(int marker) {
    System.out.println("Mug(" + marker + ")");
  }
}

public class Mugs {
  Mug mug1;
  Mug mug2;
  {                                         // [1]
    mug1 = new Mug(1);
    mug2 = new Mug(2);
    System.out.println("mug1 & mug2 initialized");
  }
  Mugs() {
    System.out.println("Mugs()");
  }
  Mugs(int i) {
    System.out.println("Mugs(int)");
  }
  public static void main(String[] args) {
    System.out.println("Inside main()");
    new Mugs();
    System.out.println("new Mugs() completed");
    new Mugs(1);
    System.out.println("new Mugs(1) completed");
  }
}
/* Output:
Inside main()

Mug(1)
Mug(2)
mug1 & mug2 initialized
Mugs()
new Mugs() completed

Mug(1)
Mug(2)
mug1 & mug2 initialized
Mugs(int)
new Mugs(1) completed
*/

```

［1］除了缺少static关键字外，实例初始化子句看起来与静态初始化子句完全相同。此语法对于支持匿名内部类的初始化是必需的（参见第11章），但也可以用来保证无论用哪个显式的构造器，某些操作都会发生。从输出可以看到，实例初始化子句在构造器之前执行。

### 6.8 数据初始化

根据经验，你应该只在其中一个重载方法上使用可变参数列表，或者压根儿就不使用它。

### 6.10 新特性：局部变量类型推断(type inference)

```java
// housekeeping/TypeInference.java
// {NewFeature} Since JDK 11

class Plumbus {}

public class TypeInference {
  void method() {
    // Explicit type:
    String hello1 = "Hello";
    // Type inference:
    var hello = "Hello!";
    // Works for user-defined types:
    Plumbus pb1 = new Plumbus();
    var pb2 = new Plumbus();
  }
  // Also works for static methods:
  static void staticMethod() {
    var hello = "Hello!";
    var pb2 = new Plumbus();
  }
}

class NoInference {
  String field1 = "Field initialization";
  // var field2 = "Can't do this";
  // void method() {
  //   var noInitializer; // No inference data
  //   var aNull = null;  // No inference data
  // }
  // var inferReturnType() {
  //   return "Can't infer return type";
  // }
}

```

## 第7章 实现隐藏(访问控制)

访问控制级别：从“最多访问”到 “最少访冋”依次是：public，protected，包内访问（package access，没有关键字）和 private。

只要能确定是类的“辅助”方法，这个方法就可以设为Private,以确保在包的其他 地方不会意外地使用它，从而让自己无法再更改或删除 将方法指定为Private让你保留 了这些选择。

在只有包访问权限的类中声明一个public构造器，实际上并不会使这个构造器成为public的，编译器应该在声明处将其标记为一个错误。

对于类访问权限，只有两种选择：包访问权限和public(内部类除外)

```Java
// hiding/Lunch.java
// Demonstrates class access specifiers. Make a class
// effectively private with private constructors:

class Soup1 {
  private Soup1() {}
  public static Soup1 makeSoup() {          // [1]
    return new Soup1();
  }
}

class Soup2 {
  private Soup2() {}
  private static Soup2 ps1 = new Soup2();   // [2]
  public static Soup2 access() {
    return ps1;
  }
  public void f() {}
}

// Only one public class allowed per file:
public class Lunch {
  void testPrivate() {
    // Can't do this! Private constructor:
    //- Soup1 soup = new Soup1();
  }
  void testStatic() {
    Soup1 soup = Soup1.makeSoup();
  }
  void testSingleton() {
    Soup2.access().f();
  }
}

```

Soup1和Soup2展示了如何通过将所有构造器设为private来阻止直接创建类的对象.记住，如果你没有明确创建至少一个构造器，无参构造器(没有参数的构造函数)就会自动创建 如果我们自己编写了无参构造器，它就不会自动创建。通过将它设为private, 没有人可以创建该类的对象 但是其他人要如何使用这个类呢？前面的示例提供了两种方式。Soup1创建了一个静态方法，用来生成Soup1的新对象并返回对它的引用.如果想要在返回之前对Soup1执行额外的操作，或者计算一下Soup1对象生成的数量(可能是为了限制它们的多少)，这种方式就十分有用了。

Soup2使用了所谓的设计模式(design pattern )。我们使用的这个特定模式称为单例模式(Singleton ),因为它从始至终都只有一个对象被创建，Soup2类的对象是作为Soup2 的静态private成员被创建的。所以有且仅有一个，并且只能通过public方法access()来 获取它。

### 7.5 新特性：模块

在JDK9之前,Java程序会依赖整个Java库。这意味着即使最简单的程序也带有大量从未使用过的库代码。如果你使用了组件A,那么Java语言没有提供任何支持来告诉编译器，组件A依赖了哪些其他组件。如果没有这些信息，编译器唯一能做的就是将整个 Java库包含在内。

还有一个更重要的问题。尽管包访问似乎提供了有效的隐藏，使类不能在该包外使用， 但还是可以使用反射（参见第19章）来规避它。多年来，一些Java程序员一直在访问部分底层的Java库组件，而这些库组件从未打算要被外部直接使用。这些程序员的代码与隐藏的组件耦合了起来。这意味着Java库设计者无法在不破坏用户代码的情况下修改这些组件。这极大地阻碍了对Java库的改逬 为了解决第二个问题，库组件需要一个对外部程序员完全不可用的选项

```sh
java --list-modules
java --describe-module java.base
```

## 第8章 复用

初始化引用有下列4种方式：

1. 在定义对象时。这意味着它们将始终在调用构造器之前被初始化 
2. 在该类的构造器中 
3. 在对象实际使用之前。这通常称为延迟初始化(lazy initialization )。在对象创建成本高昂且不需要每次都创建的情况下，它可以减少开销 
4. 使用实例初始化

```java
// reuse/Bath.java
// Constructor initialization with composition

class Soap {
  private String s;
  Soap() {
    System.out.println("Soap()");
    s = "Constructed";
  }
  @Override public String toString() { return s; }
}

public class Bath {
  private String // Initializing at point of definition:
    s1 = "Happy",
    s2 = "Happy",
    s3, s4;
  private Soap castile;
  private int i;
  private float toy;
  public Bath() {
    System.out.println("Inside Bath()");
    s3 = "Joy";
    toy = 3.14f;
    castile = new Soap();
  }
  // Instance initialization:
  { i = 47; }
  @Override public String toString() {
    if(s4 == null) // Delayed initialization:
      s4 = "Joy";
    return
      "s1 = " + s1 + "\n" +
      "s2 = " + s2 + "\n" +
      "s3 = " + s3 + "\n" +
      "s4 = " + s4 + "\n" +
      "i = " + i + "\n" +
      "toy = " + toy + "\n" +
      "castile = " + castile;
  }
  public static void main(String[] args) {
    Bath b = new Bath();
    System.out.println(b);
  }
}
/* Output:
Inside Bath()
Soap()
s1 = Happy
s2 = Happy
s3 = Joy
s4 = Joy
i = 47
toy = 3.14
castile = Constructed
*/
```

因此，考虑到继承。作为一般规则，应该将所有字段设为private,将所有方法设为public (稍后你将学到。protected成员也允许子类访问) 

### 8.7 向上转型

```Java
// reuse/Wind.java
// Inheritance & upcasting

class Instrument {
  public void play() {}
  static void tune(Instrument i) {
    // ...
    i.play();
  }
}

// Wind objects are instruments
// because they have the same interface:
public class Wind extends Instrument {
  public static void main(String[] args) {
    Wind flute = new Wind();
    Instrument.tune(flute); // Upcasting
  }
}
```

### 8.8 final关键字

#### 8.8.1 final数据

1. 空白final：对final执行赋值的操作只能发生在两个地方：要么在字段定义处使用表达式逬行赋值，要么在每个构造器中。这保证了 final字段在使用前总是被初始化。
2. final参数：可以读取这个参数, 但不能修改它

#### 8.8.2 final方法

类中的任何private方法都是隐式的final。

#### 8.8.3 final类

将整个类定义为final时（通过在其定义前加上final关键字），就阻止了该类的所有继承。这样做是因为，出于某种原因，你希望自己对这个类的设计永远不要被修改；或者 出于安全考虑，你不希望它有子类。

### 8.9 初始化及类的加载

Java类的代码在第一次使用时才加载，通常是在构造该类的第一个对象时，但在访问静态字段或静态方法时也会触发加载。

Java类的构造器是一个静态方法，当一个类的任何静态成员被访问时，都会触发构造器的加载。

静态初始化发生在初次使用时，所有静态对象和静态代码块都在加载时按文本顺序（在类定义中编写它们的顺序）初始化。静态成员只初始化一次。

子类的(静态)初始化可能依赖于基类成员的正确初始化，因此，初始化顺序应该是：

* 先基（父）类，后子类

* 先静态成员，后实例成员

* ```Java
  // reuse/Beetle.java
  // The full process of initialization
  
  class Insect {
    private int i = 9;
    protected int j;
    Insect() {
      System.out.println("i = " + i + ", j = " + j);
      j = 39;
    }
    private static int x1 =
      printInit("static Insect.x1 initialized");
    static int printInit(String s) {
      System.out.println(s);
      return 47;
    }
  }
  
  public class Beetle extends Insect {
    private int k = printInit("Beetle.k initialized");
    public Beetle() {
      System.out.println("k = " + k);
      System.out.println("j = " + j);
    }
    private static int x2 =
      printInit("static Beetle.x2 initialized");
    public static void main(String[] args) {
      System.out.println("Beetle constructor");
      Beetle b = new Beetle();
    }
  }
  /* Output:
  static Insect.x1 initialized
  static Beetle.x2 initialized
  Beetle constructor
  i = 9, j = 0
  Beetle.k initialized
  k = 47
  j = 39
  */
  ```

## 第9章 多态

### 9.3 构造器和多态

一个复杂对象的构造器调用顺序如下：

1. 发生任何其他事情之前，为对象分配的存储空间会先被初始化为二进制零 
2. 如前面所述的那样调用基类的构造器 此时被重写的draw()方法会被调用(是的， 这发生在RoundGlyph构造器被调用之前)，由于第1步的缘故，此时会发现radius值为零 
3. 按声明的顺序来初始化成员 
4. 子类构造器的主体代码被执行

```java
// polymorphism/PolyConstructors.java
// Constructors and polymorphism
// don't produce what you might expect

class Glyph {
  void draw() { System.out.println("Glyph.draw()"); }
  Glyph() {
    System.out.println("Glyph() before draw()");
    draw();
    System.out.println("Glyph() after draw()");
  }
}

class RoundGlyph extends Glyph {
  private int radius = 1;
  RoundGlyph(int r) {
    radius = r;
    System.out.println(
      "RoundGlyph.RoundGlyph(), radius = " + radius);
  }
  @Override void draw() {
    System.out.println(
      "RoundGlyph.draw(), radius = " + radius);
  }
}

public class PolyConstructors {
  public static void main(String[] args) {
    new RoundGlyph(5);
  }
}
/* Output:
Glyph() before draw()
RoundGlyph.draw(), radius = 0
Glyph() after draw()
RoundGlyph.RoundGlyph(), radius = 5
*/
```

### 9.4 协变返回类型

```java 
// polymorphism/CovariantReturn.java

class Grain {
  @Override public String toString() {
    return "Grain";
  }
}

class Wheat extends Grain {
  @Override public String toString() {
    return "Wheat";
  }
}

class Mill {
  Grain process() { return new Grain(); }
}

class WheatMill extends Mill {
  @Override Wheat process() {
    return new Wheat();
  }
}

public class CovariantReturn {
  public static void main(String[] args) {
    Mill m = new Mill();
    Grain g = m.process();
    System.out.println(g);
    m = new WheatMill();
    g = m.process();
    System.out.println(g);
  }
}
/* Output:
Grain
Wheat
*/

```

