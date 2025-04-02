
# Chapter 1 Java入门

| Java语言 | JDBC（数据库设计相关）  |
| -------- | ----------------------- |
|          | JSP（Web设计相关）      |
|          | Android                 |
|          | XML（数据交换技术）     |
|          | Java EE(网络中间件设计) |

Java特点：面向对象、平台无关、多线程

## 1.3 安装jdk

### jdk的主要内容：

- 开发工具

  位于bin子目录中。指工具和实用程序，可帮助开发、执行、调试以java编程语言编写的程序，例如，编译器javac.exe和解释器java.exe

- Java运行环境

  位于jre子目录中。运行环境包括Java虚拟机、类库以及其他支持执行java程序

- 附加库

  位于lib子目录中。开发工具所需的其他类库和支持文件

- C头文件

  位于include子目录中。支持使用Java本机界面、JVM工具界面以及Java平台的其他能进行本机代码编程的头文件

- 源代码

  位于jdk安装目录之根目录中的是src.zip文件是Java核心api的所有类的Java编程语言源文件（即Java.\*、Javax.\*和某些org.\*包的源文件，但不包括com.sun.*包的源文件）

### 系统环境的设置

```
JAVA_HOME  F:\Program Files\Java\jdk1.8.0_112

path       %JAVA_HOME%\bin
```

没安装过Java的开发产品 ，不用设置classpath

## 1.4 Java程序的开发步骤

- 编写源文件

- 编译源文件

- 运行程序

  编译源文件产生字节码，使用解释器，去执行字节码。

# Java语言

## 1. Java基础

### 1.1 为什么Java代码可以实现一次编写、到处运行？

JVM（Java虚拟机）是Java跨平台的关键。

在程序运行前，Java源代码（.java）需要经过编译器编译成字节码（.class）。在程序运行时，JVM负责将字节码翻译成特定平台下的机器码并运行，也就是说，只要在不同的平台上安装对应的JVM，就可以运行字节码文件。

同一份Java源代码在不同的平台上运行，它不需要做任何的改变，并且只需要编译一次。而编译好的字节码，是通过JVM这个中间的“桥梁”实现跨平台的，JVM是与平台相关的软件，它能将统一的字节码翻译成该平台的机器码。

**注意事项**

1. 编译的结果是生成字节码、不是机器码，字节码不能直接运行，必须通过JVM翻译成机器码才能运行；
2. 跨平台的是Java程序、而不是JVM，JVM是用C/C++开发的软件，不同平台下需要安装不同版本的JVM。

### 1.2 一个Java文件里可以有多个类吗（不含内部类）？

1. 一个java文件里可以有多个类，但最多只能有一个被public修饰的类；
2. 如果这个java文件中包含public修饰的类，则这个类的名称必须和java文件名一致。

### 1.3 说一说你对Java访问权限的了解

Java语言为我们提供了三种访问修饰符，即private、protected、public，在使用这些修饰符修饰目标时，一共可以形成四种访问权限，即private、default、protected、public，注意在不加任何修饰符时为default访问权限。

在修饰**成员变量/成员方法**时，该成员的四种访问权限的含义如下：

- private：该成员可以被该类**内部成员**访问；
- default：该成员可以被该类内部成员访问，也可以被同一包下其他的类访问；
- protected：该成员可以被该类内部成员访问，也可以被同一包下其他的类访问，还可以被它的子类访问；
- public：该成员可以被任意包下，任意类的成员进行访问。

在修饰类时，该类只有两种访问权限，对应的访问权限的含义如下：

- default：该类可以被同一包下其他的类访问；
- public：该类可以被任意包下，任意的类所访问。

### 1.4 介绍一下Java的数据类型

Java数据类型包括基本数据类型和引用数据类型两大类。

基本数据类型有8个，可以分为4个小类，分别是整数类型（byte/short/int/long）、浮点类型（float/double）、字符类型（char）、布尔类型（boolean）。其中，4个整数类型中，int类型最为常用。2个浮点类型中，double最为常用。另外，在这8个基本类型当中，除了布尔类型之外的其他7个类型，都可以看做是数字类型，它们相互之间可以进行类型转换。

引用类型就是对一个对象的引用，根据引用对象类型的不同，可以将引用类型分为3类，即数组、类、接口类型。引用类型本质上就是通过指针，指向堆中对象所持有的内存空间，只是Java语言不再沿用指针这个说法而已。

**扩展阅读**

对于基本数据类型，你需要了解每种类型所占据的内存空间，面试官可能会追问这类问题：

- byte：1字节（8位），数据范围是 -2^7 ~ 2^7-1。
- short：2字节（16位），数据范围是 -2^15 ~ 2^15-1。
- int：4字节（32位），数据范围是 -2^31 ~ 2^31-1。
- long：8字节（64位），数据范围是 -2^63 ~ 2^63-1。
- float：4字节（32位），数据范围大约是 -3.4*10^38 ~ 3.4*10^38。
- double：8字节（64位），数据范围大约是 -1.8*10^308 ~ 1.8*10^308。
- char：2字节（16位），数据范围是 \u0000 ~ \uffff。
- boolean：Java规范没有明确的规定，不同的JVM有不同的实现机制。

对于引用数据类型，你需要了解JVM的内存分布情况，知道引用以及引用对象存放的位置，详见JVM部分的题目。

### 1.6 请介绍全局变量和局部变量的区别

Java中的变量分为成员变量和局部变量，它们的区别如下：

成员变量：

1. 成员变量是在类的范围里定义的变量；
2. 成员变量有默认初始值；
3. 未被static修饰的成员变量也叫实例变量，它存储于对象所在的堆内存中，生命周期与对象相同；
4. 被static修饰的成员变量也叫类变量，它存储于方法区中，生命周期与当前类相同。

局部变量：

1. 局部变量是在方法里定义的变量；
2. 局部变量没有默认初始值；
3. 局部变量存储于栈内存中，作用的范围结束，变量空间会自动的释放。

**注意事项**

Java中没有真正的全局变量，面试官应该是出于其他语言的习惯说全局变量的，他的本意应该是指成员变量。

### 1.7 请介绍一下实例变量的默认值

实例变量若为引用数据类型，其默认值一律为null。若为基本数据类型，其默认值如下：

- byte：0
- short：0
- int：0
- long：0L
- float：0.0F
- double：0.0
- char：'\u0000'
- boolean：false

**注意事项**

上述默认值规则适用于所有的成员变量，所以对于类变量也是适用的。

### 1.8 为啥要有包装类？

Java语言是面向对象的语言，其设计理念是“一切皆对象”。但8种基本数据类型却出现了例外，它们不具备对象的特性。正是为了解决这个问题，Java为每个基本数据类型都定义了一个对应的引用类型，这就是包装类。

**扩展阅读**

Java之所以提供8种基本数据类型，主要是为了照顾程序员的传统习惯。这8种基本数据类型的确带来了一定的方便性，但在某些时候也会受到一些制约。比如，所有的引用类型的变量都继承于Object类，都可以当做Object类型的变量使用，但基本数据类型却不可以。如果某个方法需要Object类型的参数，但实际传入的值却是数字的话，就需要做特殊的处理了。有了包装类，这种问题就可以得以简化。

### 1.9 说一说自动装箱、自动拆箱的应用场景

自动装箱、自动拆箱是JDK1.5提供的功能。

自动装箱：可以把一个基本类型的数据直接赋值给对应的包装类型；

自动拆箱：可以把一个包装类型的对象直接赋值给对应的基本类型；

通过自动装箱、自动拆箱功能，可以大大简化基本类型变量和包装类对象之间的转换过程。比如，某个方法的参数类型为包装类型，调用时我们所持有的数据却是基本类型的值，则可以不做任何特殊的处理，直接将这个基本类型的值传入给方法即可。



基本类型都有对应的包装类型，基本类型与其对应的包装类型之间的赋值使用自动装箱与拆箱完成。

```java
Integer x = 2;		// 装箱 调用了 Integer.valueOf(2)
int y = x;          // 拆箱 调用了 X.intValue()
```



### 1.10 如何对Integer和Double类型判断相等？

Integer、Double不能直接进行比较，这包括：

- 不能用==进行直接比较，因为它们是不同的数据类型；
- 不能转为字符串进行比较，因为转为字符串后，浮点值带小数点，整数值不带，这样它们永远都不相等；
- 不能使用compareTo方法进行比较，虽然它们都有compareTo方法，但该方法只能对相同类型进行比较。

整数、浮点类型的包装类，都继承于Number类型，而Number类型分别定义了将数字转换为byte、short、int、long、float、double的方法。所以，可以将Integer、Double先转为转换为相同的基本数据类型（如double），然后使用==进行比较。

```java
Integer i = 100;
Double d = 100.00;
System.out.println(i.doubleValue() == d.doubleValue());
```

### 1.12 说一说你对面向对象的理解

面向对象是一种更优秀的程序设计方法，它的基本思想是使用类、对象、继承、封装、消息等基本概念进行程序设计。它从现实世界中客观存在的事物出发来构造软件系统，并在系统构造中尽可能运用人类的自然思维方式，强调直接以现实世界中的事物为中心来思考，认识问题，并根据这些事物的本质特点，把它们抽象地表示为系统中的类，作为系统的基本构成单元，这使得软件系统的组件可以直接映像到客观世界，并保持客观世界中事物及其相互关系的本来面貌。

**扩展阅读**

结构化程序设计方法主张按功能来分析系统需求，其主要原则可概括为自顶向下、逐步求精、模块化等。结构化程序设计首先采用结构化分析方法对系统进行需求分析，然后使用结构化设计方法对系统进行概要设计、详细设计，最后采用结构化编程方法来实现系统。

因为结构化程序设计方法主张按功能把软件系统逐步细分，因此这种方法也被称为面向功能的程序设计方法；结构化程序设计的每个功能都负责对数据进行一次处理，每个功能都接受一些数据，处理完后输出一些数据，这种处理方式也被称为面向数据流的处理方式。

结构化程序设计里最小的程序单元是函数，每个函数都负责完成一个功能，用以接收一些输入数据，函数对这些输入数据进行处理，处理结束后输出一些数据。整个软件系统由一个个函数组成，其中作为程序入口的函数被称为主函数，主函数依次调用其他普通函数，普通函数之间依次调用，从而完成整个软件系统的功能。

每个函数都是具有输入、输出的子系统，函数的输入数据包括函数形参、全局变量和常量等，函数的输出数据包括函数返回值以及传出参数等。结构化程序设计方式有如下两个局限性：

- 设计不够直观，与人类习惯思维不一致。采用结构化程序分析、设计时，开发者需要将客观世界模型分解成一个个功能，每个功能用以完成一定的数据处理。
- 适应性差，可扩展性不强。由于结构化设计采用自顶向下的设计方式，所以当用户的需求发生改变，或需要修改现有的实现方式时，都需要自顶向下地修改模块结构，这种方式的维护成本相当高。

### 1.13 面向对象的三大特征是什么？

面向对象的程序设计方法具有三个基本特征：封装、继承、多态。其中，封装指的是将对象的实现细节隐藏起来，然后通过一些公用方法来暴露该对象的功能；继承是面向对象实现软件复用的重要手段，当子类继承父类后，子类作为一种特殊的父类，将直接获得父类的属性和方法；多态指的是子类对象可以直接赋给父类变量，但运行时依然表现出子类的行为特征，这意味着同一个类型的对象在执行同一个方法时，可能表现出多种行为特征。

**扩展阅读**

抽象也是面向对象的重要部分，抽象就是忽略一个主题中与当前目标无关的那些方面，以便更充分地注意与当前目标有关的方面。抽象并不打算了解全部问题，而只是考虑部分问题。例如，需要考察Person对象时，不可能在程序中把Person的所有细节都定义出来，通常只能定义Person的部分数据、部分行为特征，而这些数据、行为特征是软件系统所关心的部分。

### 1.14 封装的目的是什么，为什么要有封装？

封装是面向对象编程语言对客观世界的模拟，在客观世界里，对象的状态信息都被隐藏在对象内部，外界无法直接操作和修改。对一个类或对象实现良好的封装，可以实现以下目的：

- 隐藏类的实现细节；
- 让使用者只能通过事先预定的方法来访问数据，从而可以在该方法里加入控制逻辑，限制对成员变量的不合理访问；
- 可进行数据检查，从而有利于保证对象信息的完整性；
- 便于修改，提高代码的可维护性。

**扩展阅读**

为了实现良好的封装，需要从两个方面考虑：

- 将对象的成员变量和实现细节隐藏起来，不允许外部直接访问；
- 把方法暴露出来，让方法来控制对这些成员变量进行安全的访问和操作。

封装实际上有两个方面的含义：把该隐藏的隐藏起来，把该暴露的暴露出来。这两个方面都需要通过使用Java提供的访问控制符来实现。

### 1.15 说一说你对多态的理解

因为子类其实是一种特殊的父类，因此Java允许把一个子类对象直接赋给一个父类引用变量，无须任何类型转换，或者被称为向上转型，向上转型由系统自动完成。

当把一个子类对象直接赋给父类引用变量时，例如 BaseClass obj = new SubClass();，这个obj引用变量的编译时类型是BaseClass，而运行时类型是SubClass，当运行时调用该引用变量的方法时，其方法行为总是表现出子类方法的行为特征，而不是父类方法的行为特征，这就可能出现：相同类型的变量、调用同一个方法时呈现出多种不同的行为特征，这就是多态。

**扩展阅读**

多态可以提高程序的可扩展性，在设计程序时让代码更加简洁而优雅。

例如我要设计一个司机类，他可以开轿车、巴士、卡车等等，示例代码如下：

```java
class Driver {
    void drive(Car car) { ... }
    void drive(Bus bus) { ... }
    void drive(Truck truck) { ... }
}
```

在设计上述代码时，我已采用了重载机制，将方法名进行了统一。这样在进行调用时，无论要开什么交通工具，都是通过driver.drive(obj)这样的方式来调用，对调用者足够的友好。

但对于程序的开发者来说，这显得繁琐，因为实际上这个司机可以驾驶更多的交通工具。当系统需要为这个司机增加车型时，开发者就需要相应的增加driver方法，类似的代码会堆积的越来越多，显得臃肿。

采用多态的方式来设计上述程序，就会变得简洁很多。我们可以为所有的交通工具定义一个父类Vehicle，然后按照如下的方式设计drive方法。调用时，我们可以传入Vehicle类型的实例，也可以传入任意的Vehicle子类型的实例，对于调用者来说一样的方便，但对于开发者来说，代码却变得十分的简洁了。

```java
class Driver {
    void drive(Vehicle vehicle) { ... }
}
```

多态是指，针对某个类型的方法调用，其真正执行的方法取决于运行时期实际类型的方法。例如：

```java
Person p = new Student();
p.run(); // 无法确定运行时究竟调用哪个run()方法

public void runTwice(Person p) {
    p.run();
    p.run();
}
```

它传入的参数类型是`Person`，我们是无法知道传入的参数实际类型究竟是`Person`，还是`Student`，还是`Person`的其他子类，因此，也无法确定调用的是不是`Person`类定义的`run()`方法。

```java
public class Main {
    public static void main(String[] args) {
        // 给一个有普通收入、工资收入和享受国务院特殊津贴的小伙伴算税:
        Income[] incomes = new Income[] {
            new Income(3000),
            new Salary(7500),
            new StateCouncilSpecialAllowance(15000)
        };
        System.out.println(totalTax(incomes));
    }

    public static double totalTax(Income... incomes) {
        double total = 0;
        for (Income income: incomes) {
            total = total + income.getTax();
        }
        return total;
    }
}

class Income {
    protected double income;

    public Income(double income) {
        this.income = income;
    }

    public double getTax() {
        return income * 0.1; // 税率10%
    }
}

class Salary extends Income {
    public Salary(double income) {
        super(income);
    }

    @Override
    public double getTax() {
        if (income <= 5000) {
            return 0;
        }
        return (income - 5000) * 0.2;
    }
}

class StateCouncilSpecialAllowance extends Income {
    public StateCouncilSpecialAllowance(double income) {
        super(income);
    }

    @Override
    public double getTax() {
        return 0;
    }
}
```

多态具有一个非常强大的功能，就是允许添加更多类型的子类实现功能扩展，却不需要修改基于父类的代码。

#### 覆写Object方法

因为所有的`class`最终都继承自`Object`，而`Object`定义了几个重要的方法：

- `toString()`：把instance输出为`String`；
- `equals()`：判断两个instance是否逻辑相等；
- `hashCode()`：计算一个instance的哈希值。

```java
class Person {
    ...
    // 显示更有意义的字符串:
    @Override
    public String toString() {
        return "Person:name=" + name;
    }

    // 比较是否相等:
    @Override
    public boolean equals(Object o) {
        // 当且仅当o为Person类型:
        if (o instanceof Person) {
            Person p = (Person) o;
            // 并且name字段相同时，返回true:
            return this.name.equals(p.name);
        }
        return false;
    }

    // 计算hash:
    @Override
    public int hashCode() {
        return this.name.hashCode();
    }
}
```

继承可以允许子类覆写父类的方法。如果一个父类不允许子类对它的某个方法进行覆写，可以把该方法标记为`final`。用`final`修饰的方法不能被`Override`

如果一个类不希望任何其他类继承自它，那么可以把这个类本身标记为`final`。用`final`修饰的类不能被继承

### 1.16 Java中的多态是怎么实现的？

多态的实现离不开继承，在设计程序时，我们可以将参数的类型定义为父类型。在调用程序时，则可以根据实际情况，传入该父类型的某个子类型的实例，这样就实现了多态。对于父类型，可以有三种形式，即普通的类、抽象类、接口。对于子类型，则要根据它自身的特征，重写父类的某些方法，或实现抽象类/接口的某些抽象方法。

### 1.17 Java为什么是单继承，为什么不能多继承？

首先，Java是单继承的，指的是Java中一个类只能有一个直接的父类。Java不能多继承，则是说Java中一个类不能直接继承多个父类。

其次，Java在设计时借鉴了C++的语法，而C++是支持多继承的。Java语言之所以摒弃了多继承的这项特征，是因为多继承容易产生混淆。比如，两个父类中包含相同的方法时，子类在调用该方法或重写该方法时就会迷惑。

准确来说，Java是可以实现"多继承"的。因为尽管一个类只能有一个直接父类，但是却可以有任意多个间接的父类。这样的设计方式，避免了多继承时所产生的混淆。

### 1.18 说一说重写与重载的区别

**重载**：发生在同一个类中，方法名必须相同，参数类型不同、个数不同、顺序不同，方法返回值和访问修饰符可以不同，发生在编译时。

**重写**：发生在父子类中，方法名、参数列表必须相同，返回值范围小于等于父类，抛出的异常范围小于等于父类，访问修饰符的范围大于等于父类；如果父类方法访问修饰符为private则子类就不能重写该方法。

```java
public int add(int a,String b)
public String add(int a,String b)
//编译报错，重载与返回值类型无关
```

### 1.19 构造方法能不能重写？

构造方法不能重写。因为构造方法需要和类保持同名，而重写的要求是子类方法要和父类方法保持同名。如果允许重写构造方法的话，那么子类中将会存在与类名不同的构造方法，这与构造方法的要求是矛盾的。

### 1.20 介绍一下Object类中的方法

```java
public final native Class<?> getClass()//native方法，用于返回当前运行时对象的Class对象，使用了final关键字修饰，故不允许子类重写。
public native int hashCode() //native方法，用于返回对象的哈希码，主要使用在哈希表中，比如JDK中的HashMap

public boolean equals(Object obj)//用于比较2个对象的内存地址是否相等，String类对该方法进行了重写用户比较字符串的值是否相等。
    
protected native Object clone() throws CloneNotSupportedException//native方法，用于创建并返回当前对象的一份拷贝。一般情况下，对于任何对象x，表达式x.clone() != x 为true，x.clone().getClass() == x.getClass()为true。Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会发生CloneNotSupportedException异常。

public String toString() // 返回类的名字@实例的哈希码的16进制的字符串。建议Object所有的子类都重写这个方法。

public final native void notify()//native方法，并且不能重写。唤醒一个在此对象监视器上等待的线程（监视器相当于就是锁的概念）。如果有多个线程在等待只会任意唤醒一个。
    
public final native void notifyAll()//native方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。
    
public final native void wait(long timeout) throws InterruptedException//native方法，并且不能重写。暂停线程的执行。注意：sleep方法没有释放锁，而wait方法释放了锁。timeout是等待时间。
    
public final void wait(long timeout, int nanos) throws InterruptedException//多了nanos参数，这个参数表示额外时间（以毫微秒为单位，范围是0-999999）。所以超时的时间还需要加上nanos毫秒。
    
public final void wait () throws InterruptedException//跟之前的2个wait方法一样，只不过该方法一直等待，没有超时间这个概念
    
    
protected void finalize() throws Throwable {} //实例被垃圾回收器回收的时候触发的操作
```

**扩展阅读**

Object类还提供了一个finalize()方法，当系统中没有引用变量引用到该对象时，垃圾回收器调用此方法来清理该对象的资源。并且，针对某一个对象，垃圾回收器最多只会调用它的finalize()方法一次。

注意，finalize()方法何时调用、是否调用都是不确定的，我们也不要主动调用finalize()方法。从JDK9开始，这个方法被标记为不推荐使用的方法。

### 1.21 说一说hashCode()和equals()的关系

hashCode()用于获取哈希码（散列码），eauqls()用于比较两个对象是否相等，它们应遵守如下规定：

- 如果两个对象相等，则它们必须有相同的哈希码。
- 如果两个对象有相同的哈希码，则它们未必相等。

**扩展阅读**

在Java中，Set接口代表无序的、元素不可重复的集合，HashSet则是Set接口的典型实现。

当向HashSet中加入一个元素时，它需要判断集合中是否已经包含了这个元素，从而避免重复存储。由于这个判断十分的频繁，所以要讲求效率，绝不能采用遍历集合逐个元素进行比较的方式。实际上，HashSet是通过获取对象的哈希码，以及调用对象的equals()方法来解决这个判断问题的。

HashSet首先会调用对象的hashCode()方法获取其哈希码，并通过哈希码确定该对象在集合中存放的位置。假设这个位置之前已经存了一个对象，则HashSet会调用equals()对两个对象进行比较。若相等则说明对象重复，此时不会保存新加的对象。若不等说明对象不重复，但是它们存储的位置发生了碰撞，此时HashSet会采用链式结构在同一位置保存多个对象，即将新加对象链接到原来对象的之后。之后，再有新添加对象也映射到这个位置时，就需要与这个位置中所有的对象进行equals()比较，若均不相等则将其链到最后一个对象之后。

### 1.22 为什么要重写hashCode()和equals()？

Object类提供的equals()方法默认是用==来进行比较的，也就是说只有两个对象是同一个对象时，才能返回相等的结果。而实际的业务中，我们通常的需求是，若两个不同的对象它们的内容是相同的，就认为它们相等。鉴于这种情况，Object类中equals()方法的默认实现是没有实用价值的，所以通常都要重写。

由于hashCode()与equals()具有联动关系（参考“说一说hashCode()和equals()的关系”一题），所以equals()方法重写时，通常也要将hashCode()进行重写，使得这两个方法始终满足相关的约定。

### 1.23 ==和equals()有什么区别？

==运算符：

- 作用于基本数据类型时，是比较两个数值是否相等；
- 作用于引用数据类型时，是比较两个对象的内存地址是否相同，即判断它们是否为同一个对象；

equals()方法：

- 没有重写时，Object默认以 == 来实现，即比较两个对象的内存地址是否相同；
- 进行重写后，一般会按照对象的内容来进行比较，若两个对象内容相同则认为对象相等，否则认为对象不等。

### 1.24 String类有哪些方法？

String类是Java最常用的API，它包含了大量处理字符串的方法，比较常用的有：

- char charAt(int index)：返回指定索引处的字符；
- String substring(int beginIndex, int endIndex)：从此字符串中截取出一部分子字符串；
- String[] split(String regex)：以指定的规则将此字符串分割成数组；
- String trim()：删除字符串前导和后置的空格；
- int indexOf(String str)：返回子串在此字符串首次出现的索引；
- int lastIndexOf(String str)：返回子串在此字符串最后出现的索引；
- boolean startsWith(String prefix)：判断此字符串是否以指定的前缀开头；
- boolean endsWith(String suffix)：判断此字符串是否以指定的后缀结尾；
- String toUpperCase()：将此字符串中所有的字符大写；
- String toLowerCase()：将此字符串中所有的字符小写；
- String replaceFirst(String regex, String replacement)：用指定字符串替换第一个匹配的子串；
- String replaceAll(String regex, String replacement)：用指定字符串替换所有的匹配的子串。

**注意事项**

String类的方法太多了，你没必要都记下来，更不需要一一列举。面试时能说出一些常用的方法，表现出对这个类足够的熟悉就可以了。另外，建议你挑几个方法仔细看看源码实现，面试时可以重点说这几个方法。

### 1.25 String可以被继承吗？

String类由final修饰，所以不能被继承。

**扩展阅读**

在Java中，String类被设计为不可变类，主要表现在它保存字符串的成员变量是final的。

- Java 9之前字符串采用char[]数组来保存字符，即 private final char[] value；
- Java 9做了改进，采用byte[]数组来保存字符，即 private final byte[] value；

之所以要把String类设计为不可变类，主要是出于安全和性能的考虑，可归纳为如下4点。

- 由于字符串无论在任何 Java 系统中都广泛使用，会用来存储敏感信息，如账号，密码，网络路径，文件处理等场景里，保证字符串 String 类的安全性就尤为重要了，如果字符串是可变的，容易被篡改，那我们就无法保证使用字符串进行操作时，它是安全的，很有可能出现 SQL 注入，访问危险文件等操作。
- 在多线程中，只有不变的对象和值是线程安全的，可以在多个线程中共享数据。由于 String 天然的不可变，当一个线程”修改“了字符串的值，只会产生一个新的字符串对象，不会对其他线程的访问产生副作用，访问的都是同样的字符串数据，不需要任何同步操作。
- 字符串作为基础的数据结构，大量地应用在一些集合容器之中，尤其是一些散列集合，在散列集合中，存放元素都要根据对象的 hashCode() 方法来确定元素的位置。由于字符串 hashcode 属性不会变更，保证了唯一性，使得类似 HashMap，HashSet 等容器才能实现相应的缓存功能。由于 String 的不可变，避免重复计算 hashcode，只要使用缓存的 hashcode 即可，这样一来大大提高了在散列集合中使用 String 对象的性能。
- 当字符串不可变时，字符串常量池才有意义。字符串常量池的出现，可以减少创建相同字面量的字符串，让不同的引用指向池中同一个字符串，为运行时节约很多的堆内存。若字符串可变，字符串常量池失去意义，基于常量池的 String.intern() 方法也失效，每次创建新的字符串将在堆内开辟出新的空间，占据更多的内存。

因为要保证String类的不可变，那么将这个类定义为final的就很容易理解了。如果没有final修饰，那么就会存在String的子类，这些子类可以重写String类的方法，强行改变字符串的值，这便违背了String类设计的初衷。

#### 概览

String 被声明为 final，因此它不可被继承。(Integer 等包装类也不能被继承）

在 Java 8 中，String 内部使用 char 数组存储数据。

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];
}
```

在 Java 9 之后，String 类的实现改用 byte 数组存储字符串，同时使用 `coder` 来标识使用了哪种编码。

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final byte[] value;

    /** The identifier of the encoding used to encode the bytes in {@code value}. */
    private final byte coder;
}
```

value 数组被声明为 final，这意味着 value 数组初始化之后就不能再引用其它数组。并且 String 内部没有改变 value 数组的方法，因此可以保证 String 不可变。

##### 不可变的好处

##### 1. 可以缓存 hash 值

因为 String 的 hash 值经常被使用，例如 String 用做 HashMap 的 key。不可变的特性可以使得 hash 值也不可变，因此只需要进行一次计算。

##### 2.String Pool 的需要

如果一个 String 对象已经被创建过了，那么就会从 String Pool 中取得引用。只有 String 是不可变的，才可能使用 String Pool。

![](D:\Study\自学\笔记\img\image-20191210004132894.png)

##### 3.安全性

String 经常作为参数，String 不可变性可以保证参数不可变。例如在作为网络连接参数的情况下如果 String 是可变的，那么在网络连接过程中，String 被改变，改变 String 的那一方以为现在连接的是其它主机，而实际情况却不一定是。

##### 4. 线程安全

String 不可变性天生具备线程安全，可以在多个线程中安全地使用。

##### String Pool

字符串常量池（String Pool）保存着所有字符串字面量（literal strings），



### 缓存池

new Integer(123) 与 Integer.valueOf(123) 的区别在于：

- new Integer(123) 每次都会新建一个对象；
- Integer.valueOf(123) 会使用缓存池中的对象，多次调用会取得同一个对象的引用。

```java
Integer x = new Integer(123);
Integer y = new Integer(123);
System.out.println(x == y); //false
Integer z = Integer.valueOf(123);
Integer k = Integer.valueOf(123);
System.out.println(z == k); //true
```

valueOf() 方法的实现比较简单，就是先判断值是否在缓存池中，如果在的话就直接返回缓存池的内容。

```java
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        reutrn IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
```

在 Java 8 中，Integer 缓存池的大小默认为 -128~127。

```java
static final int low = -128;
static final int high;
static final Integer cache[];
static {
    // high value may be configured by property
    int h = 127;
    String integerCacheHighPropValue = 					                       		sun.misc.VM.getSaveProperty("java.lang.Integer.IntegerCache.high");
    if (integerCacheHighPropValue != null) {
        try {
            int i = parseInt(integerCacheHighPropValue);
            i = Math.max(i,127);
            // Maximum array size is Integer.MAX_VALUE
            h = Math.min(i,Integer.MAX_VALUE - (-low) -1);
        } catch( NumberFormatException nfe) {
            // If the property cannot be parsed into an int, ignore it.
        }
    }
    high = h;
    
    cache = new Integer[(high - low) + 1];
    int j = low;
    for(int k = 0; k < cache.length; k++) 
        cache[k] = new Integer(j++);
    // range [-128, 127] must be interned (JLS7 5.1.7)
    assert IntegerCache.high >= 127;
}
```

编译器会在自动装箱过程调用 valueOf() 方法，因此多个值相同且值在缓存池范围内的 Integer 实例使用自动装箱来创建，那么就会引用相同的对象。

```java
Integer m = 123;
Integer n = 123;
System.out.println(m == n); //true

```

基本类型对应的缓冲池如下：

- boolean values true and false
- all byte values
- short values between -128 and 127
- int values between -128 and 127
- char in the range \u0000 to \u007F

在使用这些基本类型对应的包装类型时，如果该数值范围在缓冲池范围内，就可以直接使用缓冲池中的对象。

在 jdk 1.8 所有的数值类缓冲池中，Integer 的缓冲池 IntegerCache 很特殊，这个缓冲池的下界是 - 128，上界默认是 127，但是这个上界是可调的，在启动 jvm 的时候，通过 -XX:AutoBoxCacheMax=<size> 来指定这个缓冲池的大小，该选项在 JVM 初始化的时候会设定一个名为 java.lang.IntegerCache.high 系统属性，然后 IntegerCache 初始化的时候就会读取该系统属性来决定上界。



### 1.26 说一说String、StringBuffer和StringBuilder有什么区别

#### 1.可变性

- String 不可变
- StringBuffer 和 StringBuilder 可变

#### 2.线程安全

- String 不可变，因此是线程安全的

- StringBuilder 不是线程安全的

- StringBuffer 是线程安全的，内部使用 synchronized 进行同步

- 场景：经常需要会改变字符串内容的使用后两个

  优先使用StringBuilder，多线程**使用共享变量**时使用**StringBuffer**

### StringBuilder

```java
String s = "";
for (int i = 0; i < 1000; i++) {
    s = s + "," + i;
}
```

虽然可以直接拼接字符串，但是，在循环中，每次循环都会创建新的字符串对象，然后扔掉旧的字符串。这样，绝大部分字符串都是临时对象，不但浪费内存，还会影响GC效率。

为了能高效拼接字符串，Java标准库提供了`StringBuilder`，它是一个可变对象，可以预分配缓冲区，这样，往`StringBuilder`中新增字符时，不会创建新的临时对象：

```java
StringBuilder sb = new StringBuilder(1024);
for (int i = 0; i < 1000; i++) {
    sb.append(',');
    sb.append(i);
}
String s = sb.toString();
```

```java
//链式操作
public class Main {
    public static void main(String[] args) {
        var sb = new StringBuilder(1024);
        sb.append("Mr ")
          .append("Bob")
          .append("!")
          .insert(0, "Hello, ");
        System.out.println(sb.toString()); //Hello, Mr Bob!
    }
}
```

### StringJoiner

```java
//Hello Bob, Alice, Grace!
public class Main {
    public static void main(String[] args) {
        String[] names = {"Bob", "Alice", "Grace"};
        var sb = new StringBuilder();
        sb.append("Hello ");
        for (String name : names) {
            sb.append(name).append(", ");
        }
        // 注意去掉最后的", ":
        sb.delete(sb.length() - 2, sb.length());
        sb.append("!");
        System.out.println(sb.toString());
    }
}

```

```java
//Hello Bob, Alice, Grace!
import java.util.StringJoiner;

public class Main {
    public static void main(String[] args) {
        String[] names = {"Bob", "Alice", "Grace"};
        var sj = new StringJoiner(", ", "Hello ", "!");
        for (String name : names) {
            sj.add(name);
        }
        System.out.println(sj.toString());
    }
}
```

### 包装类型

```java
public class Main {
    public static void main(String[] args) {
        int i = 100;
        // 通过new操作符创建Integer实例(不推荐使用,会有编译警告):
        Integer n1 = new Integer(i);
        // 通过静态方法valueOf(int)创建Integer实例:
        Integer n2 = Integer.valueOf(i);
        // 通过静态方法valueOf(String)创建Integer实例:
        Integer n3 = Integer.valueOf("100");
        System.out.println(n3.intValue());
    }
}
```

```java
//自动拆箱/装箱
int i = 100;
Integer n = Integer.valueOf(i);
int x = n.intValue();

Integer n = 100; // 编译器自动使用Integer.valueOf(int)
int x = n; // 编译器自动使用Integer.intValue()
```

注意：自动装箱和自动拆箱只发生在编译阶段，目的是为了少写代码。

装箱和拆箱会影响代码的执行效率，因为编译后的`class`代码是严格区分基本类型和引用类型的。并且，自动拆箱执行时可能会报`NullPointerException`：

```java
//NullPointerException
public class Main {
    public static void main(String[] args) {
        Integer n = null;
        int i = n;
    }
}
```

### 字符串和编码

实际上字符串在`String`内部是通过一个`char[]`数组表示的，因此，按下面的写法也是可以的：

```java
String s2 = new String(new char[] {'H', 'e', 'l', 'l', 'o', '!'});
```

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "HELLO".toLowerCase();
        System.out.println(s1 == s2);      //false
        System.out.println(s1.equals(s2)); //true
    }
}
```

结论：两个字符串比较，必须总是使用`equals()`方法。

要忽略大小写比较，使用`equalsIgnoreCase()`方法。

`String`类还提供了多种方法来搜索子串、提取子串。常用的方法有：

```java
// 是否包含子串:
"Hello".contains("ll"); // true
```

注意到`contains()`方法的参数是`CharSequence`而不是`String`，因为`CharSequence`是`String`的父类。

搜索子串的更多的例子：

```java
"Hello".indexOf("l"); // 2
"Hello".lastIndexOf("l"); // 3
"Hello".startsWith("He"); // true
"Hello".endsWith("lo"); // true
"Hello".substring(2); // "llo"
"Hello".substring(2, 4); "ll"
 "  \tHello\r\n ".trim(); // "Hello"   使用trim()方法可以移除字符串首尾空白字符。空白字符包括空格，\t，\r，\n：
```

另一个`strip()`方法也可以移除字符串首尾空白字符。它和`trim()`不同的是，类似中文的空格字符`\u3000`也会被移除：

```java
"\u3000Hello\u3000".strip(); // "Hello"
" Hello ".stripLeading(); // "Hello "
" Hello ".stripTrailing(); // " Hello"
```

要在字符串中替换子串，有两种方法。一种是根据字符或字符串替换：

```java
String s = "hello";
s.replace('l', 'w'); // "hewwo"，所有字符'l'被替换为'w'
s.replace("ll", "~~"); // "he~~o"，所有子串"ll"被替换为"~~"
```

另一种是通过正则表达式替换：

```java
String s = "A,,B;C ,D";
s.replaceAll("[\\,\\;\\s]+", ","); // "A,B,C,D"
```

要分割字符串，使用`split()`方法，并且传入的也是正则表达式

```java
String s = "A,B,C,D";
String[] ss = s.split("\\,"); // {"A", "B", "C", "D"}
```

拼接字符串使用静态方法`join()`，它用指定的字符串连接字符串数组：

```java
String[] arr = {"A", "B", "C"};
String s = String.join("***", arr); // "A***B***C"
```

字符串提供了`formatted()`方法和`format()`静态方法，可以传入其他参数，替换占位符，然后生成新的字符串：

```java
public class Main {
    public static void main(String[] args) {
        String s = "Hi %s, your score is %d!";
        System.out.println(s.formatted("Alice", 80)); //Hi Alice, your score is 80!
        System.out.println(String.format("Hi %s, your score is %.2f!", "Bob", 59.5));//Hi Bob, your score is 59.50!
    }
}
```

有几个占位符，后面就传入几个参数。参数类型要和占位符一致。我们经常用这个方法来格式化信息。常用的占位符有：

- `%s`：显示字符串；
- `%d`：显示整数；
- `%x`：显示十六进制整数；
- `%f`：显示浮点数。

占位符还可以带格式，例如`%.2f`表示显示两位小数。如果你不确定用啥占位符，那就始终用`%s`，因为`%s`可以显示任何数据类型。

要把任意基本类型或引用类型转换为字符串，可以使用静态方法`valueOf()`。这是一个重载方法，编译器会根据参数自动选择合适的方法：

```java
String.valueOf(123); // "123"
String.valueOf(45.67); // "45.67"
String.valueOf(true); // "true"
String.valueOf(new Object()); // 类似java.lang.Object@636be97c
```

要把字符串转换为其他类型，就需要根据情况。例如，把字符串转换为`int`类型：

```java
int n1 = Integer.parseInt("123"); // 123
int n2 = Integer.parseInt("ff", 16); // 按十六进制转换，255
```

把字符串转换为`boolean`类型

```java
boolean b1 = Boolean.parseBoolean("true"); // true
boolean b2 = Boolean.parseBoolean("FALSE"); // false
```

要特别注意，`Integer`有个`getInteger(String)`方法，它不是将字符串转换为`int`，而是把该字符串对应的系统变量转换为`Integer`

```java
Integer.getInteger("java.version"); // 版本号，11
```

`String`和`char[]`类型可以互相转换，方法是：

```java
char[] cs = "Hello".toCharArray(); // String -> char[]
String s = new String(cs); // char[] -> String
```

如果修改了`char[]`数组，`String`并不会改变：

```java
//String <-> char[]
public class Main {
    public static void main(String[] args) {
        char[] cs = "Hello".toCharArray();
        String s = new String(cs);
        System.out.println(s); //Hello
        cs[0] = 'X';
        System.out.println(s); //Hello
    }
}
```

这是因为通过`new String(char[])`创建新的`String`实例时，它并不会直接引用传入的`char[]`数组，而是会复制一份，所以，修改外部的`char[]`数组不会影响`String`实例内部的`char[]`数组，因为这是两个不同的数组。

从`String`的不变性设计可以看出，如果传入的对象有可能改变，我们需要复制而不是直接引用。

在Java中，`char`类型实际上就是两个字节的`Unicode`编码。如果我们要手动把字符串转换成其他编码，可以这样做：

```java
byte[] b1 = "Hello".getBytes(); // 按系统默认编码转换，不推荐
byte[] b2 = "Hello".getBytes("UTF-8"); // 按UTF-8编码转换
byte[] b2 = "Hello".getBytes("GBK"); // 按GBK编码转换
byte[] b3 = "Hello".getBytes(StandardCharsets.UTF_8); // 按UTF-8编码转换
```

注意：转换编码后，就不再是`char`类型，而是`byte`类型表示的数组。

如果要把已知编码的`byte[]`--->`String`，可以这样做：

```java
byte[] b = ...
String s1 = new String(b, "GBK"); // 按GBK转换
String s2 = new String(b, StandardCharsets.UTF_8); // 按UTF-8转换
```



### 1.28 使用字符串时，new和""推荐使用哪种方式？

先看看 "hello" 和 new String("hello") 的区别：

- 当Java程序直接使用 "hello" 的字符串直接量时，JVM将会使用常量池来管理这个字符串；
- 当使用 new String("hello") 时，JVM会先使用常量池来管理 "hello" 直接量，再调用String类的构造器来创建一个新的String对象，新创建的String对象被保存在堆内存中。

显然，采用new的方式会多创建一个对象出来，会占用更多的内存，所以一般建议使用直接量的方式创建字符串。

### 1.29 说一说你对字符串拼接的理解

拼接字符串有很多种方式，其中最常用的有4种，下面列举了这4种方式各自适合的场景。

1. \+ 运算符：如果拼接的都是字符串直接量，则适合使用 + 运算符实现拼接；
2. StringBuilder：如果拼接的字符串中包含变量，并不要求线程安全，则适合使用StringBuilder；
3. StringBuffer：如果拼接的字符串中包含变量，并且要求线程安全，则适合使用StringBuffer；
4. String类的concat方法：如果只是对两个字符串进行拼接，并且包含变量，则适合使用concat方法；

**扩展阅读**

采用 + 运算符拼接字符串时：

- 如果拼接的都是字符串直接量，则在编译时编译器会将其直接优化为一个完整的字符串，和你直接写一个完整的字符串是一样的，所以效率非常的高。
- 如果拼接的字符串中包含变量，则在编译时编译器采用StringBuilder对其进行优化，即自动创建StringBuilder实例并调用其append()方法，将这些字符串拼接在一起，效率也很高。但如果这个拼接操作是在循环中进行的，那么每次循环编译器都会创建一个StringBuilder实例，再去拼接字符串，相当于执行了 new StringBuilder().append(str)，所以此时效率很低。

采用StringBuilder/StringBuffer拼接字符串时：

- StringBuilder/StringBuffer都有字符串缓冲区，缓冲区的容量在创建对象时确定，并且默认为16。当拼接的字符串超过缓冲区的容量时，会触发缓冲区的扩容机制，即缓冲区加倍。
- 缓冲区频繁的扩容会降低拼接的性能，所以如果能提前预估最终字符串的长度，则建议在创建可变字符串对象时，放弃使用默认的容量，可以指定缓冲区的容量为预估的字符串的长度。

采用String类的concat方法拼接字符串时：

- concat方法的拼接逻辑是，先创建一个足以容纳待拼接的两个字符串的字节数组，然后先后将两个字符串拼到这个数组里，最后将此数组转换为字符串。
- 在拼接大量字符串的时候，concat方法的效率低于StringBuilder。但是只拼接2个字符串时，concat方法的效率要优于StringBuilder。并且这种拼接方式代码简洁，所以只拼2个字符串时建议优先选择concat方法。

### 1.30 两个字符串相加的底层是如何实现的？

如果拼接的都是字符串直接量，则在编译时编译器会将其直接优化为一个完整的字符串，和你直接写一个完整的字符串是一样的。

如果拼接的字符串中包含变量，则在编译时编译器采用StringBuilder对其进行优化，即自动创建StringBuilder实例并调用其append()方法，将这些字符串拼接在一起。

### 1.31 String a = "abc"; ，说一下这个过程会创建什么，放在哪里？

JVM会使用常量池来管理字符串直接量。在执行这句话时，JVM会先检查常量池中是否已经存有"abc"，若没有则将"abc"存入常量池，否则就复用常量池中已有的"abc"，将其引用赋值给变量a。

### 1.32 new String("abc") 是去了哪里，仅仅是在堆里面吗？

在执行这句话时，JVM会先使用常量池来管理字符串直接量，即将"abc"存入常量池。然后再创建一个新的String对象，这个对象会被保存在堆内存中。并且，堆中对象的数据会指向常量池中的直接量。

### 1.33 接口和抽象类有什么区别？

从设计目的上来说，二者有如下的区别：

接口体现的是一种规范。对于接口的实现者而言，接口规定了实现者必须向外提供哪些服务；对于接口的调用者而言，接口规定了调用者可以调用哪些服务，以及如何调用这些服务。当在一个程序中使用接口时，接口是多个模块间的耦合标准；当在多个应用程序之间使用接口时，接口是多个程序之间的通信标准。

抽象类体现的是一种模板式设计。抽象类作为多个子类的抽象父类，可以被当成系统实现过程中的中间产品，这个中间产品已经实现了系统的部分功能，但这个产品依然不能当成最终产品，必须有更进一步的完善，这种完善可能有几种不同方式。

从使用方式上来说，二者有如下的区别：

- 接口里只能包含抽象方法、静态方法、默认方法和私有方法，不能为普通方法提供方法实现；抽象类则完全可以包含普通方法。
- 接口里只能定义静态常量，不能定义普通成员变量；抽象类里则既可以定义普通成员变量，也可以定义静态常量。
- 接口里不包含构造器；抽象类里可以包含构造器，抽象类里的构造器并不是用于创建对象，而是让其子类调用这些构造器来完成属于抽象类的初始化操作。
- 接口里不能包含初始化块；但抽象类则完全可以包含初始化块。
- 一个类最多只能有一个直接父类，包括抽象类；但一个类可以直接实现多个接口，通过实现多个接口可以弥补Java单继承的不足。

**扩展阅读**

接口和抽象类很像，它们都具有如下共同的特征：

- 接口和抽象类都不能被实例化，它们都位于继承树的顶端，用于被其他类实现和继承。
- 接口和抽象类都可以包含抽象方法，实现接口或继承抽象类的普通子类都必须实现这些抽象方法。



- 接口的方法默认是 public，所有方法在接口中不能有实现(Java 8 开始接口方法可以有默认实现），抽象类可以 有非抽象的方法
- 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是public static final 类型
- 抽象类只能继承一个，接口可以实现多个
- 一个类实现接口的话要实现接口的所有方法，而抽象类不一定
- 接口不能用 new 实例化，但可以声明，但是必须引用一个实现该接口的对象 
- 从设计层面来说，抽象是对类的抽象，是一种模板设计，接口是行为的抽象，是一种行为的规范。

**备注**:在JDK8中，接口也可以定义静态方法，可以直接用接口名调用。实现类和实现是不可以调用的。如果同时实现 两个接口，接口中定义了一样的默认方法，必须重写，不然会报错。

接口的设计目的，是对类的行为进行约束（更准确的说是一种“有”约束，因为接口不能规定类不可以有什么行为），也就是提供一种机制，可以强制要求不同的类具有相同的行为。它只约束了行为的有无，但不对如何实现行为进行限制。

而抽象类的设计目的，是代码的复用。当不同的类具有某些相同的行为（记为行为集合A），且其中一部分行为实现方式一致（A的非真子集，记为B），可以让这些类都派生于一个抽象类。在这个抽象类中是实现了B，避免让所有的子类来实现B，这样就达到了代码复用的目的。而A-B的部分，留给各个子类自己实现。正是因为A-B在这里没有实现，所以抽象类不允许实例化出来。

抽象类是对类本质的抽象，表达的是**is a** 的关系，比如：**BMW is a car**。抽象类包含并实现子类的通用特性，将子类存在差异化的特性进行抽象，交由子类去实现。

而接口是对行为的抽象，表达的是 **like a**的关系。比如：**Bird like a Aircraft**。（都可以飞），但其本质上**is a bird**。接口的核心是定义行为，即实现类可以做什么，至于实现类主体是谁、是如何实现的，接口并不关心。



使用场景：当你关注一个事物的本质的时候，用抽象类；关注行为时，用接口。

抽象类的功能要远超过接口，但是，定义抽象类的代价高。因为高级语言来说每个类只能继承一个类。在这个类中，你必须继承或编写出其所有子类的所有共性。

虽然接口在功能上会弱化许多，但是它只是针对一个动作的描述。而且你可以在一个类中同时实现多个接口。在设计阶段会降低难度。

### 1.36 遇到过异常吗，如何处理？

在Java中，可以按照如下三个步骤处理异常：

1. 捕获异常

   将业务代码包裹在try块内部，当业务代码中发生任何异常时，系统都会为此异常创建一个异常对象。创建异常对象之后，JVM会在try块之后寻找可以处理它的catch块，并将异常对象交给这个catch块处理。

2. 处理异常

   在catch块中处理异常时，应该先记录日志，便于以后追溯这个异常。然后根据异常的类型、结合当前的业务情况，进行相应的处理。比如，给变量赋予一个默认值、直接返回空值、向外抛出一个新的业务异常交给调用者处理，等等。

3. 回收资源

   如果业务代码打开了某个资源，比如数据库连接、网络连接、磁盘文件等，则需要在这段业务代码执行完毕后关闭这项资源。并且，无论是否发生异常，都要尝试关闭这项资源。将关闭资源的代码写在finally块内，可以满足这种需求，即无论是否发生异常，finally块内的代码总会被执行。

### Java中的异常处理

![](D:\Study\自学\笔记\img\Throwable.png)

在 Java 中，所有的异常都有一个共同的祖先java.lang包中的 **Throwable**类。Throwable： 有两个重要的子类： **Exception（异常）** 和 **Error（错误）** ，二者都是 Java 异常处理的重要子类，各自都包含大量子类。 

**Error（错误）:是程序无法处理的错误**，表示运行应用程序中较严重问题。大多数错误与代码编写者执行的操作无关，而表示代码运行时 JVM（Java 虚拟机）出现的问题。例如，Java虚拟机运行错误（Virtual MachineError），当 JVM 不再有继续执行操作所需的内存资源时，将出现OutOfMemoryError这些异常发生时，Java虚拟机（JVM）一般会选择线程终止。

 这些错误表示故障发生于虚拟机自身、或者发生在虚拟机试图执行应用时，如Java虚拟机运行错误（Virtual MachineError）、类定义错误（NoClassDefFoundError）等。这些错误是不可查的，因为它们在应用程序的控制和处理能力之外，而且绝大多数是程序运行时不允许出现的状况。对于设计合理的应用程序来说，即使确实发生了错误，本质上也不应该试图去处理它所引起的异常状况。在 Java中，错误通过Error的子类描述。

**Exception（异常）:是程序本身可以处理的异常。**Exception 类有一个重要的子类 **RuntimeException**。 RuntimeException 异常由Java虚拟机抛出。**NullPointerException**（要访问的变量没有引用任何对象时，抛出该 异常）、**ArithmeticException**（算术运算异常，一个整数除以0时，抛出该异常）和 **ArrayIndexOutOfBoundsException** （下标越界异常）。

#### Throwable类常用方法

- **public string getMessage()**:返回异常发生时的详细信息
- **public string toString()**:返回异常发生时的简要描述
- **public string getLocalizedMessage()**:返回异常对象的本地化信息。使用Throwable的子类覆盖这个方法,可以声称本地化信息。如果子类没有覆盖该方法，则该方法返回的信息与getMessage（）返回的结果相同
- **public void printStackTrace()**:在控制台上打印Throwable对象封装的异常信息



#### 异常处理总结

- try块：用于捕获异常。其后可接零个或多个catch块，如果没有catch块，则必须跟一个finally块。
- catch 块：用于处理try捕获到的异常。
- finally 块：无论是否捕获或处理异常，finally块里的语句都会被执行。当在try块或catch块中遇到return语句时，finally语句块将在方法返回之前被执行。

##### 在以下4种特殊情况下，finally块不会被执行：

1. 在finally语句块中发生了异常。 
2. 在前面的代码中用了System.exit()退出程序。
3. 程序所在的线程死亡。 
4. 关闭CPU。

### 1.40 在finally中return会发生什么？

在通常情况下，不要在finally块中使用return、throw等导致方法终止的语句，一旦在finally块中使用了return、throw语句，将会导致try块、catch块中的return、throw语句失效。

**详细解析**

当Java程序执行try块、catch块时遇到了return或throw语句，这两个语句都会导致该方法立即结束，但是系统执行这两个语句并不会结束该方法，而是去寻找该异常处理流程中是否包含finally块，如果没有finally块，程序立即执行return或throw语句，方法终止；如果有finally块，系统立即开始执行finally块。只有当finally块执行完成后，系统才会再次跳回来执行try块、catch块里的return或throw语句；如果finally块里也使用了return或throw等导致方法终止的语句，finally块已经终止了方法，系统将不会跳回去执行try块、catch块里的任何代码。

### 1.41 说一说你对static关键字的理解

在Java类里只能包含成员变量、方法、构造器、初始化块、内部类（包括接口、枚举）5种成员，而static可以修饰成员变量、方法、初始化块、内部类（包括接口、枚举），以static修饰的成员就是类成员。类成员属于整个类，而不属于单个对象。

对static关键字而言，有一条非常重要的规则：类成员（包括成员变量、方法、初始化块、内部类和内部枚举）不能访问实例成员（包括成员变量、方法、初始化块、内部类和内部枚举）。因为类成员是属于类的，类成员的作用域比实例成员的作用域更大，完全可能出现类成员已经初始化完成，但实例成员还不曾初始化的情况，如果允许类成员访问实例成员将会引起大量错误。

### 1.42 static修饰的类能不能被继承?

static修饰的类可以被继承。

**扩展阅读**

如果使用static来修饰一个内部类，则这个内部类就属于外部类本身，而不属于外部类的某个对象。因此使用static修饰的内部类被称为类内部类，有的地方也称为静态内部类。

static关键字的作用是把类的成员变成类相关，而不是实例相关，即static修饰的成员属于整个类，而不属于单个对象。外部类的上一级程序单元是包，所以不可使用static修饰；而内部类的上一级程序单元是外部类，使用static修饰可以将内部类变成外部类相关，而不是外部类实例相关。因此static关键字不可修饰外部类，但可修饰内部类。

静态内部类需满足如下规则：

1. 静态内部类可以包含静态成员，也可以包含非静态成员；

2. 静态内部类不能访问外部类的实例成员，只能访问它的静态成员；

3. 外部类的所有方法、初始化块都能访问其内部定义的静态内部类；

4. 在外部类的外部，也可以实例化静态内部类，语法如下：

   ```java
   外部类.内部类 变量名 = new 外部类.内部类构造方法();
   ```

#### 1.43 static和final有什么区别？

static关键字可以修饰成员变量、成员方法、初始化块、内部类，被static修饰的成员是类的成员，它属于类、不属于单个对象。以下是static修饰这4种成员时表现出的特征：

- 类变量：被static修饰的成员变量叫类变量（静态变量）。类变量属于类，它随类的信息存储在方法区，并不随对象存储在堆中，类变量可以通过类名来访问，也可以通过对象名来访问，但建议通过类名访问它。
- 类方法：被static修饰的成员方法叫类方法（静态方法）。类方法属于类，可以通过类名访问，也可以通过对象名访问，建议通过类名访问它。
- 静态块：被static修饰的初始化块叫静态初始化块。静态块属于类，它在类加载的时候被隐式调用一次，之后便不会被调用了。
- 静态内部类：被static修饰的内部类叫静态内部类。静态内部类可以包含静态成员，也可以包含非静态成员。静态内部类不能访问外部类的实例成员，只能访问外部类的静态成员。外部类的所有方法、初始化块都能访问其内部定义的静态内部类。

final关键字可以修饰类、方法、变量，以下是final修饰这3种目标时表现出的特征：

- final类：final关键字修饰的类不可以被继承。
- final方法：final关键字修饰的方法不可以被重写。
- final变量：final关键字修饰的变量，一旦获得了初始值，就不可以被修改。

**扩展阅读**

变量分为成员变量、局部变量。

final修饰成员变量：

- 类变量：可以在声明变量时指定初始值，也可以在静态初始化块中指定初始值；
- 实例变量：可以在声明变量时指定初始值，也可以在初始化块或构造方法中指定初始值；

final修饰局部变量：

- 可以在声明变量时指定初始值，也可以在后面的代码中指定初始值。

*注意：被 final 修饰的任何形式的变量，一旦获得了初始值，就不可以被修改！*

### final

1. 修饰成员变量

- 如果final修饰的是类变量，只能在静态初始化中指定初始值或者声明该类变量时指定初始值。

- 如果final修饰的是成员变量（**实例变量和类变量**），可以在非静态初始化块、声明该变量或者构造器中执行初始值。

	- 类变量也叫静态变量，即在变量前加static 的变量；

    实例变量也叫对象变量，即没加static 的变量；

    区别在于：类变量是所有对象共有，其中一个对象将它值改变，其他对象得到的就是改变后的结果；

    而实例变量则为对象私有，某一个对象将其值改变，不影响其他对象；

2. 修饰局部变量

- 系统不会为局部变量进行初始化，局部变量必须由程序员显式初始化。因此使用final修饰局部变量时，即可以在定义时指定默认值（后面的代码不能对变量再赋值），也不可以不指定默认值，而在后面的代码中对final变量赋初值。

```java
public class FinalVar {
	final static int a = 0;//在声明的时候就需要赋值 或 静态代码块赋值
	/**
	static {
		a = 0;
	}
	*/
	
	final int b = 0;//在声明的时候需要赋值 或 代码块中赋值 或 构造器中赋值
	/*
	{
		b = 0;
	}
	*/
	
	public static void main(String[] args) {
		final int localA; //局部变量只声明没有初始化，不会报错，与final无关
		localA = 0;//在使用之前一定要赋值
		//localA = 1; 但是不允许第二次赋值。
	}
}
```

3. 修饰基本类型数据和引用类型数据

- 如果是基本数据类型变量，则其数值一旦在初始化之后便不再改变；
- 如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象。**但是引用的值可以变**。

```java
public class FinalReferenceTest {
    public static void main(String[] args) {
        final int[] iArr = {1,2,3,4};
        iArr[2] = -3;//合法
        iArr = null;//非法，对iArr不能重新赋值
        
        final Person p = new Person(25);
        p.setAge(24);//合法
        p = null;//非法
    }
}
```




### 局部内部类和匿名内部类只能访问局部final变量

```java
public class Test {
    public static void main(String[] args) {
    }
    //局部final变量a,b
    public void test(final int b) {
        final int a = 10;
        //匿名内部类
        new Thread() {
            public void run() {
                System.out.println(a);
                System.out.println(b);
            };
        }.start();
    }
}

class OutClass {
    private int age = 12;

    public void outPrint(final int x) {
        class InClass {
            public void InPrint() {
                System.out.println(x);
                System.out.println(age);
            }
        }
        new InClass().InPrint();
    }
}

```

首先，需要知道一点：内部类和外部类是处于同一个级别，内部类不会因为定义在方法中就会随着方法的执行完毕就被销毁。

这里就会产生一个问题：当外部类的方法结束时，局部变量就会被销毁，但是内部类对象可能还存在（只是没有人再引用它时，才会死亡）。这里就出现了一个矛盾：内部类对象访问了一个不存在的变量。为了解决这个问题，就将局部变量复制了一份作为内部类的成员变量，这样当局部变量死亡后，内部类仍可以访问它，实际访问的是局部变量的“copy”。这样好像延长了局部变量的生命周期。

将局部变量复制为内部类的成员变量时，必须保证这两个变量是一样的，也就是说如果我们在内部类中修改了成员变量，方法中的局部变量也得跟着改变，怎么解决这个问题呢？

就将局部变量设置为final，对它初始化后，我就不让你再去修改这个变量，就保证了内部类的成员变量和方法的局部变量的一致性。这实际也是一种妥协。使得局部变量与内部类建立的拷贝保持一致。

### 1.44 说一说你对泛型的理解

Java集合有个缺点—把一个对象“丢进”集合里之后，集合就会“忘记”这个对象的数据类型，当再次取出该对象时，该对象的编译类型就变成了Object类型（其运行时类型没变）。

Java集合之所以被设计成这样，是因为集合的设计者不知道我们会用集合来保存什么类型的对象，所以他们把集合设计成能保存任何类型的对象，只要求具有很好的通用性。但这样做带来如下两个问题：

- 集合对元素类型没有任何限制，这样可能引发一些问题。例如，想创建一个只能保存Dog对象的集合，但程序也可以轻易地将Cat对象“丢”进去，所以可能引发异常。
- 由于把对象“丢进”集合时，集合丢失了对象的状态信息，只知道它盛装的是Object，因此取出集合元素后通常还需要进行强制类型转换。这种强制类型转换既增加了编程的复杂度，也可能引发ClassCastException异常。

从Java 5开始，Java引入了“参数化类型”的概念，允许程序在创建集合时指定集合元素的类型，Java的参数化类型被称为泛型（Generic）。例如 List<String>，表明该List只能保存字符串类型的对象。

有了泛型以后，程序再也不能“不小心”地把其他对象“丢进”集合中。而且程序更加简洁，集合自动记住所有集合元素的数据类型，从而无须对集合元素进行强制类型转换。

### 1.45 介绍一下泛型擦除

在严格的泛型代码里，带泛型声明的类总应该带着类型参数。但为了与老的Java代码保持一致，也允许在使用带泛型声明的类时不指定实际的类型。如果没有为这个泛型类指定实际的类型，此时被称作raw type（原始类型），默认是声明该泛型形参时指定的第一个上限类型。

当把一个具有泛型信息的对象赋给另一个没有泛型信息的变量时，所有在尖括号之间的类型信息都将被扔掉。比如一个 List<String> 类型被转换为List，则该List对集合元素的类型检查变成了泛型参数的上限（即Object）。

上述规则即为泛型擦除，可以通过下面代码进一步理解泛型擦除：

```java
List<String> list1 = ...; 
List list2 = list1; // list2将元素当做Object处理
```

**扩展阅读**

从逻辑上来看，List<String> 是List的子类，如果直接把一个List对象赋给一个List<String>对象应该引起编译错误，但实际上不会。对泛型而言，可以直接把一个List对象赋给一个 List<String> 对象，编译器仅仅提示“未经检查的转换”。

上述规则叫做泛型转换，可以通过下面代码进一步理解泛型转换：

```java
List list1 = ...; 
List<String> list2 = list1; // 编译时警告“未经检查的转换”
```

### 1.46 List<? super T>和List<? extends T>有什么区别？

- ? 是类型通配符，List<?> 可以表示各种泛型List的父类，意思是元素类型未知的List；
- List<? super T> 用于设定类型通配符的下限，此处 ? 代表一个未知的类型，但它必须是T的父类型；
- List<? extends T> 用于设定类型通配符的上限，此处 ? 代表一个未知的类型，但它必须是T的子类型。

**扩展阅读**

在Java的早期设计中，允许把Integer[]数组赋值给Number[]变量，此时如果试图把一个Double对象保存到该Number[]数组中，编译可以通过，但在运行时抛出ArrayStoreException异常。这显然是一种不安全的设计，因此Java在泛型设计时进行了改进，它不再允许把 List<Integer> 对象赋值给 List<Number> 变量。

数组和泛型有所不同，假设Foo是Bar的一个子类型（子类或者子接口），那么Foo[]依然是Bar[]的子类型，但G<Foo> 不是 G<Bar> 的子类型。Foo[]自动向上转型为Bar[]的方式被称为型变，也就是说，Java的数组支持型变，但Java集合并不支持型变。Java泛型的设计原则是，只要代码在编译时没有出现警告，就不会遇到运行时ClassCastException异常。

### 1.47 说一说你对Java反射机制的理解

Java程序中的对象在运行时可以表现为两种类型，即编译时类型和运行时类型。例如 Person p = new Student(); ，这行代码将会生成一个p变量，该变量的编译时类型为Person，运行时类型为Student。

有时，程序在运行时接收到外部传入的一个对象，该对象的编译时类型是Object，但程序又需要调用该对象的运行时类型的方法。这就要求程序需要在运行时发现对象和类的真实信息，而解决这个问题有以下两种做法：

- 第一种做法是假设在编译时和运行时都完全知道类型的具体信息，在这种情况下，可以先使用instanceof运算符进行判断，再利用强制类型转换将其转换成其运行时类型的变量即可。
- 第二种做法是编译时根本无法预知该对象和类可能属于哪些类，程序只依靠运行时信息来发现该对象和类的真实信息，这就必须使用反射。

具体来说，通过反射机制，我们可以实现如下的操作：

- 程序运行时，可以通过反射获得任意一个类的Class对象，并通过这个对象查看这个类的信息；
- 程序运行时，可以通过反射创建任意一个类的实例，并访问该实例的成员；
- 程序运行时，可以通过反射机制生成一个类的动态代理类或动态代理对象。

### 1.48 Java反射在实际项目中有哪些应用场景？

Java的反射机制在实际项目中应用广泛，常见的应用场景有：

- 使用JDBC时，如果要创建数据库的连接，则需要先通过反射机制加载数据库的驱动程序；
- 多数框架都支持注解/XML配置，从配置中解析出来的类是字符串，需要利用反射机制实例化；
- 面向切面编程（AOP）的实现方案，是在程序运行时创建目标对象的代理类，这必须由反射机制来实现。

### 1.49 说一说Java的四种引用方式

Java对象的四种引用方式分别是强引用、软引用、弱引用、虚引用，具体含义如下：

- 强引用：这是Java程序中最常见的引用方式，即程序创建一个对象，并把这个对象赋给一个引用变量，程序通过该引用变量来操作实际的对象。当一个对象被一个或一个以上的引用变量所引用时，它处于可达状态，不可能被系统垃圾回收机制回收。
- 软引用：当一个对象只有软引用时，它有可能被垃圾回收机制回收。对于只有软引用的对象而言，当系统内存空间足够时，它不会被系统回收，程序也可使用该对象。当系统内存空间不足时，系统可能会回收它。软引用通常用于对内存敏感的程序中。
- 弱引用：弱引用和软引用很像，但弱引用的引用级别更低。对于只有弱引用的对象而言，当系统垃圾回收机制运行时，不管系统内存是否足够，总会回收该对象所占用的内存。当然，并不是说当一个对象只有弱引用时，它就会立即被回收，正如那些失去引用的对象一样，必须等到系统垃圾回收机制运行时才会被回收。
- 虚引用：虚引用完全类似于没有引用。虚引用对对象本身没有太大影响，对象甚至感觉不到虚引用的存在。如果一个对象只有一个虚引用时，那么它和没有引用的效果大致相同。虚引用主要用于跟踪对象被垃圾回收的状态，虚引用不能单独使用，虚引用必须和引用队列联合使用。

## 2. 集合类

### 2.1 Java中有哪些容器（集合类）？

#### List和Set的区别

- List：有序，按对象进入的顺序保存对象，可重复，允许多个Null元素对象，可以使用Iterator取出所有元素，再逐一遍历，还可以使用get（int index）获取指定下表的元素。
- Set：无序，不可重复，最多允许有一个Null元素对象，取元素时只能用Iterator接口取出所有元素，再逐一遍历各个元素。

Java中的集合类主要由Collection和Map这两个接口派生而出，其中Collection接口又派生出三个子接口，分别是Set、List、Queue。所有的Java集合类，都是Set、List、Queue、Map这四个接口的实现类，这四个接口将集合分成了四大类，其中

- Set代表无序的，元素不可重复的集合；
- List代表有序的，元素可以重复的集合；
- Queue代表先进先出（FIFO）的队列；
- Map代表具有映射关系（key-value）的集合。

这些接口拥有众多的实现类，其中最常用的实现类有HashSet、TreeSet、ArrayList、LinkedList、ArrayDeque、HashMap、TreeMap等。

**扩展阅读**

Collection体系的继承树：

![](D:\Study\自学\笔记\img\74C2C3389688C6364FF2DE8AA768A039.jpg)

Map体系的继承树：

![](D:\Study\自学\笔记\img\E26BABF74692B006DA33C112A6FD5EEC.jpg)

*注：紫色框体代表接口，其中加粗的是代表四类集合的接口。蓝色框体代表实现类，其中有阴影的是常用实现类。*

### 2.2 Java中的容器，线程安全和线程不安全的分别有哪些？

java.util包下的集合类大部分都是线程不安全的，例如我们常用的HashSet、TreeSet、ArrayList、LinkedList、ArrayDeque、HashMap、TreeMap，这些都是线程不安全的集合类，但是它们的优点是性能好。如果需要使用线程安全的集合类，则可以使用Collections工具类提供的synchronizedXxx()方法，将这些集合类包装成线程安全的集合类。

java.util包下也有线程安全的集合类，例如Vector、Hashtable。这些集合类都是比较古老的API，虽然实现了线程安全，但是性能很差。所以即便是需要使用线程安全的集合类，也建议将线程不安全的集合类包装成线程安全集合类的方式，而不是直接使用这些古老的API。

从Java5开始，Java在java.util.concurrent包下提供了大量支持高效并发访问的集合类，它们既能包装良好的访问性能，有能包装线程安全。这些集合类可以分为两部分，它们的特征如下：

- 以Concurrent开头的集合类：

  以Concurrent开头的集合类代表了支持并发访问的集合，它们可以支持多个线程并发写入访问，这些写入线程的所有操作都是线程安全的，但读取操作不必锁定。以Concurrent开头的集合类采用了更复杂的算法来保证永远不会锁住整个集合，因此在并发写入时有较好的性能。

- 以CopyOnWrite开头的集合类：

  以CopyOnWrite开头的集合类采用复制底层数组的方式来实现写操作。当线程对此类集合执行读取操作时，线程将会直接读取集合本身，无须加锁与阻塞。当线程对此类集合执行写入操作时，集合会在底层复制一份新的数组，接下来对新的数组执行写入操作。由于对集合的写入操作都是对数组的副本执行操作，因此它是线程安全的。

**扩展阅读**

java.util.concurrent包下线程安全的集合类的体系结构：

![](D:\Study\自学\笔记\img\53AA859E1B3A9CD7709DF9366999B88D.jpg)

### 2.3 Map接口有哪些实现类？

Map接口有很多实现类，其中比较常用的有HashMap、LinkedHashMap、TreeMap、ConcurrentHashMap。

对于不需要排序的场景，优先考虑使用HashMap，因为它是性能最好的Map实现。如果需要保证线程安全，则可以使用ConcurrentHashMap。它的性能好于Hashtable，因为它在put时采用分段锁/CAS的加锁机制，而不是像Hashtable那样，无论是put还是get都做同步处理。

对于需要排序的场景，如果需要按插入顺序排序则可以使用LinkedHashMap，如果需要将key按自然顺序排列甚至是自定义顺序排列，则可以选择TreeMap。如果需要保证线程安全，则可以使用Collections工具类将上述实现类包装成线程安全的Map。

#### 2.4 描述一下Map put的过程

HashMap是最经典的Map实现，下面以它的视角介绍put的过程：

1. 首次扩容：

   先判断数组是否为空，若数组为空则进行第一次扩容（resize）；

2. 计算索引：

   通过hash算法，计算键值对在数组中的索引；

3. 插入数据：

   - 如果当前位置元素为空，则直接插入数据；
   - 如果当前位置元素非空，且key已存在，则直接覆盖其value；
   - 如果当前位置元素非空，且key不存在，则将数据链到链表末端；
   - 若链表长度达到8，则将链表转换成红黑树，并将数据插入树中；

4. 再次扩容

   如果数组中元素个数（size）超过threshold，则再次进行扩容操作。

**扩展阅读**

HashMap添加数据的详细过程，如下图：

![](D:\Study\自学\笔记\img\18330EB2310CB83A25FA317E65ED60EB.png)

### 2.5 如何得到一个线程安全的Map？

1. 使用Collections工具类，将线程不安全的Map包装成线程安全的Map；
2. 使用java.util.concurrent包下的Map，如ConcurrentHashMap；
3. 不建议使用Hashtable，虽然Hashtable是线程安全的，但是性能较差。

### 2.6 HashMap有什么特点？

1. HashMap是线程不安全的实现；
2. HashMap可以使用null作为key或value。

### 2.7 JDK7和JDK8中的HashMap有什么区别？

JDK7中的HashMap，是基于数组+链表来实现的，它的底层维护一个Entry数组。它会根据计算的hashCode将对应的KV键值对存储到该数组中，一旦发生hashCode冲突，那么就会将该KV键值对放到对应的已有元素的后面， 此时便形成了一个链表式的存储结构。

JDK7中HashMap的实现方案有一个明显的缺点，即当Hash冲突严重时，在桶上形成的链表会变得越来越长，这样在查询时的效率就会越来越低，其时间复杂度为O(N)。

JDK8中的HashMap，是基于数组+链表+红黑树来实现的，它的底层维护一个Node数组。当链表的存储的数据个数大于等于8的时候，不再采用链表存储，而采用了红黑树存储结构。这么做主要是在查询的时间复杂度上进行优化，链表为O(N)，而红黑树一直是O(logN)，可以大大的提高查找性能。

### 2.8 介绍一下HashMap底层的实现原理

它基于hash算法，通过put方法和get方法存储和获取对象。

存储对象时，我们将K/V传给put方法时，它调用K的hashCode计算hash从而得到bucket位置，进一步存储，HashMap会根据当前bucket的占用情况自动调整容量(超过Load Facotr则resize为原来的2倍)。获取对象时，我们将K传给get，它调用hashCode计算hash从而得到bucket位置，并进一步调用equals()方法确定键值对。

如果发生碰撞的时候，HashMap通过链表将产生碰撞冲突的元素组织起来。在Java 8中，如果一个bucket中碰撞冲突的元素超过某个限制(默认是8)，则使用红黑树来替换链表，从而提高速度。

### 2.9 介绍一下HashMap的扩容机制

1. 数组的初始容量为16，而容量是以2的次方扩充的，一是为了提高性能使用足够大的数组，二是为了能使用位运算代替取模预算(据说提升了5~8倍)。
2. 数组是否需要扩充是通过负载因子判断的，如果当前元素个数为数组容量的0.75时，就会扩充数组。这个0.75就是默认的负载因子，可由构造器传入。我们也可以设置大于1的负载因子，这样数组就不会扩充，牺牲性能，节省内存。
3. 为了解决碰撞，数组中的元素是单向链表类型。当链表长度到达一个阈值时（7或8），会将链表转换成红黑树提高性能。而当链表长度缩小到另一个阈值时（6），又会将红黑树转换回单向链表提高性能。
4. 对于第三点补充说明，检查链表长度转换成红黑树之前，还会先检测当前数组数组是否到达一个阈值（64），如果没有到达这个容量，会放弃转换，先去扩充数组。所以上面也说了链表长度的阈值是7或8，因为会有一次放弃转换的操作。

**扩展阅读**

例如我们从16扩展为32时，具体的变化如下所示：

![](D:\Study\自学\笔记\img\B7A9F3ADBA028FE6FDE22C94D566B4F1.png)

因此元素在重新计算hash之后，因为n变为2倍，那么n-1的mask范围在高位多1bit(红色)，因此新的index就会发生这样的变化：

![](D:\Study\自学\笔记\img\FB03BC4205AD26DC0210B12412AAC145.png)

因此，我们在扩充HashMap的时候，不需要重新计算hash，只需要看看原来的hash值新增的那个bit是1还是0就好了，是0的话索引没变，是1的话索引变成“原索引+oldCap”。可以看看下图为16扩充为32的resize示意图：

![](D:\Study\自学\笔记\img\C2928A93915A4AEF2709862EBAC8515C.png)

这个设计确实非常的巧妙，既省去了重新计算hash值的时间，而且同时，由于新增的1bit是0还是1可以认为是随机的，因此resize的过程，均匀的把之前的冲突的节点分散到新的bucket了。

### 2.10 HashMap中的循环链表是如何产生的？

在多线程的情况下，当重新调整HashMap大小的时候，就会存在条件竞争，因为如果两个线程都发现HashMap需要重新调整大小了，它们会同时试着调整大小。在调整大小的过程中，存储在链表中的元素的次序会反过来，因为移动到新的bucket位置的时候，HashMap并不会将元素放在链表的尾部，而是放在头部，这是为了避免尾部遍历。如果条件竞争发生了，那么就会产生死循环了。

### 2.11 HashMap为什么用红黑树而不用B树？

**参考答案**

B/B+树多用于外存上时，B/B+也被成为一个磁盘友好的数据结构。

HashMap本来是数组+链表的形式，链表由于其查找慢的特点，所以需要被查找效率更高的树结构来替换。如果用B/B+树的话，在数据量不是很多的情况下，数据都会“挤在”一个结点里面，这个时候遍历效率就退化成了链表。

### 2.12 HashMap为什么线程不安全？

**参考答案**

HashMap在并发执行put操作时，可能会导致形成循环链表，从而引起死循环。

### 2.13 HashMap如何实现线程安全？

**参考答案**

1. 直接使用Hashtable类；
2. 直接使用ConcurrentHashMap；
3. 使用Collections将HashMap包装成线程安全的Map。

### 2.14 HashMap是如何解决哈希冲突的？

为了解决碰撞，数组中的元素是单向链表类型。当链表长度到达一个阈值时，会将链表转换成红黑树提高性能。而当链表长度缩小到另一个阈值时，又会将红黑树转换回单向链表提高性能。

### 2.15 说一说HashMap和HashTable的区别

**参考答案**

1. Hashtable是一个线程安全的Map实现，但HashMap是线程不安全的实现，所以HashMap比Hashtable的性能高一点。
2. Hashtable不允许使用null作为key和value，如果试图把null值放进Hashtable中，将会引发空指针异常，但HashMap可以使用null作为key或value。

**扩展阅读**

从Hashtable的类名上就可以看出它是一个古老的类，它的命名甚至没有遵守Java的命名规范：每个单词的首字母都应该大写。也许当初开发Hashtable的工程师也没有注意到这一点，后来大量Java程序中使用了Hashtable类，所以这个类名也就不能改为HashTable了，否则将导致大量程序需要改写。

与Vector类似的是，尽量少用Hashtable实现类，即使需要创建线程安全的Map实现类，也无须使用Hashtable实现类，可以通过Collections工具类把HashMap变成线程安全的Map。

### 2.16 HashMap与ConcurrentHashMap有什么区别？

HashMap是非线程安全的，这意味着不应该在多线程中对这些Map进行修改操作，否则会产生数据不一致的问题，甚至还会因为并发插入元素而导致链表成环，这样在查找时就会发生死循环，影响到整个应用程序。

Collections工具类可以将一个Map转换成线程安全的实现，其实也就是通过一个包装类，然后把所有功能都委托给传入的Map，而包装类是基于synchronized关键字来保证线程安全的（Hashtable也是基于synchronized关键字），底层使用的是互斥锁，性能与吞吐量比较低。

ConcurrentHashMap的实现细节远没有这么简单，因此性能也要高上许多。它没有使用一个全局锁来锁住自己，而是采用了减少锁粒度的方法，尽量减少因为竞争锁而导致的阻塞与冲突，而且ConcurrentHashMap的检索操作是不需要锁的。

### 2.17 介绍一下ConcurrentHashMap是怎么实现的？

JDK 1.7中的实现：

在 jdk 1.7 中，ConcurrentHashMap 是由 Segment 数据结构和 HashEntry 数组结构构成，采取分段锁来保证安全性。Segment 是 ReentrantLock 重入锁，在 ConcurrentHashMap 中扮演锁的角色，HashEntry 则用于存储键值对数据。一个 ConcurrentHashMap 里包含一个 Segment 数组，一个 Segment 里包含一个 HashEntry 数组，Segment 的结构和 HashMap 类似，是一个数组和链表结构。

![](D:\Study\自学\笔记\img\A064CF0DD49D1B3694548913C28728DB.png)

JDK 1.8中的实现：

JDK1.8 的实现已经摒弃了 Segment 的概念，而是直接用 Node 数组+链表+红黑树的数据结构来实现，并发控制使用 Synchronized 和 CAS 来操作，整个看起来就像是优化过且线程安全的 HashMap，虽然在 JDK1.8 中还能看到 Segment 的数据结构，但是已经简化了属性，只是为了兼容旧版本。

![](D:\Study\自学\笔记\img\9C8ABF1CD3475339A49DE3B9E1696FE7.png)

### 2.18 ConcurrentHashMap是怎么分段分组的？

get操作：

Segment的get操作实现非常简单和高效，先经过一次再散列，然后使用这个散列值通过散列运算定位到 Segment，再通过散列算法定位到元素。get操作的高效之处在于整个get过程都不需要加锁，除非读到空的值才会加锁重读。原因就是将使用的共享变量定义成 volatile 类型。

put操作：

当执行put操作时，会经历两个步骤：

1. 判断是否需要扩容；
2. 定位到添加元素的位置，将其放入 HashEntry 数组中。

插入过程会进行第一次 key 的 hash 来定位 Segment 的位置，如果该 Segment 还没有初始化，即通过 CAS 操作进行赋值，然后进行第二次 hash 操作，找到相应的 HashEntry 的位置，这里会利用继承过来的锁的特性，在将数据插入指定的 HashEntry 位置时（尾插法），会通过继承 ReentrantLock 的 tryLock() 方法尝试去获取锁，如果获取成功就直接插入相应的位置，如果已经有线程获取该Segment的锁，那当前线程会以自旋的方式去继续的调用 tryLock() 方法去获取锁，超过指定次数就挂起，等待唤醒。

### 2.19 说一说你对LinkedHashMap的理解

LinkedHashMap使用双向链表来维护key-value对的顺序（其实只需要考虑key的顺序），该链表负责维护Map的迭代顺序，迭代顺序与key-value对的插入顺序保持一致。

LinkedHashMap可以避免对HashMap、Hashtable里的key-value对进行排序（只要插入key-value对时保持顺序即可），同时又可避免使用TreeMap所增加的成本。

LinkedHashMap需要维护元素的插入顺序，因此性能略低于HashMap的性能。但因为它以链表来维护内部顺序，所以在迭代访问Map里的全部元素时将有较好的性能。

### 2.20 请介绍LinkedHashMap的底层原理

**参考答案**

LinkedHashMap继承于HashMap，它在HashMap的基础上，通过维护一条双向链表，解决了HashMap不能随时保持遍历顺序和插入顺序一致的问题。在实现上，LinkedHashMap很多方法直接继承自HashMap，仅为维护双向链表重写了部分方法。

如下图，淡蓝色的箭头表示前驱引用，红色箭头表示后继引用。每当有新的键值对节点插入时，新节点最终会接在tail引用指向的节点后面。而tail引用则会移动到新的节点上，这样一个双向链表就建立起来了。





# 获取用键盘输入常用的的两种方法

**方法1：通过 Scanner**

```java
Scanner input = new Scanner(System.in);
String s = input.nextLine();
input.close();
```

**方法2：通过 BufferedReader**

```java
BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
String s = input.readLine();
```



# 2.2 Java 集合框架

## 2.2.1 Arraylist 与 LinkedList 异同

**1. 是否保证线程安全：** ArrayList 和 LinkedList 都是不同步的，也就是不保证线程安全；

**2. 底层数据结构：** Arraylist 底层使用的是Object数组；

LinkedList 底层使用的是双向链表数据结构（JDK1.6之 前为循环链表，JDK1.7取消了循环。注意双向链表和双向循环链表的区别：）； 

**3. 插入和删除是否受元素位置的影响： ① ArrayList 采用数组存储，所以插入和删除元素的时间复杂度受元素位置的影响。**比如：执行 add(E e) 方法的时候， ArrayList 会默认在将指定的元素追加到此列表的末尾，这种情况时间复杂度就是O(1)。但是如果要在指定位置 i 插入和删除元素的话（ add(int index, E element) ）时间复杂度就为 O(n-i)。因为在进行上述操作的时候集合中第 i 和第 i 个元素之后的(n-i)个元素都要执行向后位/向前移一位的操作。

**② LinkedList 采用链表存储，所以插入，删除元素时间复杂度不受元素位置的影响，都是近似 O（1）而数组为近似 O（n）。**

**4. 是否支持快速随机访问：** LinkedList 不支持高效的随机元素访问，而 ArrayList 支持。快速随机访问就是通过元素的序号快速获取元素对象(对应于 get(int index) 方法)。

**5.内存空间占用：** ArrayList的空间浪费主要体现在在list列表的结尾会预留一定的容量空间，

而LinkedList的空间花费则体现在它的每一个元素都需要消耗比ArrayList更多的空间（因为要存放直接后继和直接前驱以及数据）。



**补充内容：RandomAccess接口**

```java
public interface RandomAccess{
}
```

查看源码我们发现实际上 RandomAccess 接口中什么都没有定义。所以，在我看来 RandomAccess 接口不过是一个 标识罢了。标识什么？ 标识实现这个接口的类具有随机访问功能。

在binarySearch（）方法中，它要判断传入的list 是否RamdomAccess的实例，如果是，调用 indexedBinarySearch（）方法，如果不是，那么调用iteratorBinarySearch（）方法

```java
public static <T>
int binarySearch(List<? extends Comparable<? super T>> list, T key) {
	if (list instanceof RandomAccess || list.size()<BINARYSEARCH_THRESHOLD)
		return Collections.indexedBinarySearch(list, key);
	else
		return Collections.iteratorBinarySearch(list, key);
}

```

ArrayList 实现了 RandomAccess 接口， 而 LinkedList 没有实现。为什么呢？我觉得还是和底层数据结构有关！ ArrayList 底层是数组，而 LinkedList 底层是链表。数组天然支持随机访问，时间复杂度为 O（1），所以称为快速随机访问。链表需要遍历到特定位置才能访问特定位置的元素，时间复杂度为 O（n），所以不支持快速随机访问。 ArrayList 实现了 RandomAccess 接口，就表明了他具有快速随机访问功能。 RandomAccess 接口只是标识，并不 是说 ArrayList 实现 RandomAccess 接口才具有快速随机访问功能的！



**下面再总结一下 list 的遍历方式选择：**

- 实现了RandomAccess接口的list，优先选择普通for循环 ，其次foreach,
- 未实现RandomAccess接口的list， 优先选择iterator遍历（foreach遍历底层也是通过iterator实现的），大 size的数据，千万不要使用普通for循环

## 2.2.2 ArrayList 与 Vector 区别

**线程安全**：**当多个线程访问某个方法时，不管你通过怎样的调用方式或者说这些线程如何交替的执行，我们在主程序中不需要去做任何的同步，这个类的结果行为都是我们设想的正确行为，那么我们就可以说这个类时线程安全的。**

**Vector类**的所有方法都是**同步**的。可以由两个线程安全地访问一个Vector对象、但是一个线程访问Vector的话代码要在同步操作上耗费大量的时间。

**Arraylist不是同步**的，所以在不需要保证线程安全时时建议使用Arraylist。

## 2.2.3 HashMap的底层实现

### JDK1.8之前

JDK1.8 之前 HashMap 底层是 **数组和链表** 结合在一起使用也就是 **链表散列**。**HashMap 通过 key 的 hashCode 经过扰动函数处理过后得到 hash 值，然后通过 (n - 1) & hash 判断当前元素存放的位置（这里的 n 指的是数组的长度），如果当前位置存在元素的话，就判断该元素与要存入的元素的 hash 值以及 key 是否相同，如果相同的话，直接覆盖，不相同就通过拉链法解决冲突。**

**所谓扰动函数指的就是 HashMap 的 hash 方法。使用 hash 方法也就是扰动函数是为了防止一些实现比较差的 hashCode() 方法 换句话说使用扰动函数之后可以减少碰撞。**

**JDK 1.8 HashMap 的 hash 方法源码:**

JDK 1.8 的 hash方法 相比于 JDK 1.7 hash 方法更加简化，但是原理不变。

```java
static final int hash(Object key) {
	int h;
	// key.hashCode()：返回散列值也就是hashcode
	// ^ ：按位异或
	// >>>:无符号右移，忽略符号位，空位都以0补齐
	return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}

```

## 2.2.4 HashSet 和 HashMap 区别

如果你看过 HashSet 源码的话就应该知道：HashSet 底层就是基于 HashMap 实现的。（HashSet 的源码非常非常 少，因为除了 clone() 方法、writeObject()方法、readObject()方法是 HashSet 自己不得不实现之外，其他方法都是 直接调用 HashMap 中的方法。）

| HashMap                                                | HashSet                                                      |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| 实现Map接口                                            | 实现Set                                                      |
| 存储键值对                                             | 仅存储对象                                                   |
| 调用put()向map中添加元素                               | 调用add()方法向Set中添加元素                                 |
| HashMap使用键（key）计算HashCode                       | HashSet使用成员对象来计算hashcode值，对于两个对象来说hashcode可能相同，所以equals（）方法用来判断对象的相等性，如果两个对象不同的话，那么返回false |
| HashMap相对于HashSet较快，因为它是使用唯一的键获取对象 | HashSet较HashMap来说比较慢                                   |

## 2.2.5 ConcurrentHashMap 和 Hashtable 的区别

ConcurrentHashMap 和 Hashtable 的区别主要体现在实现**线程安全**的方式上不同。

- 底层数据结构： JDK1.7的 ConcurrentHashMap 底层采用 **分段的数组+链表** 实现，JDK1.8 采用的数据结构跟 HashMap1.8的结构一样，**数组+链表/红黑二叉树**。

  Hashtable 和 JDK1.8 之前的 HashMap 的底层数据结构类似都是采用 **数组+链表** 的形式，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的；

- 实现线程安全的方式（重要）： ① 在JDK1.7的时候，**ConcurrentHashMap（分段锁）** 对整个桶数组进行了分割**分段(Segment)**，每一把锁只锁容器其中一部分数据，多线程访问容器里不同数据段的数据，就不会存在锁竞争，提高并发访问率。 到了 JDK1.8 的时候已经摒弃了Segment的概念，而是直接用 **Node数组+链表+红黑树**的数据结构来实现，并发控制使用 **synchronized 和 CAS** 来操作。（JDK1.6以后 对 synchronized锁做了很多优化） 整个看起来就像是优化过且线程安全的 HashMap，虽然在JDK1.8中还能看到 Segment 的数据结构， 但是已经简化了属性，只是为了兼容旧版本；

  ② Hashtable(同一把锁) :使用 **synchronized** 来保证线程安全， 效率非常低下。当一个线程访问同步方法时，其他线程也访问同步方法，可能会进入阻塞或轮询状态，如使用 put 添加元素，另一个线程不能使用 put 添加元素，也不能使用 get，竞争会越来越激烈效率越低。

可参考：http://www.cnblogs.com/chengxiao/p/6842045.html

## 2.2.6 HashMap 和 Hashtable 的区别

1. 线程是否安全： HashMap 是非线程安全的，HashTable 是**线程安全**的；HashTable 内部的方法基本都经过 synchronized 修饰。（如果你要保证线程安全的话就使用 ConcurrentHashMap 吧！）；
2. 效率： 因为线程安全的问题，HashMap 要比 HashTable 效率高一点。另外，HashTable 基本被淘汰，不要在 代码中使用它；
3. 对Null key 和Null value的支持： HashMap 中，null 可以作为键，这样的键只有一个，可以有一个或多个键 所对应的值为 null。。但是在 **HashTable** 中 put 进的键值只要有一个 null，直接抛出 **NullPointerException**。
4. 初始容量大小和每次扩充容量大小的不同 ： ①创建时如果不指定容量初始值，**Hashtable** 默认的初始大小为**11**，之后每次扩充，容量变为原来的**2n+1**。**HashMap**默认的初始化大小为**16**。之后每次扩充，容量变为原来的**2倍**。②创建时如果给定了容量初始值，那么 Hashtable 会直接使用你给定的大小，而 HashMap会将其扩充为**2的幂次方大小**（HashMap 中的 tableSizeFor() 方法保证，下面给出了源代码）。也就是说 HashMap 总是使用2的幂作为哈希表的大小,后面会介绍到为什么是2的幂次方。
5. 底层数据结构： JDK1.8 以后的 HashMap 在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）时，将链表转化为**红黑树**，以减少搜索时间。Hashtable 没有这样的机制。

## 2.2.7 集合框架底层数据结构总结

### Collection

#### 1. List

- **Arraylist： **Object数组
- **Vector： **Object数组 
- **LinkedList： **双向链表(JDK1.6之前为循环链表，JDK1.7取消了循环)

#### 2. Set

- **HashSet（无序，唯一）: **基于 HashMap 实现的，底层采用 HashMap 来保存元素
- **LinkedHashSet:**LinkedHashSet 继承于 HashSet，并且其内部是通过 LinkedHashMap 来实现的。有点类似于我们之前说的LinkedHashMap 其内部是基于 Hashmap 实现一样，不过还是有一点点区别的。
- **TreeSet（有序，唯一）:**红黑树(自平衡的排序二叉树。

### Map

- **HashMap:**JDK1.8之前HashMap由数组+链表组成的，数组是HashMap的主体，链表则是主要为了解决哈希 冲突而存在的（“拉链法”解决冲突）.JDK1.8以后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默 认为8）时，将链表转化为红黑树，以减少搜索时间
- **LinkedHashMap: **LinkedHashMap 继承自 HashMap，所以它的底层仍然是基于拉链式散列结构即由数组和 链表或红黑树组成。另外，LinkedHashMap 在上面结构的基础上，增加了一条双向链表，使得上面的结构可以 保持键值对的插入顺序。同时通过对链表进行相应的操作，实现了访问顺序相关逻辑。
- **HashTable: **数组+链表组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的
- **TreeMap: **红黑树（自平衡的排序二叉树）

# 2.3 Java多线程

关于 Java多线程，在面试的时候，问的比较多的就是①悲观锁和乐观锁（ 具体可以看我的这篇文章：面试必备之乐观锁与悲观锁）、②synchronized和lock区别以及volatile和synchronized的区别，③可重入锁与非可重入锁的区别、④多线程是解决什么问题的、⑤线程池解决什么问题、⑥线程池的原理、⑦线程池使用时的注意事项、⑧AQS原理、⑨ReentranLock源码，设计原理，整体过程 等等问题.





# 2022/3/16

## CSS

1. 为什么需要CSS
2. CSS的分类：标签样式表、类样式表、ID样式表、组合样式
3. CSS从位置上的分类：嵌入式样式表、内部样式表、外部样式表

```html
<html>
    
    <head>
        <meta charset="utf-8">
        <style type="text/css">
            /*被style标签包围的范围是CSS环境，可以写CSS代码*/
            <!--内部样式表-->
            /*标签样式表*/
            p{
                color:red;
            }
            
            /*类样式*/
            .f20{
                font_size:20px;
            }
            
            /*ID样式*/
            #p4{
                background-color:pink;
                font-size:24px;
                font-weight:bolder;
                font-style:italic;
                font-family:"华文彩云";
            }
            
            /*组合样式*/
            div p{
                color:blue;
            }
            
            div .f32{
                font-size:32px;
                font-family:"黑体";
            }
        </style>
        <!--引用外部样式表-->
        <link rel="stylesheet" href="css/demo01.css">
    </head>
    <body>
        <!--
        <p>
            <font color="red">这里是段落一</font>
        </p>
        <p>
            <font color="red">这里是段落二</font>
        </p>
		-->
       	<p>这里是段落一</p> 
        <p>这里是段落二</p>
        <p class="f20">这里是段落三</p>
        <p id="p4">这里是段落四</p><!--id属性在整个HTML文档中，尽量保持唯一（虽然重复也不会报错）-->
        
        <div>
            <!--嵌入式样式表-->
            <p><span style="font-size:60px;font-weight:bolder;color:yellow;">Hello</span></p>
            <span class="f32">World</span>
            <p class="f32">!!!</p>
        </div>
        
        
    </body>
</html>
```

4. CSS盒子模型

- border
- margin
- padding

```html
<html>   
   	<head>
       <meta charset="utf-8">
        <style type="text/css">
            #div1{
                width:400px;
                height:400px;
                background-color:greencolor;
                
                /*border边框样式*/
             /*  	border-width:1px;	/*边框粗细*/
              /*  border-style:solid;	/*边框样式*/
             /*   border-color:blue;	/*边框颜色*/
              	border:4px double blue;  
                
                border-top:4px dotted blue;
                
            }
            
            #div2{
                width:200px;
                height:200px;
                background-color:darkorange;
                
                margin-top:100px;
                margin-left:100px;
                
                /*margin:100px; 一个值:四个方向一致；两个值:上下、左右；三个值:上、左右、下；四个值：上、右、下、左；*/
                
                /*padding : 填充*/
                
               	padding-top:50px;
                padding-left:50px;
            }
            
             #div3{
                width:100px;
                height:100px;
                background-color:aquamarine;
 
            }
            
            body{
                padding:0;
                margin:0;
            }
        </style>
    </head>
   	<body>
        <div id="div1">
            <div id="div2">
                <div id="div3">&nbsp;</div>
            </div>
        </div>
    </body>
</html>
```

5. CSS布局

position：absolute --绝对定位，需配合left，right

​					relative --相对定位，float，margin，padding一起使用

```html
<html>   
   	<head>
       <meta charset="utf-8">
        <style type="text/css">
            body{
                marging:0;
                padding:0;
            }
            #div1{
                width:200px;
                height:50px;
                background-color:greenyellow;
                
                /*绝对定位*/
                position:absolute;
                left:100px;
                top:100px;
            }
            
            #div2{
                width:200px;
                height:50px;
                background-color:pink;
                
                /*相对定位*/
                position:relative;
                float:left;
                margin-left:20px;
            }  
            
            #div3{
                height:50px;
                background-color:darkorange;
            }
            
           #div4{
                width:200px;
                height:50px;
                background-color:aqua;
               
               	float:left;
            }
            
           #div5{
                width:200px;
                height:50px;
                background-color:olivedrab;
               
               	float:left;
            }
                
            div{
                position:relative;
            }
        </style>
    </head>
   	<body>
        <!--
		<div id="div1">&nbsp;</div>
        <div id="div2">&nbsp;</div>
		-->
		<div id="div3">
          	<div id="div4">&nbsp;</div>
			<div id="div5">&nbsp;</div>

        </div>
		
    </body>
</html>
```

# 2022/3/20

| 标签名                                                       | 功能                   |
| ------------------------------------------------------------ | ---------------------- |
| h1~h6                                                        | 1级标题~6级标题        |
| p                                                            | 段落                   |
| [a](https://heavy_code_industry.gitee.io/code_heavy_industry/pro001-javaweb/note/note001-HTML-a.html) | 超链接                 |
| ul/li                                                        | 无序列表               |
| [img](https://heavy_code_industry.gitee.io/code_heavy_industry/pro001-javaweb/note/note001-HTML-img.html) | 图片                   |
| div                                                          | 定义一个前后有换行的块 |
| span                                                         | 定义一个前后无换行的块 |
| table                                                        | 定义整个表格           |
| tr                                                           | 定义表格的行           |
| [td](https://heavy_code_industry.gitee.io/code_heavy_industry/pro001-javaweb/note/note001-HTML-td.html) | 定义表格行中的单元格   |
| th                                                           | 定义表格行中的表头     |
| [form](https://heavy_code_industry.gitee.io/code_heavy_industry/pro001-javaweb/note/note001-HTML-form.html) | 定义整个表单           |
| [input](https://heavy_code_industry.gitee.io/code_heavy_industry/pro001-javaweb/note/note001-HTML-input.html) | 定义具体表单项         |
| [button](https://heavy_code_industry.gitee.io/code_heavy_industry/pro001-javaweb/note/note001-HTML-button.html) | 定义按钮               |
| [select](https://heavy_code_industry.gitee.io/code_heavy_industry/pro001-javaweb/note/note001-HTML-select.html) | 定义整个下拉列表       |
| [option](https://heavy_code_industry.gitee.io/code_heavy_industry/pro001-javaweb/note/note001-HTML-option.html) | 定义下拉列表中的列表项 |
| [textarea](https://heavy_code_industry.gitee.io/code_heavy_industry/pro001-javaweb/note/note001-HTML-textarea.html) | 定义多行文本框         |

| 符号本身 | 实体的转义符号 |
| -------- | -------------- |
| <        | &lt;           |
| >        | &gt;           |
| 空格     | &nbsp;         |

# AOP术语

- 连接点

类里面哪些方法可以被增强，这些方法称为连接点

- 切入点

实际被真正增强的方法，称为切入点

- 通知（增强）

1. 实际增强的逻辑部分称为通知（增强）
2. 通知有多种类型
  - 前置通知
  - 后置通知
  - 环绕通知
  - 异常通知
  - 最终通知

- 切面

是动作，把通知应用到切入点过程

- 切入点表达式

语法结构： execution([权限修饰符] [返回类型] [类全路径] [方法名称] ([参数列表]) )





# 2022/4/15

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 1, 2, 3, 5, 8 };
        System.out.println(Arrays.toString(ns));
    }
}

int[] ns = { 1, 1, 2, 3, 5, 8 };
for (int n : ns) {
    System.out.print(n + ", ");
}
```

```java
//冒泡排序
import java.util.Arrays;

public class Main {
	public static void main(String[] args) {
		int[] ns = {28,12, 89, 73, 65, 18, 96, 50, 8, 36};
        //排序前：
        System.out.println("排序前："+Arrays.toString(ns));
        for (int i = 0; i < ns.length - 1;i++) {
			for(int j = 0; j < ns.length - i -1; j++) {
				if(ns[j] > ns[j+1]) {
					int temp = ns[j];
					ns[j] = ns[j+1];
					ns[j+1] = temp;
				}
			}
			
		}
		System.out.println("排序后："+Arrays.toString(ns));

	}
}

import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] ns = { 28, 12, 89, 73, 65, 18, 96, 50, 8, 36 };
        Arrays.sort(ns);
        System.out.println(Arrays.toString(ns));
    }
}
```

![](D:\Study\自学\笔记\img\alg-sort-fast-1.jpg)

快速排序的时间复杂度在最坏情况下是O(N2)，平均的时间复杂度是O(N*lgN)。

快速排序是不稳定的算法，它不满足稳定算法的定义。



```java
//快排
import java.util.Arrays;

public class QuickSort {
    public static void main(String[] args) {

        int a[] = {30,40,60,10,20,50};
        System.out.println("排序前："+Arrays.toString(a));

        QuickSort(a,0,a.length-1);
        System.out.println("排序后："+Arrays.toString(a));

    }

    static void QuickSort(int[] a, int low, int high) {
        if(low < high) {
            int pivotpos = Partition(a,low,high);
            QuickSort(a,low,pivotpos-1);
            QuickSort(a,pivotpos+1,high);
        }
    }

    static int Partition(int[] a, int low, int high) {
        int pivot=a[low];
        while (low < high) {
            while(low<high&&a[high]>=pivot) --high;
            a[low] = a[high];
            while(low < high && a[low]<=pivot) ++low;
            a[high]= a[low];
        }

        a[low] = pivot;
        return low;
    }

}


```

## 可变参数

```Java
class Group {
    private String[] names;

    public void setNames(String... names) {
        this.names = names;
    }
}

//调用方法时可写
Group g = new Group();
g.setNames("Xiao Ming", "Xiao Hong", "Xiao Jun"); // 传入3个String
g.setNames("Xiao Ming", "Xiao Hong"); // 传入2个String
g.setNames("Xiao Ming"); // 传入1个String
g.setNames(); // 传入0个String


//可变参数可以写成String[]类型
class Group {
    private String[] names;

    public void setNames(String[] names) {
        this.names = names;
    }
}
//调用方需要自己先构造String[]，比较麻烦。例如：
Group g = new Group();
g.setNames(new String[] {"Xiao Ming", "Xiao Hong", "Xiao Jun"}); // 传入1个String[]
```

结论：引用类型参数的传递，调用方的变量，和接收方的参数变量，指向的是同一个对象。双方任意一方对这个对象的修改，都会影响对方（因为指向同一个对象嘛）。

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Person(String name) {
        this(name, 18); // 调用另一个构造方法Person(String, int)
    }

    public Person() {
        this("Unnamed"); // 调用另一个构造方法Person(String)
    }
}
```

这种把一个子类类型安全地变为父类类型的赋值，被称为向上转型（upcasting）。

向上转型实际上是把一个子类型安全地变为更加抽象的父类型：

```java
Student s = new Student();
Person p = s; // upcasting, ok
Object o1 = p; // upcasting, ok
Object o2 = s; // upcasting, ok
```

```java
Person p = new Student();
if (p instanceof Student) {
    // 只有判断成功才会向下转型:
    Student s = (Student) p; // 一定会成功
}
```

因此，继承是is关系，组合是has关系



## 继承

注意：方法名相同，方法参数相同，但方法返回值不同，也是不同的方法。在Java程序中，出现这种情况，编译器会报错。

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Student();
        p.run(); // 应该打印Student.run
    }
}

class Person {
    public void run() {
        System.out.println("Person.run");
    }
}

class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student.run");
    }
}
```





## 抽象类

```java
class Person {
    public abstract void run();
}
```

把一个方法声明为`abstract`，表示它是一个抽象方法，本身没有实现任何方法语句。因为这个抽象方法本身是无法执行的，所以，`Person`类也无法被实例化。编译器会告诉我们，无法编译`Person`类，因为它包含抽象方法。

必须把`Person`类本身也声明为`abstract`，才能正确编译它：

```java
abstract class Person {
    public abstract void run();
}
```

抽象方法实际上相当于定义了“规范”。

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Student();
        p.run();
    }
}

abstract class Person {
    public abstract void run();
}

class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student.run");
    }
}

```

## 接口

|            | abstract class       | interface                   |
| :--------- | :------------------- | --------------------------- |
| 继承       | 只能extends一个class | 可以implements多个interface |
| 字段       | 可以定义实例字段     | 不能定义实例字段            |
| 抽象方法   | 可以定义抽象方法     | 可以定义抽象方法            |
| 非抽象方法 | 可以定义非抽象方法   | 可以定义default方法         |

```ascii
┌───────────────┐
│   Iterable    │
└───────────────┘
        ▲                ┌───────────────────┐
        │                │      Object       │
┌───────────────┐        └───────────────────┘
│  Collection   │                  ▲
└───────────────┘                  │
        ▲     ▲          ┌───────────────────┐
        │     └──────────│AbstractCollection │
┌───────────────┐        └───────────────────┘
│     List      │                  ▲
└───────────────┘                  │
              ▲          ┌───────────────────┐
              └──────────│   AbstractList    │
                         └───────────────────┘
                                ▲     ▲
                                │     │
                                │     │
                     ┌────────────┐ ┌────────────┐
                     │ ArrayList  │ │ LinkedList │
                     └────────────┘ └────────────┘
```

```java
List list = new ArrayList(); // 用List接口引用具体子类的实例
Collection coll = list; // 向上转型为Collection接口
Iterable it = coll; // 向上转型为Iterable接口
```

## 静态字段和静态方法

实例字段在每个实例中都有自己的一个独立“空间”，但是静态字段只有一个共享“空间”，所有实例都会共享该字段。

```java
Person.number = 99;
System.out.println(Person.number); // 推荐类名访问静态字段
```

不推荐用`实例变量.静态字段`去访问静态字段，因为在Java程序中，实例对象并没有静态字段。在代码中，实例对象能访问静态字段只是因为编译器可以根据实例类型自动转换为`类名.静态字段`来访问静态对象。

静态方法类似其它编程语言的函数。

```java
public class Main {
    public static void main(String[] args) {
        Person.setNumber(99);
        System.out.println(Person.number);
    }
}

class Person {
    public static int number;

    public static void setNumber(int value) {
        number = value;
    }
}
```

因为静态方法属于`class`而不属于实例，因此，静态方法内部，无法访问`this`变量，也无法访问实例字段，它只能访问静态字段。

通过实例变量也可以调用静态方法，但这只是编译器自动帮我们把实例改写成类名而已。

通常情况下，通过实例变量访问静态字段和静态方法，会得到一个编译警告。

静态方法经常用于工具类。例如：

- Arrays.sort()
- Math.random()

静态方法也经常用于辅助方法。注意到Java程序的入口`main()`也是静态方法。

因为`interface`是一个纯抽象类，所以它不能定义实例字段。但是，`interface`是可以有静态字段的，并且静态字段必须为`final`类型：

```java
public interface Person {
    public static final int MALE = 1;
    public static final int FEMALE = 2;
}
```

- 静态字段属于所有实例“共享”的字段，实际上是属于`class`的字段；
- 调用静态方法不需要实例，无法访问`this`，但可以访问静态字段和其他静态方法；
- 静态方法常用于工具类和辅助方法。

## 包

`import static`的语法，它可以导入可以导入一个类的静态字段和静态方法：

```java
package main;

// 导入System类的所有静态字段和静态方法:
import static java.lang.System.*;

public class Main {
    public static void main(String[] args) {
        // 相当于调用System.out.println(…)
        out.println("Hello, world!");
    }
}
```

`final`修饰符不是访问权限，它可以修饰`class`、`field`和`method`；

## 内部类

```java
public class Main {
    public static void main(String[] args) {
        Outer outer = new Outer("Nested"); // 实例化一个Outer
        Outer.Inner inner = outer.new Inner(); // 实例化一个Inner
        inner.hello();
    }
}

class Outer {
    private String name;

    Outer(String name) {
        this.name = name;
    }

    class Inner {
        void hello() {
            System.out.println("Hello, " + Outer.this.name);
        }
    }
}

```

Inner Class和普通Class相比，除了能引用Outer实例外，还有一个额外的“特权”，就是可以修改Outer Class的`private`字段，因为Inner Class的作用域在Outer Class内部，所以能访问Outer Class的`private`字段和方法。

观察`asyncHello()`方法，我们在方法内部实例化了一个`Runnable`。`Runnable`本身是接口，接口是不能实例化的，所以这里实际上是定义了一个实现了`Runnable`接口的匿名类，并且通过`new`实例化该匿名类，然后转型为`Runnable`。在定义匿名类的时候就必须实例化它，定义匿名类的写法如下：

```java
Runnable r = new Runnable() {
    // 实现必要的抽象方法...
};
```

## idea快捷键

Ctrl + H

同理，如果你想查看接口 `BeanDefinition` 继承的接口 `AttributeAccessor` 被哪些类实现的话，只需要把鼠标移动到 `AttributeAccessor` 类名上，然后使用快捷键 `Ctrl + H` 即可。

Ctrl + N
快速检索类



# 2022/4/18

## 枚举类

为了让编译器能自动检查某个值在枚举的集合内，并且，不同用途的枚举需要不同的类型来标记，不能混用，我们可以使用`enum`来定义枚举类：

```java
//enum
public class Main {
    public static void main(String[] args) {
        Weekday day = Weekday.SUN;
        if (day == Weekday.SAT || day == Weekday.SUN) {
            System.out.println("Work at home!");
        } else {
            System.out.println("Work at office!");
        }
    }
}

enum Weekday {
    SUN, MON, TUE, WED, THU, FRI, SAT;
}
```

优点：首先，`enum`常量本身带有类型信息，即`Weekday.SUN`类型是`Weekday`，编译器会自动检查出类型错误。例如，下面的语句不可能编译通过：

```java
int day = 1;
if (day == Weekday.SUN) { // Compile error: bad operand types for binary operator '=='
}
```

其次，不可能引用到非枚举的值，因为无法通过编译。

最后，不同类型的枚举不能互相比较或者赋值，因为类型不符。例如，不能给一个`Weekday`枚举类型的变量赋值为`Color`枚举类型的值：

```java
Weekday x = Weekday.SUN; // ok!
Weekday y = Color.RED; // Compile error: incompatible types
```

### enum的比较

使用`enum`定义的枚举类是一种引用类型。前面我们讲到，引用类型比较，要使用`equals()`方法，如果使用`==`比较，它比较的是两个引用类型的变量是否是同一个对象。因此，引用类型比较，要始终使用`equals()`方法，但`enum`类型可以例外。

这是因为`enum`类型的每个常量在JVM中只有一个唯一实例，所以可以直接用`==`比较：

```java
if (day == Weekday.FRI) { // ok!
}
if (day.equals(Weekday.SUN)) { // ok, but more code!
}
```

### enum类型

通过`enum`定义的枚举类，和其他的`class`有什么区别？

答案是没有任何区别。`enum`定义的类型就是`class`，只不过它有以下几个特点：

- 定义的`enum`类型总是继承自`java.lang.Enum`，且无法被继承；
- 只能定义出`enum`的实例，而无法通过`new`操作符创建`enum`的实例；
- 定义的每个实例都是引用类型的唯一实例；
- 可以将`enum`类型用于`switch`语句。

```java
//name() 返回常量名
String s = Weekday.SUN.name(); // "SUN"

//ordinal() 返回定义的常量的顺序，从0开始计数
int n = Weekday.MON.ordinal(); // 1

```

要编写健壮的代码，就不要依靠`ordinal()`的返回值。因为`enum`本身是`class`，所以我们可以定义`private`的构造方法，并且，给每个枚举常量添加字段：

```java
//这样就无需担心顺序的变化，新增枚举常量时，也需要指定一个int值。
public class Main {
    public static void main(String[] args) {
        Weekday day = Weekday.SUN;
        if (day.dayValue == 6 || day.dayValue == 0) {
            System.out.println("Work at home!");
        } else {
            System.out.println("Work at office!");
        }
    }
}

enum Weekday {
    MON(1), TUE(2), WED(3), THU(4), FRI(5), SAT(6), SUN(0);

    public final int dayValue;

    private Weekday(int dayValue) {
        this.dayValue = dayValue;
    }
}

```

```java
//覆写toString()的目的是在输出时更有可读性。
//注意：判断枚举常量的名字，要始终使用name()方法，绝不能调用toString()！
public class Main {
    public static void main(String[] args) {
        Weekday day = Weekday.SUN;
        if (day.dayValue == 6 || day.dayValue == 0) {
            System.out.println("Today is " + day + ". Work at home!");
        } else {
            System.out.println("Today is " + day + ". Work at office!");
        }
    }
}

enum Weekday {
    MON(1, "星期一"), TUE(2, "星期二"), WED(3, "星期三"), THU(4, "星期四"), FRI(5, "星期五"), SAT(6, "星期六"), SUN(0, "星期日");

    public final int dayValue;
    private final String chinese;

    private Weekday(int dayValue, String chinese) {
        this.dayValue = dayValue;
        this.chinese = chinese;
    }

    @Override
    public String toString() {
        return this.chinese;
    }
}
```

```java
//switch
public class Main {
    public static void main(String[] args) {
        Weekday day = Weekday.SUN;
        switch(day) {
        case MON:
        case TUE:
        case WED:
        case THU:
        case FRI:
            System.out.println("Today is " + day + ". Work at office!");
            break;
        case SAT:
        case SUN:
            System.out.println("Today is " + day + ". Work at home!");
            break;
        default:
            throw new RuntimeException("cannot process " + day);
        }
    }
}

enum Weekday {
    MON, TUE, WED, THU, FRI, SAT, SUN;
}

```

### 小结

Java使用`enum`定义枚举类型，它被编译器编译为`final class Xxx extends Enum { … }`；

通过`name()`获取常量定义的字符串，注意不要使用`toString()`；

通过`ordinal()`返回常量定义的顺序（无实质意义）；

可以为`enum`编写构造方法、字段和方法

`enum`的构造方法要声明为`private`，字段强烈建议声明为`final`；

`enum`适合用在`switch`语句中。

## 记录类

```java
public class Main {
    public static void main(String[] args) {
        Point p = new Point(123, 456);
        System.out.println(p.x()); //123
        System.out.println(p.y()); //456
        System.out.println(p);     //Point[x=123, y=456]
    }
}

public record Point(int x, int y) {}
```

相当于

```java
public final class Point extends Record {
    private final int x;
    private final int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int x() {
        return this.x;
    }

    public int y() {
        return this.y;
    }

    public String toString() {
        return String.format("Point[x=%s, y=%s]", x, y);
    }

    public boolean equals(Object o) {
        ...
    }
    public int hashCode() {
        ...
    }
}
```

除了用`final`修饰class以及每个字段外，编译器还自动为我们创建了构造方法，和字段名同名的方法，以及覆写`toString()`、`equals()`和`hashCode()`方法。

换句话说，使用`record`关键字，可以一行写出一个不变类。

和`enum`类似，我们自己不能直接从`Record`派生，只能通过`record`关键字由编译器实现继承。

### 构造方法

编译器默认按照`record`声明的变量顺序自动创建一个构造方法，并在方法内给字段赋值。那么问题来了，如果我们要检查参数，应该怎么办？

假设`Point`类的`x`、`y`不允许负数，我们就得给`Point`的构造方法加上检查逻辑：

```java
public record Point(int x, int y) {
    public Point {
        if (x < 0 || y < 0) {
            throw new IllegalArgumentException();
        }
    }
}
```

注意到方法`public Point {...}`被称为Compact Constructor，它的目的是让我们编写检查逻辑，编译器最终生成的构造方法如下：

```java
public final class Point extends Record {
    public Point(int x, int y) {
        // 这是我们编写的Compact Constructor:
        if (x < 0 || y < 0) {
            throw new IllegalArgumentException();
        }
        // 这是编译器继续生成的赋值代码:
        this.x = x;
        this.y = y;
    }
    ...
}
```

作为`record`的`Point`仍然可以添加静态方法。一种常用的静态方法是`of()`方法，用来创建`Point`：

```java
public record Point(int x, int y) {
    public static Point of() {
        return new Point(0, 0);
    }
    public static Point of(int x, int y) {
        return new Point(x, y);
    }
}
```

这样我们可以写出更简洁的代码：

```java
var z = Point.of();
var p = Point.of(123, 456);
```

### 小结

从Java 14开始，提供新的`record`关键字，可以非常方便地定义Data Class：

- 使用`record`定义的是不变类；
- 可以编写Compact Constructor对参数进行验证；
- 可以定义静态方法。

## BigInteger

```java
BigInteger i1 = new BigInteger("1234567890");
BigInteger i2 = new BigInteger("12345678901234567890");
BigInteger sum = i1.add(i2); // 12345678902469135780
```
`BigInteger`转换成`long`型：

```java
BigInteger i = new BigInteger("123456789000");
System.out.println(i.longValue()); // 123456789000
System.out.println(i.multiply(i).longValueExact()); // java.lang.ArithmeticException: BigInteger out of long range
```

`BigInteger`和`Integer`、`Long`一样，也是不可变类，并且也继承自`Number`类。因为`Number`定义了转换为基本类型的几个方法：

- 转换为`byte`：`byteValue()`
- 转换为`short`：`shortValue()`
- 转换为`int`：`intValue()`
- 转换为`long`：`longValue()`
- 转换为`float`：`floatValue()`
- 转换为`double`：`doubleValue()`

因此，通过上述方法，可以把`BigInteger`转换成基本类型。如果`BigInteger`表示的范围超过了基本类型的范围，转换时将丢失高位信息，即结果不一定是准确的。如果需要准确地转换成基本类型，可以使用`intValueExact()`、`longValueExact()`等方法，在转换时如果超出范围，将直接抛出`ArithmeticException`异常。

```java
//BigInteger to float
import java.math.BigInteger;
public class Main {
    public static void main(String[] args) {
        BigInteger n = new BigInteger("999999").pow(99);
        float f = n.floatValue();
        System.out.println(f); //Infinity
    }
}
```

### 小结

`BigInteger`用于表示任意大小的整数；

`BigInteger`是不变类，并且继承自`Number`；

将`BigInteger`转换成基本类型时可使用`longValueExact()`等方法保证结果准确。

## BigDecimal

和`BigInteger`类似，`BigDecimal`可以表示一个任意大小且精度完全准确的浮点数。

```java
BigDecimal bd = new BigDecimal("123.4567");
System.out.println(bd.multiply(bd)); // 15241.55677489
```

```java
//BigDecimal用scale()表示小数位数，例如：
BigDecimal d1 = new BigDecimal("123.45");
BigDecimal d2 = new BigDecimal("123.4500");
BigDecimal d3 = new BigDecimal("1234500");
System.out.println(d1.scale()); // 2,两位小数
System.out.println(d2.scale()); // 4
System.out.println(d3.scale()); // 0
```

通过`BigDecimal`的`stripTrailingZeros()`方法，可以将一个`BigDecimal`格式化为一个相等的，但去掉了末尾0的`BigDecimal`：

```java
BigDecimal d1 = new BigDecimal("123.4500");
BigDecimal d2 = d1.stripTrailingZeros();
System.out.println(d1.scale()); // 4
System.out.println(d2.scale()); // 2,因为去掉了00

BigDecimal d3 = new BigDecimal("1234500");
BigDecimal d4 = d3.stripTrailingZeros();
System.out.println(d3.scale()); // 0
System.out.println(d4.scale()); // -2
```

如果一个`BigDecimal`的`scale()`返回负数，例如，`-2`，表示这个数是个整数，并且末尾有2个0。

可以对一个`BigDecimal`设置它的`scale`，如果精度比原始值低，那么按照指定的方法进行四舍五入或者直接截断：

```java
import java.math.BigDecimal;
import java.math.RoundingMode;
public class Main {
    public static void main(String[] args) {
        BigDecimal d1 = new BigDecimal("123.456789");
        BigDecimal d2 = d1.setScale(4, RoundingMode.HALF_UP); // 四舍五入，123.4568
        BigDecimal d3 = d1.setScale(4, RoundingMode.DOWN); // 直接截断，123.4567
        System.out.println(d2);
        System.out.println(d3);
    }
}
```

对`BigDecimal`做加、减、乘时，精度不会丢失，但是做除法时，存在无法除尽的情况，这时，就必须指定精度以及如何进行截断：

```java
BigDecimal d1 = new BigDecimal("123.456");
BigDecimal d2 = new BigDecimal("23.456789");
BigDecimal d3 = d1.divide(d2, 10, RoundingMode.HALF_UP); // 保留10位小数并四舍五入
BigDecimal d4 = d1.divide(d2); // 报错：ArithmeticException，因为除不尽
```

还可以对`BigDecimal`做除法的同时求余数：

```java
import java.math.BigDecimal;
public class Main {
    public static void main(String[] args) {
        BigDecimal n = new BigDecimal("12.345");
        BigDecimal m = new BigDecimal("0.12");
        BigDecimal[] dr = n.divideAndRemainder(m);
        System.out.println(dr[0]); // 102
        System.out.println(dr[1]); // 0.105
    }
}
```

调用`divideAndRemainder()`方法时，返回的数组包含两个`BigDecimal`，分别是商和余数，其中商总是整数，余数不会大于除数。我们可以利用这个方法判断两个`BigDecimal`是否是整数倍数：

```java
BigDecimal n = new BigDecimal("12.75");
BigDecimal m = new BigDecimal("0.15");
BigDecimal[] dr = n.divideAndRemainder(m);
if (dr[1].signum() == 0) {
    // n是m的整数倍
}
```

### 比较BigDecimal

```java
BigDecimal d1 = new BigDecimal("123.456");
BigDecimal d2 = new BigDecimal("123.45600");
System.out.println(d1.equals(d2)); // false,因为scale不同
System.out.println(d1.equals(d2.stripTrailingZeros())); // true,因为d2去除尾部0后scale变为2
System.out.println(d1.compareTo(d2)); // 0
```

必须使用`compareTo()`方法来比较，它根据两个值的大小分别返回负数、正数和`0`，分别表示小于、大于和等于。

>  *总是使用compareTo()比较两个BigDecimal的值，不要使用equals()！*

```java
//BigDecimal的源码
public class BigDecimal extends Number implements Comparable<BigDecimal> {
    private final BigInteger intVal;
    private final int scale;
}
```

实际上一个`BigDecimal`是通过一个`BigInteger`和一个`scale`来表示的，即`BigInteger`表示一个完整的整数，而`scale`表示小数位数：

### 小结

`BigDecimal`用于表示精确的小数，常用于财务计算；

比较`BigDecimal`的值是否相等，必须使用`compareTo()`而不能使用`equals()`。

## 常用工具类

### Math

```java
//绝对值
Math.abs(-100); // 100
//取最大最小
Math.max(100, 99); // 100
Math.min(1.2, 2.3); // 1.2
```

计算x<sup>y</sup>次方

```java
Math.pow(2, 10); // 2的10次方=1024
```

计算√x：

```java
Math.sqrt(2); // 1.414...
```

计算e<sup>x</sup>次方：

```java
Math.exp(2); // 7.389...
```

计算以e为底的对数：

```java
Math.log(4); // 1.386...
```

计算以10为底的对数：

```java
Math.log10(100); // 2
```

三角函数：

```java
Math.sin(3.14); // 0.00159...
Math.cos(3.14); // -0.9999...
Math.tan(3.14); // -0.0015...
Math.asin(1.0); // 1.57079...
Math.acos(1.0); // 0.0
```

Math还提供了几个数学常量：

```java
double pi = Math.PI; // 3.14159...
double e = Math.E; // 2.7182818...
Math.sin(Math.PI / 6); // sin(π/6) = 0.5
```

生成一个随机数x，x的范围是`0 <= x < 1`：

```java
Math.random();
```

```java
// 区间在[MIN, MAX)的随机数
public class Main {
    public static void main(String[] args) {
        double x = Math.random(); // x的范围是[0,1)
        double min = 10;
        double max = 50;
        double y = x * (max - min) + min; // y的范围是[10,50)
        long n = (long) y; // n的范围是[10,50)的整数
        System.out.println(y);
        System.out.println(n);
    }
}
```

```java
Random r = new Random();
r.nextInt(); // 2071575453,每次都不一样
r.nextInt(10); // 5,生成一个[0,10)之间的int
r.nextLong(); // 8811649292570369305,每次都不一样
r.nextFloat(); // 0.54335...生成一个[0,1)之间的float
r.nextDouble(); // 0.3716...生成一个[0,1)之间的double
```

这是因为我们创建`Random`实例时，如果不给定种子，就使用系统当前时间戳作为种子，因此每次运行时，种子不同，得到的伪随机数序列就不同。

如果我们在创建`Random`实例时指定一个种子，就会得到完全确定的随机数序列：

```java
//伪随机
import java.util.Random;
public class Main {
    public static void main(String[] args) {
        Random r = new Random(12345);
        for (int i = 0; i < 10; i++) {
            System.out.println(r.nextInt(100));
        }
/*51
80
41
28
55
84
75
2
1
89*/
    }
}
```

前面我们使用的`Math.random()`实际上内部调用了`Random`类，所以它也是伪随机数，只是我们无法指定种子。

### SecureRandom

```java
//真随机
SecureRandom sr = new SecureRandom();
System.out.println(sr.nextInt(100));
```

`SecureRandom`无法指定种子，它使用RNG（random number generator）算法。JDK的`SecureRandom`实际上有多种不同的底层实现，有的使用安全随机种子加上伪随机数算法来产生安全的随机数，有的使用真正的随机数生成器。实际使用的时候，可以优先获取高强度的安全随机数生成器，如果没有提供，再使用普通等级的安全随机数生成器：

```java
import java.util.Arrays;
import java.security.SecureRandom;
import java.security.NoSuchAlgorithmException;

public class Main {
    public static void main(String[] args) {
        SecureRandom sr = null;
        try {
            sr = SecureRandom.getInstanceStrong(); // 获取高强度安全随机数生成器
        } catch (NoSuchAlgorithmException e) {
            sr = new SecureRandom(); // 获取普通的安全随机数生成器
        }
        byte[] buffer = new byte[16];
        sr.nextBytes(buffer); // 用安全随机数填充buffer
        System.out.println(Arrays.toString(buffer));
    }
}
```

`SecureRandom`的安全性是通过操作系统提供的安全的随机种子来生成随机数。这个种子是通过CPU的热噪声、读写磁盘的字节、网络流量等各种随机事件产生的“熵”。

### 小结

Java提供的常用工具类有：

- Math：数学计算
- Random：生成伪随机数
- SecureRandom：生成安全的随机数

# 2022/4/24



### Comparable与Comparator的区别

`Comparable & Comparator`都是用来实现集合中元素的比较、排序的，

只是 Comparable 是在集合内部定义的方法实现的排序，

`Comparator` 是在集合外部实现的排序，所以，如想实现排序，就需要在集合外定义`Comparator`接口的方法或在集合内实现 `Comparable`接口的方法，`Comparator`位于包java.util下，而`Comparable`位于包java.lang下。

Java中有两种方式来提供比较功能。第一种是实现java.lang.Comparable接口，使你的类天生具有比较的能力，此接口很简单，只有一个`compareTo`一个方法。此方法接收另一个Object为参数，如果当前对象小于参数则返回负值，如果相等则返回零，否则返回正值，也就是：
 **x.compareTo(y) 来“比较x和y的大小”。若返回“负数”，意味着“x比y小”；返回“零”，意味着“x等于y”；返回“正数”，意味着“x大于y”。**

使用Comparable比较的例子：

```java
class Person implements Comparable<Person>{
    @Override
     public int compareTo(Person person) {
          return name.compareTo(person.name);
          //return this.name - person.name;
     }
}
ArrayList<Person> list = new ArrayList<Person>();
// 添加对象到ArrayList中
list.add(new Person("aaa", 10));
list.add(new Person("bbb", 20));
list.add(new Person("ccc", 30));
list.add(new Person("ddd", 40));
Collections.sort(list); //这里会自动调用Person中重写的compareTo方法。
```

使用Comparator比较的例子：

```java
public class ComparatorDemo {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
                new Person("Joe", 24),
                new Person("Pete", 18),
                new Person("Chris", 21)
        );
        Collections.sort(people, new LexicographicComparator());
        System.out.println(people);
        //[{name=Chris, age=21}, {name=Joe, age=24}, {name=Pete, age=18}]
        Collections.sort(people, new Comparator<Person>() {
            @Override
            public int compare(Person a, Person b) {
                // TODO Auto-generated method stub
                 return a.age < b.age ? -1 : a.age == b.age ? 0 : 1;
            }
        });
        System.out.println(people);
        //[{name=Pete, age=18}, {name=Chris, age=21}, {name=Joe, age=24}]
    }
}

class LexicographicComparator implements Comparator<Person> {
    @Override
    public int compare(Person a, Person b) {
        return a.name.compareToIgnoreCase(b.name);
    }
}

class Person {
    String name;
    int age;
    Person(String n, int a) {
        name = n;
        age = a;
    }
    @Override
    public String toString() {
        return String.format("{name=%s, age=%d}", name, age);
    }
}
```

可以通过两种方式去实现自定义排序：
 第一种:
 定义一个类去实现`Comparator`接口，重写其中的`compare`方法。
 第二种：
 其实只是语法不同，在内部就`new`这个接口并重写里面的`compare`方法。
