# Java基础

## Java历史

1、诞生于SUN（Stanford University Network）
2、Java之父：詹姆斯.高斯林
3、2009年SUN被Oracle甲骨文公司收购
4、于1996年发布JDK1.0正式版
比较有有代表性的几个版本：JDK1.2（引入了集合框架等）、JDK1.4（引入了NIO）、JDK1.5（枚举、泛型、可变参数、foreach循环、自动装箱拆箱。。。）、JDK1.7（switch对字符串的支持，try...with...resource）、JDK1.8（接口、日期时间API、Optional类、Lambda表达式和StreamAPI）

## Java的特点

### 1、面向对象

- 类与对象，类的成员
- 三个基本特征：封装、继承、多态
- 高级特性
- 相关关键字

### 2、健壮性

- 内存自动分配，有垃圾回收机制自动进行回收

### 3、跨平台

- Write Once ,Run Anywhere.
- 原理：使用JVM，不同的操作系统使用不同的JVM，而Java程序编译成字节码，运行JVM上

## 环境搭建

### 1、JDK、JRE、JVM

- JDK：Java Development Kit，Java的开发工具集，包含JRE + 开发工具（javac.exe，java.exe，javadoc.exe，jar.exe）
- JRE：Java Runtime Enviroment，Java运行环境，包括JVM + 核心类库
- JVM：Java Virtual Machine，Java的虚拟机

### 2、环境变量的配置

- path：windows操作系统寻找命令工具的路径，在path中进行登记

	- D:\ProgramFiles\Java\jdk1.8.0_141\bin;

- JAVA_HOME + path

	- JAVA_HOME

		- D:\ProgramFiles\Java\jdk1.8.0_141

	- path

		- %JAVA_HOME%\bin;

	- 这两个变量要么同时在用户级环境变量，要么都在系统级环境变量

## 第一个Java应用程序

### 1、Java程序编写的步骤

- （1）编辑，编写源代码，保存成“.java”结尾的源文件

	- 源文件的构成

		- 类{
	方法{
		语句;
	}
}

- （2）编译：把源文件编译成1个或多个的字节码文件

	- 编译的工具：javac.exe
	- 编译的格式：

		- javac  源文件名.java

			- 源文件名.java后缀名必须写
			- 源文件名不区分大小写

		- javac  -encoding  字符编码  源文件名.java

- （3）运行：运行字节码文件

	- 运行工具：java.exer
	- 格式：

		- java  类名

			- 类名，不带后缀名
			- 类名是严格区分大小写

### 2、Java程序的入口

- 主方法
- public static void main(String[] args){
}

### 3、输出语句

- System.out.print(xxx);

	- 如果原样输出的字符串，那么就加""
	- 其他的变量或数值就不用加""

- System.out.println(xxx);

### 4、相关的问题

- （1）主方法一定要在public的类中？

	- 不是
	- 绝大部分都在public的类中

- （2）一个源文件只能写一个class

	- 不是

- （3）类名与源文件名是否必须一致

	- 不是
	- 但是当这个类是public时，那么就必须一致

- （4）一个源文件只能有一个public修饰的类

## DOS命令

### （1）列出当前目录的内容

- dir

### （2）切换盘符

- 盘符:

### （3）进入到某个目录

- cd  目录的路径
- cd  ..

	- 回到上一级

- cd /

	- 回到根目录

- cd .

	- 还是在当前目录

### （4）创建目录

- md  新目录

	- 只能创建一级

### （5）删除目录

- rd 目录

	- 只能删除空目录

### （6）删除文件

- del 文件名.扩展名

	- 删除一个文件

- del 目录

	- 删除目录中的所有文件

## 进制（了解）

### 二进制

- 只有0和1
- 二进制转十进制

	- 从最右边开始依次是2的0次

### 十进制

- 0-9
- 转二进制

	- 整数部分

		- 除2取余，倒取

	- 小数部分

		- 乘2取整，顺

### 八进制

- 0-7
- 通过二进制

	- 三个二进制值代表一个八进制值
	- 从右边开始

### 十六进制

- 0-9，A~F大小写都可以
- 通过二进制

	- 四个二进制值代表一个八进制值
	- 从右边开始

# Java基础语法

## 1、标识符

### 凡是在程序中需要自己命名的地方都是标识符，例如：变量名、包名、类名等

### 标识符的命名规则

- 1、Java的标识符只能使用26英文字母大小写，0-9的数字，下划线(_)和美元符号($)
- 2、标识符中不能包含空格
- 3、数字不能开头
- 4、不能使用关键字和保留字和特殊值

  - 50个

    - class
    - 基本数据类型

      - byte,short,int,long,float,double,char,boolean

    - public
    - static
    - void

  - 3个

    - true
    - false
    - null

- 5、Java严格区分大小写
- 6、Java标识符没有长度限制，但是不宜太长

### 标识符的命名规范

- 总原则

  - 见名知意，有意义

- 1、类名，接口名

  - 所有单词的首字母大写

    - XxxYyyZzz
    - 例如：String，System，HelloWorld

- 2、变量名

  - 第一个单词首字母小写，其余单词首字母大写

    - xxxYyyZzz
    - 例如：age，maxValue

- 3、包名

  - 所有字母都小写，单词之间使用.分割

    - xxx.yyy.zzz
    - 例如：java.lang

- 4、常量名

  - 所有字母都大写，单词之间使用下划线_

    - XXX_YYY_ZZZ	
    - 例如：MAX_VALUE

## 2、变量

### 变量是代表内存的一块存储区域

### 变量三要素

- 变量名

  - 给这块存储区域命名，就不用内存地址访问

- 变量值

  - 这块内存中存的数据

- 数据类型

  - 决定这块内存的大小

### 使用要求

- 1、先声明后使用

  - 声明格式

    - 数据类型  变量名;

- 2、在使用之前必须赋值
  - 赋值格式

    - 变量名 = 值;

      - 这个值可以是常量值，表达式

- 3、变量的作用域

  - 从声明处开始，到它所属的}结束
  - 同一个作用域不能同名

## 3、数据类型

### 基本数据类型

- 整型

  - byte

    - 占1个字节
    - 存储范围是 -128~127

  - short

    - 占2个字节

  - int

    - 占4个字节
    - 默认类型

  - long

    - 占8个字节
    - 需要在数字后面加L或小写l

- 浮点型

  - float

    - 占4个字节
    - 需要在数字后面加F或f

  - double

    - 占8个字节
    - 默认类型

- 字符型

  - char

    - 占2个字节
    - 存储的是字符的Unicode编码值
    - 三种方式

      - '一个字符'
      - '转义字符'

        - 退格  \b

        - 回车   \r

        - 换行  \n

        - \\\
        - \\'
        - \\"
        - Tab键  \t

      - '\u字符的Unicode编码值的十六进制形式'

- 布尔型

  - boolean  只能赋值为true或false

- 基本数据类型的转换

  - 1、自动类型转换
    - byte,short,char -->int ->long -->float -->double

      - （1）byte,short,char只要算术运算都要升级为int或以上

        - 例如：byte + byte升级为int
        - 例如：byte + double 升级为double
        - 例如：byte + short升级int

      - （2）boolean不参与
      - （3）和字符串拼接的结果都是String字符串

  - 2、强制类型转换

    - double-->float-->long-->int-->byte,short,char

      - （1）例如： char  c = (char)97;

        - 相当于把'a'字符赋值给c

    - 需要强制类型转换符(类型)
    - 有可能溢出或损失精度，需谨慎

### 引用数据类型

- 类

  - 例如：String，System

- 接口
- 数组

## 4、运算符

### 算术运算符

- 正号	+

- 负号 	-

    - 例如：int a = -5;  int b = -a;

- 加法	+

- 减法	-

- 乘法	*

- 除法	/
    - 注意：

      - 当整数与整数相除，结果只保留整数部分
      - 当整数与整数相除，被除数/除数 ，除数不能为0，报异常
      - 当浮点数相除，如果除数为0，结果是无穷大，非数字

- 取模，求余数	%
    - 特殊
      - 会忽略模数的负号

- 自增	++
    - 对于自增变量来说，一定会自增1
    - 但是对于表达式的结果，看++在前或在后

      - i++
        - 这个表达式的结果是与i自增前的结果一样
		- 例如：int i=0;int j = i++;	j=0,i=1

      - ++i
        - 这个表达式的结果是与i自增后的结果一样
          - 例如：int i=0;int j = ++i;		j=1,i=1

- 自减
  	- 同自增

### 赋值运算符

- 基本赋值运算符	=	把右边的结果赋值给左边的变量

- 扩展赋值运算符	+=, -=,.....

    - 隐含强制类型转换	例如：short s = 1;  s += 1; 	等价于 s = (short)(s+1);

### 比较运算符

- 大于	>

- 小于	 <

- 大于等于	>=

- 小于等于	<=

- 等于	==

- 不等于	!=

- 结果一定是boolean值，所以比较表达式常常用于条件表达式

### 逻辑运算符

- 逻辑与	&

    - 只有左右两边的值都为true，结果才为true

      - true  & true = true
      - true & false = false
      - false & true = false
      - false & false = false

- 逻辑或

  - |

    - 只要左右两边的值有一个为true，结果就为true

      - true  | true = true
      - true | false = true
      - false | true = true
      - false | false = false

- 逻辑异或

  - ^

    - 只有左右两边一个为true,另一个为false，结果才为true

      - true  ^ true = false
      - true ^ false = true
      - false ^ true = true
      - false ^ false = false

- 逻辑非

  - !

    - !true 即为false
    - !false即为true

- 短路与

  - &&

    - 结果与&一样

      - 只有左右两边的值都为true，结果才为true

        - true  & true = true
        - true & false = false
        - false & true = false
        - false & false = false

    - 不同的是

      - 如果左边的表达式为false，右边的表达式就不计算了，出现短路现象

- 短路或

  - ||

    - 结果与|一样

      - 只要左右两边的值有一个为true，结果就为true

        - true  | true = true
        - true | false = true
        - false | true = true
        - false | false = false

    - 不同的是

      - 如果左边的表达式为true，右边的表达式就不计算了，出现短路现象

### 条件运算符

- 格式

  - 条件表达式 ?  表达式1 ： 表达式2
  - 整个表达式的结果看条件表达式，如果条件表达式为true，那么就取表达式1的结果，否则取表达式2的结果

### 位运算符

- 左移

  - <<

    - 相当于乘以2的几次

      - 例如：1 << 3

        - 相当于 1 * 2的3次方

    - 右边补0
- 右移

  - 相当于除以2的几次
    
    - 例如：16 >> 3
    
      - 相当于 16 / 2的3次方
    
  - 左边补什么，看最高位，最高位是1，就补1，是0就补0
- 无符号右移
  - ">>>"
  - 不管最高位是什么，左边都补0
  - 结果一定是正数
- 按位与

  - &

    - 运算规则，对应位

      - 1 & 1 = 1
      - 1&0 = 0
      - 0&1 = 0
      - 0&0=0
- 按位或

  - |

    - 运算规则，对应位

      - 1 | 1 = 1
      - 1|0 = 1
      - 0|1 = 1
      - 0|0=0
- 按位异或

  - ^

    - 运算规则，对应位

      - 1^ 1 = 0
      - 1^0 = 1
      - 0^1 = 1
      - 0^|0=0
- 按位取反

  - ~

    - 运算规则，对应位，原来是1，变成0，原来是0，变成1
- 所有都是直接用二进制计算（补码）

# 流程控制语句结构

## 顺序结构

### 同一个方法中，从上往下，顺序执行

## 分支结构

### 条件判断

- 1、单分支条件判断		语法

    - if(条件表达式){
      当条件表达式为true时，要执行的语句块
      }

    - （1）如果条件成立，就执行语句块，如果条件不成立，就不执行语句块
    - （2）{}可以省略，默认只带一句，建议不要省略

- 2、双分支条件判断		语法

    - if(条件表达式){
      当条件表达式为true时，要执行的语句块1
      }else{
      当条件表达式为false时，要执行的语句块2
      }

    - （1）如果条件成立，就执行语句块1，如果条件不成立，就执行语句块2
    - （2）{}可以省略，默认只带一句，建议不要省略
    - （3）else不可以单独存在的，必须有if配对

- 3、多分支条件判断		语法

    - if(条件表达式1){
      当条件表达式1为true时，要执行的语句块1
      }else if(条件表达式2){
      当条件表达式2为true时，要执行的语句块2
      }else if(条件表达式3){
      当条件表达式3为true时，要执行的语句块3
      }
      .....
      else{
      当以上所有条件表达式都不成立时，要执行的语句块n+1
      }

    - （1）如果条件表达式1成立，执行语句块1，如果条件表达式1不成立才会去判断条件表达2，如果条件表达式2成立，那么执行语句块2，如果条件表达式2不成立，才会去看条件表达式3，依次类推。只有一个分支会被执行
    - （2）{}可以省略，默认只带一句，建议不要省略
    - （3）else不可以单独存在的，必须有if配对
    - （4）多个条件表达式的范围
      - 互斥，没有交集
        ```java
         //两个条件没有交集
        //顺序可以互换
        if(age>=0 && age<18){
              System.out.println("未成年");
              }else if(age >=18 && age<60){
              System.out.println("成年");
              }
        ```

      - 包含
        ```java
         //顺序不可以调整
         //范围小的在上面，范围大的在下面
        if(age<18){
              System.out.println("未成年");
              }else if(age<60){
              System.out.println("成年");
              }
        ```
        

- 4、嵌套

  - 在任意一个语句块中，都还可以嵌套任意一种分支结构
  - 当外部的条件成立的情况下，才会进行内部的条件判断

    ```java
    if(条件表达式1){
    	if(条件表达式2){
    		当条件表达式1成立，并且条件表达式2也成立时执行
    	}else if(条件表达式3){
    		当条件表达式1成立，并且条件表达式2不成立，条件表达式3成立时执行
    	}else{
    		当条件表达式1成立，并且条件表达式2不成立，条件表达式3不成立时执行
    	}
    }else{
    	if(条件表达式4){
    		当条件表达式1不成立，条件表达式4成立，执行
    	}else if(条件表达式5){
    		当条件表达式1不成立，条件表达式4不成立，条件表达式5成立，执行
    	}else{
    		当条件表达式1不成立，条件表达式4不成立，条件表达式5也不成立，执行
    }
    }
    ```
### 选择结构

- 语法结构

  ```java
  switch(表达式){
  	case 常量值:
  		语句块;
  		break;
  	case 常量值:
  		语句块;
  		break;
  	....
  	default:
  		语句块;
  		break;
  }
  ```

- 表达式类型要求

  - 基本数据类型：byte，short，char，int
  - 引用数据类型：枚举（JDK1.5之后），String（JDK1.7之后）

- 执行过程

  - 入口：
    （1）当与某个case匹配
    （2）当与所有case都不匹配，如果有default，从default进入
  - 出口：
    （1）switch结束的
    （2）break;

- 其他要求

  - (1)case后面必须是常量或常量表达式
  - (2)所有case后面的值必须不相同
  - (3)case后面常量值的类型与表达式的类型要一致

### 条件判断与选择结构的取舍

- （1）凡是可以使用switch...case一定可以用if..else代替，凡是反过来不一定
- （2）当所有的条件判断是“常量的等值判断”，那么建议使用switch...case，可读性更好，效率更高

## 循环结构

### 1、for循环

- 语法结构

```java
  for(初始化表达式①;  循环条件②;  迭代表达式④){
  循环体语句（要重复的代码）③
  }
```
- 执行的过程

  （1）初始化表达式①

  （2）循环条件的判断②

  （3）如果条件成立，执行循环体语句③一次

  （4）迭代表达式④

  （5）回到（2），直到循环条件不成立，结束for循环

- 注意

  （1）for(;;)中两个分号不可以省略，但是表达式可以省略

  （2）适用于起始条件和终止条件明确，循环次数比较明显的情况

### 2、while循环

- 语法结构

```java
while(循环条件){
  循环体语句;
  }
```

- 执行过程

  （1）循环条件判断

  （2）如果条件成立，执行循环体语句一次

  （3）回到（1），直到循环条件不成立，结束while循环

- 注意

  （1）循环条件明显，次数不明显

  （2）经常这样使用while(true)  和 break 结合

### 3、do..while循环

- 语法结构

```java
do{
  循环体语句;
  }while(循环条件);
```

- 执行过程

  （1）先执行一次循环体语句

  （2）再判断循环条件，是否继续下一次

  （3）如果循环条件成立，执行下一次循环体语句

  （4）回到（2），直到循环条件不成立，结束do..while

- 注意

  （1）和while的最大区别，至少执行一次

### 4、foreach

### 5、嵌套

（1）无论哪种循环，循环中都可以嵌套任一种循环结构

（2）执行过程

- 外循环循环一次，内循环循环一轮

### 作用：重复执行某些代码

## 跳转、中断

### 1、break

- 可以适用于switch和循环

- 默认表示结束当层循环或switch

- break 标签;

  表示结束指定的循环

  标签:循环

```java
  out_label:for(int i = 1; i<=5; i++){
  		inner_label:while(true){
  			System.out.println("请输入数字：");
  			int num = input.nextInt();
  			if(num>0){
  				positive ++;
  			}else if(num<0){
  				negative++;
  			}else{
  				break inner_label;//结束的是while内层循环
  				break out_label;
  			}
  		}
  }
```


### 2、continue

- 只能用于循环
- 表示提前结束当层本次循环，进入下一次循环

### 3、return

- 结束当前方法

# 方法

方法(Method)：又称为函数（Function），代表一个独立功能，目的为了代码重用
## 声明的格式
【修饰符列表】 返回值类型  方法名（【形参列表】）【抛出异常列表】{
		方法体，方法功能的实现代码;
		【return  【返回值】;】

}

四种形式

- 1、无参无返回值
  - 【修饰符列表】 void 方法名()【抛出的异常列表】 {
    方法体;
    }
  - public static void 方法名(){
    方法体;
    }
  
- 2、有参无返回值

  - [修饰符列表] void 方法名(形参列表)[抛出的异常列表]{
    方法体;
    }
  - public static void 方法名(形参列表){
    方法体;
    }

- 3、无参有返回值

  - [修饰符列表] 返回值类型 方法名()[抛出的异常列表]{
    方法体;
    }
  - public static 返回值类型 方法名(){
    方法体;
    return 返回值;
    }

- 4、有参有返回值

  - [修饰符列表] 返回值类型 方法名(形参列表)[抛出的异常列表]{
    方法体;
    }
  - public static 返回值类型 方法名(形参列表){
    方法体;
    return 返回值;
    }

## 调用格式

### 本类中

- 不需要在方法名前面加前缀

### 其他类中

- 需要在方法名前面加前缀

  - 如果被调用的方法是static

    - 前缀是 类名.
    - 类名.方法名

  - 如果被调用的方法是非static

    - 前缀是  对象名.
    - 对象名.方法名

### 不管是本类中还是其他类中，对于方法签名的关注点是一样：

- 【修饰符列表】 返回值类型  方法名（【形参列表】）【抛出异常列表】
- 目前

  - 有无形参列表

    - 如果有形参，调用是必须传实参，而且实参的个数与形参的个数一致，类型兼容
    - 如果没有形参，调用是也不用传实参

  - 有无返回值

    - 如果有返回值，调用时就可以接收
    - 如果无返回值，调用时不能用变量接收，只能单独成一个语句

### 四种形式

- 1、无参无返回值

  - 本类中

    - 方法名();

      单独一个语句

  - 其他类中

    - 类名.方法名();

      单独一个语句

    - 对象名.方法名();

      单独一个语句

- 2、有参无返回值

  - 本类中

    - 方法名(实参列表);

      单独一个语句

  - 其他类中

    - 类名.方法名(实参列表);

      单独一个语句

    - 对象名.方法名(实参列表);

      单独一个语句

- 3、无参有返回值

  - 本类中

    - 变量 = 方法名();

      - 方法的调用作为表达式
      - 把方法调用的返回值赋值给变量

  - 其他类中

    - 变量 = 类名.方法名();

      - 方法的调用作为表达式
      - 把方法调用的返回值赋值给变量

    - 变量 = 对象名.方法名();

      - 方法的调用作为表达式
      - 把方法调用的返回值赋值给变量

- 4、有参有返回值

  - 本类中

    - 变量 = 方法名(实参列表);

      - 方法的调用作为表达式
      - 把方法调用的返回值赋值给变量

  - 其他类中

    - 变量 = 类名.方法名(实参列表);

      - 方法的调用作为表达式
      - 把方法调用的返回值赋值给变量

    - 变量 = 对象名.方法名(实参列表);

      - 方法的调用作为表达式
      - 把方法调用的返回值赋值给变量

## 方法的参数传递机制

### 形参的类型是基本数据类型

- 值传递机制

  - 形参的修改是不会影响实参

### 形参的类型是引用数据类型

- ？

## 方法的重载Overload

### 概念

- 在同一个类中，方法名相同，形参列表不同的两个或多个方法构成方法的重载
- 和返回值类型无关

# 面向对象

## 面向对象和面向过程的区别

- 都是编程思想

- 面向过程注重过程，步骤，怎么做	执行者

- 面向对象注重对象，谁来做	指挥者

## 面向对象学习

### 1、类与对象

（1）类与对象的概念

（2）类与对象的关系

（3）如何设计类，类的成员

（4）如何创建对象

### 2、面向对象的三个基本特征和高级特性

- 基本特性

  - 封装
  - 继承
  - 多态

- 高级特性

  - 枚举
  - 接口
  - 抽象
  - 泛型
  - 注解
  - 可变参数
  - 自动装箱与拆箱
  - foreach
  - Lambda表达式
  - .....

### 3、相关的关键字和API

- 关键字

  - class
  - new
  - this
  - 权限修饰符

    - public
    - protected
    - 缺省
    - private

  - super
  - ...

- API

  - 集合
  - 异常
  - IO
  - 网络编程
  - 线程
  - ....

## 1、类与对象

### (1)类与对象的概念

- 类：对一类具有相同特征的事物的抽象描述
- 对象：类的实例，是具体的个体

### (2)类与对象的关系

- 类是对象的设计图，创建的模板
- 对象是类的实例，是一个具体的个体

### (3)类的设计，成员

（1）属性

- 属性的特点

  - （1）声明的位置    

    在类中方法外

  - （2）保存的位置

    - static	在方法区

    - 非static     在堆中

  - （3）默认值

    - byte,short,int,long是0，float,double是0.0，boolean是false，char是\u0000，引用数据类型都是null

  - （4）作用域

    在整个类中

  - （5）生命周期

    随着对象的创建而创建，到垃圾回收为止

- 属性声明格式

  - [修饰符]  数据类型  属性名 【=显式值】; 

    修饰符	private	私有化


（2）构造器

- 构造器的作用

  （1）和new一起创建对象

  （2）为属性赋值

- 如何声明

  无参

  [修饰符] 类名(){
  }

  有参

  [修饰符] 类名(形参列表){
  }

- 特点

  - 构造器的特点：
    （1）构造器名与类名必须相同
    （2）构造器没有返回值
    （3）构造器可以重载
    （4）如果一个类没有声明过构造器，编译器将默认添加一个无参构造
    如果这个类声明了构造器，编译器将不再自动添加无参构造

- 如何调用

  - （1）和new一起  

    new 构造器()
    new 构造器(实参列表)

  - （2）在本类的其他构造器中或子类的构造器中

    在本类的其他构造器中：this()或this(实参列表)
    在子类的构造器中：super()或super(实参列表)

（3）方法

无参无返回值

有参无返回值

无参有返回值

有参有返回值

（4）代码块

按位置分
在类中方法外
- 是否有static修饰

	- 有static修饰的：静态代码块

    语法结构

```java
class 类{
    static{
    静态代码块
    }
}
```

​									特点

- 随着类的加载并初始时而执行，而且一个类的静态代码块只执行一次

- 而且父类的静态代码块优先于子类的静态代码块

- 静态代码块肯定优先于构造块和构造器

  ​					作用

  - 为静态变量（类变量）初始化（赋值）

    

- 没有static修饰的：非静态代码块，构造块

    语法结构

```java
class 类{
    {
    非静态代码块
    }
}

```

- 特点

  - 每次创建对象时调用，而且先于构造器调用

- 作用

  - 为实例变量初始化（赋值），一般是多个构造器中重复的代码提取到构造块
- 在方法中

  - 局部代码块（了解）

- 相关的面试题

  - 赋值和执行的顺序

    - 父类的静态代码块 -- 》子类的静态代码块  --》父类的构造块--》父类的构造器 --》子类的构造块 --》子类的构造器
  - ![屏幕截图 2022-04-19 115047](D:\Study\自学\笔记\img\屏幕截图 2022-04-19 115047.png)
  
- 关于static的重写问题
  
  - 静态的方法和属性，没有编译时类型和运行时类型的区别，只有编译时类型，换句话说没有重写（覆盖）一说
  
```java
package com.atguigu.static_.buchong;
/*
* 静态的方法：不存在编译时和运行时类型，只有编译时类型
* 静态的属性：不存在编译时和运行时类型，只有编译时类型
*/
public class Test {
    public static void main(String[] args) {
        SuperClass s = new SubClass();
        s.test();//父类的方法
        System.out.println(s.info);//尚硅谷
        SubClass sub = new SubClass();
        sub.test();//子类的方法
        System.out.println(sub.info);//atguigu

    }

}

class SuperClass{
    static String info = "尚硅谷";
    public static void test(){
        System.out.println("父类的方法");
    }
}
class SubClass extends SuperClass{
    static String info = "atguigu";
    public static void test(){
        System.out.println("子类的方法");
    }    
}
```

   

（5）内部类

- 什么情况下使用内部类

  （1）当一个事物的内部，还有一个部分需要一个完整的结构进行描述，而这个内部的完整的结构又只为外部事物提供服务，那么整个内部的完整结构最好使用内部类
  （2）内部类可以访问外部类的所有的成员，包括私有的

- 形式

  成员

  - 静态内部类
```java
[修饰符] class 外部类{
    [修饰符] static class 内部类{
    }
}
```
- 修饰符的问题

  - （1）权限修饰符

    - 4种

  - （2）static

    - 必须得有

  - （3）final（极少）

    - 可以

    - 表示不能被继承

  - （4）abstract（极少）

    - 可以

    - 表示可以包含抽象方法，需要子类继承

- 静态内部类的成员

  - 所有都可以，包括静态的

- 使用问题

  - （1）在静态内部类中使用外部类的成员

    - 只能使用外部类的静态成员

  - （2）在外部类中使用静态内部类

    - 都可以

  - （3）在外部类的外面，其他类中

    - （1）用静态内部类的静态成员

      - 外部类名.内部类名.静态成员

    - （2）用静态内部类的非静态成员

      - 需要静态内部类的对象
      - 外部类名.内部类   变量 = new   外部类名.内部类();
        变量.成员....
    
  - 非静态内部类，通常称为成员内部类

    

```java
[修饰符] class 外部类{
    [修饰符] class 内部类{
    }
}
```

- 修饰符的问题

（1）权限修饰符

- 4种

（2）static

- 没有

（3）final（极少）

- 可以

- 表示不能被继承

（4）abstract（极少）

- 可以

- 表示可以包含抽象方法，需要子类继承

- 非静态内部类的成员

  - 除了静态成员，其他都可以

- 使用的问题

  （1）在非静态成员内部类中使用外部类的成员

  - 都可以

  （2）在外部类中使用非静态成员内部类

  - 在外部类的静态成员中不能使用非静态成员内部类

    - 静态  （不能用） 非静态

      - 原因，静态的成员先加载，非静态只有创建对象才有

  （3）在外部类的外面使用非静态成员内部类

  - 依赖于外部类的对象

  - 形式一

    （1）先创建外部类的对象

    - 外部类  out = new  外部类();

    （2）通过外部类的对象创建内部类的对象

    - 外部类.内部类  in = out.new 内部类();

    （3）通过内部类对象调用它的成员

    - in.成员

  - 形式二

（1）在外部类中提供一个方法，用来返回内部类的对象

```java
class 外部类{
    class  内部类{
    }

    public 内部类  getInnerInstance(){
        return new 内部类();
    }

}
```

（2）创建外部类的对象

​	外部类  out = new  外部类();

（3）通过外部类的对象，获取内部类的对象

​	外部类.内部类  in = out.getInnerInstance();

（4）通过内部类对象调用它的成员

​	in.成员

面试题

如何继承非静态成员的内部类

```java
class Outer{
    class Inner{
    }
}
class Other extends Outer.Inner{
    Other(Outer out){
        out.super();
    }
}
```

- 局部

	- 有名字的局部内部类，通常称为局部内部类

		- 格式
 ```java
[修饰符] class 外部类{
    [修饰符] 返回值类型  方法名([形参列表]){
        [修饰符] class 内部类{
        }
    }

}
 ```

- 修饰符的问题
	
    （1）权限修饰符
	
    - 都不行
	
    （2）static
	
    - 没有
	
    （3）final（极少）
	
    - 可以
	
    - 表示不能被继承
	
    （4）abstract（极少）
	
    - 可以
	
    - 表示可以包含抽象方法，需要子类继承
	
    - 有名字的局部内部类的成员
	
    - 除了静态成员，其他都可以
	
    - 使用
	
    （1）在内部类中使用外部类的成员
	
    - 受所在方法的约束，如果所在方法是静态的，那么只能使用外部类的静态成员，如果所在方法是非静态的，那么都可以使用
	
    （2）在内部类中使用外部类的局部变量
	
    - 必须是final修饰
	
    - JDK1.8之前，必须显式声明
    - JDK1.8之后，默认就是final修饰
	
    - （3）在外部类中使用内部类
	
    - 只能在声明它的方法中使用，而且在声明之后使用
	
    - 和局部变量的作用域一样
	
    （4）在外部类的外面
	
    - 不可以
	
    （5）在外部类的其他方法中
	
    - 不可以
	
    - 匿名内部类
	
```java
new 父类/父接口(){
    方法
}
```

- 修饰符
	
    - 一个都没有
	
    - 匿名内部类的成员
	
    	- 除了非静态的都可以，但是一般很少自定义方法等成员，它的成员都是重写父类的，父接口的方法
	
    - 匿名内部类的特点
	
    （1）声明类和创建对象同时进行， 只有一个对象
	
```java
public static void main(String[] args) {
    //Object的一个子类对象
    new Object(){
        public void test(){
            System.out.println(this.getClass());
        }
    }.test();
    //Object的另一个子类对象
    new Object(){
        public void test(){
            System.out.println(this.getClass());
        }
    }.test();
}
```


​					（2）子类一定会调用父类的构造器		

```java

class MyClass{
    private String info;
    MyClass(String info){
        this.info = info;
    }
}
//创建一个MyClass的子类对象，使用匿名内部类
MyClass m = new MyClass("参数"){

};
```

匿名内部类的使用形式				

- 形式一					

   匿名内部类的匿名对象直接调用方法	

```java
new Object(){
    public void test(){
        System.out.println(this.getClass());
    }
}.test(); 
```

- 形式二					

   与父类或父接口构成多态引用					 

```java
class MyClass{
    public void test(){
        System.out.println("父类的测试方法");
    }
}

MyClass m = new MyClass(){
    public void test(){
        System.out.println("重写");
    }
};

m.test();
```

- 形式三					

   匿名内部类的匿名对象作为实参					  	

```java
MyClass[] arr = new MyClass[5];
Arrays.sort(arr, new Comparator(){
    @Override
    public int compare(Object o1, Object o2) {
        return 0;
    }
});		  			
```

- 使用其他要求				

  （1）在内部类中使用外部类的成员					

   受所在方法的约束，如果所在方法是静态的，那么只能使用外部类的静态成员，如果所在方法是非静态的，那么都可以使用				- （2）在内部类中使用外部类的局部变量					

   必须是final修饰						

  - JDK1.8之前，必须显式声明						
  - JDK1.8之后，默认就是final修饰

### （4）类的声明格式

```java
[修饰符] class 类名{
//属性列表
//构造器列表
//get/set方法
//其他方法
}
```

### （5）如何创建对象

- new 类名()

  用无参构造

- new 类名(实参列表)

  用有参构造

- 匿名对象和有名对象

  Student stu = new Student();

  - stu对象名，也可以称为对象的引用

  - 匿名对象

    System.out.println(new Student());

- 对象的内存图

  ![](D:\Study\自学\笔记\img\屏幕截图 2022-04-19 124709.png)

## 2、面向对象的基本特征

### 封装

封装的作用

- 安全
- 使用方便    对于使用者屏蔽实现细节


- 概念

  - 狭义

    属性的封装

    （1）属性私有化：private

    （2）提供公共get/set方法

  - 广义

    方法

    类

    包

    组件

    系统

### 继承

- 什么情况下需要继承？继承的好处是什么？

  - 为了代码重用

    （1）当有一个父类，如果再声明类时，发现这些类与已经存在的父类有很多相同特征，那么就可以通过继承的方式来简化代码

    （2）已经很多类，发现这些类有很多共同的特点，那么我们可以把这些共同的特点抽取到一个父类中，以便简化代码

  - 逻辑的角度

    表示is-a的关系

- 如何继承

```java
[修饰符] class  子类名  extends  父类名{
}
```

- 继承后对几个成员的影响

  - 属性

    （1）子类继承父类时，一定会继承父类的所有的属性，包括私有的，但是由于私有的关键字private的原因，在子类中无法直接操作它，但是可以通过get/set方式操作它

    （2）当子类的属性与父类的属性重名时，而且父类的属性没有私有化，如果要访问父类的属性那么通过super.属性进行访问，如果子类中没有通过super.属性访问，那这个属性就表示是子类自己的

  - 面试题

```java
package com.atguigu.review;
public class Test {
	public static void main(String[] args) {
		Student stu = new Student();
		System.out.println(stu.getInfo());//年龄：10
		System.out.println(stu.getAge());//结果？20   如果子类重写，答案是10
	}
}

class Person{
	int age = 20;
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
}

class Student extends Person{

	int age = 10;
	/*public int getAge(){
		return age;
	}*/
	public String getInfo(){
		return "年龄：" + age;

	}
}
```

  - 方法

    （1）子类继承父类时，一定会继承父类的所有的方法，包括私有的，但是由于private，在子类中无法直接操作，但是可以间接操作

    （2）当父类的方法实现不适用于子类时，子类可以对父类的方法的进行重写

  - 构造器

    （1）子类继承父类时，不会继承父类的构造器

    （2）子类继承父类时，一定会调用父类的构造器

    - 如果父类有无参构造，那么子类会默认去调用父类的无参构造
      如果父类没有无参构造，只有有参构造，那么子类必须在子类构造器中手动调用父类的有参构造
    - 调用父类的无参构造的语句：super();
      调用父类的有参构造的语句：super(实参列表);
      而且这两个语句必须在子类的构造器的首行。

- 继承的原则

  （1）单继承

  - 在Java中只支持单继承，也就是说一个类只能有一个直接父类     --》一个唯一的亲生父亲

  （2）多层继承

  - 在Java中父类还可以有父类，而且在子类中会继承父类以及父类的父类的所有的属性与方法			--》代代相传

    - 子类对象在寻找一个方法、属性时，如果本类中找不到，会去直接父类中查找，如果直接父类中也找不到，在往上找，找到为止，一直追溯到java.lang.Object根父类中
    - 通过super.属性和方法时，先从直接父类中查找，如果没有，再往上找，直到找到为止，一直可以到java.lang.Object

  （3）一个类可以有很多个子类，子类还可以有子类

  - 子孙满堂
  - 开枝散叶

### 多态

- 多态的表现形式

  （1）方法的重载：同一个类中，功能多种实现形式
  方法的重写：父子类中，功能的不同实现形式

  （2）对象的多态性

  - 编译时类型与运行时的类型不一致，编译时看“左边”，运行时看“右边”，
    编译时从“父类”中寻找方法，运行时执行的是“子类”重写过的代码
  - 对象的多态性的前提：
    （1）继承
    （2）方法的重写
    （3）多态引用

    - 多态引用

      - Person p = new Student();

    - 本态引用

      - Person p = new Person();
      - Student s = new Student();

- 多态的应用

  （1）多态参数

  （2）多态数组

- 类型的转换

  - 向上转型

    - 子类的对象赋值给父类的变量
    - 自动完成

  - 向下转型

    - 把父类的变量赋值给子类的变量

    - 强制类型转换

    - 如果想要向下转型成功

      父类的变量本身指向的就是该子类的对象

    - 如何避免ClassCastException

      在向下转型之前，加判断

      - if(变量  instanceof  子类类型){
        子类类型  temp = (子类类型)变量;
        }

    - 什么情况下需要向下转型

      - 因为一个对一旦向上转型后，那么就无法访问该子类对象中特有的方法，只能访问父类有的方法
      - 如果需要通过该对象，访问子类的特有的方法等，那么就需要向下转型

## 3、关键字

### class

- 声明类

### new

- 创建实例，创建对象
- 在堆中申请一块空间
- 只要new就创建新的对象
- new后面一定是构造器

### this

- 当前对象

  （1）如果在构造器中，表示正在被创建的那个对象
  （2）如果在其他方法中，表示调用该方法的那个对象

- 使用

  - （1）this.属性

    当成员变量（属性名）与局部变量（形参）重名时，使用this.属性进行区别

  - （2）this.方法

    - 表示调用“当前类”的方法
    - 如果子类继承了父类，子类没有重写父类的方法，this.方法也可能是从父类继承的方法
    - 如果子类继承了父类，子类重写父类的方法，this.方法就代表子类重写过的代码

  - （3）this()或this(实参列表)

    - 表示调用本类的其他构造器，而且必须在构造器的首行

### super

- 父类引用
- 使用

  （1）super.属性

  当子类的属性与父类的属性重名时，而且父类的属性没有私有化
  如果需要调用父类的属性，那么通过super.属性进行区别

  （2）super.方法

  当子类的方法重写了父类的方法时，
  如果需要调用父类的被重写的方法，那么通过super.方法进行调用

  （3）super()或super(实参列表)

  当子类需要调用父类的构造器时，通过super()或super(实参列表)进行调用

调用父类的无参构造的语句：super();
调用父类的有参构造的语句：super(实参列表);
而且这两个语句必须在子类的构造器的首行。

### 权限修饰符

- 三个单词，四种形式：
  public；公共的，范围：任意位置，可以修饰类、成员
  protected：受保护的，范围：本包或子类中，可以修饰成员
  缺省：默认的，范围：本包，可以修饰类、成员
  private：私有的，范围：本类中，可以修饰成员
- ![](D:\Study\自学\笔记\img\屏幕截图 2022-04-19 130042.png)

### static

- 静态的
- 可以修饰成员

  （1）属性

  这个属性就称为类变量，它的值是所有对象共享的，存储在方法区
  它的get/set方法也是静态的

  （2）方法

  这个方法就称为类方法，调用它不需要创建对象，直接可以通过”类名.方法“调用

  （3）代码块	

  用static修饰的代码块称为静态代码块。
  随着类的加载并初始时而执行，而且一个类的静态代码块只执行一次
  为静态变量赋值，如果静态变量有显式初始化和静态代码块初始化，它俩属于同级，谁在前谁先执行

  （4）内部类

### final

- 最终的

- 可以修饰

  （1）类

  这个类不能被继承，俗称“太监类”

  （2）方法

  这个方法不能被重写，像“圣旨”

  （3）变量

  成员变量

  - 常量	值不能被修改

  - 必须手动初始化

```java
package com.atguigu.review;
public class TestFinal {
}
class Human{
//	private static final String country = "中国";
	private static final String country;
	static{
		country = "中国";
	}
}
class Person{
//	final String country = "中国";
	private final String country;
	private String name;
/*	{
		country = "中国";
	}*/
	Person(){
		country = "中国";
	}
	public Person(String name) {
		super();
		country = "中国";
		this.name = name;
	}
}
```

- 局部变量

  - 常量

    值不能被修改

  - 必须手动初始化


​        

### native

- 原生的
- 可以修饰

  - 方法

    （1）表示这个方法的方法体是非Java语言实现

    （2）对于使用这个方法者来说，和普通的Java 方法一样使用

    （3）如果有需要，也可以进行重写

## 4、包

### 包的作用

（1）避免类的重名
（2）访问权限的控制
（3）便于管理

### 如何声明包

- package 包;
- 要求

  - 必须在源文件的首行，一个源文件只能有一句
  - 遵循命名规范，所有字母都小写，单词之间使用.，一般以公司的域名倒置

### 如何使用其他包的类

- 需要import 包.类名;
- 要求

  - 在package和class声明之间，可以多句
  - 被使用的类必须是public 或 protected（父子类）

- 形式

  - 一一列举

    - import java.util.Random;
      import java.util.Scanner;

  - 某个包的类

    - import java.util.*;

  - 静态导入

    - import static java.lang.Math.*;
    - System.out.println(PI);
      System.out.println(sqrt(4));

## Overload和Override的区别

Overload：方法的重载

在同一类，方法名称相同，形参列表不同的两个或多个方法称为重载。

Override：方法的重写

​	在子类继承父类时，如果父类的方法实现不适用于子类，子类就可以对父类的方法进行重写，覆盖。

![](D:\Study\自学\笔记\img\屏幕截图 2022-04-19 130624.png)

# 数组

## 数组的概念

数组的作用	用来保存、管理一组相同数据类型的数据

把一组具有相同数据类型的变量使用同一个名字来进行管理，并且这些元素按照一定的顺序进行排列。这同一个名字我们称为【数组名】，每一个元素通过编号进行区别，这个编号我们称为【下标】或索引。元素的总个数就是【数组的长度】。

## 数组如何声明和初始化

### 数组的声明

- 数组的类型   数组名;

- 数组的元素的类型[]  数组名;

  推荐的方式

- 数组的元素的类型  数组名[];

### 初始化

- 动态初始化

  格式：

  数组名 = new  元素的类型[数组的长度];

- 静态初始化

  格式

  数组名 = new  元素的类型[]{元素列表};

  - 元素列表的每一个元素使用,分割
  - 元素列表的个数就是数组的长度

  简写形式

  - 数组的元素的类型[]  数组名 = {元素列表};

    只有声明和静态初始化在一行，才可以这么简写

## 数组的元素

### 表示形式

数组名[下标]

- 下标的范围

  - [0，数组的长度-1]

    [0,  数组名.length -1]

  - [0，数组的长度)

### 赋值

- 数组名[下标] = 值;

## 数组的长度

数组名.length

## 数组的遍历

```java
for循环
    for(int i=0; i<数组名.length; i++){
    }
foreach循环
    for(数组的元素的类型   元素的临时名 : 数组名){
    }
```

## 数组的算法

（1）在数组中找最大值/最小值

```java
//找最大值
public static int max(int[] arr){
	//第一步：假设第一个元素最大
	int max = arr[0];
		//遍历后面的元素和max比较
	for (int i = 1; i < arr.length; i++) {
		//当有比max的值，就把max修改为它的值
		if(max < arr[i]){
			max = arr[i];
		}
	}
		return max;
}
```

（2）在数组中找最大值、最小值的下标

```java
//找最大值的下标
public static int maxIndex(int[] arr){
	//第一步：假设第一个元素最大
	int index = 0;
	//arr[index] 和 后续的元素一一比较
	for (int i = 1; i < arr.length; i++) {
		//当有比max的值，就把max修改为它的值
		if(arr[index] < arr[i]){
			index = i;
		}
	}
	return index;
}
```

（3）数组元素的累加和，平均值

```java
//求数组元素的总和
public static long sum(int[] arr){
    long sum = 0;
    for (int i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}
public static double avg(int[] arr){
    double sum = sum(arr);
    return sum/arr.length;
}
```

（4）反转

```java
//反转
public static void reverse(int[] arr){
    //如果有5个元素，应该交换2次或3次      arr.length/2
    //如果有6个元素，应该交换3次          arr.length/2
    //数组的首尾对应位置交换
    //次数
    for(int i=0; i<arr.length/2; i++){
        //首尾交换
        int temp = arr[i];
        arr[i] = arr[arr.length-1-i];
        arr[arr.length-1-i] = temp;
    }
}
//反转部分
public static void reverse(int[] arr, int start ,int end){
    //次数     
    //假设start = 1, end = 5   次数2次   (end + 1 - start)/2  (5+1-1)/2  2
    //假设start = 1, end = 6  次数3次    (end + 1 - start)/2  (6+1-1)/2  3
    for(int i=0; i< (end + 1 - start)/2; i++){
        //首尾交换
        //arr[start],arr[start+1]...
        //arr[end],arr[end-1]...
        int temp = arr[start + i];
        arr[start + i] = arr[end -i];
        arr[end-i] = temp;
    }
}
```

（5）复制

```java
//复制一个数组，从原数组的[0]元素开始复制，新数组的长度由使用者决定
public static int[] copy(int[] src, int newLength){
    //1、创建新数组的对象
    int[] newArray = new int[newLength];
    //2、把原数组的元素复制到新数组中
    for(int i=0; i<newArray.length && i<src.length; i++){
        newArray[i] = src[i];
    }
    return newArray;
}

//复制一个数组，从原数组的[start]元素开始复制，新数组的长度由使用者决定
public static int[] copy(int[] src, int start, int newLength){
    //1、创建新数组
    int[] newArray = new int[newLength];
    //2、把原数组的元素从[start]复制到新数组的[0]...
    for(int i=0; i<newArray.length && start+i<src.length; i++){
        newArray[i] = src[start+i];
    }
    return newArray;
}
```

（6）排序

```java
//假设数组5个元素
public static void pubSort3(int[] arr){
    //方式二：把大的往右沉
    //每一轮从左边开始比较
    //比较的轮数依然是n-1轮
    for(int i=1; i<arr.length; i++){
        //每一轮从左边开始比较
        /*
		* 第一轮：i=1， 比较4次，j=0,1,2,3   ,j<arr.length-i  j<5-1 j<4 
		* 第二轮：i=2，比较3次，j=0,1,2      ,j<arr.length-i  j<5-2 j<3
		* ...
		*/
        for(int j=0; j<arr.length-i; j++){
            //如果左边的元比右边的元素大，交换
            if(arr[j] > arr[j+1]){
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

//假设数组5个元素
public static void pubSort2(int[] arr){
    //排序规则：每一轮通过相邻元素的比较，把小的往左边冒（或把大的往右边沉），每一轮都是把本轮的最小值冒出来（最大值沉下去）
    //经过n-1轮完成最终的排序
    //(1)方式一：把小的往左边冒，注意，每一轮都是从最右边往左边比较
    //i=0,i=1,i=2,i=3  i<5-1 -->  i<4 -->  i<=3
    for(int i=0; i<arr.length-1; i++){//一共n-1轮
        //每一轮都要从最右边往左边比较
        /*
		* 第一轮：比较n-1次，比较4次， i=0, j=4,3,2,1 ,j>i
		* 第二轮：比较3次，i=1, j=4,3,2 ,j>i
		* ....
		*/
        for(int j=arr.length-1; j>i; j--){
            //相邻的元素比较，而且如果右边的比左边的小，需要交换
            if(arr[j] < arr[j-1]){
                int temp = arr[j];
                arr[j] = arr[j-1];
                arr[j-1] = temp;
            }
        }
    }
}

//冒泡排序：从小到大
//如果数组是5个元素
public static void pubSort(int[] arr){
    //排序规则：每一轮通过相邻元素的比较，把小的往左边冒（或把大的往右边沉），每一轮都是把本轮的最小值冒出来（最大值沉下去）
    //经过n-1轮完成最终的排序
    //(1)方式一：把小的往左边冒，注意，每一轮都是从最右边往左边比较
    for(int i=1; i<arr.length; i++){//一共n-1轮
        //每一轮都要从最右边往左边比较
        /*
		* 第一轮：比较n-1次，比较4次， i=1, j=4,3,2,1 ,j>=i
		* 第二轮：比较3次，i=2, j=4,3,2 ,j>=i
		* ....
		*/
        for(int j=arr.length-1; j>=i; j--){
            //相邻的元素比较，而且如果右边的比左边的小，需要交换
            if(arr[j] < arr[j-1]){
                int temp = arr[j];
                arr[j] = arr[j-1];
                arr[j-1] = temp;
            }
        }
    }
}


//直接选择排序
//基本原理：将待排序的元素分为已排序（初始为空）和未排序两组，依次将未排序的元素中值最小的元素放入已排序的组中。
//[3,2,1,5,4]  从小到大排序
/*
	 * 第一次：所有元素都属于未排序   把未排序的元素中的最小值找出来    arr[2] = 1 ，放入已排序组中     和第一个元素交换
	 * [1,2,3,5,4]
	 * 第二次：已排序的是[1]，未排序的是[2,3,5,4]，把未排序元素中的最小值找出  arr[1]=2，放入已排序组中  
	 * 【1,2】，【3,5,4】
	 * ...
	 * 
	 */
//假设5个元素
public static void selectSort(int[] arr){
    //次数
    for(int i=0; i<arr.length-1; i++){
        //第一次，找最小值
        //假设每一轮的未排序元素的第一个最小
        int index = i;
        //找出本轮最小值
        /*
		* int i=0 ,从哪些元素中找最小值  [0]~[4]   j=1,2,3,4
		* int i=1，从哪些元素中找最小值[1]~[4]    j=2,3,4
		* ...
		*/
        for(int j=i+1; j<arr.length; j++){
            if(arr[index] > arr[j]){
                index = j;
            }
        }

        //找出arr[index]值最小，下标是index
        //arr[i] 和 arr[index]交换
        if(i!=index){
            int temp = arr[i];
            arr[i] = arr[index];
            arr[index] = temp;
        }
    }
}
```

（7）数组的扩容

```java
private void kuorong(){
    //先扩容
    int[] newArray = new int[arr.length*2];
    //通过循环把原数组中的内容复制到新数组中
    for(int i=0; i<arr.length; i++){
        newArray[i] = arr[i];
    }
    //把新家的地址记录下来，下次存、取元素都从新家操作，旧家不要了
    arr = newArray;
}
```

（8）数组的元素插入

```java
package com.atguigu.array;
public class MyArrayList {
    private int[] arr = new int[5];//装数据
    private int total;//记录实际存储的元素的个数
    //在index插入数据data
    public void insert(int index, int data){
        //如果当前数组已满，需要先扩容
        if(total >= arr.length){
            //(1)先创建一个新的更大的数组
            int[] newArray = new int[arr.length*2];
            //(2)把原来数组中的数据复制到新数组中
            for(int i=0; i<arr.length; i++){
                newArray[i] = arr[i];
            }
            //(3)使得arr指向新数组
            arr = newArray;
        }
        //1、先把index右边的元素右移
        /*
		 * 假设total=3,index=1
		 * 现在有值arr[0],arr[1],arr[2]，需要移动的是arr[2],arr[1]
		 * 假设total=5,index=1
		 * 现在有值arr[0],arr[1],arr[2],arr[3],arr[4]，需要移动的是,arr[4],arr[3],arr[2],arr[1]
		 */
        for(int i = total-1; i>=index; i--){
            //右边的元素=左边的元素
            arr[i+1] = arr[i];
        }
        //在index位置插入data
        arr[index]= data;
        //元素个数加1
        total++;
    }
}
```

（9）数组的元素删除

```java
package com.atguigu.array;
public class MyArrayList {
	private int[] arr = new int[5];//装数据
	private int total;//记录实际存储的元素的个数
	//删除指定位置的元素
	public void delete(int index){
		//(1)把index右边的元素左移
		/*
		 * 假设现在total=3,index =1
		 * 有值的是arr[0],arr[1],arr[2]，需要移动的是arr[2]
		 * 假设现在total=5,index =1
		 * 现在有值arr[0],arr[1],arr[2],arr[3],arr[4]，需要移动的似乎arr[2],arr[3],arr[4]
		 */
		for(int i = index+1; i<total; i++){
			//左边的元素=右边的元素
			arr[i-1] = arr[i];
		}
		//(2)把最后一个元素的位置置为“空”（还原到默认值）
		arr[total-1] = 0;
		//(3)元素个数减一
		total--;

	}

}
```

```java
package com.atguigu.array;
public class MyArrayList {
    private int[] arr = new int[5];//装数据
    private int total;//记录实际存储的元素的个数
    //删除指定位置的元素
    public void delete(int index){
        //(1)把index右边的元素左移
        /*
		 * 假设现在total=3,index =1
		 * 有值的是arr[0],arr[1],arr[2]，需要移动的是arr[2]
		 * 假设现在total=5,index =1
		 * 现在有值arr[0],arr[1],arr[2],arr[3],arr[4]，需要移动的似乎arr[2],arr[3],arr[4]
		 */
        for(int i = index+1; i<total; i++){
            //左边的元素=右边的元素
            arr[i-1] = arr[i];
        }
        //(2)把最后一个元素的位置置为“空”（还原到默认值）
        arr[total-1] = 0;
        //(3)元素个数减一
        total--;
    }

    public int findValue(int value){
        //挨个遍历，一共有total，遍历total个
        for (int i = 0; i < total; i++) {
            if(arr[i] == value){
                return i;
            }
        }
        return -1;
    }
    public void deleteValue(int value){
        //1、先找到value在数组中的index，这里以第一次找到为准
        int index = findValue(value);
        //2、删除index位置的元素
        if(index!=-1){
            delete(index);
        }
    }

}
```

（10）在数组中查找某个值的下标

```java
package com.atguigu.array;
public class MyArrayList {
	private int[] arr = new int[5];//装数据
	private int total;//记录实际存储的元素的个数
	//删除指定位置的元素
	public void delete(int index){
		//(1)把index右边的元素左移
		/*
		 * 假设现在total=3,index =1
		 * 有值的是arr[0],arr[1],arr[2]，需要移动的是arr[2]
		 * 假设现在total=5,index =1
		 * 现在有值arr[0],arr[1],arr[2],arr[3],arr[4]，需要移动的似乎arr[2],arr[3],arr[4]
		 */
		for(int i = index+1; i<total; i++){
			//左边的元素=右边的元素
			arr[i-1] = arr[i];
		}
		//(2)把最后一个元素的位置置为“空”（还原到默认值）
		arr[total-1] = 0;
		//(3)元素个数减一
		total--;
	}

	public int findValue(int value){
		//挨个遍历，一共有total，遍历total个
		for (int i = 0; i < total; i++) {
			if(arr[i] == value){
				return i;
			}
		}
		return -1;
	}

	public void deleteValue(int value){
		//1、先找到value在数组中的index，这里以第一次找到为准
		int index = findValue(value);
		//2、删除index位置的元素
		if(index!=-1){
			delete(index);
		}
	}
}
```
## 二维数组

如何声明

- 数组类型  数组名;

  - 数组类型是xx\[][]

- 元素的类型\[][]  数组名;

### 如何创建二维数组对象及初始化

- 动态初始化

  - 数组名 = new 元素的数据类型\[行长度][每一行的列长度];

    每一行的列数相同

  - 数组名 = new 元素的数据类型\[行长度][];

    - 每一行的列数不确定
    - 每一行的行对象暂时是null
    - 创建每一行的行对象，即为行分配空间

      数组名[行下标] = new  元素的类型[该行的列数];

- 静态初始化

  - 数组名 = new 元素的数据类型\[][]{{x,x,x,x,....},{x,x,x},{x,x,x,x,x,x,x},.....};

    {}中嵌套{}，里面的一个{}代表一行

### 二维数组的长度，即行数

- 二维数组名.length

### 二维数组的行对象

- 二维数组名[行下标]

  行下标的范围[0,二维数组名.length-1]

### 二维数组的每一行的列数

- 二维数组名[行下标].length

### 二维数组的每一个元素

- 二维数组名\[行下标][列下标]

  注意列下标

  - 每一行的列下标的范围可能是不一样
  - [0, 二维数组名[行下标].length)

- 二维数组名\[行下标][列下标] = 值

### 二维数组的遍历

- for

```java
for(int i=0; i<数组名.length; i++){
    for(int j=0; j<数组名[i].length; j++){
        数组名[i][j]表示一个元素
    }
}
```

- 增强for	

```java
for(行类型  hang : 二维数组名){
    for(元素类型  lie : hang){
        lie就是代表每一个元素
    }
}
```
## 数组的内存图

### 一维数组

- 元素是基本数据类型

  ![](D:\Study\自学\笔记\img\屏幕截图 2022-04-19 175352.png)

- 元素是引用数据类型，又称为对象数组

![](D:\Study\自学\笔记\img\屏幕截图 2022-04-19 175525.png)

### 二维数组

- 元素是基本数据类型

  规则

  ![](D:\Study\自学\笔记\img\屏幕截图 2022-04-19 175644.png)

  不规则

  ![image-20220419175746346](C:\Users\26871\AppData\Roaming\Typora\typora-user-images\image-20220419175746346.png)

- 元素是引用数据类型

  规则

  ![](D:\Study\自学\笔记\img\屏幕截图 2022-04-19 175910.png)

  不规则

  ![image-20220419175950547](C:\Users\26871\AppData\Roaming\Typora\typora-user-images\image-20220419175950547.png)

## 数组的工具类

### java.util.Arrays

### 静态方法

（1）int   Arrays.binarySearch(int[] a ,int key)

- 在a数组中查找key的下标
- （1）数组a必须是有序的，否则结果不一定正确
- （2）如果key在a中存在，就返回它的下标，如果不存在，返回(-(插入点)-1)

（2）Arrays.fill(int[] a, int value)

给数组a的每一个元素都赋值为value

（3）Arrays.sort(int[])

排序，从小到大

（4）String  Arrays.toString(int[] a)

把数组的元素列表用字符串返回，形式[元素1，元素2，元素3.。。]

## 命令行参数

### 主方法的参数

### java命令

- java   包.类名   参数1  参数2   参数3 ....

  - 参数之间使用空格

### eclipse

![](D:\Study\自学\笔记\img\屏幕截图 2022-04-19 180106.png)

## 可变参数

可变参数属于形参

要求

- 一个方法只能有一个可变参数，而且只能是最后一个
- 在声明它的方法中，当做数组处理
- 对于调用这个方法者，可变参数的位置可以传，[0~n]个实参，也可以传对应类型数组对象

### 可变参数的重载问题

- 对于编译器来说不属于重载

- 不属于重载

```java
//如果传一个整数时，不知道用谁好
public static void main(String[] args) {
  System.out.println(getSum(1));
  }
public static int getSum(int... args){
	return 0;
}
public static int getSum(int a,int... args){
	return 0;
}
```

```java
public static int getSum(int... args){return 0;}
public static int getSum(int[] args){}
```

	-  但是它俩不完全等价		
	-  因为int... args既可以传数组对象，又可以传 n个元素值		
	-  int[]只能传数组对象

- 属于重载

```java
//优先于确定参数个数
public static void main(String[] args) {
    System.out.println(getSum(1));
}

public static int getSum(int... args){
    return 0;
}
public static int getSum(int a){
    System.out.println("一个参数");
    return 0;
}
```

# JavaSE  API

## java.lang.Object

它是所有类型的根父类

一个类如果没有显式声明它的父类，这个类的直接父类就是Object

### 理解

1. Object类的所有方法，在所有对象中都有，包括数组对象

2. Object类的变量可以接受任意类型的对象
   Object类型的形参可以接受任意类型的对象作为实参
   Object[]类型的数组可以接受任意类型的对象作为它的元素

3. 所有对象创建时，都会调用Object的无参构造

### 方法

1. 无参构造
Object() 
所有对象创建时，都会调用Object的无参构造
2. protected Object clone() throws CloneNotSupportedException

如果子类要支持克隆，子类需要实现Cloneable接口，否则报CloneNotSupportedException

3. public boolean equals(Object obj)


- 指示其他某个对象obj是否与此对象this“相等”。 
- Object中的equals，等价于“==”比较，比较的是对象的地址
- 如果子类需要比较的是属性的内容，那么一定要重写这个方法

4. public int hashCode()
- 在Object中默认这个方法返回的是 和“地址”相关的值
- 如果重写了equals，那么必须重写hashCode方法，而且参与equals比较的属性，一定要参与hashCode的计算
- 它俩的关系：
  - 两个对象的equals()返回true，两个对象的hashCode值？一定相等
    两个对象的hashCode值不相等，两个对象equals方法结果？一定不相等
    两个对象的hashCode值相等，两个对象equals方法结果？不一定相等
    
5. public final Class<?> getClass()
    返回某个对象的运行时类型，而不是编译时类型
  
6. protected void finalize() throws Throwable
    当这个对象被垃圾回收机制回收之前调用，而且只会调用一次

7. public String toString()
  - 在Object中默认返回的是这个对象的运行是类型@这个对象的hash值的十六进制表现形式
  - 子类完全可以重写

8. 剩下的notify,notifyAll和wait在多线程中使用

## 包装类

java.lang

### 装箱与拆箱

- 装箱

  ```java
  //JDK1.5之前手动装箱
  Integer i = new Integer(整数);
  //JDK1.5之后自动装箱
  Ineteger i = 整数;
  ```

- 拆箱

  ```java
  //JDK1.5之前手动拆箱
  Integer i = new Integer(整数);
  int num = i.intValue();
  //JDK1.5之后自动拆箱
  Integer i = new Integer(整数);
  int num = i;
  ```

  

- 原则：只能是对应的包装类和基本数据类型之间进行转换

### 对应的关系

- byte	Byte

- short	Short

- int	Integer

- long	Long

- char	Character

- float	Float

- double	Double

- boolean	Boolean

### 其他方法

- 字符串与基本数据类型的转换

  public static int parseInt(String s)throws NumberFormatException

  - 如果包含字母等非数字字符，会报错

  public static int parseInt(String s, int radix)throws NumberFormatException

  - 可以包含字母，但是要在基数范围内
  - 例如基数radix是20，可以包含的范围是0-9,a,b,c,d,e,f,g,h,i,j

  public static Integer valueOf(String s) throws NumberFormatException

  public static Integer valueOf(String s,int radix) throws NumberFormatException

- 像Integer中

  public static String toBinaryString(int i)	二进制形式

  public static String toOctalString(int i)	八进制形式

  public static String toHexString(int i)	十六进制形式

- 像Character中

  public static char toLowerCase(char ch)	转小写

  public static char toUpperCase(char ch)	转大写


### 包装类对象的缓存问题（常量对象）

- Byte,Short,Integer,Long	-128~127

- Float,Double	没有缓存

- Character	0~127

- Boolean true	false

## java.lang.String

### 字符串类型的特点

1、不能被继承
	- 因为String是final修饰的类
2、字符串对象是常量对象，一旦创建就不能修改，一旦修改就是新对象
3、因为字符串对象是常量对象，那么可以共享，字符串常量对象是在常量池中
	- 常量池在哪里
		- JDK1.6，方法区
		- JDK1.7，堆
		- JDK1.8，元空间
4、任何字符串字面量都是String的对象
5、字符串底层使用字符数组存储
6、字符数组是private final修饰符

### 拼接和比较

1、创建对象的个数

```java
//一个，在常量池
String str1 = "hello";
String str2 = "hello";
```

```java
//三个 一个在常量池 两个在堆中
String str1 = new String("hello");
String str2 = new String("hello");
```

2、拼接和比较

  - 原则：+两边都是常量，结果也是常量，+两边有一个是变量，结果就不是常量，在堆中，如果结果使用了intern()，那么是常量

```java
@Test
public void test3(){
    String str1 = "hello";
    String str2 = "java";
    String str3 = "hellojava";
    String str4 = "hello" + "java";//常量与常量拼接，还是常量
    String str5 = "hello" + str2;//常量与变量拼接，结果在堆中
    String str6 = str1 + str2;//变量与变量拼接，结果也在堆中
    System.out.println("str3 == str4  " + (str3 == str4));//true
    System.out.println("str3 == str5  " + (str3 == str5));//false
    System.out.println("str3 == str6  " + (str3 == str6));//false
    final String str7 = "hello";
    final String str8 = "java";
    String str9 = str7 + str8;//常量与常量拼接
    System.out.println("str3 == str9   " + (str3 == str9));//true
    String str10 = (str1 + str2).intern();//intern()的结果放常量池
    System.out.println(str3 == str10);//true
}
```

### 常用的方法
1、基本方法

1. int length()
	返回字符串的长度，即字符的个数
	
2. 字符串的比较
	boolean equals(String other)
      - this和other进行内容比较
      - 对Object的equals进行重写
      - 严格区分大小写

	boolean equalsIgnoreCase(String anotherString)
      - this和anotherString进行内容比较
      - 不区分大小写

	自然排序
	public int compareTo(String anotherString)
		如果是ASCII范围内，按照ASCII值的顺序
	定制排序
	java.text.Collator
```java
String str3 = "中国";//Z
String str4 = "美国";//M
//如果想要按照字典顺序
//找定制排序，实现了java.util.Comparator接口，重写int compare(String s1,String s2)
//java.text.Collator
Collator c = Collator.getInstance();
int result = c.compare(str3, str4);
System.out.println(result);//中 > 美
```
3. 去掉前后空格
	- String trim()

4. 转大小写
	- String toUpperCase()
	- public String toLowerCase()
5. 是否是空字符串

```java
//方式一
"".equals(字符串)
//方式二
 isEmpty()
```
2、和字节相关

  - 编码：把字符串转成字节数组

    - byte[] getBytes()	平台默认编码方式进行编码

    - byte[] getBytes(字符编码方式)	按照指定的编码方式

  - 解码：把字节数组转成字符串
    - new String(byte[])
    - new String(byte[],int offset, int length)
    - new String(byte[], 字符解码方式)
    - ....
  - 乱码
    （1）编码方式与解码方式不一致
    （2）缺字节
    3、和字符相关
  - 把字符串转字符数组
    - char[]  toCharArray()

  - 把字符数组转字符串
    - new String(char[])
    - new String(char[],int offset, int count	)
    - ....

  - 取指定位置的字符
    - char charAt(index)

4、是否以xx开头和结尾
    - boolean startsWith(xx)
    - boolean endsWith(xx)

5、字符串截取
  - String subString(int start)	从[start,最后]
  - String subString(int start, int end)	从[start,end)

6、拆分
 String[]  split(支持正则)

7、查找
  - 是否包含	boolean contains(子串)
  - 查找索引位置
    - int indexOf(xxx)
      - 如果存在返回索引
      - 如果不存在返回-1
    - int lastIndexOf(xx)

8、替换
  - String  replace(目标子串， 新子串)
  - String  replaceAll(目标子串， 新子串)	支持正则
  - String  replaceFirst(目标子串， 新子串)

## java.lang.StringBuffer和java.lang.StringBuilder

StringBuffer是JDK1.0就有，是线程安全的

StringBuilder是JDK1.5引入，是线程不安全

和String的区别

（1）String对象是常量对象，是不能修改的，StringBuffer和StringBuilder是字符串缓冲区，可变字符序列，可以修改的
  - String一旦涉及修改就产生新的String对象
  - StringBuilder和StringBuffer不会产生新的StringBuilder和StringBufffer对象

（2）赋值的方式
  - 只有String支持，String str  = "xxx";

（3）拼接
  - String支持+ 每一次拼接产生新对象，浪费空间和时间

  - append 不会产生新对象

### 常用的方法
（1）拼接
  - append(xx)
  - 支持连写 sBuilder.append(xx).append(yyy).append(zzz)...

- （2）插入
  - insert(index，xx）

- （3）删除
  - delete(start, end)

- （4）替换
  - setCharAt(index, char)

- （5）反转
  - reverse()
- ....

## JDK1.8之前日期时间

### java.util.Date

（1）两个构造器
  - new Date()
    - 获取当前系统日期时间
  - new Date(long 毫秒)
    - 根据毫秒数获取日期时间对象

（2）把某个日期时间对象转成毫秒数
  - long  getTime()

### java.lang.System

- long System.currentTimeMillis()

### java.util.Calendar

（1）获取实例对象
  - Calendar.getInstance()
    - 获取平台默认
  - Calendar.getInstance(时区，语言环境)

（2）get(常量字段）
  - YEAR
  - MONTH
  - ....

### java.text.DateFormat及其java.text.SimpleDateFormat

（1）构造器
  - SimpleDateFormat sf = new SimpleDateFormat("模式");

（2）把日期转成字符串
  - public final String format(Date date)

- （3）把字符串转成日期
  - public Date parse(String source)

## JDK1.8日期时间

### 相关的包

### 本地日期时间

- java.time.LocalDate
- java.time.LocalTme
- java.time.LocalDateTime
- 对应旧版本java.util.Calendar
- 方法列表

![](D:\Study\自学\笔记\img\屏幕截图 2022-04-20 222432.png)

### 日期时间格式化
- java.time.format.DateTimeFormatter
  - format 把日期时间对象转字符串
  - parse 把字符串转日期时间对象

- 三种形式获取DateTimeFormatter对象


```java
//标准格式的常量对象
LocalDate date = LocalDate.now();
System.out.println(date.format(DateTimeFormatter.ISO_DATE));
DateTimeFormatter formatter = DateTimeFormatter.ISO_DATE;
String format = formatter.format(LocalDate.now());
```
```java
//Style    
DateTimeFormatter dt = DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL);
String string = dt.format(LocalDate.now());
/*- FormatStyle.FULL
  - 日期
- FormatStyle.LONG
  - 日期时间
  - 日期
  - 时间
- FormatStyle.MEDIUM 
  - 日期
  - 日期时间
  - 时间
- FormatStyle.SHORT
  - 日期
  - 日期时间
  - 时间*/
```

```java
//自定义格式
DateTimeFormatter op = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
System.out.println(op.format(LocalDateTime.now()));
```

### 日期的间隔

- Period

### 时间的间隔

- Duration

## java.lang.Math

## 排序

java.lang.Comparable

java.lang.Comparator

# 23种设计模式

## 设计模式

套路
框架
- 设计模式 + 反射 + 泛型 + 注解/配置文件等

## 单例设计模式

### 最简单，考的最多的一个设计模式

### 要点

（1）构造器私有化
（2）在本类中创建这个唯一的实例

### 分类

```java
//饿汉式
//形式一
class Hungry{
    public static final Hungry INSTANCE = new Hungry();
    private Hungry(){
    }
}

//形式二
class Hungry{
    private static final Hungry INSTANCE = new Hungry();
    private Hungry(){
    }
    public static Hungry getInstance(){
        return INSTANCE;
    }
}
```
```java
//懒汉式
//形式一：（有线程安全问题）
class Lazy{
    private static Lazy instance;
    private Lazy(){
    }
    //延迟创建对象
    public static Lazy getInstance(){
        if(instance == null){
            instance = new Lazy();
        }
        return instance;
    }
}
//形式二：解决线程安全问题
//懒汉式
class Lazy{
    //2、在类中声明一个静态变量用来存储这个唯一的对象
    private static Lazy instance;
    //1、构造器私有化
    private Lazy(){
    }

    //3、提供一个静态方法用来返回这个唯一的对象，并在第一次获取这个对象时，创建这个唯一的对象

    /*synchronized public static Lazy getInstance(){
		if(instance == null){
			instance = new Lazy();
		}
		return instance;
	}*/
    //考虑的性能
    public static Lazy getInstance(){
        if(instance == null){//为了效率高
            synchronized(Lazy.class){
                if(instance == null){//双重条件判断，更安全
                    instance = new Lazy();
                }
            }
        }
        return instance;
    }
}

```

```java
//枚举式
enum Single{
    INSTANCE
}
//特殊的饿汉式
```

## 模板设计模式（识别）

### 使用的情景

- 当某个功能在实现时，它的主体的算法结构是确定的，只是其中的某一个或几个步骤无法给出具体的实现，那么这个时候，把这个或几个的步骤抽取成抽象方法，由子类去给出具体的实现，那么子类继承父类时，既可以保留父类的主体算法结构，又可以对这几个抽象部分给出具体的实现

### 示例代码

```java
/*例如：计算某段代码的执行时间
    算法结构：
    1、获取开始时间
    2、执行代码
    3、获取结束时间
    4、计算差值*/
public abstract class CalTime{
    public final long getTime(){
        //1、获取开始时间
        long start = System.currentTimeMillis();
        //2、执行代码
        doWork();
        //3、获取结束时间
        long end = System.currentTimeMillis();
        //4、计算差值
        return end - start;
    }
    protected abstract void doWork();
}
class MyCalTime extends CalTime{
    public void doWork(){
        .......
    }
}
```

## 工厂设计模式

### 为什么要用工厂模式

- 把创建对象者与对象的使用者分离（把创建者与使用者分离）
- 解耦合

### 形式

1、简单工厂模式

- 特点
  一个工厂生产所有产品
- 缺点
  增加一个新产品， 就要修改工厂类代码
  违反了“对扩展开发，对修改关闭”的面向对象的设计原则
- 优点
  类少，简单
- 示例代码
```java
//1、产品的接口
interface  Car{
    void run();
}
//2、各种产品
class Benz implements Car{
    public void run(){
        ...
    }
}
class BMW implements Car{
    public void run(){
        ...
    }
}
//3、工厂
class SimpleFactory {
    public static Car getCar(String type){
        if("benz".equals(type)){
            return new Benz();
        }else if("bmw".equals(type)){
            return new BMW();
        }
        return null;
    }
}
//4、使用者
Car  car = SimpleFactory.getCar("benz");
car.run();
```
2、工厂方法模式
- 特点
  一个产品配一个工厂
- 缺点
  类比较多
- 优点
  增加一个新产品，对原来的代码不需要修改，只需要增加对应的工厂即可
- 示例代码

3、抽象工厂设计模式

# 面向对象高级特性

## 抽象

### 为什么会有抽象类

- 当子类中都有一个共同的方法，每一个子类都有不同的实现，在父类中又要体现所有子类的共同的特点，所以要体现有这个方法，但是在父类中又无法给出具体的实现，那么这个时候就需要把这个方法声明为抽象的，而包含抽象方法的类，必须是抽象类
- 某个父类仅仅是表示一个抽象的概念，不希望它被实例化，这个时候父类中可能没有抽象方法，但是我们也把它声明为抽象类

### 如何声明抽象类

```java
[public/缺省] abstract class 类名{
}
```

### 如何声明抽象方法

```java
[public/protected/缺省]  abstract   返回值类型   方法名([形参列表]);
//抽象方法是不能private,static,final修饰的
```

### 抽象类的特点

（1）抽象类不能实例化
（2）抽象类可以包含抽象方法，也可以没有抽象方法。
如果一个类有抽象方法，那么这个类必须是抽象类，
如果一个抽象类没有抽象方法，那么它的用意是不想实例化，用它仅仅表示一个抽象的概念。
（3）抽象类生来就是用来被继承的，那么子类在继承它的时候，必须重写（实现）抽象父类的抽象方法，否则该子类也得是抽象类。
（4）抽象类的变量与子类的对象构成多态引用。
（5）抽象类除了不能实例化，可以包含抽象方法，其他的和非抽象类是一样的，
可以有成员变量（类变量、实例变量）、构造器、代码块（静态代码块和非静态代码块）
方法（静态方法、非静态方法）

### 抽象类不能实例化，为什么要有构造器呢？

- 子类在继承该类时，一定要调用它的构造器，为属性初始化。

  因为构造器的作用有两点

  （1）和new一起创建对象

  （2）为属性初始化

## 接口

### 接口即代表行为标准，功能标准

### 如何声明一个接口？

```java
[public/缺省] interface 接口名{
}
```

### 如何实现接口？

```java
[public/缺省] class 子类名 [extends 父类名] implements  接口名1，接口名2。。。{
//要实现接口的所有抽象方法
}
```

### 接口的特点

- JDK1.7：
  （1）接口不能实例化
  （2）接口只能有全局静态的常量和公共的抽象方法
  （3）接口中不能有构造器，因为它没有属性需要初始化，又不能创建对象
  （4）接口生来用来被实现的，那么实现类（像子类）在实现它时，必须实现（和重写要求一样）接口的所有抽象方法，否则该实现类也得是抽象类
  （5）一个类可以同时实现多个接口
  （6）一个类还可以继承父类又实现接口，但是必须先继承后实现
  （7）接口与接口之间是继承关系，一个接口可以继承多个接口
  （8）接口与实现类的对象之间构成多态引用

- JDK1.8

  - 其他的和JDK1.7一样，不一样的是：
    JDK1.8之后，接口中除了全局静态的常量和公共的抽象方法以外，可以有静态方法和默认方法

    - 接口中的静态方法

      - 当接口的所有实现类，对这个方法的实现是一样的，这个方法就设计在接口中，设计为静态方法

      - 如何调用

        接口名.方法

    - 接口中的默认方法

      - 当接口的大多数实现类，对这个方法的实现是一样，那么这个方法的实现就可以在接口中提供默认实现，如果某个实现类觉得他不合适，只需要重写它即可

      - 如何调用

        - 实现类外

          - 实现类对象.方法

        - 实现类中

          - 如果实现类要重写该默认方法，但是又想调用接口中的默认实现
          - 接口名.super.方法

      - 什么情况下需要重写

        - 接口中的默认实现不适合该实现类

        - 必须重写

          一个类同时实现了多个接口，而多个接口中都相同的默认方法（方法名和形参列表都相同），这个时候实现类必须做出选择，要重写，如果需要保留其中一个的话，通过接口名.super.方法，保留它的默认实现

      - 类优先原则

        - 当一个类继承了父类，又实现了接口，而且父类中的某个方法与接口中的默认方法一样（方法名和形参列表），默认保留的是父类中的方法实现

## 枚举

### 枚举是指某个类型的对象是有限个，在类型中一一创建并列举它的对象

### JDK1.5之前，如何解决
（1）构造器私有化
（2）通过常量的方式创建好所有对象

```java
//示例
class Week{
	public static final Week MONDAY = new Week();
	public static final Week TUESDAY = new Week();
	public static final Week WEDNESDAY = new Week();
	public static final Week THURSDAY = new Week();
	public static final Week FRIDAY = new Week();
	public static final Week SATURDAY = new Week();
	public static final Week SUNDAY = new Week();
	private Week(){
	}
}
Week w = Week.MONDAY;
```



### JDK1.5之后，如何解决

- 如何声明

```java
//1
[修饰符] enum  枚举类型名{
    常量对象列表
}
//2
[修饰符] enum  枚举类型名{
    常量对象列表;
    其他成员;
}
```

- 特点

  （1）枚举类型中的构造器都是私有化

  （2）常量对象列表必须在首行，如果常量对象列表后面还有其他的代码，那么要用;结束

  （3）枚举类型不能继承别的类型，因为它默认继承java.lang.Enum

  - 它有一些方法

    - name()	返回常量对象名

    - ordinal()返回常量对象的序号，从0开始

    - 实现了java.lang.Comparable接口，重写compareTo()，按照常量对象的顺序排序

      如果自己的枚举类中不适合，可以重写

    - toString()

      返回常量对象名

      可以重写

  - API中没有的方法

    - 枚举类型名.values()

      返回枚举常量对象组成的数组

    - 枚举类型名.valueOf（常量对象的名称）

      返回某一个指定的对象

  （4）switch对枚举加入支持

  ```java
  switch(枚举类型表达式){
      case 常量对象名1:
          语句;
          [break;]
      case 常量对象名2:
          语句;
          [break;]
      case 常量对象名3:
          语句;
          [break;]	
      default:
          语句;
          [break;]		
  }
  ```

## 注解

### 概念

- 代码级别的注释
- 给代码读取的注释

  不同普通的注释（给人看的）

  - 单行注释
  - 多行注释

### 四种

1、编译器的格式检查
（1）@Override：告知编译器对该方法按照“重写”的要求进行格式检查
（2）@SuppressWarnings：告知编译器抑制警告
（3）@Deprecated：告知编译器某个元素是已过时，有人用了就弹出警告

2、文档注释
（1）@version
  - 指定当前版本
（2）@author
  - 指定作者
（3）@since
  - 指定从哪个版本开始
（4）@see
 另请参阅
（5）param
  - 指定当前方法的形参信息
  - 可以多个
  - 只有方法有形参才能标记
  - 格式：
    - @param  形参名  形参类型   形参的描述信息
    （6）@return
  - 指定当前方法的返回值信息
  - 一个方法只能有一个，如果方法是void，就不能标记@return
  - 格式
    - @return  返回值的类型  返回值的描述
    （7）@exception
  - 指定当前方法抛出异常的信息
  - 可以多个
  - 只有方法抛出异常才能标记
  - 格式
    - @exception  异常类型  异常的描述
- 结合javadoc.exe
3、JUnit的单元测试
- 白盒测试，程序员自己的测试，在程序员知道当前的代码的功能的
- @Test
  - 加在方法上
  - 这个方法必须是公共的，无参，无返回值，不能是static
- @Before
  - 在@Test标记的方法之前运行
- @After
  - 在@Test标记的方法之后运行
  4、各大框架等替代配置文件

### 注解的三个部分

1、声明
一般都是别人声明好的

2、使用

3、读取

- 例如：@Override等，由javac.exe
- 例如：@author,@param等，由javadoc.exe
- 例如：@Test等，由JUnit相关的类读取
- 例如：@WebServlet等，由Tomcat读取
- ...
- 如果自己要读取，通过反射，而且只能读取@Retention(RetentionPolicy.RUNTIME)

### 注解的声明

（1）无参
- 声明格式
```java
@元注解
[修饰符]  @interface  注解名{}
```
- 使用格式
  @注解名

（2）有参
- 声明格式
```java
@元注解
[修饰符]  @interface  注解名{
    配置参数
}
```
  - 配置参数
    - 格式
      数据类型  参数名();
    - 一个注解可以有多个配置参数
    - 配置参数可以有默认值

      数据类型  参数名() default 默认值;

    - 配置参数的类型有要求

      类型只能是八种基本数据类型、String类型、Class类型、enum类型、Annotation类型、以上所有类型的数组

- 使用格式

  @注解(参数赋值)

  - 如果配置参数有默认值，那么可以在使用时不需要赋值
  - 如果配置参数只有一个，而且名称是value，那么可以在赋值时省略value=
  - 参数赋值的格式

    - 参数名 = 参数值
    - 如果多个使用,分割
    - 如果配置参数的类型是数组类型

      - 如果只有一个元素，那么可以省略{}
      - 如果是多个元素，那么需要{}

### 元注解

- @Target
  - 指定某个注解它的使用目标位置
  - 如何指定它
    - 它配置参数的类型是一个枚举数组
      - ElementType枚举类型
        - 常量对象有：TYPE, FIELD,METHOD等
    - 配置参数的名称是value
    - 如果只有一个
      - @Target(ElementType.METHOD)
    - 如果是多个
      - @Target({ElementType.METHOD,ElementType.FIELD,。。。。})
- @Retention
  - 指定某个注解的生命周期，可以保留到什么阶段
  - 如何指定它
    - 它的配置参数的类型是一个枚举类型
      - RetentionPolicy类型
        - 常量对象有三个
          - SOURCE,CLASS,RUNTIME
    - 配置参数的名称是value
    - @Retention(RetentionPolicy.RUNTIME)
- @Documented
  - 表示是否javadoc读取
- @Inherited
  - 是否被子类继承
- 在java.lang.annotation包

# 异常

## 1、什么是异常

### 哪些不是异常

- 语法错误
- 逻辑错误

### 不可预知的非正常的情况

- 例如：网络中断，用户不合适的输入，硬盘已满，操作系统崩溃，内存溢出等

## 2、异常的体系结构

### java.lang.Throwable

所有异常和错误的超类
（1）只有这个类型或它子类的对象才能被“抛出”
（2）只有这个类型或它子类的对象才能被“捕获”

### 分为两大类

![](D:\Study\自学\笔记\img\分为两大类.png)

## 异常的处理机制

### 1、过程描述

- Java虚拟机会在发生异常的那句代码的位置，创建一个异常的对象，并且抛出，这个时候，它会检测有没有try..catch，如果有对应的catch，那么程序正常运行，如果没有合适的catch，会被往上抛出，如果一路上都没有被catch，最终会导致程序终止运行。

### 2、两种方式

- try...catch

```java
try{
    可能发生异常的代码
}catch(异常的类型 e){
    捕获该异常后如何处理
}catch(异常的类型 e){
    捕获该异常后如何处理
}catch(异常的类型 e){
    捕获该异常后如何处理
}
...
finally{
    不管是否发生异常都要执行的代码
}
下面的代码
```

  - 执行特点

  （1）如果try中没有异常，那么如果有finally，就执行finally，然后再执行[下面的代码]

  （2）如果try中有异常，try剩下的代码就不执行了，直接去找对应的catch，如果有对应的catch，就执行，然后如果有finally，就执行finally，然后再执行[下面的代码]

  （3）如果try中有异常，try剩下的代码就不执行了，直接去找对应的catch，如果没有对应的catch，然后如果有finally，就执行finally，[下面的代码]就不执行，抛出上级

- 语法特点

	- 可能没有catch
	- 可能没有finally
	- 多个catch异常类型的顺序是"子上父下"

- return和finally并存如何执行

	- 如果finally中有return，那么一定是从finally中返回
	- 如果finally中没有return，会先执行finally中的语句，然后return结束，但是返回的值是在执行finally之前就赋好值的

- throws

  - 语法结构

    [修饰符] 返回值类型  方法名(形参列表) 抛出的异常列表

  - 注意

    (1)throws后面可以是多个异常，不分顺序

    (2)如果方法重写

    重写方法抛出的异常<=被重写方法抛出的异常类型

## 自定义异常

### 1、自定义异常一定要继承Throwable或它的子类

- 原因是因为

  （1）只有这个类型或它子类的对象才能被“抛出”

  （2）只有这个类型或它子类的对象才能被“捕获”

### 2、一般来说声明两个或以上的构造器
（1）无参构造
（2）异常类型(String message)

### 3、都需要序列化

### 4、自定义异常的对象只能自己new并手动抛出，使用throw关键字

当然抛出后，就可以通过throws继续往上抛或使用try..catch处理

## 异常的关键字

### try

尝试执行某些代码，看是否发生异常

### catch

捕获异常

### finally

不管是否发生异常都要执行的代码

### throw

- 手动抛出异常

  - 系统预定义异常
  - 用户自定义异常

### throws

把异常抛出上级

## 异常

### 抛
1、JVM new并且抛出
2、自己new并通过throw抛出

### 处理
1、throws继续抛给上级
2、当下处理try..catch

### 捕获
- try..catch

# 集合

## 概念

### 集合是一个容器

- 是一个用来装对象的容器

### 数据结构

1、物理结构
- 数组也是一个容器
  - 缺点
    （1）长度固定
    （2）无法直接获取有效元素的个数
  - 在实际开发中，基本数据类型一般用数组，引用数据类型一般用集合
  - 数组是依据“数组名+下标”来确定某个元素，数组名中存储的是数组的首地址

- 链表
  - 不仅仅存储数据，还有存储前/后元素的引用

2、逻辑结构
  - 动态数组
    底层是数组，可以通过扩容的方式实现动态数组
  - 链表
    结合Node

    ```java
    //双向链表
    class Node{
        Node pre;
        Object data;
        Node next;
    }
    //单向链表
    class Node{
        Object data;
        Node next;
    }
    ```

  - 树

    - 经典的代表

      ```java
      //二叉树
      class Node{
      Node left;
      Object data;
      Node right;
      }
      ```

      

  - 栈

    - 先进后出
    - 添加的顺序
    - 出栈的顺序

  - 队列

    - 先进先出
    - 添加的顺序
    - 出队列的顺序

  - 堆
  - ....

## Collection

### java.util.Collection是一个接口，是个根接口

### Collection没有直接的实现类，它有两个子接口

- java.util.List

  *请描述List的各种实现类的区别*

  *ArrayList：动态数组（JDK1.2），每次扩容为原来的1.5倍，支持Iterator和foreach迭代，线程不安全的*

  *Vector：旧版的动态数组（JDK1.0），默认每次扩容为原来的2倍，支持旧版Enumeration，还支持Iterator和foreach迭代，线程安全的*

  *LinkedList：双向链表，在添加和删除时效率比较高，不需要移动大量的元素，只需要修改前后元素引用关系*

  *Stack：Stack是Vector的子类，具有后进先出的特点*

  - 有序的（添加顺序），可重复的

    - java.util.Vector动态数组

      - JDK1.0就有，最早
      - 支持Enumeration迭代方式(当然也支持Iterator，foreach)

      - 线程安全的
      - 扩容算法

        - 如果没有指定扩容参数，那么默认扩大为原来的2倍(默认初始容量是10)

        - 如果指定了扩容参数，那么就按照指定参数值进行扩容

    - java.util.ArrayList动态数组

      - 相对Vector来说新一点
      - 只支持Iterator，foreach
      - 线程不安全的
      - 扩容算法(扩大为原来的1.5倍)

    - java.util.LinkedList双向链表

      - 相对于动态数组来说的优势(在插入和删除操作比较频繁时，链表的方式效率更高)

      - 相对于动态数组来说的劣势(如果根据索引信息来查找的话，每次都要现统计)

    - java.util.Stack

      - 是Vector的子类
      - 特征的方法

        - peek()

          查看栈顶的元素，但不移除

        - pop()

          获取栈顶的元素，并移除

        - push()

          压入栈，添加的位置在栈顶

        - search(Object)

          返回位置，以 1 为基数

      - 逻辑结构

      - 底层

        - 数组
        - 每次添加到后面，栈顶是数组的后面[size-1]号元素，栈底是数组的[0]元素

  - 列表，序列
  - 补充Collection的方法

    - 和index相关的方法

       (1)添加
      - add(int index, E element) 
      - addAll(int index, Collection<? extends E> c) 

      （2）删除
      - remove(int index) 

      （3）查找
      - indexOf(Object o) 
      - lastIndexOf(Object o) 
      - get(int index) 

      （4）替换
      - set(int index, E element) 

      （5）截取
      - subList(int fromIndex, int toIndex)

- java.util.Set

  5、请描述Set的各种实现类的区别

  HashSet：无序的，不可重复的，依据元素的hashCode()和equals方法

  HashSet底层实现是HashMap，它的value是一个Object的常量对象

  TreeSet：不保证添加顺序，但是会按照元素的“大小”顺序进行排列，不可重复，

  依据元素的自然排序Comparable（compareTo())或定制排序Comparator(compare())规则进行排序

  TreeSet底层实现是TreeMap，它的value是一个Object的常量对象

  LinkedHashSet：是HashSet的子类，除了有HashSet的特点，它还要在HashSet基础上维护元素的添加的顺序，所以在添加和删除时比HashSet慢一点

  LinkedHashSet的底层实现是LinkedHashMap，它的value是一个Object的常量对象

  - 无序的（添加顺序），不可重复的

    - java.util.HashSet

      - 无序，不可重复
      - 依赖于元素的hashCode和equals方法
      - equals和hashCode

        - hash值不同，这两个对象一定不同，可以不调用equals
        - equals如果相同，hashCode一定相同
        - hash值相同，这两个对象不一定相等，所以一定要调用equals方法进行确认

    - java.util.TreeSet

      - 不按添加顺序，但是按照元素“大小”顺序存储，不可重复
      - 不可重复，依据元素是否“大小相等”

        调用元素的compareTo或定制比较器的compare

      - 添加到TreeSet的元素一定要支持可比较大小，可排序

        - 自然排序

          - 要求元素类型本身要实现java.lang.Comparable接口，并重写int compareTo(Object)方法

        - 定制排序

          - 要为TreeSet指定一个定制比较器对象

            TreeSet set = new TreeSet(定制比较器对象);

    - java.util.LinkedHashSet

      - 比较HashSet多了一个顺序维护，所以在添加和删除时，比HashSet效率低，遍历查找时效率高
      - 继承HashSet

  - 底层实现

    - HashSet

      HashMap

    - TreeSet

      TreeMap

    - LinkedHashSet

      LinkedHashMap

  - Set的元素其实也是一对，只不过它的value是共享同一个常量对象Object对象

### 遍历

（1）直接foreach

- 语法结构

```java
for(集合的元素类型  element : 集合名){
}
```

- 在遍历时，效率高，但是不适用于遍历的同时对集合进行修改，特别是影响集合元素个数的操作

（2）Iterator迭代器

- 语法结构

```java
Iterator iter = 集合对象.iterator();
while(iter.hasNext()){
    Object element = iter.next();
    //可以使用iter.remove()进行移除
}
```

- Iterator是一个接口

  在每一类集合中，都有自己的实现类，通过内部类的形式来实现Iterator接口

### 继承关系图

![](D:\Study\自学\笔记\img\屏幕截图 2022-04-21 115430.png)

### Collection的常用方法

（1）添加
- add(Object obj)
  添加一个元素到集合中
- addAll(Collection other)
  把other集合中的元素一一添加到当前集合中，一次添加多个
  

（2）删除
- remove(Object obj)
  删除一个元素
- removeAll(Collection other)
  从当前集合中删除它俩的交集
  - this -  this ∩ other

（3）查找
- contains(Object obj)
  在当前集合中查找一个元素
- containsAll(Collection c)
  判断c是否是当前集合的子集

（4）其他
- size()
  获取有效元素的个数
- retainsAll(Collection other)
  把this ∩ other赋值给当前集合
  - this =  this ∩ other

（5）遍历
- Iterator iterator()
- Object[] toArray()

## Map

### Map的特点

- Map的元素，即存储的映射关系（key,value），其类型是Entry类型，它是Map的内部子接口，在各种Map的实现类中，都用内部类的方式来实现Entry接口
- Map的key不可重复，而且一旦添加到map中，key不建议修改，特别是参与hashCode和equals方法的属性，或参与compareTo或compare方法比较的属性

### Map的常用方法

- 常用的方法

1、添加
    - put(key,value)
    - putAll(Map)

2、有效键值对数
    - size

3、根据key获取value
    - get(key)

4、是否包含某个key/value
    - containsKey()
    - containsValue()

5、删除
    - remove(key)

6、和迭代相关
    - 遍历所有的key
      Set  keySet()
    - 遍历所有的value
      Collection values()

    - 遍历所有的映射关系
      Set  entrySet()
      Set的元素是Entry类型

### Map的常见实现类
- Hashtable
  JDK1.0就有的，属于旧版HashMap，线程安全的

- HashMap
  它的key不可重复的，依据key的hashCode()和equals()方法，线程不安全的
  JDK1.7时底层实现是数组+链表
  JDK1.8时底层实现是数组+链表+红黑树

- TreeMap
  它的key不可重复的，按照key的“大小”顺序进行排列,
  依据key的自然排序Comparable（compareTo())或定制排序Comparator(compare())规则进行排序

- LinkedHashMap
  它是HashMap的子类，在HashMap的基础上同时要维护添加的顺序

- Properties
  Properties是Hashtable的子类，它的key和value的类型都是String类型

### 高频面试题：HashMap的底层实现过程
- JDK1.7时底层实现是数组+链表
  当我们要添加一个新的映射关系时，
      (1)先取出key，算出它的hash值
      (2)如果数组是空的，会先建立一个长度为16的数组table
      (3)如果数组不为空，这个时候要判断数组的长度是否达到临界点（数组长度*0.75），如果已经达到临界点，应该先对数组进行扩容，扩大为2倍,一旦扩容，要重头开始（以前元素要重新排序位置，对新添加的映射关系也要重写计算key的hash值，和index）
      (4)会根据key的hash值与table数组的长度做一个“按位与&”的运算，计算出要存储的下标index
      (5)先判断table[index]是否为空，如果为空，直接放进去，放进去之前会构建一个Entry类型对象
      (6)如果table[index]不是空的，那么调用key的equals方法与table[index]的key做比较，如果table[index]下面还有链表，可能需要与table[index]下面的链表的元素一一比较，直到遇到了equals为true或都不相同
      (7)如果有一个equals返回true，那么就把value给替换
      (8)如果equals都不相等，那么把当前映射关系构建的Entry对象，放在此链表的表头，把原来的对象作为我的next
  
- JDK1.8时底层实现是数组+链表+红黑树

  - 		当我们要添加一个新的映射关系时，
      (1)先取出key，算出它的hash值
      (2)如果数组是空的，会先建立一个长度为16的数组table
      (3)如果数组不为空，这个时候要判断数组的长度是否达到临界点（数组长度*0.75），如果已经达到临界点，应该先对数组进行扩容，扩大为2倍,一旦扩容，要重头开始（以前元素要重新排序位置，对新添加的映射关系也要重写计算key的hash值，和index）
      (4)会根据key的hash值与table数组的长度做一个“按位与&”的运算，计算出要存储的下标index
      (5)先判断table[index]是否为空，如果为空，直接放进去，放进去之前会构建一个Entry类型对象
      (6)如果table[index]不是空的，那么调用key的equals方法与table[index]的key做比较，如果table[index]下面有树或者链表，可能需要与table[index]下面的链表或树的元素一一比较，直到遇到了equals为true或都不相同
      (7)如果有一个equals返回true，那么就把value给替换
      (8)如果都不相等，如果现在已经是树，就直接添加到该树的叶子节点上。
      (9)如果都不相等，如果现在不是树，而是链表，看当前链表的长度是否达到8个，如果没有达到8个，直接添加到链表的尾部
      (10)如果已经达到8个，此时要检查数组table的长度是否达到64，如果没有达到64，先扩容，一旦扩容，一切从头开始
      (11)如果达到64，把该链表变成一颗红黑树
  - 		什么时候树会变回链表？
      每次进行resize()，会检查树的叶子节点的总数是否<6个，如果<6个，会把这个红黑树变回链表

## 集合框架图

![](D:\Study\自学\笔记\img\屏幕截图 2022-04-21 120129.png)

## 集合工具类

### java.util.Collections

- 操作集合的各种静态方法

  1、Collections.addAll(Collection, T... elements)

  2、binarySearch(List, T target)

  - 对List的元素类型有要求，必须支持可比较大小

  3、max/min(Collection)

  - 对Collection的元素类型有要求，必须支持可比较大小

  4、sort(List)

  - 元素必须实现Comparable

  5、sort(List,Comparator)

  - 按照指定比较器进行排序

  6、如果想要获得线程安全的集合对象

  - synchronizedXXX(集合)

  7、。。。。

# 泛型

## 概念

类型参数，参数化的类型

比喻：标签

## 形式

### 1、泛型类、泛型接口

- 语法格式

```java
[修饰符]  class/interface  类名/接口名<类型参数列表>{
}
```

  

  - 多个之间使用,分割
  - 类型参数习惯命名

    - 原则：尽量见名知意，尽量是1个大写字母，或大写字母加数字
    - E Element

    - K Key

    - V Value

    - T Type

    - T1,T2
    - U1,U2
    - R ReturnType

- 注意

  （1）泛型形参由泛型实参决定

  - 在使用这个泛型类时


```java
//（1）创建对象
ArrayList<Student> list = new ArrayList<Student>();
//（2）继承类或实现接口
class Student implements Comparable<Student>
```

  （2）泛型实参必须指定为引用数据类型，不能是基本数据类型

  （3）泛型形参在声明它的类或接口中，当做某种已知的类型来使用的，可以用它声明属性、方法的形参类型，方法的返回值类型，方法的局部变量类型等

  （4）泛型形参不能用于

  - 不能作为异常的类型
  - 不能用于静态成员上面

  （5）泛型

  - 不能用于创建数组对象

### 2、泛型方法

- 语法格式

  - [修饰符]  <类型参数列表>  返回值类型   方法名(形参列表)

- 泛型方法可以是静态方法，也可以是非静态方法
- 静态方法如果要用泛型，只能使用泛型方法的形式
- 泛型方法的类型形参只适用于当前方法，和别的方法无关
- 泛型方法的泛型形参由调用该方法时实参的类型决定

  - 此时实参，即决定了泛型方法形参的值，又决定了泛型方法形参的类型

- 泛型方法的泛型形参也不能是指定为基本数据类型，可以用它的包装类，也不能用于异常类型

## 泛型的通配符

### 1、?

- 代表任意类型

  如果是集合，例如ArrayList<?>，这样的集合不能添加元素

### 2、?  extends 父类

- 上限

  - ?代表父类本身或父类的子类类型可以
  - 如果是集合，例如ArrayList<?  extends 父类>，这样的集合不可以添加

### 3、?  super 子类

- 下限

  - ?代表子类本身或子类的父类类型可以
  - 如果是集合，例如ArrayList<?  super 子类>，这样的集合，可以添加，仅限于添加子类或子类的子类对象

## JDK1.7的简写法

ArrayList<String> list = new ArrayList<>();

# IO流

## IO

### I

- input
- 输入

### O

- output
- 输出

## IO流的分类

### 1、按照IO流的数据流动方向分

- 输入流
- 输出流

### 2、按照IO流的数据处理的最小单位分

- 字节流
- 字符流

### 3、根据IO流的作用分

- 节点流

  例如：文件IO流

  连接文件节点

- 处理流

  - 在节点流的基础上增加其他功能，例如缓冲，编码解码，序列化等

## IO流的四个抽象基类，超级父类

### InputStream

- 字节输入流

### OutputStream

- 字节输出流

### Reader

- 字符输入流

### Writer

- 字符输出流

## 和文件相关的IO流

### 类型

- FileInputStream

  - 文件字节输入流
  - 读取任意类型的文件

- FileOutputStream

  - 文件字节输出流
  - 写数据到任意类型的文件

- FileReader

  - 文件字符输入流
  - 只能读取纯文本文件

    - .java
    - .txt
    - .html
    - .js
    - .css
    - ....

- FileWriter

  - 文件字符输出流
  - 只能把数据保存到纯文本文件中

### 读取

（1）读取一个纯文本文件

```java
//形式一：
//(1)指定要读取的文件
File file = new File("upload/exam.txt");
//(2)创建文本文件的输入流
FileReader fr = null;
try{
    fr = new FileReader(file);
    //(3)在当前程序中创建一个字符数组，用来保存每一次读取的文本信息
    char[] data = new char[10];
    //(4)用来记录每一次读取的字符个数
    int len;
    //(5)用来拼接从文件读取的信息
    StringBuilder sb = new StringBuilder();
    //(6)循环读取
    while((len = fr.read(data))!=-1){
        sb.append(new String(data,0,len));
    }
    System.out.println(sb);
}catch(Exception e){
    //....
}finally{
    //(7)释放资源
    try{
        if(fr!=null){
            fr.close();
        }
    }catch(Exception e){
    }
}
//形式二：
File file = new File("upload/exam.txt");
try(
    FileReader fr = new FileReader(file);
){
    char[] data = new char[10];
    int len;
    StringBuilder sb = new StringBuilder();
    while((len = fr.read(data))!=-1){
        sb.append(new String(data,0,len));
    }
    System.out.println(sb);
}catch(Exception e){
    //....
}
```

（2）读取任意类型的文件

```java
//(1)指定文件
File file = new File(".....");
//(2)创建字节输入流
try(
    FileInputStream fis = new FileInputStream(file);
){
    //(3)创建字节数组，用来存储每次读取的内容
    byte[] data = new byte[1024];
    //(4)用len记录每次读取的字节数
    int len;
    //(5)循环读取
    while( (len = fis.read(data)) !=-1){
        //......
    }
}catch(Exception e){
    //...
}
```



### 保存

（1）把数据保存到一个纯文本文件

```java
//(1)指定要保存的文件
File file = new File("....");
try(
	FileWriter fw = new FileWriter(file);
){
	String info = "....."; //要写入到文件的数据内容
	fw.write(info);
	//或
	char[] data = new char[1024];
	//...把数据保存到data中
	fw.write(data，0，len);
}catch(Exception e){
	//....
}
```

（2）把数据保存到一个任意类型的文件

```java
//(1)指定要保存的文件
File file = new File("....");
try(
    FileOutputSream fos  = new FileOutputSream(file);
){
    byte[] data = ....; //用来存储要输出到文件的内容
    fos.write(data,0 ,len);
}catch(Exception e){
    //....
}
```

### 复制

- 一边读一边写

  - 纯文本文件

```java
    	public static void main(String[] args) {
    		//(1)创建源文件对象
    		File src = new File("1.txt");
    		//(2)创建目标文件对象
    		File dest = new File("2.txt");
    		//(3)创建输入流
    		FileReader fr = null;
    		//(4)创建输出流
    		FileWriter fw = null;
    		try {
    			fr = new FileReader(src);
    //			fw = new FileWriter(dest);//覆盖模式
    			fw = new FileWriter(dest,true);//追加模式
    			//(5)一边读一边写
    			//从fr读一些，就写入fw一些
    			char[] data = new char[6];//1024
    			while(true){
    				int len = fr.read(data);
    				if(len == -1){
    					break;
    				}
    				fw.write(data,0,len);//本次读了几个字符，就写几个字符
    			}
    		} catch (FileNotFoundException e) {
    			e.printStackTrace();
    		} catch (IOException e) {
    			e.printStackTrace();
    		} finally{
    			try {
    				if(fr!=null){
    					fr.close();
    				}
    			} catch (IOException e) {
    				e.printStackTrace();
    			}
    			try {
    				if(fw!=null){
    					fw.close();
    				}
    			} catch (IOException e) {
    				e.printStackTrace();
    			}
    		}
    	}
```

  - 任意类型文件

```java
public static void main(String[] args) {
    // (1)创建源文件对象
    File src = new File("2.jpeg");// 完整的描述：路径+文件名+后缀名
    // (2)创建目标文件对象
    File dest = new File("3.jpg");
    // (3)创建输入流
    // (4)创建输出流
    try (
        FileInputStream fis = new FileInputStream(src); 
        FileOutputStream fos = new FileOutputStream(dest);
    ) {
        byte[] data = new byte[10];
        int len;
        while ((len = fis.read(data)) != -1) {
            fos.write(data, 0, len);
        }
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

### File

- 用来表示一个文件或者一个目录

  实际上是一个抽象的路径名

- 获取文件或目录的一些信息

  （1）获取文件的大小

  - long length()

  - 如果要获取目录的大小，必须编写递归

    ```java
    public long getDirLength(File dir){
        if(dir.isFile()){//如果是文件，直接返回文件的大小
            return dir.length();
        }else if(dir.isDirectory()){
            long sum = 0;
            File[] listFiles = dir.listFiles();
            for (File sub : listFiles) {
                //				sum += 下一级的大小;
                sum += getDirLength(sub);
            }
            return sum;
        }
        return 0;//既不是文件又不是文件夹，不存在
    }
    ```

  - 如果文件不存在，返回0

  （2）获取文件或目录的名称

  - String getName()

  （3）获取文件或目录的路径

  - 	String getPath()：获取路径
     String getAbsolutePath()：获取绝对路径
     String getCanonicalPath()：获取规范路径，例如：../   /

  （4）获取文件的后缀名

  - String name = file.getName();//得到文件名   包含扩展名
  - String ext = name.substring(name.lastIndexOf('.'));

  （5）获取文件的最后修改时间

  - long  lastModified()

    - 毫秒数

  - 如果文件不存在，返回0

  （6）获取上一级目录

  - String getParent()
  - File getParentFile()

- 判断

  （1）是否是文件

  - isFile()

    仅当file代表的文件存在，并且是个文件，才返回true

  - 如果文件不存在，返回false

  （2）是否是目录

  - isDirectory()

    仅当file对象代表的目录存在，并且是个文件夹目录，才返回true

  - 如果对应的不存在，返回false

  （3）是否存在

  - exists()

  （4）是否隐藏

  - isHidden()

  （5）文件是否可读

  - canRead()

  （6）文件是否可写

  - canWrite()

- 操作

  （1）创建文件

  - createNewFile()

  （2）创建目录

  - mkdir()

    如果父目录不存在，那么创建失败

  - mkdirs()

    如果父目录不存在，也一并创建

  （3）删除文件或目录

  - delete()

  - 只能删空目录

  - 如果要删除有内容的目录，需要使用递归

    ```java
    public void delDir(File file){		
        //如果是目录
        if(file.isDirectory()){
            //(2)先获取下一级，并删除下一级
            //a：获取下一级
            File[] listFiles = file.listFiles();
            //b：遍历并删除下一级
            for (File sub : listFiles) {
                //这是一个重复的过程
                delDir(sub);//调用自己
            }
        }
        //删除自己
        file.delete();
    }
    ```

（4）重命名

- renameTo(File newFile)

操作文件夹

- 获取它的下一级

  - String[] list();
  - File[] listFiles()

## 处理流

### 缓冲流

- 作用：增加缓冲区，提供效率
- 类型

  - BufferedInputStream

    - 包装InputStream

      例如：FileInputStream、DataInputStream、ObjectInputStream等

  - BufferedOutputStream

    - 包装OutputStream

      例如：FileOutputStream、DataOutputStream、ObjectOutputStream等

  - BufferedReader

    - 包装Reader

      例如：FileReader、InputStreamReader等

    - String readLine()

      判断是否读完，使用 ==null

  - BufferedWriter

    - 包装Writer

      例如：FileWriter，OutputStreamWriter等

    - write(String) + newLine()

  - 缓冲区的大小

    - 字节流

      8192字节

    - 字符流

      8192字符

### 数据流

- 作用：可以处理Java的基本数据类型+字符串（UTF-8修改版）
- 类型

  - DataOutputStream

    - writeXxx()

      - writeInt(int)
      - writeDouble(double)
      - writeChar(char)
      - writeUTF(String)

  - DataInputStream

    - readXxx()

      - int readInt()
      - double readDouble()
      - char readChar()
      - String readUTF()

- 注意：

  （1）DataOutputStream写，用DataInputStream读取

  （2）写的顺序和读的顺序要一致

  - 写与读之间需要配置文件等形式进行沟通顺序和类型

### 对象流

- 作用：可以处理Java对象等
- 类型

  - ObjectOutputStream

    - writeObject(Object)
    - 对象的序列化

  - ObjectInputStream

    - Object  readObject()
    - 对象的反序列化

- 注意

  （1）凡是要序列化的对象，它的类型必须实现java.io.Serializable接口

  - 否则会报：NotSerializableExecption

  （2）如果属性涉及到其他的引用数据类型，那么这个类型也必须实现java.io.Serializable接口

  （3）如果某个属性不想要序列化，那么可以在属性之前加transient

  - 一旦加了这个关键字修饰，该属性的值会在序列化的过程中，被忽略
  - 一旦加了这个关键字修饰，该属性在反序列化的过程中，它的值就赋默认值

  （4）在实现java.io.Serializable接口时，最好加一个常量：序列化版本ID

  - private static final long serialVersionUID = 1L;

  （5）静态的属性不能序列化

### 打印流

- 作用：可以打印各种类型的数据，最终都是以字符的形式打印，如果是引用数据类型，就调用它的toString()
- 类型

  - PrintStream

    - 代表

      System.out

    - 方法

      - print(xxx)
      - println(xxx)

  - PrintWriter

    - 方法

      - print(xxx)
      - println(xxx)

## NIO（了解）

### NIO

- Non - Blocking IO

  非阻塞式IO

### NIO和IO的区别

- 区别一

  - IO是面向流，是单向的，从某个流中要么只能读，要么只能写

    - 例如：要读文件

      - FileInputStream
      - FileReader

    - 类型即决定可以进行的操作

  - NIO是面向通道+缓冲区，即可以是单向的，又可以是双向的

    - 例如：ByteBuffer

      - put	往里写

      - get 往外读

    - 例如：FileChannel

      - 既可以指定为只读
      - 又可以指定为可读可写

- 区别二

  - IO是阻塞式的，一旦某个线程在读，此时没有可读的数据，会一直等待
  - NIO是非阻塞式

- 区别三

  - NIO可以使用选择器

### 和新的IO的API相关的

- Path

  是一个接口

- Paths

  - 用来获取Path的对象
  - Paths.get(URI)
  - Paths.get(String first, String...  others)

- Files

  - 工具类

    - 静态方法

  - 和Path用来替代原来的File
  - 方法

    - 创建文件

      - createFile

        - 如果文件已存在，直接报异常

      - 和File类的createNewFile()区别

        - 如果文件已存在，不提示

    - 创建目录

      - createDirectory

        - 替代原来的File的mkdir
        - 不同的是，如果目录已存在，就会报异常

      - createDirectories

        - 替代原来的File的mkdirs
        - 不同的是，如果目录已存在，就会报异常

    - 复制文件

      - copy
      - 区别

        - 如果目标文件不存在，直接创建
        - 如果目标文件已存在，要看是覆盖模式吗
        - 默认情况下，已存在，会报异常

    - 读取文件

      - readAllLines(Path path) 

        - 读取文件，返回List<String>
        - 默认是StandardCharsets.UTF_8
        - 可以自己指定字符编码方式

          - Charset.forName(字符集名称)

    - ....

### 通道

- 主要是四种类型

  - 和文件读取和存储相关的

    FileChannel

  - 和TCP服务器端使用

    ServerSocketChannel

  - 和TCP的客户端使用

    SocketChannel

  - 和UDP的两端使用

    DatagramChannel

- 必须和缓冲区结合才能使用
- 它的对象的创建

  - 例如：

    - FileChannel.open(xxx)

### 缓冲区

- 主要是7大类型

  - ByteBuffer

    - MappedByteBuffer

  - ShortBuffer
  - IntBuffer
  - LongBuffer
  - FloatBuffer
  - DoubleBuffer
  - CharBuffer
  - 除了boolean

- 属性

  （1）capacity：容量

  - 总大小，一旦创建就固定

  （2）limit：限制

  - 可读或可写的最大索引的位置

  （3）position：当前位置

  - 当前正在读或写的位置

  （4）mark：标记的位置

  - 0<=mark<=position<=limit<=capacity

- 方法

   (1)put
  - 往缓冲区写
  - 或者调用通道.read(xx)
    - 也相当于往缓冲区写

  （2）get
  - 从缓冲区取
  - 或者调用通道.write(xx)
    - 也相当于从缓冲区取数据

  （3）flip()
  - 切换读写模式

  （4）clear（）
  - 重新使用缓冲区

- 示例

（1）读文件

  ```java
  @Test
  public void test() throws IOException{
      Path path = Paths.get("1.txt");
      FileChannel fc = FileChannel.open(path, StandardOpenOption.READ);//打开通道
      ByteBuffer bb = ByteBuffer.allocate(1024);
      StringBuilder sb = new StringBuilder();
      while(true){
          //把数据放到缓冲区
          int len = fc.read(bb);//把数据装到缓冲区    对于缓冲区来说是存储，相当于put
          if(len<=0){
              break;
          }
          //切换
          bb.flip();
          //从缓冲区读取数据
          byte[] data = new byte[10];
          bb.get(data,0,bb.limit());
          //	System.out.println(new String(data,0,bb.limit()));
          sb.append(new String(data,0,bb.limit()));
          bb.clear();
      }
      System.out.println(sb);
  }
  ```

（2）复制文件

```java
@Test
public void testCopy()throws Exception{
    long start = System.currentTimeMillis();
    FileChannel fc = FileChannel.open(Paths.get("software/ideaIU-Ultimate-2017.1.4.exe"), StandardOpenOption.READ);
    FileChannel to = FileChannel.open(Paths.get("2.exe"), StandardOpenOption.WRITE,StandardOpenOption.CREATE_NEW);
    ByteBuffer bb = ByteBuffer.allocate(10);//定义缓冲区大小
    while(fc.read(bb)!=-1){//读取数据到缓冲区，即往缓冲区写  相当于put
        bb.flip();//修改limit为position  然后position为0       没有这个，就从position开始读到limit,limit=capacity，position为写完的位置
        to.write(bb);
        bb.clear();//limit变成capicity  position=0   没有这个，那么就会重复写第一次读取的内容，一会文件大小就很大，爆了
    }
    fc.close();
    to.close();
    long end = System.currentTimeMillis();
    System.out.println("ByteBuffer:"+ (end-start));
}
```

（3）物理映射复制文件（速度超快）

```java
@Test
public void test2()throws Exception{
    long start = System.currentTimeMillis();
    FileChannel from = FileChannel.open(Paths.get("software/ideaIU-Ultimate-2017.1.4.exe"), StandardOpenOption.READ);
    FileChannel to = FileChannel.open(Paths.get("3.exe"), StandardOpenOption.READ,StandardOpenOption.WRITE,StandardOpenOption.CREATE_NEW);//如果CREAD,如果文件已经存在不会报错，但是会从文件头开始写
    MappedByteBuffer fbb = from.map(MapMode.READ_ONLY, 0, from.size());
    MappedByteBuffer tbb = to.map(MapMode.READ_WRITE, 0, from.size());
    tbb.put(fbb);
    from.close();
    to.close();
    long end = System.currentTimeMillis();
    System.out.println("ByteBuffer:"+ (end-start));
}
```

## length

### 数组

数组的长度
- int  len = arr.length;
  - 属性

### 字符串的长度
int len = str.length();

### 文件的长度
long len = file.length();

## org.apache工具包

# 多线程

## 概念

### 程序

为了完成某个任务或功能，选择某个编程语言而编写的一组代码指令的集合

### 进程

程序的一次运行，是操作系统管理和调度的最小单位，每一个进程之间内存是相互独立的，如果进程之间要通信比较麻烦，可以通过文件，或网络通信方式等

### 线程

是进程中的其中一条执行路径，是CPU调度任务的最小单位

线程是共享同一个进程的内存

## 如何开启主线程以外的线程

### 方式一：继承java.lang.Thread类

- 步骤

  ①继承Thread类
  ②重写public void run(){}
  编写线程体，即该线程需要完成的任务代码
  ③创建线程对象
  ④启动线程：线程对象.start();

### 方式二：实现java.lang.Runnable接口

- 步骤

  ①实现java.lang.Runnable接口
  ②实现public void run(){}
  编写线程体，即该线程需要完成的任务代码
  ③创建线程对象
  ④启动线程：借助Thread类的对象
  new Thread(自定义线程对象).start();

### 经典面试题

- 两种方式的区别

  - 区别：
    （1）继承Thread类会有单继承的限制
    实现Runnable接口不会有单继承的限制
    （2）继承Thread类的方式，共享数据方面比较麻烦，使用static方式	
    实现Runnable接口，共享数据时，只需要共用同一个的Runnable接口的实现类的对象即可
    （3）继承Thread类的方式，同步的锁的选择要么选择一个static对象作为锁，要么选择“类名.class即当前类Class对象”	
    实现Runnable接口，同步锁可以直接选择this对象

## 线程安全问题

### 前提条件

（1）有多个线程
（2）共享数据
（3）多条语句操作共享数据

### 解决方法

- 同步synchronized

  - 形式
    - 同步代码块
      ```java
      synchronized(锁对象){
      同步代码，即需要加锁的代码
      }
      ```
    - 同步方法
      ```java
      synchronized [修饰符] 返回值类型 方法名(形参列表)抛出的异常列表
      ```

      

  - 同步锁
    （1）任意类型的对象
    （2）保证使用共享数据的多个线程，共用同一个锁对象

  - 锁的范围
    同步代码块：范围
    （1）不能太大：机会不均匀
    （2）不能太小：安全问题没解决
    （3）最好锁一次任务代码

  - 同步方法的锁：
    静态方法的锁：当前类的Class对象，即当前类名.class
    非静态方法的锁：当前对象，this

## 线程通信

### 问题：生产者消费者问题

- 问题

  现象描述
  - 有多个线程共享一个缓冲区（例如：数据仓库，文件等），有的线程往里放数据，有的线程往外取数据

    - 问题有两个
      - 问题：线程安全问题
        - 因为有共享数据
        - 如何解决：同步

      - 问题：缓冲区大小有限的
        - 如何解决：线程通信

### 线程通信的方法
（1）wait()
（2）notify()和notifyAll()

- 在java.lang.Object
  - 为什么？
    - 线程通信依赖于锁对象，即wait()和notify()是由锁对象调用
    - 锁对象可能是任意类型的对象，那么这些方法只能在Object类中声明

- 面试题：wait()和sleep()的异同？
  - 同
    - 这两个方法都会导致当前线程从运行状态到阻塞状态

  - 不同
    - 从阻塞回到就绪状态
      - sleep()睡眠时间到了
      - wait()也可以设置时间，但更多时候是通过notify()
    - 声明的类不同
      - wait是Object中，非静态方法
      - sleep是Thread类中，静态方法

    - 锁释放问题
      - sleep：不会释放锁的
        - 例如：在卫生间睡着了，锁还在手上
      - wait()：会释放锁的
        - 例如：抢到锁了，但是因为一些条件不满足，就释放锁，由其他线程执行

## java.lang.Thread

### 方法

1、获取线程名称的方法
- getName()

2、获取当前线程对象
- Thread.currentThread()

3、线程休眠
- Thread.sleep(毫秒)
- Thread.sleep(毫秒，纳秒)

4、线程的优先级
- getPriority()
- setPriority()
  - 优先级的范围是1-10
    - MAX_PRIORITY:10
    - MIN_PRIORITY:1
    - NORMAL_PRIORITY:5
- 注意：业务逻辑不能依赖于优先级

5、加塞
- join()
  - 这句代码写在那个线程体中，哪个线程被加塞，被调用这个join()的线程加塞

6、run()：所有线程都要写

7、start()：启动线程

### 生命周期

![](D:\Study\自学\笔记\img\屏幕截图 2022-04-21 171811.png)

# 反射机制

## 为什么要用反射？

### 因为Java是静态的强类型语言，在编译阶段就需要确定类型

- Java为了实现“动态性“特征，引入了反射机制

  - 变量可以使用Object声明，然后在运行时确定某个对象的运行时类型
  - 或者在运行时动态的”注入“某个类型的对象，动态的创建某个类型的对象

    - 例如：用这个类型的Class对象，然后创建它的实例

  - 。。。。

### 例如：JS等是动态的弱类型的语言，在运行时确定变量的类型，根据赋的值确定变量的类型

## 反射的根源

### java.lang.Class

- Class 类的实例表示正在运行的 Java 应用程序中的类和接口。枚举是一种类，注释是一种接口。每个数组属于被映射为 Class 对象的一个类，所有具有相同元素类型和维数的数组都共享该 Class 对象。基本的 Java 类型（boolean、byte、char、short、int、long、float 和 double）和关键字 void 也表示为 Class 对象。 

  - 示例代码

    ```java
    @Test
    public void test() {
        Class c1 = int.class;
        Class c2 = void.class;
        Class c3 = String.class;
        Class c4 = Comparable.class;
        Class c5 = ElementType.class;
        Class c6 = Override.class;
        Class c7 = int[].class;
    
        int[] arr1 = new int[5];
        int[] arr2 = new int[10];
    
        System.out.println(arr1.getClass() == arr2.getClass());
        System.out.println(int[].class == arr2.getClass());
    
        int[][] arr3 = new int[5][10];
        System.out.println(arr1.getClass());
        System.out.println(arr3.getClass());
    }
    ```

### 四种获取Class对象的方式

（1）如果类型已知：
- 类型名.class

（2）如果对象存在
- 对象.getClass()

（3）如果在编译阶段未知，但是运行阶段可以获取它的类型全名称
- Class.forName("类型全名称")

（4）如果在编译阶段未知，但是运行阶段可以获取它的类型全名称
- 类加载对象.loadClass("类型全名称")

## 相关的API（了解）

### java.lang.Class

- 方法

（1）获取类型名：
    - getName()

（2）创建实例对象
    - newInstance()
      - 这个类型必须有无参构造
      - Class对象.newInstance()

（3）获取包的信息
    - getPackage()

（4）获取父类
    - Class  getSuperClass()
      - 不带泛型
    - Type  getGenericSuperClass()
      - 可以带泛型

（5）获取父接口
    - Class[]  getInterfaces()
      - 不带泛型
    - Type[]  getGenericInterfaces()
      - 可以带泛型

（6）获取该类型的属性
    - 获取全部可访问的公共的属性
      - Field[]   getFields()
    - 获取全部已声明的属性
      - Field[]  getDeclaredFields()
    - 获取某一个公共的属性
      - Field  getField("属性名")
    - 获取某一个声明过的属性，可能是私有的等
      - Field  getDeclaredField("属性名")
      - 通过属性名就可以唯一确定一个属性

（7）获取该类的构造器
    - 获取全部的公共的构造器
    - 获取全部已声明的构造器
    - 获取某一个公共的构造器
    - 获取某一个已声明的构造器
      - Constructor  getDeclaredConstructor(形参列表的类型Class列表...  )
      - 通过构造器的形参列表就可以唯一确定一个构造器

（8）获取该类的方法
    - 获取全部的公共的方法
    - 获取全部已声明的方法
    - 获取某一个公共的方法
    - 获取某一个已声明的方法
      - Method getDeclaredMethod("方法名", 形参列表的类型Class列表 ....)
      - 通过方法的名称+形参列表才能唯一确定一个方法

（9）获取类上的注解
    - 获取所有的注解/注释
      -  Annotation[] getAnnotations() 
    - 获取指定的注解
      - <A extends Annotation>  A   getAnnotation(Class<A> annotationClass) 

### java.lang.reflect
- Package
  - 获取包名
    - getName()

- Modifier
  - Modifier.toString(mod)

- Constructor
  - 创建实例对象
    - newInstance(Object ...)
      - 如果无参，那么就直接“构造器对象.newInstance()”
      - 如果有参：构造器对象.newInstance(给构造器的实参列表)

- Field
  （1）setAccessible(true)
  （2）Object  get(实例对象)
    - Object  属性对象.get(实例对象)
    - 原来是：  实例对象.get属性名();

（3）set(实例对象， 属性的新值)
    - 属性对象.set（实例对象，属性值）
    - 原来是：实例对象.set属性名（属性值）

- Method
  （1）setAccessible(true)
    - 如果方法不是public才需要

（2）Object invoke(实例对象, 传给被调用方法的实参列表)
    - Object  returnValue = 方法对象.invoke(实例对象，实参列表...）
      - 如果原来的方法对象是没有返回值，即是void，那么returnValue是null
    - 原来：
      - 有返回值
        - 变量 = 实例对象.方法名(实参列表)
      - 无返回值
        - 实例对象.方法名(实参列表);

### 示例代码

```java
package com.atguigu.reflect;
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;
import java.nio.charset.Charset;
import java.util.Arrays;
/*
 * 有了Class对象后，都可以做什么事？你想干啥干啥
 * 1、获取类的详细信息
 * 2、创建实例对象
 * 3、获取属性，设置属性
 * 4、获取方法，设置方法
 * ...
 */

public class TestReflectAPI {
    public static void main(String[] args) throws Exception {
        Object obj = "hello";
        Class clazz = obj.getClass();

        //1、获取类名
        System.out.println("类名：" + clazz.getName());

        //2、获取包信息
        /*
		 * 所有的包有共同点-->Package
		 */
        Package pack = clazz.getPackage();
        System.out.println("包名：" + pack.getName());

        //3、获取类的修饰符
        int mod = clazz.getModifiers();
        //每一种修饰符，有一个常量表示
        //这个常量在Modifier类型声明
        System.out.println(Modifier.toString(mod));

        //4、父类
        Class superclass = clazz.getSuperclass();
        System.out.println("父类：" + superclass);

        //5、接口
        Class[] interfaces = clazz.getInterfaces();
        System.out.println("接口们：");
        for (Class class1 : interfaces) {
            System.out.println(class1);
        }		

        //6、属性：Field
        /*
		 * 属性共同点：  修饰符   数据类型   属性名      属性对应set值，get值的操作
		 * 任意类型的一个属性对应Field对象
		 * 
		 * 一切皆对象
		 */
        //		Field[] fields = clazz.getFields();//返回公共的属性
        /*		Field[] fields = clazz.getDeclaredFields();
		System.out.println("属性们：");
		for (Field field : fields) {
			System.out.println("属性的类型："+field.getType());
			System.out.println("属性的名称："+field.getName());
			System.out.println("属性的所有信息："+field);
		}*/

        //单独获取某个属性对象，例如：获取value属性
        //假设从配置文件中知晓属性名是value
        //		Field field = clazz.getField("value");//得到公共的
        Field field = clazz.getDeclaredField("value");//得到已声明的
        System.out.println(field);
        //设置属性值，获取属性值
        //先有对象，才能有属性值

        //		获取"hello"对象的value属性值
        field.setAccessible(true);//设置可访问

        Object object = field.get(obj);
        char[] v = (char[]) object;
        System.out.println(Arrays.toString(v));
        v[0] = 'w';
        v[1] = 'o';
        v[2] = 'r';
        v[3] = 'l';
        v[4] = 'd';


        //参数一：哪个对象的field属性，第二个参数：设置为xx新值
        //		field.set("hello", "world");//因为是final	

        System.out.println(obj);

        //7、创建对象    创建Class对应的类型的对象
        //		Object obj = clazz.newInstance();
        //		System.out.println(obj);

        //8、构造器
        //		clazz.getConstructors()//获取所有公共的构造器
        //		clazz.getDeclaredConstructors();//获取所有该类拥有的构造器


        /*
		 * 构造器的共同特点：修饰符   构造器名   形参列表      可以创建对象的操作
		 */

        /*
		 * 构造器可以重载，构造器的名称都一样
		 * 如何在类中唯一确定一个构造器：靠形参列表（个数和类型）
		 */
        //		 Constructor c = clazz.getDeclaredConstructor();//获取无参构造
        //		 Object newInstance = c.newInstance();//用无参构造创建对象
        //		 System.out.println("对象："+newInstance);

        //public String(char value[])
        Constructor c = clazz.getDeclaredConstructor(char[].class);//char[]数组类型
        //用有参构造创建对象，需要实参列表
        char[] params= {'c','h','a','i'};
        Object newInstance = c.newInstance(params);
        System.out.println("对象："+newInstance);

        //9、方法
        /*
		 * 所有方法共同特点：
		 * 修饰符  返回值类型  方法名（形参列表）抛出的异常列表
		 * 方法可以被调用
		 */
        //		clazz.getMethods()//获取所有公共的方法
        //		clazz.getDeclaredMethods();//获取所有方法
        /*
		 * 方法可以重载，如何在一个类中，唯一确定方法：方法名+形参列表（个数和类型）
		 *
		 * toString()
		 */
        Method m = clazz.getDeclaredMethod("toString");//获取无参的方法
        System.out.println(m);

        //调用方法
        //参数一：那个实例对象调用m方法，参数二：传给m方法的实参列表
        Object returnValue = m.invoke(obj);
        System.out.println(returnValue);

        // public byte[] getBytes(Charset charset) 
        Method m2 = clazz.getDeclaredMethod("getBytes", Charset.class);
        Object returnValue2 = m2.invoke(obj, Charset.forName("GBK"));
        System.out.println(returnValue2);
        byte[] data = (byte[]) returnValue2;
        System.out.println(Arrays.toString(data));
    }
}
```




## 如何获取类上的泛型

### 步骤
（1）先得到类的Class对象
（2）获取它的父类
  - Type  getGenericSuperClass() 可以带泛型

（3）类型转换
  - 如果是父类是这样的类型    父类名<泛型实参>
  - ParameterizedType  p = (ParameterizedType )type;

（4）获取泛型实参
  - Type[] getActualTypeArguments()  

### 示例代码

```java
package com.atguigu.reflect;
import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;
import java.util.Date;

public class TestGenericType {
    public static void main(String[] args) {
        GenericSub g = new GenericSub();
        System.out.println(g.getType1());
        System.out.println(g.getType2());

        GenericSub2 g2 = new GenericSub2();
        System.out.println(g2.getType1());
        System.out.println(g2.getType2());
    }
}
//T叫做类型形参
abstract class GenericSuper<T,U>{
    private Class<T> type1;
    private Class<U> type2;

    public GenericSuper(){
        Class clazz = this.getClass();//this是当前对象，在构造器中，就是代表那个正在创建的对象

        //Type是包含Class等的所有类型
        Type gs = clazz.getGenericSuperclass();
        //GenericSuper<String>：参数化的类型
        ParameterizedType p  = (ParameterizedType) gs;
        //获取类型实参
        Type[] arr = p.getActualTypeArguments();
        type1 = (Class<T>) arr[0];
        type2 = (Class<U>) arr[1];
    }
    public Class<T> getType1() {
        return type1;
    }
    public Class<U> getType2() {
        return type2;
    }
}
//String是类型实参
class GenericSub extends GenericSuper<String,Integer>{
}
class GenericSub2 extends GenericSuper<Date,Double>{
}
```

### 核心代码

```java
		Class clazz = GenericSub.class;
//		Class sup = clazz.getSuperclass();//得不到泛型的信息
//		System.out.println(sup);

		//Type是包含Class等的所有类型
		Type gs = clazz.getGenericSuperclass();
		//GenericSuper<String>：参数化的类型
		ParameterizedType p  = (ParameterizedType) gs;
		//获取类型实参
		Type[] arr = p.getActualTypeArguments();
		System.out.println(arr[0]);
		System.out.println(arr[1]);
```

## 获取注解

### 获取类上的注解

- 步骤

  （1）先得到类的Class对象

  （2）

  - 获取指定的注解

    - <A extends Annotation>  A   getAnnotation(Class<A> annotationClass) 
    - 可以获取到的注解，必须声明周期是RUNTIME

  （3）获取注解的配置参数的值

- 示例代码

```java
package com.atguigu.reflect;

import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import org.junit.Test;
@MyAnnoation
public class TestAnnotatio {

    @MyAnnoation(value = "尚硅谷")
    private String info;
    //获取类上的注解信息
    @Test
    public void test() {
        // 1、先得到Class对象
        Class clazz = TestAnnotatio.class;
        // 2、获取类上的注解信息：得到MyAnnoation注解对象
        MyAnnoation m = (MyAnnoation) clazz.getAnnotation(MyAnnoation.class);
        // 3、得到注解的配置参数的值
        String value = m.value();
        System.out.println(value);
    }
}

@Retention(RetentionPolicy.RUNTIME) // 为了在反射阶段可以读取到该注解的信息，生命周期一定要在RUNTIME
@interface MyAnnoation {
    String value() default "atguigu";
}
```


### 获取属性上的注解

- 步骤
（1）先得到类的Class对象
（2）获取属性对象
（3）获取指定的注解
      - <A extends Annotation>  A   getAnnotation(Class<A> annotationClass) 
          - 可以获取到的注解，必须声明周期是RUNTIME
        （4）获取注解的配置参数的值

- 示例代码

  ```java
  package com.atguigu.reflect;
  import java.lang.annotation.Retention;
  import java.lang.annotation.RetentionPolicy;
  import java.lang.reflect.Field;
  import org.junit.Test;
  public class TestAnnotatio {
      @MyAnnoation(value = "尚硅谷")
      private String info;
      //获取属性上的注解信息
      @Test
      public void test2() throws Exception {
          // 1、获取Class对象
          Class clazz = TestAnnotatio.class;
          // 2、先获取属性对象
          Field field = clazz.getDeclaredField("info");
          // 3、得到注解对象
          MyAnnoation m = (MyAnnoation) field.getAnnotation(MyAnnoation.class);
          // 4、得到属性值
          System.out.println(m.value());
      }
  }
  @Retention(RetentionPolicy.RUNTIME) // 为了在反射阶段可以读取到该注解的信息，生命周期一定要在RUNTIME
  @interface MyAnnoation {
      String value() default "atguigu";
  }
  ```
## 类加载器

### 类加载的过程（了解）

- 双亲委托模式/机制

  - 某个类加载器接到加载任务，先把加载任务交给“父”加载器，层层往上，一直到引导类加载器，如果“父”加载器可以加载，那么就由“父”加载器加载，如果不可以，传回它的“子”加载器，“子”加载器尝试加载，如果可以，那么就加载，如果不可以，再往回传，一到回到最初接到任务的那个加载器，如果它可以，也正常加载，如果它也不能加载，报异常：ClassNotFoundException
  - 作用：安全

### 类加载器的体系结构

1、引导类加载器BootStrap
- 非Java语言实现的
  - 获取不到它的对象，只能得到null
- 加载核心类库rt.jar
- 加载sun.boot.class.path路径下的内容

2、扩展类加载器ExtClassLoader
- 加载jre/ext目录
- java.ext.dirs路径下的内容

3、应用程序类加载器，系统类加载器AppClassLoader
- 加载用户自定义的类型
- 加载src目录下的内容（bin）

4、自定义类加载器

### 类加载的作用
（1）加载类

（2）加载资源文件

```java
@Test
public void test8()throws Exception{
    Properties pro = new Properties();
    //JavaSE和Web项目
    //在web项目中，因为项目部署到tomcat中运行，又因为tomcat用自己的类加载器的
    //把配置文件放在了src中，最终代码在WEB-INFO的classes目录
    //可以用类加载器加载这个配置文件，但是不是系统类加载器
    //this.getClass().getClassLoader()目的是得到tomcat的自定义类加载器对象
   pro.load(this.getClass().getClassLoader().getResourceAsStream("3.properties"));
    System.out.println(pro.getProperty("user3"));
}

@Test
public void test7()throws Exception{
    Properties pro = new Properties();
    //JavaSE和Web都可以
    //把配置文件放在了项目根目录下，在src外面
    //不可以用类加载器加载这个配置文件
    //可以使用FileInputStream获取
    pro.load(new FileInputStream("2.properties"));
    System.out.println(pro.getProperty("user2"));
}
```

# 网络编程

## 网络编程的三个要素

### 1、IP地址或主机名

- InetAddress
- String：192.168.24.71

  - 每一个整数是1~255

- 域名：www.baidu.com

  - 通过域名解析器，找对对应的ip地址

### 2、端口号

- 0~65535

- 建议不要使用

  - 0~1023

    用于基础服务

  - tomcat/jboss

    8080

  - mysql

    3306

  - oracle

    1521

  - sql server

    1433

  - 浏览器：http

    80

  - ....

### 3、网络协议

- OSI理想参考模型

  ![](D:\Study\自学\笔记\img\屏幕截图 2022-04-21 174756.png)

- TCP/IP的四层实现模式

- 传输层

  - TCP

    - 面向连接的，可靠的，适用于大数据传输，速率相对低，在传输之前会先“三次握手”，在断开之前会“四次挥手”

  - UDP

    - 非面向连接的，不可靠的，适用于数据比较小的，<=64kb，相对速率高
  
- 应用层

  - http/https
  - ftp

## 网络编程的API

### Socket

- 套接字

  - 表示通信的两个端点，两边各一个

- 分类

  - 流套接字

    - 用于TCP的通信

      - ServerSocket

        - 转门用于服务器用来监听和接收客户端的连接

      - Socket

        - 用于服务器和客户端的通信

  - 数据报套接字

    - 用于UDP的通信

      - DatagramSocket

        - 用于UDP的两端的通信

### TCP编程步骤

- 服务器

  1、先创建ServerSocket

  - ServerSocket server = new ServerSocket(端口号);

    - 指定端口号进行监听，客户端通过这个端口号与它进行连接和通信

  2、接收客户端的连接

  - Socket socket = server.accept();

    - 每一个客户端就要有自己的一个Socket
    - 如果希望不同的客户端通信“同时”进行，需要每一个socket用一个线程进行维护

  3、通过socket进行收或发消息

  - 收消息

    - InputStream is = socket.getInputStream();

      - 可以在此基础上，包装缓冲流，转换流，对象流，打印流，数据流等

  - 发消息

    - OutputStream out = socket.getOutputStream();

      - 可以在此基础上，包装缓冲流，转换流，对象流，打印流，数据流等

  4、与客户端断开连接

  - socket.close();

- 客户端

  1、先与服务器建立连接，通过创建一个Socket，要指定服务器的IP和端口号

  - Socket socket = new Socket(服务器的IP，服务器的监听端口号);

  2、通过socket进行收或发消息

  - 收消息

    - InputStream is = socket.getInputStream();

      - 可以在此基础上，包装缓冲流，转换流，对象流，打印流，数据流等

  - 发消息

    - OutputStream out = socket.getOutputStream();

      - 可以在此基础上，包装缓冲流，转换流，对象流，打印流，数据流等

  - 收和发可以用不同的线程进行维护

  3、与客户端断开连接

  - socket.close();

- 示例一

```java
package com.atguigu.tcp1;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;
import org.junit.Test;
/*
 * TCP:面向连接
 * 通信的两端分角色：服务器端和客户端
 * 
 * 服务器端等着被连接，客户端主动连接
 * 
 * 服务器端：
 * 1、ServerSocket：用来接收客户端的连接信息
 * 2、Socket：用来与某个客户端进行通信
 * 
 * 客户端：
 * 1、Socket：用来与服务器进行通信
 * 
 */
public class TestTCP1 {
    @Test
    public void server()throws Exception{
        //1、创建ServerSocket，看成：开启服务器 ，需要指定一个端口号，监听是否有客户端来连接
        ServerSocket ss = new ServerSocket(9090);

        while(true){
            System.out.println("等待您的链接....");
            //2、等待客户端的连接，接收客户端的连接（如果没有人连接，那么这句代码会阻塞）
            //一旦有客户端连接成功，那么就会产生一个Socket对象，专门负责和这个客户端通信
            Socket socket = ss.accept();

            System.out.println(socket.getInetAddress().getHostAddress()+"连接成功");

            //3、可以接收消息，或发生消息
            //例如：先发：“欢迎登陆”
            //在接收消息

            //发消息：输出流，OutputStream
            OutputStream output = socket.getOutputStream();
            output.write("欢迎登陆".getBytes());
            socket.shutdownOutput();

            //收消息
            InputStream is = socket.getInputStream();

            byte[] data = new byte[1024];
            int len;
            StringBuilder sb = new StringBuilder();
            while((len= is.read(data)) !=-1){
                sb.append(new String(data,0,len));
            }
            System.out.println("服务器收到的消息：" + sb);

            //4、关闭连接
            socket.close();//只是与某个客户端断开
        }

        //5、服务器关闭
        //		ss.close();
    }

    @Test
    public void client()throws Exception{
        //1、创建一个Socket，要指定服务器的IP和端口号
        Socket socket = new Socket("192.168.24.71",9090);

        //2、接收消息
        InputStream is = socket.getInputStream();

        byte[] data = new byte[1024];
        int len;
        StringBuilder sb = new StringBuilder();
        while((len= is.read(data)) !=-1){
            sb.append(new String(data,0,len));
        }
        System.out.println("客户端收到的消息：" + sb);

        //3、发送消息
        String info = "马上吃饭了";
        OutputStream out = socket.getOutputStream();
        out.write(info.getBytes());

        //3、关闭连接
        socket.close();
    }
}
```

- 示例二

  ```java
  package com.atguigu.tcp2;
  import java.io.BufferedReader;
  import java.io.IOException;
  import java.io.InputStream;
  import java.io.InputStreamReader;
  import java.io.OutputStream;
  import java.net.ServerSocket;
  import java.net.Socket;
  import java.util.Scanner;
  import org.junit.Test;
  public class TestTCP2 {
      @Test
      public void server()throws Exception{
          //1、创建ServerSocket
          ServerSocket server = new ServerSocket(9999);
  
          while(true){
              //2、等待客户端的连接，接收客户端的连接
              Socket socket = server.accept();
              String clientIp = socket.getInetAddress().getHostAddress();
  
              System.out.println(clientIp+"上线了");
  
              //每一个客户端需要一个线程单独维护它的通信，“同时”与服务器通信的效果
              new MessageHandler(socket).start();
          }
      }
  
      //和服务器连接上以后，从键盘输入消息，给服务器发送，一直到从键盘输入byebye，在与服务端口连接
      @Test
      public void client()throws Exception{
          //1、连接服务器
          Socket socket = new Socket("192.168.24.71",9999);
  
          OutputStream out = socket.getOutputStream();
  
          //2，从键盘输入给服务器发送
          Scanner input = new Scanner(System.in);
          while(true){
              System.out.println("输入要发送的内容：");
              String info = input.nextLine();
  
              if("byebye".equals(info)){
                  break;
              }
  
              //给服务器发送
              out.write((info+"\n").getBytes());
          }
  
          //3、断开
          socket.close();
      }
  }
  class MessageHandler extends Thread{
      private Socket socket;
  
      public MessageHandler(Socket socket) {
          super();
          this.socket = socket;
      }
      public void run(){
          try {
              //3、和一个客户端多次通信，接收到消息后，在控制台打印
              InputStream input = socket.getInputStream();
              InputStreamReader isr = new InputStreamReader(input);
              BufferedReader br = new BufferedReader(isr);
  
              String str;
              while((str = br.readLine())!=null){
                  System.out.println(socket.getInetAddress().getHostAddress() +"说："+ str);
              }
  
              //4、断开
              socket.close();
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  }
  ```

- 示例三：群聊

```java
//服务器
package com.atguigu.tcp2;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Scanner;
import org.junit.Test;
public class TestTCP2 {
    @Test
    public void server()throws Exception{
        //1、创建ServerSocket
        ServerSocket server = new ServerSocket(9999);

        while(true){
            //2、等待客户端的连接，接收客户端的连接
            Socket socket = server.accept();
            String clientIp = socket.getInetAddress().getHostAddress();

            System.out.println(clientIp+"上线了");

            //每一个客户端需要一个线程单独维护它的通信，“同时”与服务器通信的效果
            new MessageHandler(socket).start();
        }
    }

    //和服务器连接上以后，从键盘输入消息，给服务器发送，一直到从键盘输入byebye，在与服务端口连接
    @Test
    public void client()throws Exception{
        //1、连接服务器
        Socket socket = new Socket("192.168.24.71",9999);

        OutputStream out = socket.getOutputStream();

        //2，从键盘输入给服务器发送
        Scanner input = new Scanner(System.in);
        while(true){
            System.out.println("输入要发送的内容：");
            String info = input.nextLine();

            if("byebye".equals(info)){
                break;
            }

            //给服务器发送
            out.write((info+"\n").getBytes());
        }

        //3、断开
        socket.close();
    }
}
class MessageHandler extends Thread{
    private Socket socket;

    public MessageHandler(Socket socket) {
        super();
        this.socket = socket;
    }
    public void run(){
        try {
            //3、和一个客户端多次通信，接收到消息后，在控制台打印
            InputStream input = socket.getInputStream();
            InputStreamReader isr = new InputStreamReader(input);
            BufferedReader br = new BufferedReader(isr);

            String str;
            while((str = br.readLine())!=null){
                System.out.println(socket.getInetAddress().getHostAddress() +"说："+ str);
            }

            //4、断开
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
//客户端
package com.atguigu.tcp3;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.PrintStream;
import java.net.Socket;
import java.net.SocketException;
import java.util.Scanner;
/*
 * 
 */
public class TestTCPClient{
    public static void main(String[] args) throws Exception{
        //1、连接服务器
        Socket socket = new Socket("192.168.24.71",9090);

        //2、创建两个线程，一个收，一个发
        SendThread send = new SendThread(socket);
        send.start();
        RecevierThread r = new RecevierThread(socket);
        r.start();

        send.join();

        r.setExit(true);

        //3、关闭
        socket.close();
    }
}
class SendThread extends Thread{
    private Socket socket;

    public SendThread(Socket socket) {
        super();
        this.socket = socket;
    }
    @Override
    public void run() {
        try {
            OutputStream output = socket.getOutputStream();
            PrintStream ps = new PrintStream(output);

            Scanner input = new Scanner(System.in);
            while(true){
                System.out.println("请输入要发送的内容：");
                String info = input.nextLine();
                if("bye".equals(info)){
                    break;
                }
                //给服务器发送
                ps.println(info);
            }

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
class RecevierThread extends Thread{
    private Socket socket;
    private boolean exit = false;

    public RecevierThread(Socket socket) {
        super();
        this.socket = socket;
    }
    @Override
    public void run() {
        try {
            InputStream is = socket.getInputStream();
            InputStreamReader isr = new InputStreamReader(is);
            BufferedReader br = new BufferedReader(isr);

            String str;
            while(exit==false){
                try {
                    str = br.readLine();
                } catch (SocketException e) {
                    break;
                }
                if(str==null){
                    break;
                }
                System.out.println("收到的消息：" + str);
            }

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    public void setExit(boolean exit) {
        this.exit = exit;
    }

}
```


### UDP编程步骤

- 发送端

  1、创建一个DatagramSocket

  2、准备发送的数据，并且打包

  - DatagramPacket

    - 要指定：发送的数据，长度，接收方的IP，接收方的端口号

  3、通过DatagramSocket的send(数据报)

  4、关闭

- 接收端

  1、创建一个DatagramSocket

  - 要指定 监听的端口号

  2、准备一个DatagramPacket，用来接收数据

  - 要指定装数据一个字节数组，以及长度

  3、通过DatagramSocket的receive(数据报)

  4、拆解数据

  - 通过DatagramPacket对象.getData()数据，DatagramPacket对象.getLength()实际接收的数据长度

  5、关闭

- 示例代码

```java
  package com.atguigu.udp;
  import java.net.DatagramPacket;
  import java.net.DatagramSocket;
  import java.net.InetAddress;
  import org.junit.Test;
  /*
   * UDP:非面向连接的
   * 
   * 有发送端和接收端两个应用程序
   */
  public class TestUDP {
      @Test
      public void send()throws Exception{
          //1、创建Socket
          DatagramSocket ds = new DatagramSocket();
  
          //2、把数据打包成一个数据报，包
          String str = "双十二购物快乐";
          byte[] bytes = str.getBytes();
          InetAddress ip = InetAddress.getByName("192.168.24.71");
          DatagramPacket dp = new DatagramPacket(bytes, bytes.length, ip,8989);
  
          //3、通过socket发送出去
          ds.send(dp);
          System.out.println("发送完毕");
  
          //4、释放资源
          ds.close();
      }
  
      @Test
      public void reveive()throws Exception{
          //1、创建Socket
          DatagramSocket ds = new DatagramSocket(8989);//为它指定一个端口号，在端口号一直监听着
  
          //2、先创建一个数据报等着
          byte[] data = new byte[1024];
          DatagramPacket dp  = new DatagramPacket(data, data.length);
  
          //3、准备接受数据，从socket中接收数据，如果此时没有数据，这句代码会阻塞
          ds.receive(dp);
  
          //4、拆出数据
          String str = new String(dp.getData(),0,dp.getLength());
          System.out.println("收到的数据是：" + str);
  
          //5、关闭
          ds.close();
      }
  }
```

### URL编程

- 在TCP的基础上

  - 服务器端

    - Web服务器

  - 客户端

    1、创建URL的对象

    - URL url = new URL(网址);

      - 网址：协议://主机名:端口号/文件路径名?参数名=参数值&参数名=参数值...
      - 例如：http://localhost:8080/1108web/index.html
      - 例如：http://localhost:8080/1108web/login?username=xx&password=xx

    2、与服务器建立连接

    - InputStream is = url.openStream();

      - 这种方式只能使用get方法与服务器进行通信

        - 如果要给服务器传参数只能在网址后面通过?参数名=参数值&参数名=参数值...

    - HttpURLConnection tc = (HttpURLConnection)url.openConnection();

      - 这种方式可以使用post方法与服务器进行通信

        - 如果要给服务器传数据，那么需要hc.setDoOutput(true);
        - 然后用OutputStream进行发送数据

    3、处理接收到数据

- 示例代码

  - 示例一

```java
package com.atguigu.url;
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URL;
/*
    * tomcat：是一个服务器
    * 浏览器：客户端
    */
public class TestURL {
    public static void main(String[] args) throws Exception{
        //自定义客户端
        URL url = new URL("http://192.168.24.71:8080/1108JavaWeb/index.html");
        /*System.out.println("协议：" + url.getProtocol());
    System.out.println("主机名：" + url.getHost());
    System.out.println("端口号：" + url.getPort());
    System.out.println("路径名：" + url.getPath());*/

        InputStream input = url.openStream();
        InputStreamReader isr = new InputStreamReader(input);
        BufferedReader br  = new BufferedReader(isr);	

        String str ;
        while((str=br.readLine())!=null){
            System.out.println(str);
        }
    }
}
```


  - 示例二：get
```java
package com.atguigu.url;
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URL;
public class TestURL2 {
    public static void main(String[] args) throws Exception{
        URL url = new URL("http://192.168.24.71:8080/myweb/login?username=admin&pass=123");
        InputStream input = url.openStream();
        InputStreamReader isr = new InputStreamReader(input);
        BufferedReader br  = new BufferedReader(isr);	

        String str ;
        while((str=br.readLine())!=null){
            System.out.println(str);
        }
    }
}
```

  - 示例三：post

```java
package com.atguigu.url;
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.PrintStream;
import java.net.HttpURLConnection;
import java.net.URL;
public class TestURL3 {
    public static void main(String[] args) throws Exception{
        URL url = new URL("http://192.168.24.71:8080/myweb/login");
        HttpURLConnection hc = (HttpURLConnection) url.openConnection();

        hc.setDoOutput(true);
        OutputStream output = hc.getOutputStream();
        PrintStream ps = new PrintStream(output);
        //		output.write("username=chai&pass=123".getBytes());
        ps.println("username=chai&pass=123");

        InputStream input = hc.getInputStream();
        InputStreamReader isr = new InputStreamReader(input);
        BufferedReader br  = new BufferedReader(isr);	

        String str ;
        while((str=br.readLine())!=null){
            System.out.println(str);
        }
    }
}
```

# Lambda表达式与StreamAPI

JDK1.8

这两个的目的都是想要使得Java能够实现函数式编程

Lambada表达式主要针对接口，函数式接口进行的优化，简化代码

StreamAPI主要是针对集合的处理操作进行的优化，简化代码

## Lambda表达式

是一个匿名的函数，为了把方法体的实现代码当做数据一样进行传递

### JDK1.8之前，用匿名内部类完成

```java
Runnable r = new Runnable(){
    public void run(){
        ......
    }
}
//目的就是传递run()方法的实现代码
```

```java
new Thread(new Runnable(){
    public void run(){
        ......
    }
}).start();
```

### 使用Lambda表达式

- Runnable r = () -> {....};
- new Thread(() -> {....}).start();

### 语法

- 格式： (形参列表) ->  {Lambda体}

### 四种形式

（1）无参无返回值

- 格式

  - () -> {Lambda体}

- 说明：

  （1）无参，()

  （2）如果Lambda体是多句语句，那么{}是不可以省略

  （3）如果Lambda体是1句语句，那么{}如果不省略，那么语句后面要加; ，即{;}

  （4）如果Lambda体是1句语句，那么{;}可以省略

- 代表

  - Runnable r = ()  -> {System.out.println("hello");};
  - Runnable r = ()  -> System.out.println("hello");

（2）有参无返回值

- 格式

  - (形参列表) -> {Lambda体}

- 说明：

  （1）如果Lambda体是多句语句，那么{}是不可以省略

  （2）如果Lambda体是1句语句，那么{}如果不省略，那么语句后面要加; ，即{;}

  （3）如果Lambda体是1句语句，那么{;}可以省略

  （4）如果参数列表的参数类型是可以确定的，那么类型可以省略，如果形参个数是多个，那么()不可以省略

  （5）如果参数列表的个数只有1个，类型可以确定，()可以省略,形参名不可以省略，但是形参名可以和接口的抽象方法的形参名不一样

- 代表

  - 消费型
  - Consumer<T>   void  accept(T t)
  - java.lang.Iterable<T>

    - forEach(Consumer<T>)
    - 集合对象.forEach(t  -> System.out.println(t));

（3）无参有返回值

- 格式

  - () -> {Lambda体}

    - Lambda体中，肯定有return语句

- 说明：

  （1）无参，()不可以省略

  （2）如果Lambda体是多句语句，那么{}是不可以省略，，每一个语句后面要;，并且必须有return 返回值;的语句

  （3）如果Lambda体是1句语句，那么{}如果不省略，那么一定是{return 返回值;}的语句

  （4）如果Lambda体是1句语句，那么{;}可以省略，而且return要省略

- 代表

  - 供给型
  - Supplier<T>   T get()
  - java.util.Optional<T>   orElseGet(Supplier)

    - Optional<String> opt = Optional.ofNullable(address);
    - String address = opt.orElseGet(() -> new String("北京"));

（4）有参有返回值

- 格式

  - (形参列表) -> {Lambda体}

- 说明：

  （1）如果Lambda体是多句语句，那么{}是不可以省略，并且必须有return 返回值;的语句

  （2）如果Lambda体是1句语句，那么{}如果不省略，那么一定是{return 返回值;}的语句

  （3）如果Lambda体是1句语句，那么{;}可以省略，而且return也可以省略

  （4）参数列表，如果类型可以确定，那么类型可以省略,()不可以省略

  （5）参数列表，如果类型可以确定，并且参数个数只有一个，那么类型和()都可以省略

- 代表

  - java.util.Comparator<T>： int compare(T t1, T t2)

    - Comparator<Student> com = (t1,t2) -> t1.getId() - t2.getId();

  - Predicate<T>  : boolean  test(T t)

    - Predicate<Employee>  p = t -> t.getSalary() > 10000;

  - Function<T,R> :  R apply(T t)

    - 如果Employee对象的薪资低于10000，涨薪10%，并且返回新工作
    - Function<Employee, Double>  f = e -> {
      if(e.getSalary()<10000){
      e.setSalary(e.getSalary()*1.1;
      }
      return e.getSalary();	
      }

### 使用的形式

1、给函数式接口的变量赋值：多态引用

- Comparator<Student> com = (t1,t2) -> t1.getId() - t2.getId();

2、给函数式接口的形参赋值：多态参数

- new TreeSet( (t1,t2) -> t1.getId() - t2.getId());

### 函数式接口

- 函数式接口也是接口，是个特殊的接口，SAM型接口

  - SAM：Single  Abstract  Method

    - 使用注解声明@FunctionInterface

- 在这个类接口中只有一个抽象方法，但是可以有静态方法和默认方法以及Object中的方法

- 只有函数式接口的变量或形参才能用Lambda表达式赋值

- 四个核心的函数式

  1、消费型

  - Consumer<T>   void  accept(T t)
  - 还有延伸版

    - BiConsumer<T,U>: void  accept(T t,U u)
    - 。。。。

  2、供给型

  - Supplier<T>   T get()
  - DoubleSupplier   Double get()
  - ....

  3、功能型

  - Function<T,R>  R  apply(T t)
  - 延伸版

    - BiFunction<T,U,R>  R apply(T t,U u)
    - BinaryOperator<T>  T apply(T t2, T t2)
    - ....

  4、断定型

  - Predicate<T>  : boolean  test(T t)
  - 延伸版

    - BiPredicate<T,U>  boolean test(T t ,U u)
    - ....

### 再简化版

- 方法引用

  - 条件

    （1）Lambda体通过调用一个现成的方法来完成

    （2）Lambda的形参列表刚好是用于这个方法的实参

  - 形式有三种

    （1）实例对象::实例方法名

    - 集合对象.forEach(t -> System.out.println(t));
    - 集合对象.forEach(System.out::println)

    （2）类名::静态方法名

    - Supplier<Double>  s = () -> Math.random();

      - Supplier<Double>  s = Math::random;

    - BiFunction<Integer,Integer,Integer> b = (a,b) -> Math.max(a,b);

      - BiFunction<Integer,Integer,Integer> b = Math::max;

    （3）类名::实例方法名

    - Comparator<String>  c = (t1,t2)  ->  t1.compareTo(t2);

      - Lambda表达式的形参的第一个作为调用方法的对象，第二个，作为这个实例方法的实参
      - Comparator<String>  c = String::compareTo;

- 构造器引用

  - 条件

    （1）Lambda体通过调用一个构造器完成，返回这个新建的对象

    （2）Lambda的形参列表刚好是用于这个构造器的实参

  - 示例

    - Fuction<String ,Employee>  f = name -> new Employee(name);
    - Fuction<String ,Employee>  f = Employee::new;

- 数组构造引用

  - 条件

    （1）Lambda体通过创建一个数组对象完成，返回这个新建的数组对象

    （2）Lambda的形参列表刚好是用于这个数组对象的创建的长度

  - 示例

    - Fuction<Integer ,Employee[]>  f = len -> new Employee[len];
    - Fuction<Integer ,Employee[]>  f = Employee[]::new;

## StreamAPI

### 作用

- Stream API ( java.util.stream) 把真正的函数式编程风格引入到Java中。这是目前为止对Java类库最好的补充，因为Stream API可以极大提高Java程序员的生产力，让程序员写出高效率、干净、简洁的代码。
  Stream 是 Java8 中处理集合的关键抽象概念，它可以指定你希望对集合进行的操作，可以执行非常复杂的查找、过滤和映射数据等操作。 使用Stream API 对集合数据进行操作，就类似于使用 SQL 执行的数据库查询。也可以使用 Stream API 来并行执行操作。简言之，Stream API 提供了一种高效且易于使用的处理数据的方式。

### 特点

1、Stream不负责存储数据

2、Stream的操作不影响数据源，每次操作返回一个新的Stream

3、Stream的中间操作是一个“懒惰求值”，一直要到终结操作，才会一口气完成

### 步骤

1、创建Stream

- 四种方式

  1、Collection集合对象.stream()

  - ArrayList<String> list = new ArrayList<>();
    。。。	
    //创建stream
    Stream<String> stream = list.stream();

  2、Arrays.stream(数组对象)

  - String[] arr = {"hello","world","java","lambda","stream"};
    Stream<String> stream = Arrays.stream(arr);

  3、Stream.of(T...)

  - Stream<String> stream = Stream.of("hello","world","java","lambda","stream");

  4、无限流

  - Stream.iterator(..)

    - 示例

```java
@Test
public void test4(){
    //Interface UnaryOperator<T>是特殊的Function<T,T>： T apply(T t)
    Stream<Integer> stream = Stream.iterate(1, x -> x+2);

    //中间操作
    stream = stream.limit(10);//取前面的10个
    stream.forEach(System.out::println);
}
```

  - Stream.generate(xx)

    - 示例
```java
@Test
public void test5(){
    //Supplier<T> ：T  apply()
    //		Stream<Double> generate = Stream.generate(() -> Math.random());
    Stream<Double> stream = Stream.generate(Math::random);

    //		stream = stream.limit(5);
    //		stream.forEach(System.out::println);
    stream.limit(5).forEach(System.out::println);
}
```

2、中间操作

（1）筛选与切片
A：过滤：filter
B：去重：distinct
C：取前面的几个：limit
D：跳过前面几个：skip

要取中间几个：skip + limit

（2）映射
	A：map(Function)：对Stream中的每一个元素执行某个操作，返回值组成一个新的Stream
	B：返回值是特殊类型
 		* mapToInt()
 		* mapToLong()
 		* mapToDouble()
	C：flatMap(Function)：对stream的每一个元素执行某个操作，返回值是一个stream，这些个stream再合成一个大的stream

（3）排序
   A：sorted()：自然排序
   B：sorted(Comparator)：定制排序

3、终结操作

（1）遍历
- forEach(Consumer)

（2）匹配与查找
	A：allMatch(Predicate p)：每一个元素是否都满足某个条件
	B：anyMatch(Predicate p)：是否有一个元素满足条件
	C：noneMatch(Predicate p)：是否所有元素都不满足
	D：findFirst（）:返回第一个
	E：findAny()：如果是并行流，返回的结果是任意一个，如果是一个稳定的流，返回的结果是和findFirst()一样
	F：count()：统计
	G：max(Comparator)
	H:min(Comparator)

（3）规约

```java
//A:
Optional<T> reduce(BinaryOperator<T> accumulator)
    //BinaryOperator<T>是一个BiFunction<T,T,T>接口：T apply(T t1, T t2)
    //B:
T reduce(T identity,BinaryOperator<T> accumulator)
```


（4）收集
```java
<R,A> R collect(Collector<? super T,A,R> collector)
    
```

Collector 接口中方法的实现决定了如何对流执行收集的操作

Collectors 实用类提供了很多静态方法，可以方便地创建常见收集器实例，例如、List，Set,Map

# Optional类

## java.util.Optional<T>

尽量避免空指针

### 1、创建Optional对象

（1）创建一个空Optional

- Optional.empty()

（2）创建一个包装了对象的Optional

- Optional.of(obj)

  obj必须是非空，否则异常

（3）创建一个包装对象可能为空的Optional

- Optional.ofNullable(obj)

  obj可能为空

### 2、获取包装的对象

（1）get()

- 如果Optional包装的对象不为空，正常返回，如果为空，报异常

（2）orElse(T other)

- 如果Optional包装的对象不为空，正常返回，如果为空，返回other对象

（3）orElseGet(Supplier)

- 如果Optional包装的对象不为空，正常返回，如果为空，返回由供给型接口提供的对象
- Supplier接口：T  get()

（4）orElseThrow(Supplier<? extends X> exceptionSupplier)

- 如果Optional包装的对象不为空，正常返回，如果为空，报异常，报的异常是由Supplier提供的异常对象

### 3、是否存在

（1）boolean isPresent()

- 表示判断Optional中的包装的对象是否存在，如果存在就返回true，否则就是false

（2）ifPresent(Consumer<? super T> consumer) 

- 如果存在，就执行Consoumer指定的操作，如果不存在就不做
- Consumer： void accept(T t)

### 4、过滤

- Optional<T> filter(Predicate<? super T> predicate)  

  - 对Optional中包装的对象进行过滤，按照Predicate的条件进行判断，如果满足，返回它，如果不满足，返回empty的Optional

### 5、映射

- <U> Optional<U> map(Function<? super T,? extends U> mapper) 
  - 对Optional包装对象，执行Function中的apply方法，apply方法返回的结果可以是任意结果，map方法的结果，把apply方法的结果包装成一个Optional对象

- <U> Optional<U> flatMap(Function<? super T,Optional<U>> mapper)  

  - 对Optional包装对象，执行Function中的apply方法，apply方法返回的结果是一个Optional，map方法的结果，把apply方法的结果直接返回

