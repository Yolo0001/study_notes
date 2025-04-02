# Spring教程目录

## 第一章 IOC容器

### 第一节 Spring简介

####  3、Spring Framework

Spring 基础框架，可以视为 Spring 基础设施，基本上任何其他 Spring 项目都是以 Spring Framework 为基础的。

 ①Spring Framework优良特性
- 非侵入式：使用 Spring Framework 开发应用程序时，Spring 对应用程序本身的结构影响非常小。对领域模型可以做到零污染；对功能性组件也只需要使用几个简单的注解进行标记，完全不会破坏原有结构，反而能将组件结构进一步简化。这就使得基于 Spring Framework 开发应用程序时结构清晰、简洁优雅。
- 控制反转：IOC——Inversion of Control，翻转资源获取方向。把自己创建资源、向环境索取资源变成环境将资源准备好，我们享受资源注入。
- 面向切面编程：AOP——Aspect Oriented Programming，在不修改源代码的基础上增强代码功能。
- 容器：Spring IOC 是一个容器，因为它包含并且管理组件对象的生命周期。组件享受到了容器化的管理，替程序员屏蔽了组件创建过程中的大量细节，极大的降低了使用门槛，大幅度提高了开发效率。
- 组件化：Spring 实现了使用简单的组件配置组合成一个复杂的应用。在 Spring 中可以使用 XML 和 Java 注解组合这些对象。这使得我们可以基于一个个功能明确、边界清晰的组件有条不紊的搭建超大型复杂应用系统。
- 声明式：很多以前需要编写代码才能实现的功能，现在只需要声明需求即可由框架代为实现。
- 一站式：在 IOC 和 AOP 的基础上可以整合各种企业应用的开源框架和优秀的第三方类库。而且 Spring 旗下的项目已经覆盖了广泛领域，很多方面的功能性需求可以在 Spring Framework 的基础上全部使用 Spring 来实现。

 ②Spring Framework五大功能模块

| 功能模块                | 功能介绍                                                    |
| ----------------------- | ----------------------------------------------------------- |
| Core Container          | 核心容器，在 Spring 环境下使用任何功能都必须基于 IOC 容器。 |
| AOP&Aspects             | 面向切面编程                                                |
| Testing                 | 提供了对 junit 或 TestNG 测试框架的整合。                   |
| Data Access/Integration | 提供了对数据访问/集成的功能。                               |
| Spring MVC              | 提供了面向Web应用程序的集成功能。                           |

### 第二节 IOC容器概念

我们即将要学习的 IOC 容器也是一个复杂容器。它们不仅要负责**创建**组件的对象、**存储**组件的对象，还要负责**调用**组件的方法让它们工作，最终在特定情况下**销毁**组件。

 [1]Servlet生命周期

| 名称       | 时机                                                         | 次数 |
| ---------- | ------------------------------------------------------------ | ---- |
| 创建对象   | 默认情况：接收到第一次请求 修改启动顺序后：Web应用启动过程中 | 一次 |
| 初始化操作 | 创建对象之后                                                 | 一次 |
| 处理请求   | 接收到请求                                                   | 多次 |
| 销毁操作   | Web应用卸载之前                                              | 一次 |

 [2]Filter生命周期

| 生命周期阶段 | 执行时机         | 执行次数 |
| ------------ | ---------------- | -------- |
| 创建对象     | Web应用启动时    | 一次     |
| 初始化       | 创建对象后       | 一次     |
| 拦截请求     | 接收到匹配的请求 | 多次     |
| 销毁         | Web应用卸载前    | 一次     |

#### 3、IOC思想

IOC：Inversion of Control，翻译过来是**反转控制**。

DI：Dependency Injection，翻译过来是**依赖注入**。

DI 是 IOC 的另一种表述方式：即组件以一些预先定义好的方式（例如：setter 方法）接受来自于容器的资源注入。相对于IOC而言，这种表述更直接。



所以结论是：IOC 就是一种反转控制的思想， 而 DI 是对 IOC 的一种具体实现。

#### 4、 IOC容器在Spring中的实现

Spring 的 IOC 容器就是 IOC 思想的一个落地的产品实现。IOC 容器中管理的组件也叫做 bean。在创建 bean 之前，首先需要创建 IOC 容器。Spring 提供了 IOC 容器的两种实现方式：

##### ①BeanFactory

这是 IOC 容器的基本实现，是 Spring 内部使用的接口。面向 Spring 本身，不提供给开发人员使用。

##### ②ApplicationContext

BeanFactory 的子接口，提供了更多高级特性。面向 Spring 的使用者，几乎所有场合都使用 ApplicationContext 而不是底层的 BeanFactory。

> 以后在 Spring 环境下看到一个类或接口的名称中包含 ApplicationContext，那基本就可以断定，这个类或接口与 IOC 容器有关。

##### ③ApplicationContext的主要实现类

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-04-24 163550.png)

| 类型名                          | 简介                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| ClassPathXmlApplicationContext  | 通过读取类路径下的 XML 格式的配置文件创建 IOC 容器对象       |
| FileSystemXmlApplicationContext | 通过文件系统路径读取 XML 格式的配置文件创建 IOC 容器对象     |
| ConfigurableApplicationContext  | ApplicationContext 的子接口，包含一些扩展方法 refresh() 和 close() ，让 ApplicationContext 具有启动、关闭和刷新上下文的能力。 |
| WebApplicationContext           | 专门为 Web 应用准备，基于 Web 环境创建 IOC 容器对象，并将对象引入存入 ServletContext 域中。 |

### 第三节 基于XML管理bean

#### [实验一 重要]创建bean

1. 添加jar包
2. 创建组件类

```java
package com.atguigu.ioc.component;

public class HappyComponent {
    public void doWork() {
        System.out.println("component do work ...");
    }
}
```

3. 创建 Spring 配置文件

```xml
<!-- 实验一 [重要]创建bean -->
<bean id="happyComponent" class="com.atguigu.ioc.component.HappyComponent"/>
```

4. 创建测试类

```java
public class IOCTest {
    // 创建 IOC 容器对象，为便于其他实验方法使用声明为成员变量
    private ApplicationContext iocContainer = new ClassPathXmlApplicationContext("applicationContext.xml");

    @Test
    public void testExperiment01() {

        // 从 IOC 容器对象中获取bean，也就是组件对象
        HappyComponent happyComponent = (HappyComponent) iocContainer.getBean("happyComponent");
        happyComponent.doWork();

    }
}
```

5. 无参构造器

Spring 底层默认通过反射技术调用组件类的无参构造器来创建组件对象，这一点需要注意。如果在需要无参构造器时，没有无参构造器，则会抛出异常.

所以对一个JavaBean来说，**无参构造器**和**属性的getXxx()、setXxx()方法**是**必须存在**的，特别是在框架中。

#### [实验二 重要]获取bean

1、方式一：根据id获取

由于 id 属性指定了 bean 的唯一标识，所以根据 bean 标签的 id 属性可以精确获取到一个组件对象。上个实验中我们使用的就是这种方式。

2、方式二：根据类型

①指定类型的 bean 唯一

```java
@Test
public void testExperiment02() {
    HappyComponent component = iocContainer.getBean(HappyComponent.class);
    component.doWork();
}
```

②指定类型的 bean 不唯一

相同类型的 bean 在IOC容器中一共配置了两个：

```java
<!-- 实验一 [重要]创建bean -->
<bean id="happyComponent" class="com.atguigu.ioc.component.HappyComponent"/>

<!-- 实验二 [重要]获取bean -->
<bean id="happyComponent2" class="com.atguigu.ioc.component.HappyComponent"/>
```

根据类型获取时会抛出异常.

③思考

如果组件类实现了接口，根据接口类型可以获取 bean 吗？

> 可以，前提是bean唯一

如果一个接口有多个实现类，这些实现类都配置了 bean，根据接口类型可以获取 bean 吗？

> 不行，因为bean不唯一

④结论

根据类型来获取bean时，在满足bean唯一性的前提下，其实只是看：『对象 **instanceof** 指定的类型』的返回结果，只要返回的是true就可以认定为和类型匹配，能够获取到。

#### [实验三 重要]给bean的属性赋值：setter注入

1、给组件类添加一个属性

```java
public class HappyComponent {

    private String componentName;

    public String getComponentName() {
        return componentName;
    }

    public void setComponentName(String componentName) {
        this.componentName = componentName;
    }

    public void doWork() {
        System.out.println("component do work ...");
    }

}
```

2、在配置时给属性指定值

通过property标签配置的属性值会通过setXxx()方法注入，大家可以通过debug方式验证一下

```java
<!-- 实验三 [重要]给bean的属性赋值：setter注入 -->
<bean id="happyComponent3" class="com.atguigu.ioc.component.HappyComponent">
    
    <!-- property标签：通过组件类的setXxx()方法给组件对象设置属性 -->
    <!-- name属性：指定属性名（这个属性名是getXxx()、setXxx()方法定义的，和成员变量无关） -->
    <!-- value属性：指定属性值 -->
    <property name="componentName" value="veryHappy"/>
</bean>
```

3、测试

```java
@Test
public void testExperiment03() {
    
    HappyComponent happyComponent3 = (HappyComponent) iocContainer.getBean("happyComponent3");
    
    String componentName = happyComponent3.getComponentName();
    
    System.out.println("componentName = " + componentName);
    
}
```

#### [实验四 重要]给bean的属性赋值：引用外部已声明的bean

#### [实验五 重要]给bean的属性赋值：内部bean

#### [实验六 重要]给bean的属性赋值：引入外部属性文件

#### 实验七 给bean的属性赋值：级联属性赋值

#### 实验八 给bean的属性赋值：构造器注入

#### 实验九 给bean的属性赋值：特殊值处理

#### 实验十 给bean的属性赋值：使用p名称空间

#### 实验十一 给bean的属性赋值：集合属性

#### 实验十二 给bean的属性赋值：自动装配

#### 实验十三 集合类型的bean

#### 实验十四 FactoryBean机制

FactoryBean 是 Spring 提供的一种**整合第三方框架**的常用机制。和普通的 bean 不同，配置一个 FactoryBean 类型的 bean，在获取 bean 的时候得到的并不是 class 属性中配置的这个类的对象，而是 getObject() 方法的返回值。通过这种机制，Spring 可以帮我们把复杂组件创建的详细过程和繁琐细节都屏蔽起来，只把最简洁的使用界面展示给我们。

将来我们整合 Mybatis 时，Spring 就是通过 FactoryBean 机制来帮我们创建 SqlSessionFactory 对象的。

#### 实验十五 bean的作用域

在 Spring 中可以通过配置 bean 标签的 scope 属性来指定 bean 的作用域范围，各取值含义参加下表：

| 取值      | 含义                                        | 创建对象的时机   | 默认值 |
| --------- | ------------------------------------------- | ---------------- | ------ |
| singleton | 在 IOC 容器中，这个 bean 的对象始终为单实例 | IOC 容器初始化时 | 是     |
| prototype | 这个 bean 在 IOC 容器中有多个实例           | 获取 bean 时     | 否     |

如果是在WebApplicationContext环境下还会有另外两个作用域（但不常用）：

| 取值    | 含义                 |
| ------- | -------------------- |
| request | 在一个请求范围内有效 |
| session | 在一个会话范围内有效 |

#### 实验十六 bean的生命周期

### 第四节 基于注解管理bean

#### [第一个实验 重要]标记与扫描

##### 1、注解的作用

###### ①注解

和 XML 配置文件一样，注解本身并不能执行，注解本身仅仅只是做一个标记，具体的功能是框架检测到注解标记的位置，然后针对这个位置按照注解标记的功能来执行具体操作。

本质上：所有一切的操作都是 Java 代码来完成的，XML 和注解只是告诉框架中的 Java 代码如何执行。

###### ②扫描

Spring 为了知道程序员在哪些地方标记了什么注解，就需要通过扫描的方式，来进行检测。然后根据注解进行后续操作。

##### 2、新建Module

```xml
<dependencies>
    
    <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.1</version>
    </dependency>
    
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    
</dependencies>
```

##### 3、创建Spring配置文件

resources/application.xml

##### 4、创建一组组件类

###### ①使用@Component注解标记的普通组件

```java
package com.atguigu.ioc.component;

import org.springframework.stereotype.Component;

@Component
public class CommonComponent {
}
```

###### ②使用@Controller注解标记的控制器组件

这个组件就是我们在三层架构中表述层里面，使用的控制器。以前是Servlet，以后我们将会使用Controller来代替Servlet。

```java
package com.atguigu.ioc.component;

import org.springframework.stereotype.Controller;

@Controller
public class SoldierController {
}
```

###### ③使用@Service注解标记的业务逻辑组件

这个组件就是我们在三层架构中使用的业务逻辑组件。

```java
package com.atguigu.ioc.component;

import org.springframework.stereotype.Service;

@Service
public class SoldierService {

}
```

###### ④使用@Repository注解标记的持久化层组件

```java
package com.atguigu.ioc.component;

import org.springframework.stereotype.Repository;

@Repository
public class SoldierDao {
}
```

这个组件就是我们以前用的Dao类，但是以后我们整合了Mybatis，这里就变成了Mapper接口，而Mapper接口是由Mybatis和Spring的整合包负责扫描的。

由于Mybatis整合包想要把Mapper接口背后的代理类加入Spring的IOC容器需要结合Mybatis对Mapper配置文件的解析，所以这个事情是Mybatis和Spring的整合包来完成，将来由Mybatis负责扫描，也不使用@Repository注解。

##### 5、四个典型注解没有本质区别

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 180510.png)

通过查看源码我们得知，@Controller、@Service、@Repository这三个注解只是在@Component注解的基础上起了三个新的名字。

对于Spring使用IOC容器管理这些组件来说没有区别，也就是语法层面没有区别。所以@Controller、@Service、@Repository这三个注解只是给开发人员看的，让我们能够便于分辨组件的作用。

注意：虽然它们本质上一样，但是为了代码的可读性，为了程序结构严谨我们肯定不能随便胡乱标记。

##### 6、扫描

###### ①情况一：最基本的扫描方式常用

```xml
<!-- 配置自动扫描的包 -->
<!-- 最基本的扫描方式 -->
<context:component-scan base-package="com.atguigu.ioc.component"/>
```

从IOC容器中获取bean：

```java
@Test
public void testAnnotationcScanBean() {
    CommonComponent commonComponent = iocContainer.getBean(CommonComponent.class);
    
    SoldierController soldierController = iocContainer.getBean(SoldierController.class);
    
    SoldierService soldierService = iocContainer.getBean(SoldierService.class);
    
    SoldierDao soldierDao = iocContainer.getBean(SoldierDao.class);
    
    System.out.println("commonComponent = " + commonComponent);
    System.out.println("soldierController = " + soldierController);
    System.out.println("soldierService = " + soldierService);
    System.out.println("soldierDao = " + soldierDao);
}
```

###### ②情况二：指定匹配模式

```xml
    <!-- 情况二：在指定扫描包的基础上指定匹配模式 -->
    <context:component-scan
            base-package="com.atguigu.ioc.component"
            resource-pattern="Soldier*.class"/>
```

###### ③情况三：指定要排除的组件

```xml
<!-- 情况三：指定不扫描的组件 -->
<context:component-scan base-package="com.atguigu.ioc.component">
    
    <!-- context:exclude-filter标签：指定排除规则 -->
    <!-- type属性：指定根据什么来进行排除，annotation取值表示根据注解来排除 -->
    <!-- expression属性：指定排除规则的表达式，对于注解来说指定全类名即可 -->
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```

###### ④情况四：仅扫描指定组件

```xml
<!-- 情况四：仅扫描指定的组件 -->
<!-- 仅扫描 = 关闭默认规则 + 追加规则 -->
<!-- use-default-filters属性：取值false表示关闭默认扫描规则 -->
<context:component-scan base-package="com.atguigu.ioc.component" use-default-filters="false">
    
    <!-- context:include-filter标签：指定在原有扫描规则的基础上追加的规则 -->
    <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```

##### 7、组件的beanName

在我们使用 XML 方式管理 bean 的时候，每个 bean 都有一个唯一标识——id 属性的值，便于在其他地方引用。现在使用注解后，每个组件仍然应该有一个唯一标识。

###### ①默认情况

类名首字母小写就是 bean 的 id。例如：SoldierController 类对应的 bean 的 id 就是 soldierController。

###### ②使用value属性指定

```java
@Controller(value = "tianDog")
public class SoldierController {
}
```

当注解中只设置一个属性时，value属性的属性名可以省略：

```java
@Service("smallDog")
public class SoldierService {

}
```

#### [第二个实验 重要]自动装配

##### 1、设定情景

- SoldierController 需要 SoldierService
- SoldierService 需要 SoldierDao

同时在各个组件中声明要调用的方法。

###### ①在SoldierController中声明方法

```java
package com.atguigu.ioc.component;

import org.springframework.stereotype.Controller;

@Controller(value = "tianDog")
public class SoldierController {

    private SoldierService soldierService;

    public void getMessage() {
        soldierService.getMessage();
    }

}
```

###### ②在SoldierService中声明方法

```java
@Service("smallDog")
public class SoldierService {

    private SoldierDao soldierDao;

    public void getMessage() {
        soldierDao.getMessage();
    }
}
```

###### ③在SoldierDao中声明方法

```java
@Repository
public class SoldierDao {

    public void getMessage() {
        System.out.println("I am a soldier");
    }

}
```

##### 2、自动装配的实现

###### ①前提

参与自动装配的组件（需要装配别人、被别人装配）全部都必须在IOC容器中。

###### ②@Autowired注解

在成员变量上直接标记@Autowired注解即可，**不需要提供setXxx()方法**。以后我们在项目中的正式用法就是这样。

###### [1]给Controller装配Service

```java
@Controller(value = "tianDog")
public class SoldierController {
    
    @Autowired
    private SoldierService soldierService;
    
    public void getMessage() {
        soldierService.getMessage();
    }
    
}
```

###### [2]给Service装配Dao

```java
@Service("smallDog")
public class SoldierService {
    
    @Autowired
    private SoldierDao soldierDao;
    
    public void getMessage() {
        soldierDao.getMessage();
    }
}
```

##### 3、@Autowired注解其他细节

###### ①标记在其他位置

###### [1]构造器

```java
@Controller(value = "tianDog")
public class SoldierController {
    
    private SoldierService soldierService;
    
    @Autowired
    public SoldierController(SoldierService soldierService) {
        this.soldierService = soldierService;
    }
    ……
```

#### [2]setXxx()方法

```java
@Controller(value = "tianDog")
public class SoldierController {

    private SoldierService soldierService;

    @Autowired
    public void setSoldierService(SoldierService soldierService) {
        this.soldierService = soldierService;
    }
    ……
```

###### ②@Autowired 工作流程

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 181636.png)

- 首先根据所需要的组件类型到 IOC 容器中查找
  - 能够找到唯一的 bean：直接执行装配
  - 如果完全找不到匹配这个类型的 bean：装配失败
  - 和所需类型匹配的 bean 不止一个
    - 没有 @Qualifier 注解：根据 @Autowired 标记位置成员变量的变量名作为 bean 的 id 进行匹配
      - 能够找到：执行装配
      - 找不到：装配失败
    - 使用 @Qualifier 注解：根据 @Qualifier 注解中指定的名称作为 bean 的id进行匹配
      - 能够找到：执行装配
      - 找不到：装配失败

```java
@Controller(value = "tianDog")
public class SoldierController {
    
    @Autowired
    @Qualifier(value = "maomiService222")
    // 根据面向接口编程思想，使用接口类型引入Service组件
    private ISoldierService soldierService;
```

###### ③佛系装配

给 @Autowired 注解设置 required = false 属性表示：能装就装，装不上就不装。但是实际开发时，基本上所有需要装配组件的地方都是必须装配的，用不上这个属性。

```java
@Controller(value = "tianDog")
public class SoldierController {

    // 给@Autowired注解设置required = false属性表示：能装就装，装不上就不装
    @Autowired(required = false)
    private ISoldierService soldierService;
```

> WARNING
>
> 如果类中同时存在装配属性的 setXxx() 方法会使 required = false 设定失效。

#### 第三个实验 完全注解开发

##### 1、使用配置类取代配置文件

体验完全注解开发，是为了给将来学习 SpringBoot 打基础。因为在 SpringBoot 中，就是完全舍弃 XML 配置文件，全面使用注解来完成主要的配置。

###### ①创建配置类

使用 @Configuration 注解将一个普通的类标记为 Spring 的配置类。

```java
package com.atguigu.ioc.configuration;
    
import org.springframework.context.annotation.Configuration;
    
@Configuration
public class MyConfiguration {
}
```

###### ②根据配置类创建IOC容器对象

```java
// ClassPathXmlApplicationContext 根据 XML配置文件创建 IOC 容器对象
private ApplicationContext iocContainer = new ClassPathXmlApplicationContext("applicationContext.xml");

// AnnotationConfigApplicationContext 根据配置类创建 IOC 容器对象
private ApplicationContext iocContainerAnnotation = new AnnotationConfigApplicationContext(MyConfiguration.class);
```

##### 2、在配置类中配置bean

使用@Bean注解

```java
@Configuration
public class MyConfiguration {
    
    // @Bean 注解相当于 XML 配置文件中的 bean 标签
    // @Bean 注解标记的方法的返回值会被放入 IOC 容器
    // 默认以方法名作为 bean 的 id
    @Bean
    public CommonComponent getComponent() {
    
        CommonComponent commonComponent = new CommonComponent();
    
        commonComponent.setComponentName("created by annotation config");
    
        return commonComponent;
    }
    
}
```

##### 3、在配置类中配置自动扫描的包

```java
@Configuration
@ComponentScan("com.atguigu.ioc.component")
public class MyConfiguration {
    ……
```

#### 第四个实验 整合junit4

##### 1、整合的好处

- 好处1：不需要自己创建IOC容器对象了
- 好处2：任何需要的bean都可以在测试类中直接享受自动装配

##### 2、操作

###### ①加入依赖

```xml
<!-- Spring的测试包 -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>5.3.1</version>
</dependency>
```

###### ②创建测试类

```java
// junit的@RunWith注解：指定Spring为Junit提供的运行器
@RunWith(SpringJUnit4ClassRunner.class)

// Spring的@ContextConfiguration指定Spring配置文件的位置
@ContextConfiguration(value = {"classpath:applicationContext.xml"})
public class JunitIntegrationSpring {
    
    @Autowired
    private SoldierController soldierController;
    
    @Test
    public void testIntegration() {
        System.out.println("soldierController = " + soldierController);
    }
    
}
```

## 第二章 AOP面向切面编程

### 第一节 情景设定

#### 1、声明接口

```java
public interface Calculator {
    int add(int i, int j);
    int sub(int i, int j);
    int mul(int i, int j);
    int div(int i, int j);
}
```

#### 2、给接口声明一个纯净版实现

```java
package com.atguigu.proxy.imp;
    
import com.atguigu.proxy.api.Calculator;
    
public class CalculatorPureImpl implements Calculator {
    
    @Override
    public int add(int i, int j) {
        int result = i + j;
        System.out.println("方法内部 result = " + result);
        return result;
    }
    
    @Override
    public int sub(int i, int j) {
        int result = i - j;
        System.out.println("方法内部 result = " + result);
        return result;
    }
    
    @Override
    public int mul(int i, int j) {
        int result = i * j;
        System.out.println("方法内部 result = " + result);
        return result;
    }
    
    @Override
    public int div(int i, int j) {
        int result = i / j;
        System.out.println("方法内部 result = " + result);
        return result;
    }
}
```

#### 3、再声明一个带日志功能的实现

```java
package com.atguigu.proxy.imp;

import com.atguigu.proxy.api.Calculator;

public class CalculatorLogImpl implements Calculator {
    
    @Override
    public int add(int i, int j) {
        System.out.println("[日志] add 方法开始了，参数是：" + i + "," + j);
        int result = i + j;
        System.out.println("方法内部 result = " + result);
        System.out.println("[日志] add 方法结束了，结果是：" + result);
        return result;
    }
    
    @Override
    public int sub(int i, int j) {
        System.out.println("[日志] sub 方法开始了，参数是：" + i + "," + j);
        int result = i - j;
        System.out.println("方法内部 result = " + result);
        System.out.println("[日志] sub 方法结束了，结果是：" + result);
        return result;
    }
    
    @Override
    public int mul(int i, int j) {
        System.out.println("[日志] mul 方法开始了，参数是：" + i + "," + j);
        int result = i * j;
        System.out.println("方法内部 result = " + result);
        System.out.println("[日志] mul 方法结束了，结果是：" + result);
        return result;
    }
    
    @Override
    public int div(int i, int j) {
        System.out.println("[日志] div 方法开始了，参数是：" + i + "," + j);
        int result = i / j;
        System.out.println("方法内部 result = " + result);
        System.out.println("[日志] div 方法结束了，结果是：" + result);
        return result;
    }
}
```

#### 4、提出问题

##### ①现有代码缺陷

针对带日志功能的实现类，我们发现有如下缺陷：

- 对核心业务功能有干扰，导致程序员在开发核心业务功能时分散了精力
- 附加功能分散在各个业务功能方法中，不利于统一维护

##### ②解决思路

解决这两个问题，核心就是：**解耦**。我们需要把附加功能从业务功能代码中抽取出来。

##### ③困难

解决问题的困难：要抽取的代码在方法内部，靠以前把子类中的重复代码抽取到父类的方式没法解决。所以需要引入新的技术。

### 第二节 代理模式

#### 1、概念

##### ①介绍

二十三种设计模式中的一种，属于结构型模式。它的作用就是通过提供一个代理类，让我们在调用目标方法的时候，不再是直接对目标方法进行调用，而是通过代理类**间接**调用。让不属于目标方法核心逻辑的代码从目标方法中剥离出来——**解耦**。调用目标方法时先调用代理对象的方法，减少对目标方法的调用和打扰，同时让附加功能能够集中在一起也有利于统一维护。

##### ②生活中的代理

##### ③相关术语

- 代理：将非核心逻辑剥离出来以后，封装这些非核心逻辑的类、对象、方法。
- 目标：被代理“套用”了非核心逻辑代码的类、对象、方法。

> 理解代理模式、AOP的核心关键词就一个字：**套**

#### 2、静态代理

```java
public class CalculatorStaticProxy implements Calculator {
    
    // 将被代理的目标对象声明为成员变量
    private Calculator target;
    
    public CalculatorStaticProxy(Calculator target) {
        this.target = target;
    }
    
    @Override
    public int add(int i, int j) {
    
        // 附加功能由代理类中的代理方法来实现
        System.out.println("[日志] add 方法开始了，参数是：" + i + "," + j);
    
        // 通过目标对象来实现核心业务逻辑
        int addResult = target.add(i, j);
    
        System.out.println("[日志] add 方法结束了，结果是：" + addResult);
    
        return addResult;
    }
    ……
```

静态代理确实实现了解耦，但是由于代码都**写死了**，完全不具备任何的灵活性。就拿日志功能来说，将来其他地方也需要附加日志，那还得再声明更多个静态代理类，那就产生了大量重复的代码，日志功能还是分散的，没有统一管理。

提出进一步的需求：将日志功能集中到一个代理类中，将来有任何日志需求，都通过这一个代理类来实现。这就需要使用动态代理技术了。

#### 3、动态代理

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 182931.png)

##### ①生产代理对象的工厂类

JDK本身就支持动态代理，这是反射技术的一部分。下面我们还是创建一个代理类（生产代理对象的工厂类）：

```java
// 泛型T要求是目标对象实现的接口类型，本代理类根据这个接口来进行代理
public class LogDynamicProxyFactory<T> {
    
    // 将被代理的目标对象声明为成员变量
    private T target;
    
    public LogDynamicProxyFactory(T target) {
        this.target = target;
    }
    
    public T getProxy() {
        // 创建代理对象所需参数一：加载目标对象的类的类加载器
        ClassLoader classLoader = target.getClass().getClassLoader();
        // 创建代理对象所需参数二：目标对象的类所实现的所有接口组成的数组
        Class<?>[] interfaces = target.getClass().getInterfaces();
        // 创建代理对象所需参数三：InvocationHandler对象
        // Lambda表达式口诀：
        // 1、复制小括号
        // 2、写死右箭头
        // 3、落地大括号
        InvocationHandler handler = (
                                    // 代理对象，当前方法用不上这个对象
                                    Object proxy,
                                     // method就是代表目标方法的Method对象
                                     Method method,
                                     // 外部调用目标方法时传入的实际参数
                                     Object[] args)->{
            // 我们对InvocationHandler接口中invoke()方法的实现就是在调用目标方法
            // 围绕目标方法的调用，就可以添加我们的附加功能
            
            // 声明一个局部变量，用来存储目标方法的返回值
            Object targetMethodReturnValue = null;
            // 通过method对象获取方法名
            String methodName = method.getName();
            // 为了便于在打印时看到数组中的数据，把参数数组转换为List
            List<Object> argumentList = Arrays.asList(args);
            try {
                // 在目标方法执行前：打印方法开始的日志
                System.out.println("[动态代理][日志] " + methodName + " 方法开始了，参数是：" + argumentList);
                // 调用目标方法：需要传入两个参数
                // 参数1：调用目标方法的目标对象
                // 参数2：外部调用目标方法时传入的实际参数
                // 调用后会返回目标方法的返回值
                targetMethodReturnValue = method.invoke(target, args);
                // 在目标方法成功后：打印方法成功结束的日志【寿终正寝】
                System.out.println("[动态代理][日志] " + methodName + " 方法成功结束了，返回值是：" + targetMethodReturnValue);
            }catch (Exception e){
                // 通过e对象获取异常类型的全类名
                String exceptionName = e.getClass().getName();
                // 通过e对象获取异常消息
                String message = e.getMessage();
                // 在目标方法失败后：打印方法抛出异常的日志【死于非命】
                System.out.println("[动态代理][日志] " + methodName + " 方法抛异常了，异常信息是：" + exceptionName + "," + message);
    
            }finally {
                // 在目标方法最终结束后：打印方法最终结束的日志【盖棺定论】
                System.out.println("[动态代理][日志] " + methodName + " 方法最终结束了");
    
            }
            // 这里必须将目标方法的返回值返回给外界，如果没有返回，外界将无法拿到目标方法的返回值
            return targetMethodReturnValue;
        };
    
        // 创建代理对象
        T proxy = (T) Proxy.newProxyInstance(classLoader, interfaces, handler);
    
        // 返回代理对象
        return proxy;
    }
}
```

##### ②测试

```java
@Test
public void testDynamicProxy() {
    
    // 1.创建被代理的目标对象
    Calculator target = new CalculatorPureImpl();
    
    // 2.创建能够生产代理对象的工厂对象
    LogDynamicProxyFactory<Calculator> factory = new LogDynamicProxyFactory<>(target);
    
    // 3.通过工厂对象生产目标对象的代理对象
    Calculator proxy = factory.getProxy();
    
    // 4.通过代理对象间接调用目标对象
    int addResult = proxy.add(10, 2);
    System.out.println("方法外部 addResult = " + addResult + "\n");
    
    int subResult = proxy.sub(10, 2);
    System.out.println("方法外部 subResult = " + subResult + "\n");
    
    int mulResult = proxy.mul(10, 2);
    System.out.println("方法外部 mulResult = " + mulResult + "\n");
    
    int divResult = proxy.div(10, 2);
    System.out.println("方法外部 divResult = " + divResult + "\n");
}
```

##### ③练习

动态代理的实现过程不重要，重要的是使用现成的动态代理类去**套**用到其他目标对象上。

声明另外一个接口：

```java
public interface SoldierService {
    
    int saveSoldier(String soldierName);
    
    int removeSoldier(Integer soldierId);
    
    int updateSoldier(Integer soldierId, String soldierName);
    
    String getSoldierNameById(Integer soldierId);
    
}
```

```java
public class SoldierServiceImpl implements SoldierService {
    
    @Override
    public int saveSoldier(String soldierName) {
    
        System.out.println("核心业务逻辑：保存到数据库……");
    
        return 1;
    }
    
    @Override
    public int removeSoldier(Integer soldierId) {
    
        System.out.println("核心业务逻辑：从数据库删除……");
    
        return 1;
    }
    
    @Override
    public int updateSoldier(Integer soldierId, String soldierName) {
    
        System.out.println("核心业务逻辑：更新……");
    
        return 1;
    }

    @Override
    public String getSoldierNameById(Integer soldierId) {
    
        System.out.println("核心业务逻辑：查询数据库……");
    
        return "good";
    }
}
```

```java
@Test
public void testSoldierServiceDynamicProxy() {
    
    // 1.创建被代理的目标对象
    SoldierService soldierService = new SoldierServiceImpl();
    
    // 2.创建生产代理对象的工厂对象
    LogDynamicProxyFactory<SoldierService> factory = new LogDynamicProxyFactory<>(soldierService);
    
    // 3.生产代理对象
    SoldierService proxy = factory.getProxy();
    
    // 4.通过代理对象调用目标方法
    String soldierName = proxy.getSoldierNameById(1);
    System.out.println("soldierName = " + soldierName);
    
}
```

### 第三节 AOP的核心套路

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 183945.png)

### 第四节 AOP术语

#### 1、AOP概念介绍

##### ①名词解释

AOP：**A**spect **O**riented **P**rogramming面向切面编程

##### ②AOP的作用

下面两点是同一件事的两面，一枚硬币的两面：

- 简化代码：把方法中固定位置的重复的代码**抽取**出来，让被抽取的方法更专注于自己的核心功能，提高内聚性。
- 代码增强：把特定的功能封装到切面类中，看哪里有需要，就往上套，被**套用**了切面逻辑的方法就被切面给增强了

#### 2、横切关注点

从每个方法中抽取出来的同一类非核心业务。在同一个项目中，我们可以使用多个横切关注点对相关方法进行多个不同方面的增强。

这个概念不是语法层面天然存在的，而是根据附加功能的逻辑上的需要：有十个附加功能，就有十个横切关注点。

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 184916.png)

#### 3、通知[记住]

每一个横切关注点上要做的事情都需要写一个方法来实现，这样的方法就叫通知方法。

- 前置通知：在被代理的目标方法**前**执行
- 返回通知：在被代理的目标方法**成功结束**后执行（**寿终正寝**）
- 异常通知：在被代理的目标方法**异常结束**后执行（**死于非命**）
- 后置通知：在被代理的目标方法**最终结束**后执行（**盖棺定论**）
- 环绕通知：使用try...catch...finally结构围绕**整个**被代理的目标方法，包括上面四种通知对应的所有位置

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 184927.png)

#### 4、切面[记住]

封装通知方法的类。

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 184948.png)

#### 5、目标

被代理的目标对象。

#### 6、代理

向目标对象应用通知之后创建的代理对象。

#### 7、连接点

这也是一个纯逻辑概念，不是语法定义的。

把方法排成一排，每一个横切位置看成x轴方向，把方法从上到下执行的顺序看成y轴，x轴和y轴的交叉点就是连接点。

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 185002.png)

#### 8、切入点[记住]

定位连接点的方式。

每个类的方法中都包含多个连接点，所以连接点是类中客观存在的事物（从逻辑上来说）。

如果把连接点看作数据库中的记录，那么切入点就是查询记录的 SQL 语句。

Spring 的 AOP 技术可以通过切入点定位到特定的连接点。

切点通过 org.springframework.aop.Pointcut 接口进行描述，它使用类和方法作为连接点的查询条件。

### 第五节 基于注解的AOP

#### 1、基于注解的AOP用到的技术

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 185344.png" style="zoom:60%;" />

- 动态代理（InvocationHandler）：JDK原生的实现方式，需要被代理的目标类必须实现接口。因为这个技术要求**代理对象和目标对象实现同样的接口**（兄弟两个拜把子模式）。
- cglib：通过**继承被代理的目标类**（认干爹模式）实现代理，所以不需要目标类实现接口。
- AspectJ：本质上是静态代理，**将代理逻辑“织入”被代理的目标类编译得到的字节码文件**，所以最终效果是动态的。weaver就是织入器。Spring只是借用了AspectJ中的注解。

#### 2、实验操作

##### 实验一 初步实现

###### 1、加入依赖

```xml
        <!-- spring-aspects会帮我们传递过来aspectjweaver -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aspects</artifactId>
            <version>5.3.1</version>
        </dependency>
```

###### 2、准备被代理的目标资源

###### ①接口

```java
public interface Calculator {
    
    int add(int i, int j);
    
    int sub(int i, int j);
    
    int mul(int i, int j);
    
    int div(int i, int j);
    
}
```

###### ②纯净的实现类

在 Spring 下工作，所有的一切都必须放在 IOC 容器中。现在接口的实现类是 AOP 要代理的目标类，所以它也必须放入 IOC 容器。

```java
package com.atguigu.aop.imp;
    
import com.atguigu.aop.api.Calculator;
import org.springframework.stereotype.Component;
    
@Component
public class CalculatorPureImpl implements Calculator {
    
    @Override
    public int add(int i, int j) {
    
        int result = i + j;
    
        System.out.println("方法内部 result = " + result);
    
        return result;
    }
    
    @Override
    public int sub(int i, int j) {
    
        int result = i - j;
    
        System.out.println("方法内部 result = " + result);
    
        return result;
    }
    
    @Override
    public int mul(int i, int j) {
    
        int result = i * j;
    
        System.out.println("方法内部 result = " + result);
    
        return result;
    }
    
    @Override
    public int div(int i, int j) {
    
        int result = i / j;
    
        System.out.println("方法内部 result = " + result);
    
        return result;
    }
}
```

###### 3、创建切面类

```java
// @Aspect表示这个类是一个切面类
@Aspect
// @Component注解保证这个切面类能够放入IOC容器
@Component
public class LogAspect {
        
    // @Before注解：声明当前方法是前置通知方法
    // value属性：指定切入点表达式，由切入点表达式控制当前通知方法要作用在哪一个目标方法上
    @Before(value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))")
    public void printLogBeforeCore() {
        System.out.println("[AOP前置通知] 方法开始了");
    }
    
    @AfterReturning(value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))")
    public void printLogAfterSuccess() {
        System.out.println("[AOP返回通知] 方法成功返回了");
    }
    
    @AfterThrowing(value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))")
    public void printLogAfterException() {
        System.out.println("[AOP异常通知] 方法抛异常了");
    }
    
    @After(value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))")
    public void printLogFinallyEnd() {
        System.out.println("[AOP后置通知] 方法最终结束了");
    }
    
}
```

###### 4、创建Spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    
    <!-- 开启基于注解的AOP功能 -->
    <aop:aspectj-autoproxy/>
    
    <!-- 配置自动扫描的包 -->
    <context:component-scan base-package="com.atguigu.aop"/>
    
</beans>
```

###### 5、测试

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(value = {"classpath:applicationContext.xml"})
public class AOPTest {
    
    @Autowired
    private Calculator calculator;
    
    @Test
    public void testAnnotationAOP() {
    
        int add = calculator.add(10, 2);
        System.out.println("方法外部 add = " + add);
    
    }
    
}
```

打印效果如下：

> [AOP前置通知] 方法开始了 方法内部 result = 12 [AOP返回通知] 方法成功返回了 [AOP后置通知] 方法最终结束了 方法外部 add = 12

###### 6、通知执行顺序

- Spring版本5.3.x以前：
  - 前置通知
  - 目标操作
  - 后置通知
  - 返回通知或异常通知
- Spring版本5.3.x以后：
  - 前置通知
  - 目标操作
  - 返回通知或异常通知
  - 后置通知

##### 实验二 各个通知获取细节信息

###### 1、JoinPoint接口

org.aspectj.lang.JoinPoint

要点1：JoinPoint 接口通过 getSignature() 方法获取目标方法的签名（方法声明时的完整信息）

要点2：通过目标方法签名对象获取方法名

要点3：通过 JoinPoint 对象获取外界调用目标方法时传入的实参列表组成的数组

```java
// @Before注解标记前置通知方法
// value属性：切入点表达式，告诉Spring当前通知方法要套用到哪个目标方法上
// 在前置通知方法形参位置声明一个JoinPoint类型的参数，Spring就会将这个对象传入
// 根据JoinPoint对象就可以获取目标方法名称、实际参数列表
@Before(value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))")
public void printLogBeforeCore(JoinPoint joinPoint) {
    
    // 1.通过JoinPoint对象获取目标方法签名对象
    // 方法的签名：一个方法的全部声明信息
    Signature signature = joinPoint.getSignature();
    
    // 2.通过方法的签名对象获取目标方法的详细信息
    String methodName = signature.getName();
    System.out.println("methodName = " + methodName);
    
    int modifiers = signature.getModifiers();
    System.out.println("modifiers = " + modifiers);
    
    String declaringTypeName = signature.getDeclaringTypeName();
    System.out.println("declaringTypeName = " + declaringTypeName);
    
    // 3.通过JoinPoint对象获取外界调用目标方法时传入的实参列表
    Object[] args = joinPoint.getArgs();
    
    // 4.由于数组直接打印看不到具体数据，所以转换为List集合
    List<Object> argList = Arrays.asList(args);
    
    System.out.println("[AOP前置通知] " + methodName + "方法开始了，参数列表：" + argList);
}
```

需要获取方法签名、传入的实参等信息时，可以在通知方法声明JoinPoint类型的形参。

###### 2、方法返回值

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 190359.png)

在返回通知中，通过@AfterReturning注解的returning属性获取目标方法的返回值

```java
// @AfterReturning注解标记返回通知方法
// 在返回通知中获取目标方法返回值分两步：
// 第一步：在@AfterReturning注解中通过returning属性设置一个名称
// 第二步：使用returning属性设置的名称在通知方法中声明一个对应的形参
@AfterReturning(
        value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))",
        returning = "targetMethodReturnValue"
)
public void printLogAfterCoreSuccess(JoinPoint joinPoint, Object targetMethodReturnValue) {
    
    String methodName = joinPoint.getSignature().getName();
    
    System.out.println("[AOP返回通知] "+methodName+"方法成功结束了，返回值是：" + targetMethodReturnValue);
}
```

###### 3、目标方法抛出的异常

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 190438.png)

在异常通知中，通过@AfterThrowing注解的throwing属性获取目标方法抛出的异常对象

```java
// @AfterThrowing注解标记异常通知方法
// 在异常通知中获取目标方法抛出的异常分两步：
// 第一步：在@AfterThrowing注解中声明一个throwing属性设定形参名称
// 第二步：使用throwing属性指定的名称在通知方法声明形参，Spring会将目标方法抛出的异常对象从这里传给我们
@AfterThrowing(
        value = "execution(public int com.atguigu.aop.api.Calculator.add(int,int))",
        throwing = "targetMethodException"
)
public void printLogAfterCoreException(JoinPoint joinPoint, Throwable targetMethodException) {
    
    String methodName = joinPoint.getSignature().getName();
    
    System.out.println("[AOP异常通知] "+methodName+"方法抛异常了，异常类型是：" + targetMethodException.getClass().getName());
}
```

打印效果局部如下：

> [AOP异常通知] div方法抛异常了，异常类型是：java.lang.ArithmeticException
>
> java.lang.ArithmeticException: / by zero
>
> at com.atguigu.aop.imp.CalculatorPureImpl.div(CalculatorPureImpl.java:42) at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method) at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62) at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) at java.lang.reflect.Method.invoke(Method.java:498) at org.springframework.aop.support.AopUtils.invokeJoinpointUsingReflection(AopUtils.java:344)

##### 实验三 重用切入点表达式

###### 1、声明

在一处声明切入点表达式之后，其他有需要的地方引用这个切入点表达式。易于维护，一处修改，处处生效。声明方式如下：

```java
 // 切入点表达式重用
    @Pointcut("execution(public int com.atguigu.aop.api.Calculator.add(int,int)))")
    public void declarPointCut() {}
```

###### 2、同一个类内部引用

```java
   @Before(value = "declarPointCut()")
    public void printLogBeforeCoreOperation(JoinPoint joinPoint) {
```

###### 3、在不同类中引用

```java
@Around(value = "com.atguigu.spring.aop.aspect.LogAspect.declarPointCut()")
public Object roundAdvice(ProceedingJoinPoint joinPoint) {
```

###### 4、集中管理

而作为存放切入点表达式的类，可以把整个项目中所有切入点表达式全部集中过来，便于统一管理：

```java
@Component
public class AtguiguPointCut {
    
    @Pointcut(value = "execution(public int *..Calculator.sub(int,int))")
    public void atguiguGlobalPointCut(){}
    
    @Pointcut(value = "execution(public int *..Calculator.add(int,int))")
    public void atguiguSecondPointCut(){}
    
    @Pointcut(value = "execution(* *..*Service.*(..))")
    public void transactionPointCut(){}
}
```

##### 实验四 切入点表达式语法

###### 1、切入点表达式的作用

###### 2、语法细节

- 用*号代替“权限修饰符”和“返回值”部分表示“权限修饰符”和“返回值”不限
- 在包名的部分，一个“*”号只能代表包的层次结构中的一层，表示这一层是任意的。
  - 例如：*.Hello匹配com.Hello，不匹配com.atguigu.Hello
- 在包名的部分，使用“*..”表示包名任意、包的层次深度任意
- 在类名的部分，类名部分整体用*号代替，表示类名任意
- 在类名的部分，可以使用*号代替类名的一部分

```java
*Service
```

上面例子表示匹配所有名称以Service结尾的类或接口

- 在方法名部分，可以使用*号表示方法名任意
- 在方法名部分，可以使用*号代替方法名的一部分

```java
*Operation
```

上面例子表示匹配所有方法名以Operation结尾的方法

- 在方法参数列表部分，使用(..)表示参数列表任意
- 在方法参数列表部分，使用(int,..)表示参数列表以一个int类型的参数开头
- 在方法参数列表部分，基本数据类型和对应的包装类型是不一样的
  - 切入点表达式中使用 int 和实际方法中 Integer 是不匹配的
- 在方法返回值部分，如果想要明确指定一个返回值类型，那么必须同时写明权限修饰符

```java
execution(public int *..*Service.*(.., int))
```

上面例子是对的，下面例子是错的：

```java
execution(* int *..*Service.*(.., int))
```

但是public *表示权限修饰符明确，返回值任意是可以的。

- 对于execution()表达式整体可以使用三个逻辑运算符号
  - execution() || execution()表示满足两个execution()中的任何一个即可
  - execution() && execution()表示两个execution()表达式必须都满足
  - !execution()表示不满足表达式的其他方法

###### 3、总结

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 202332.png)

> TIP
>
> 虽然我们上面介绍过的切入点表达式语法细节很多，有很多变化，但是实际上具体在项目中应用时有比较固定的写法。
>
> 典型场景：在基于 XML 的声明式事务配置中需要指定切入点表达式。这个切入点表达式通常都会套用到所有 Service 类（接口）的所有方法。那么切入点表达式将如下所示：
>
> execution(* *..*Service.*(..))

##### 实验五 环绕通知

环绕通知对应整个 try...catch...finally 结构，包括前面四种通知的所有功能。

```java
// 使用@Around注解标明环绕通知方法
@Around(value = "com.atguigu.aop.aspect.AtguiguPointCut.transactionPointCut()")
public Object manageTransaction(
    
        // 通过在通知方法形参位置声明ProceedingJoinPoint类型的形参，
        // Spring会将这个类型的对象传给我们
        ProceedingJoinPoint joinPoint) {
    
    // 通过ProceedingJoinPoint对象获取外界调用目标方法时传入的实参数组
    Object[] args = joinPoint.getArgs();
    
    // 通过ProceedingJoinPoint对象获取目标方法的签名对象
    Signature signature = joinPoint.getSignature();
    
    // 通过签名对象获取目标方法的方法名
    String methodName = signature.getName();
    
    // 声明变量用来存储目标方法的返回值
    Object targetMethodReturnValue = null;
    
    try {
    
        // 在目标方法执行前：开启事务（模拟）
        System.out.println("[AOP 环绕通知] 开启事务，方法名：" + methodName + "，参数列表：" + Arrays.asList(args));
    
        // 过ProceedingJoinPoint对象调用目标方法
        // 目标方法的返回值一定要返回给外界调用者
        targetMethodReturnValue = joinPoint.proceed(args);
    
        // 在目标方法成功返回后：提交事务（模拟）
        System.out.println("[AOP 环绕通知] 提交事务，方法名：" + methodName + "，方法返回值：" + targetMethodReturnValue);
    
    }catch (Throwable e){
    
        // 在目标方法抛异常后：回滚事务（模拟）
        System.out.println("[AOP 环绕通知] 回滚事务，方法名：" + methodName + "，异常：" + e.getClass().getName());
    
    }finally {
    
        // 在目标方法最终结束后：释放数据库连接
        System.out.println("[AOP 环绕通知] 释放数据库连接，方法名：" + methodName);
    
    }
    
    return targetMethodReturnValue;
}
```

##### 实验六 切面的优先级

###### 1、概念

相同目标方法上同时存在多个切面时，切面的优先级控制切面的**内外嵌套**顺序。

- 优先级高的切面：外面
- 优先级低的切面：里面

使用 @Order 注解可以控制切面的优先级：

- @Order(较小的数)：优先级高
- @Order(较大的数)：优先级低

###### 2、实际意义

实际开发时，如果有多个切面嵌套的情况，要慎重考虑。例如：如果事务切面优先级高，那么在缓存中命中数据的情况下，事务切面的操作都浪费了。

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 202742.png" style="zoom:50%;" />

此时应该将缓存切面的优先级提高，在事务操作之前先检查缓存中是否存在目标数据。

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 202753.png" style="zoom:50%;" />

##### 实验七 没有接口的情况

在目标类没有实现任何接口的情况下，Spring会自动使用cglib技术实现代理。为了证明这一点，我们做下面的测试：

###### 1、创建目标类

请确保这个类在自动扫描的包下，同时确保切面的切入点表达式能够覆盖到类中的方法。

```java
@Service
public class EmployeeService {
    public void getEmpList() {
        System.out.println("方法内部 com.atguigu.aop.imp.EmployeeService.getEmpList");
    }
}
```

###### 2、测试

```java
 @Autowired
    private EmployeeService employeeService;
    @Test
    public void testNoInterfaceProxy() {
        employeeService.getEmpList();
        System.out.println();
    }
```

###### 3、Debug查看

###### ①没有实现接口情况

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 203056.png)

###### ②有实现接口的情况

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 203110.png)

同时我们发现：Mybatis 调用的 Mapper 接口类型的对象其实也是动态代理机制

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 203121.png)

#### 3、小结

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 185619.png" style="zoom:60%;" />

### 第六节 基于XML的AOP[了解]

#### 1、准备工作

##### ①加入依赖

和基于注解的 AOP 时一样。

##### ②准备代码

把测试基于注解功能时的Java类复制到新module中，去除所有注解。

#### 2、配置Spring配置文件

```xml
<!-- 配置目标类的bean -->
<bean id="calculatorPure" class="com.atguigu.aop.imp.CalculatorPureImpl"/>
    
<!-- 配置切面类的bean -->
<bean id="logAspect" class="com.atguigu.aop.aspect.LogAspect"/>
    
<!-- 配置AOP -->
<aop:config>
    
    <!-- 配置切入点表达式 -->
    <aop:pointcut id="logPointCut" expression="execution(* *..*.*(..))"/>
    
    <!-- aop:aspect标签：配置切面 -->
    <!-- ref属性：关联切面类的bean -->
    <aop:aspect ref="logAspect">
        <!-- aop:before标签：配置前置通知 -->
        <!-- method属性：指定前置通知的方法名 -->
        <!-- pointcut-ref属性：引用切入点表达式 -->
        <aop:before method="printLogBeforeCore" pointcut-ref="logPointCut"/>
    
        <!-- aop:after-returning标签：配置返回通知 -->
        <!-- returning属性：指定通知方法中用来接收目标方法返回值的参数名 -->
        <aop:after-returning
                method="printLogAfterCoreSuccess"
                pointcut-ref="logPointCut"
                returning="targetMethodReturnValue"/>
    
        <!-- aop:after-throwing标签：配置异常通知 -->
        <!-- throwing属性：指定通知方法中用来接收目标方法抛出异常的异常对象的参数名 -->
        <aop:after-throwing
                method="printLogAfterCoreException"
                pointcut-ref="logPointCut"
                throwing="targetMethodException"/>
    
        <!-- aop:after标签：配置后置通知 -->
        <aop:after method="printLogCoreFinallyEnd" pointcut-ref="logPointCut"/>
    
        <!-- aop:around标签：配置环绕通知 -->
        <!--<aop:around method="……" pointcut-ref="logPointCut"/>-->
    </aop:aspect>
    
</aop:config>
```

#### 3、测试

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(value = {"classpath:spring-context.xml"})
public class AOPTest {
    
    @Autowired
    private Calculator calculator;
    
    @Test
    public void testLogAspect() {
        int add = calculator.add(10, 2);
        System.out.println("add = " + add);
    }
}
```

### 第七节 AOP对获取bean的影响

#### 一、根据类型获取 bean

##### 1、情景一

- bean 对应的类没有实现任何接口

- 根据 bean 本身的类型获取 bean

  - 测试：IOC容器中同类型的 bean 只有一个

    正常获取到 IOC 容器中的那个 bean 对象

  - 测试：IOC 容器中同类型的 bean 有多个

    会抛出 NoUniqueBeanDefinitionException 异常，表示 IOC 容器中这个类型的 bean 有多个

##### 2、情景二

- bean 对应的类实现了接口，这个接口也只有这一个实现类
  - 测试：根据接口类型获取 bean
  - 测试：根据类获取 bean
  - 结论：上面两种情况其实都能够正常获取到 bean，而且是同一个对象

##### 3、情景三

- 声明一个接口

- 接口有多个实现类

- 接口所有实现类都放入 IOC 容器

  - 测试：根据接口类型获取 bean

    会抛出 NoUniqueBeanDefinitionException 异常，表示 IOC 容器中这个类型的 bean 有多个

  - 测试：根据类获取bean

    正常

##### 4、情景四

- 声明一个接口
- 接口有一个实现类
- 创建一个切面类，对上面接口的实现类应用通知
  - 测试：根据接口类型获取bean
  - 测试：根据类获取bean

原因分析：

- 应用了切面后，真正放在IOC容器中的是代理类的对象
- 目标类并没有被放到IOC容器中，所以根据目标类的类型从IOC容器中是找不到的

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 203650.png" style="zoom:50%;" />

从内存分析的角度来说，IOC容器中引用的是代理对象，代理对象引用的是目标对象。IOC容器并没有直接引用目标对象，所以根据目标类本身在IOC容器范围内查找不到。

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 203729.png)

debug查看代理类的类型：

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 203757.png" style="zoom:50%;" />

##### 5、情景五

- 声明一个类
- 创建一个切面类，对上面的类应用通知
  - 测试：根据类获取 bean，能获取到

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 203905.png)

debug查看实际类型：CGLIB

#### 二、自动装配

自动装配需先从 IOC 容器中获取到唯一的一个 bean 才能够执行装配。所以装配能否成功和装配底层的原理，和前面测试的获取 bean 的机制是一致的。

##### 1、情景一

- 目标bean对应的类没有实现任何接口

- 根据bean本身的类型装配这个bean

  - 测试：IOC容器中同类型的bean只有一个

    正常装配

  - 测试：IOC容器中同类型的bean有多个

    会抛出NoUniqueBeanDefinitionException异常，表示IOC容器中这个类型的bean有多个

##### 2、情景二

- 目标bean对应的类实现了接口，这个接口也只有这一个实现类

  - 测试：根据接口类型装配bean

    正常

  - 测试：根据类装配bean

    正常

##### 3、情景三

- 声明一个接口

- 接口有多个实现类

- 接口所有实现类都放入IOC容器

  - 测试：根据接口类型装配bean

    @Autowired注解会先根据类型查找，此时会找到多个符合的bean，然后根据成员变量名作为bean的id进一步筛选，如果没有id匹配的，则会抛出NoUniqueBeanDefinitionException异常，表示IOC容器中这个类型的bean有多个

  - 测试：根据类装配bean

    正常

##### 4、情景四

- 声明一个接口

- 接口有一个实现类

- 创建一个切面类，对上面接口的实现类应用通知

  - 测试：根据接口类型装配bean

    正常

  - 测试：根据类装配bean

    此时获取不到对应的bean，所以无法装配，抛出下面的异常：

> Caused by: org.springframework.beans.factory.BeanNotOfRequiredTypeException: Bean named 'fruitApple' is expected to be of type 'com.atguigu.bean.impl.FruitAppleImpl' but was actually of type 'com.sun.proxy.$Proxy15'

##### 5、情景五

- 声明一个类

- 创建一个切面类，对上面的类应用通知

  - 测试：根据类装配bean

    正常

#### 三、总结

##### 1、对实现了接口的类应用切面

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 204420.png)

##### 2、对没实现接口的类应用切面

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-01 204444.png)

## 第三章 声明式事务

### 第一节 JDBCTemplate

#### 1、简介

为了在特定领域帮助我们简化代码，Spring 封装了很多 『Template』形式的模板类。例如：RedisTemplate、RestTemplate 等等，包括我们今天要学习的 JDBCTemplate。

#### 2、准备工作

##### ①加入依赖

```xml
<dependencies>

    <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- Spring 持久化层支持jar包 -->
    <!-- Spring 在执行持久化层操作、与持久化层技术进行整合过程中，需要使用orm、jdbc、tx三个jar包 -->
    <!-- 导入 orm 包就可以通过 Maven 的依赖传递性把其他两个也导入 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-orm</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- Spring 测试相关 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>5.3.1</version>
    </dependency>

    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>

    <!-- MySQL驱动 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.3</version>
    </dependency>
    <!-- 数据源 -->
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.0.31</version>
    </dependency>

</dependencies>
```

##### ②jdbc.properties

```properties
atguigu.url=jdbc:mysql://localhost:3306/mybatis-example
atguigu.driver=com.mysql.jdbc.Driver
atguigu.username=root
atguigu.password=atguigu
```

##### ③Spring 配置文件

######  [1]配置数据源

```xml
<!-- 导入外部属性文件 -->
<context:property-placeholder location="classpath:jdbc.properties" />
    
<!-- 配置数据源 -->
<bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
    <property name="url" value="${atguigu.url}"/>
    <property name="driverClassName" value="${atguigu.driver}"/>
    <property name="username" value="${atguigu.username}"/>
    <property name="password" value="${atguigu.password}"/>
</bean>
```

###### [2]配置 JDBCTemplate

```xml
<!-- 配置 JdbcTemplate -->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        
    <!-- 装配数据源 -->
    <property name="dataSource" ref="druidDataSource"/>
        
</bean>
```

#### [3]在测试类装配 JdbcTemplate

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(value = {"classpath:spring-context.xml"})
public class JDBCTest {
    
    @Autowired
    private DataSource dataSource;
    
    @Autowired
    private JdbcTemplate jdbcTemplate;
        
    @Test
    public void testJdbcTemplateUpdate() {
        
    }
    
    @Test
    public void testConnection() throws SQLException {
        Connection connection = dataSource.getConnection();
    
        System.out.println("connection = " + connection);
    }
    
}
```

#### 3、基本用法

##### ①增删改操作

```java
@Test
public void testJdbcTemplateUpdate() {
    
    // 1.编写 SQL 语句。需要传参的地方写问号占位符
    String sql = "update t_emp set emp_salary=? where emp_id=?";
    
    // 2.调用 jdbcTemplate 的 update() 方法执行 update 语句
    int count = jdbcTemplate.update(sql, 999.99, 3);
    
    System.out.println("count = " + count);
    
}
```

##### ②查询：返回单个简单类型

```java
@Test
public void testJdbcTemplateQueryForSingleValue() {
    
    // 1.编写 SQL 语句
    String sql = "select emp_name from t_emp where emp_id=?";
    
    // 2.调用 jdbcTemplate 的方法执行查询
    String empName = jdbcTemplate.queryForObject(sql, String.class, 6);
    
    System.out.println("empName = " + empName);
    
}
```

##### ③查询：查询实体类类型

###### [1]封装实体类类型

```java
public class Emp {
    private Integer empId;
    private String empName;
    private Double empSalary;
    ……
```

###### [2]借助 RowMapper 完成查询

```java
@Test
public void testJdbcTemplateQueryForEntity() {
    // 1.编写 SQL 语句
    String sql = "select emp_id,emp_name,emp_salary from t_emp where emp_id=?";
    
    // 2.准备 RowMapper 对象
    RowMapper<Emp> rowMapper = new BeanPropertyRowMapper<>(Emp.class);
    
    // 3.调用 jdbcTemplate 的方法执行查询
    Emp emp = jdbcTemplate.queryForObject(sql, rowMapper, 7);
    
    System.out.println("emp = " + emp);
    
}
```

### 第二节 声明式事务概念

#### 1、编程式事务

事务功能的相关操作全部通过自己编写代码来实现：

```java
Connection conn = ...;
	
try {
	// 开启事务：关闭事务的自动提交
	conn.setAutoCommit(false);
	// 核心操作
	
	// 提交事务
	conn.commit();
}catch(Exception e){
	// 回滚事务
	conn.rollBack();
}finally{
	// 释放数据库连接
	conn.close();
}
```

编程式的实现方式存在缺陷：

- 细节没有被屏蔽：具体操作过程中，所有细节都需要程序员自己来完成，比较繁琐。
- 代码复用性不高：如果没有有效抽取出来，每次实现功能都需要自己编写代码，代码就没有得到复用。

#### 2、声明式事务

既然事务控制的代码有规律可循，代码的结构基本是确定的，所以框架就可以将固定模式的代码抽取出来，进行相关的封装。

封装起来后，我们只需要在配置文件中进行简单的配置即可完成操作。

- 好处1：提高开发效率
- 好处2：消除了冗余的代码
- 好处3：框架会综合考虑相关领域中在实际开发环境下有可能遇到的各种问题，进行了健壮性、性能等各个方面的优化

所以，我们可以总结下面两个概念：

- **编程式**：**自己写代码**实现功能
- **声明式**：通过**配置**让**框架**实现功能

#### 3、事务管理器

##### ①顶级接口

###### [1]Spring 5.2以前

```java
public interface PlatformTransactionManager {

	TransactionStatus getTransaction(TransactionDefinition definition) throws TransactionException;

	void commit(TransactionStatus status) throws TransactionException;

	void rollback(TransactionStatus status) throws TransactionException;

}
```

#### [2]从 Spring 5.2开始

PlatformTransactionManager 接口本身没有变化，它继承了 TransactionManager

```java
public interface TransactionManager {
    
}
```

> TIP
>
> TransactionManager接口中什么都没有，但是它还是有存在的意义——定义一个技术体系。

##### ②技术体系

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 123929.png)

我们现在要使用的事务管理器是org.springframework.jdbc.datasource.**DataSourceTransactionManager**，将来整合 Mybatis 用的也是这个类。

DataSourceTransactionManager类中的主要方法：

- doBegin()：开启事务
- doSuspend()：挂起事务
- doResume()：恢复挂起的事务
- doCommit()：提交事务
- doRollback()：回滚事务

### 第三节 基于注解的声明式事务

#### 实验一 准备工作

##### 1、加入依赖

```xml
  <dependencies>
    
        <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.1</version>
        </dependency>
    
        <!-- Spring 持久化层支持jar包 -->
        <!-- Spring 在执行持久化层操作、与持久化层技术进行整合过程中，需要使用orm、jdbc、tx三个jar包 -->
        <!-- 导入 orm 包就可以通过 Maven 的依赖传递性把其他两个也导入 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>5.3.1</version>
        </dependency>
    
        <!-- Spring 测试相关 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.3.1</version>
        </dependency>
    
        <!-- junit测试 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    
        <!-- MySQL驱动 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.3</version>
        </dependency>
        <!-- 数据源 -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.0.31</version>
        </dependency>
    
    </dependencies>
```

##### 2、外部属性文件

```properties
atguigu.url=jdbc:mysql://192.168.198.100:3306/mybatis-example
atguigu.driver=com.mysql.jdbc.Driver
atguigu.username=root
atguigu.password=atguigu
```

##### 3、Spring 配置文件

```xml
<!-- 配置自动扫描的包 -->
<context:component-scan base-package="com.atguigu.tx"/>

<!-- 导入外部属性文件 -->
<context:property-placeholder location="classpath:jdbc.properties" />
    
<!-- 配置数据源 -->
<bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
    <property name="url" value="${atguigu.url}"/>
    <property name="driverClassName" value="${atguigu.driver}"/>
    <property name="username" value="${atguigu.username}"/>
    <property name="password" value="${atguigu.password}"/>
</bean>
    
<!-- 配置 JdbcTemplate -->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    
    <!-- 装配数据源 -->
    <property name="dataSource" ref="druidDataSource"/>
    
</bean>
```

##### 4、测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(value = {"classpath:spring-context.xml"})
public class JDBCTest {
   
}
```

##### 5、创建组件

###### ①EmpDao

```java
@Repository
public class EmpDao {
    
    @Autowired
    private JdbcTemplate jdbcTemplate;
        
    public void updateEmpNameById(Integer empId, String empName) {
        String sql = "update t_emp set emp_name=? where emp_id=?";
        jdbcTemplate.update(sql, empName, empId);
    }
        
    public void updateEmpSalaryById(Integer empId, Double salary) {
        String sql = "update t_emp set emp_salary=? where emp_id=?";
        jdbcTemplate.update(sql, salary, empId);
    }
        
    public String selectEmpNameById(Integer empId) {
        String sql = "select emp_name from t_emp where emp_id=?";
    
        String empName = jdbcTemplate.queryForObject(sql, String.class, empId);
    
        return empName;
    }
    
}
```

EmpDao 准备好之后最好测试一下，确认代码正确。养成随写随测的好习惯。

###### ②EmpService

在三层结构中，事务通常都是加到业务逻辑层，针对Service类使用事务。

```java
@Service
public class EmpService {
    
    @Autowired
    private EmpDao empDao;
    
    // 为了便于核对数据库操作结果，不要修改同一条记录
    public void updateTwice(
            // 修改员工姓名的一组参数
            Integer empId4EditName, String newName,

            // 修改员工工资的一组参数
            Integer empId4EditSalary, Double newSalary
            ) {
    
        // 为了测试事务是否生效，执行两个数据库操作，看它们是否会在某一个失败时一起回滚
        empDao.updateEmpNameById(empId4EditName, newName);
    
        empDao.updateEmpSalaryById(empId4EditSalary, newSalary);
    
    }
    
}
```

#### 实验二 应用最基本的事务控制

##### 1、加事务前状态

###### ①搞破坏

修改 EmpDao 中的 updateEmpSalaryById()方法：

```java
public void updateEmpSalaryById(Integer empId, Double salary) {

    // 为了看到操作失败后的效果人为将 SQL 语句破坏
    String sql = "upd222ate t_emp set emp_salary=? where emp_id=?";
    jdbcTemplate.update(sql, salary, empId);
}
```

###### ②执行Service方法

```java
@Test
public void testBaseTransaction() {
    
    Integer empId4EditName = 2;
    String newName = "new-name";
    
    Integer empId4EditSalary = 3;
    Double newSalary = 444.44;
    
    empService.updateTwice(empId4EditName, newName, empId4EditSalary, newSalary);
    
}
```

效果：修改姓名的操作生效了，修改工资的操作没有生效。

##### 2、添加事务功能

###### ①配置事务管理器

resources/spring-context.xml

```xml
<!-- 配置事务管理器 -->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <!-- 事务管理器的bean只需要装配数据源，其他属性保持默认值即可 -->
    <property name="dataSource" ref="druidDataSource"/>
</bean>
```

###### ②开启基于注解的声明式事务功能

```xml
<!-- 开启基于注解的声明式事务功能 -->
<!-- 使用transaction-manager属性指定当前使用是事务管理器的bean -->
<!-- transaction-manager属性的默认值是transactionManager，如果事务管理器bean的id正好就是这个默认值，则可以省略这个属性 -->
<tx:annotation-driven transaction-manager="transactionManager"/>
```

WARNING

注意：导入名称空间时有好几个重复的，我们需要的是 **tx 结尾**的那个。

![](F:\LearninginUniversity\2022——自学\笔记\img\img003.bc58e542.png)

###### ③在需要事务的方法上使用注解

```java
//EmpService
@Transactional
public void updateTwice(
        // 修改员工姓名的一组参数
        Integer empId4EditName, String newName,
 
        // 修改员工工资的一组参数
        Integer empId4EditSalary, Double newSalary
        ) {
 
    // 为了测试事务是否生效，执行两个数据库操作，看它们是否会在某一个失败时一起回滚
    empDao.updateEmpNameById(empId4EditName, newName);
 
    empDao.updateEmpSalaryById(empId4EditSalary, newSalary);
 
}
```

###### ④测试

junit 测试方法不需要修改，执行后查看数据是否被修改。

##### 3、从日志内容角度查看事务效果

###### ①加入依赖

```xml
<!-- 加入日志 -->
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.2.3</version>
</dependency>
```

###### ②加入logback的配置文件

文件名：logback.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration debug="true">
    <!-- 指定日志输出的位置 -->
    <appender name="STDOUT"
              class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <!-- 日志输出的格式 -->
            <!-- 按照顺序分别是：时间、日志级别、线程名称、打印日志的类、日志主体内容、换行 -->
            <pattern>[%d{HH:mm:ss.SSS}] [%-5level] [%thread] [%logger] [%msg]%n</pattern>
        </encoder>
    </appender>
 
    <!-- 设置全局日志级别。日志级别按顺序分别是：DEBUG、INFO、WARN、ERROR -->
    <!-- 指定任何一个日志级别都只打印当前级别和后面级别的日志。 -->
    <root level="INFO">
        <!-- 指定打印日志的appender，这里通过“STDOUT”引用了前面配置的appender -->
        <appender-ref ref="STDOUT" />
    </root>
 
    <!-- 根据特殊需求指定局部日志级别 -->
    <logger name="org.springframework.jdbc.datasource.DataSourceTransactionManager" level="DEBUG"/>
    <logger name="org.springframework.jdbc.core.JdbcTemplate" level="DEBUG" />
 
</configuration>
```

###### ③日志中事务相关内容

###### [1]事务回滚时

> [11:37:36.965] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [ **Creating new transaction** with name [com.atguigu.tx.service.EmpService.updateTwice]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT] [11:37:37.328] [INFO ] [main] [com.alibaba.druid.pool.DruidDataSource] [{dataSource-1} inited] [11:37:37.815] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [ **Acquired Connection** [com.mysql.jdbc.JDBC4Connection@6b6776cb] for JDBC transaction] [11:37:37.818] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [ **Switching JDBC Connection** [com.mysql.jdbc.JDBC4Connection@6b6776cb] to **manual commit**]
>
> [11:44:32.311] [DEBUG] [main] [org.springframework.jdbc.core.JdbcTemplate] [Executing prepared SQL update] [11:44:32.312] [DEBUG] [main] [org.springframework.jdbc.core.JdbcTemplate] [Executing prepared SQL statement [**update t_emp set emp_name=? where emp_id=?**]] [11:44:32.339] [DEBUG] [main] [org.springframework.jdbc.core.JdbcTemplate] [Executing prepared SQL update] [11:44:32.339] [DEBUG] [main] [org.springframework.jdbc.core.JdbcTemplate] [Executing prepared SQL statement [**upd222ate t_emp set emp_salary=? where emp_id=?**]]
>
> [11:37:37.931] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [**Initiating transaction rollback**] [11:37:37.931] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [**Rolling back** JDBC transaction on Connection [com.mysql.jdbc.JDBC4Connection@6b6776cb]] [11:37:37.933] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [Releasing JDBC Connection [com.mysql.jdbc.JDBC4Connection@6b6776cb] after transaction]

###### [2]事务提交时

> [11:42:40.093] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [**Creating new transaction** with name [com.atguigu.tx.service.EmpService.updateTwice]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT] [11:42:40.252] [INFO ] [main] [com.alibaba.druid.pool.DruidDataSource] [{dataSource-1} inited] [11:42:40.655] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [**Acquired Connection** [com.mysql.jdbc.JDBC4Connection@6b6776cb] for JDBC transaction] [11:42:40.661] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [**Switching JDBC Connection** [com.mysql.jdbc.JDBC4Connection@6b6776cb] to **manual commit**] [11:42:40.681] [DEBUG] [main] [org.springframework.jdbc.core.JdbcTemplate] [Executing prepared SQL update] [11:42:40.682] [DEBUG] [main] [org.springframework.jdbc.core.JdbcTemplate] [Executing prepared SQL statement [**update t_emp set emp_name=? where emp_id=?**]] [11:42:40.710] [DEBUG] [main] [org.springframework.jdbc.core.JdbcTemplate] [Executing prepared SQL update] [11:42:40.711] [DEBUG] [main] [org.springframework.jdbc.core.JdbcTemplate] [Executing prepared SQL statement [**update t_emp set emp_salary=? where emp_id=?**]] [11:42:40.712] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [**Initiating transaction commit**] [11:42:40.712] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [**Committing JDBC transaction** on Connection [com.mysql.jdbc.JDBC4Connection@6b6776cb]] [11:42:40.714] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [**Releasing JDBC Connection** [com.mysql.jdbc.JDBC4Connection@6b6776cb] after transaction]

##### 4、debug查看事务管理器中的关键方法

类：org.springframework.jdbc.datasource.DataSourceTransactionManager

###### ①开启事务的方法

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 125942.png" style="zoom:50%;" />

###### ②提交事务的方法

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 125951.png" style="zoom:50%;" />

###### ③回滚事务的方法

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 130001.png" style="zoom:50%;" />

#### 实验三 事务属性：只读

##### 1、介绍

对一个查询操作来说，如果我们把它设置成只读，就能够明确告诉数据库，这个操作不涉及写操作。这样数据库就能够针对查询操作来进行优化。

##### 2、设置方式

```java
// readOnly = true把当前事务设置为只读
@Transactional(readOnly = true)
public String getEmpName(Integer empId) {
    return empDao.selectEmpNameById(empId);
}
```

##### 3、针对增删改操作设置只读

会抛出下面异常：

> WARNING
>
> Caused by: java.sql.SQLException: Connection is read-only. Queries leading to data modification are not allowed

##### 4、@Transactional 注解放在类上

###### ①生效原则

如果一个类中每一个方法上都使用了 @Transactional 注解，那么就可以将 @Transactional 注解提取到类上。反过来说：@Transactional 注解在类级别标记，会影响到类中的每一个方法。同时，类级别标记的 @Transactional 注解中设置的事务属性也会延续影响到方法执行时的事务属性。除非在方法上又设置了 @Transactional 注解。

对一个方法来说，离它最近的 @Transactional 注解中的事务属性设置生效。

###### ②用法举例

在类级别@Transactional注解中设置只读，这样类中所有的查询方法都不需要设置@Transactional注解了。因为对查询操作来说，其他属性通常不需要设置，所以使用公共设置即可。

然后在这个基础上，对增删改方法设置@Transactional注解 readOnly 属性为 false。

```java
@Service
@Transactional(readOnly = true)
public class EmpService {
    
    // 为了便于核对数据库操作结果，不要修改同一条记录
    @Transactional(readOnly = false)
    public void updateTwice(……) {
		……
    }
    
    // readOnly = true把当前事务设置为只读
    // @Transactional(readOnly = true)
    public String getEmpName(Integer empId) {
		……
    }
    
}
```

> TIP
>
> PS：Spring 环境下很多场合都有类似设定，一个注解如果标记了类的每一个方法那么通常就可以提取到类级别。

#### 实验四 事务属性：超时

##### 1、需求

事务在执行过程中，有可能因为遇到某些问题，导致程序卡住，从而长时间占用数据库资源。而长时间占用资源，大概率是因为程序运行出现了问题（可能是Java程序或MySQL数据库或网络连接等等）。

此时这个很可能出问题的程序应该被回滚，撤销它已做的操作，事务结束，把资源让出来，让其他正常程序可以执行。

概括来说就是一句话：超时回滚，释放资源。

##### 2、设置

###### ①@Transactional注解中的设置

```java
@Transactional(readOnly = false, timeout = 3)
public void updateTwice(
        // 修改员工姓名的一组参数
        Integer empId4EditName, String newName,

        // 修改员工工资的一组参数
        Integer empId4EditSalary, Double newSalary
        ) {

    // 为了测试事务是否生效，执行两个数据库操作，看它们是否会在某一个失败时一起回滚
    empDao.updateEmpNameById(empId4EditName, newName);

    empDao.updateEmpSalaryById(empId4EditSalary, newSalary);

}
```

###### ②Dao方法中让线程睡眠

```java
public void updateEmpSalaryById(Integer empId, Double salary) {

    try {
        TimeUnit.SECONDS.sleep(5);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }

    // 为了看到操作失败后的效果人为将 SQL 语句破坏
    String sql = "update t_emp set emp_salary=? where emp_id=?";
    jdbcTemplate.update(sql, salary, empId);
}
```

> TIP
>
> PS：注意：sleep操作如果放在执行 SQL 语句后面那就不起作用。

###### ③执行效果

执行过程中日志和抛出异常的情况：

> [16:25:41.706] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [Initiating transaction rollback] [16:25:41.706] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [Rolling back JDBC transaction on Connection [com.mysql.jdbc.JDBC4Connection@53b7f657]] [16:25:41.709] [DEBUG] [main] [org.springframework.jdbc.datasource.DataSourceTransactionManager] [Releasing JDBC Connection [com.mysql.jdbc.JDBC4Connection@53b7f657] after transaction]
>
> org.springframework.transaction.**TransactionTimedOutException**: Transaction timed out: deadline was Fri Jun 04 16:25:39 CST 2021

#### 实验五 事务属性：回滚和不回滚的异常

##### 1、默认情况

默认只针对运行时异常回滚，编译时异常不回滚。情景模拟代码如下：

```java
public void updateEmpSalaryById(Integer empId, Double salary) throws FileNotFoundException {
    
	// 为了看到操作失败后的效果人为将 SQL 语句破坏
	String sql = "update t_emp set emp_salary=? where emp_id=?";
	jdbcTemplate.update(sql, salary, empId);
    
//  抛出编译时异常测试是否回滚
	new FileInputStream("aaaa.aaa");
    
//  抛出运行时异常测试是否回滚
//  System.out.println(10 / 0);
}
```

##### 2、设置回滚的异常

- rollbackFor属性：需要设置一个Class类型的对象
- rollbackForClassName属性：需要设置一个字符串类型的全类名

```java
@Transactional(rollbackFor = Exception.class)
```

##### 3、设置不回滚的异常

在默认设置和已有设置的基础上，再指定一个异常类型，碰到它不回滚。

```java
 @Transactional(
            noRollbackFor = FileNotFoundException.class
    )
```

##### 4、回滚和不回滚异常同时设置

#### ①范围不同

不管是哪个设置范围大，都是在大范围内在排除小范围的设定。例如：

- rollbackFor = Exception.class
- noRollbackFor = FileNotFoundException.class

意思是除了 FileNotFoundException 之外，其他所有 Exception 范围的异常都回滚；但是碰到 FileNotFoundException 不回滚。

#### ②范围一致[好奇]

回滚和不回滚的异常设置了相同范围（这是有多想不开）：

- noRollbackFor = FileNotFoundException.class
- rollbackFor = FileNotFoundException.class

此时 Spring 采纳了 rollbackFor 属性的设定：遇到 FileNotFoundException 异常会回滚。

#### 实验六 事务属性：事务隔离级别

##### 1、视角需要提升

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 135221.png)

##### 2、测试的准备工作

###### ①思路

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 135311.png)

###### ②EmpService中参与测试的方法

```java
// readOnly = true把当前事务设置为只读
// @Transactional(readOnly = true)
public String getEmpName(Integer empId) {
    
    return empDao.selectEmpNameById(empId);
}
    
@Transactional(readOnly = false)
public void updateEmpName(Integer empId, String empName) {
    
    empDao.updateEmpNameById(empId, empName);
}
```

###### ③junit中执行测试的方法

```java
@Test
public void testTxReadOnly() {
    
    String empName = empService.getEmpName(3);
    
    System.out.println("empName = " + empName);
    
}

@Test
public void testIsolation() {
    
    Integer empId = 2;
    String empName = "aaaaaaaa";
    
    empService.updateEmpName(empId, empName);
    
}
```

###### ④搞破坏

为了让事务B（执行修改操作的事务）能够回滚，在EmpDao中的对应方法中人为抛出异常。

```java
public void updateEmpNameById(Integer empId, String empName) {
    String sql = "update t_emp set emp_name=? where emp_id=?";
    jdbcTemplate.update(sql, empName, empId);
    System.out.println(10 / 0);
}
```

##### 3、执行测试

在 @Transactional 注解中使用 isolation 属性设置事务的隔离级别。 取值使用 org.springframework.transaction.annotation.Isolation 枚举类提供的数值。

###### ①测试读未提交

```java
@Transactional(isolation = Isolation.READ_UNCOMMITTED)
public String getEmpName(Integer empId) {
    
    return empDao.selectEmpNameById(empId);
}
    
@Transactional(isolation = Isolation.READ_UNCOMMITTED, readOnly = false)
public void updateEmpName(Integer empId, String empName) {
    
    empDao.updateEmpNameById(empId, empName);
}
```

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 135636.png" style="zoom:67%;" />

测试结果：执行查询操作的事务读取了另一个尚未提交的修改。

###### ②测试读已提交

```java
@Transactional(isolation = Isolation.READ_COMMITTED)
public String getEmpName(Integer empId) {
    
    return empDao.selectEmpNameById(empId);
}
    
@Transactional(isolation = Isolation.READ_COMMITTED, readOnly = false)
public void updateEmpName(Integer empId, String empName) {
    
    empDao.updateEmpNameById(empId, empName);
}
```

测试结果：执行查询操作的事务读取的是数据库中正确的数据。

#### 实验七 事务属性：事务传播行为

##### 1、事务传播行为要研究的问题

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 135841.png" style="zoom:67%;" />

##### 2、propagation属性

###### ①默认值

@Transactional 注解通过 propagation 属性设置事务的传播行为。它的默认值是：

```java
Propagation propagation() default Propagation.REQUIRED;
```

###### ②可选值说明

propagation 属性的可选值由 org.springframework.transaction.annotation.Propagation 枚举类提供：

| 名称                      | 含义                                                         |
| ------------------------- | ------------------------------------------------------------ |
| REQUIRED 默认值           | 当前方法必须工作在事务中 如果当前线程上有已经开启的事务可用，那么就在这个事务中运行 如果当前线程上没有已经开启的事务，那么就自己开启新事务，在新事务中运行 所以当前方法有可能和其他方法共用事务 在共用事务的情况下：当前方法会因为其他方法回滚而受**连累** |
| **REQUIRES_NEW** 建议使用 | 当前方法必须工作在事务中 不管当前线程上是否有已经开启的事务，都要开启新事务 在新事务中运行 不会和其他方法共用事务，避免被其他方法连累 |

##### 3、测试

###### ①创建测试方法

###### [1]在EmpService中声明两个内层方法

```java
@Transactional(readOnly = false, propagation = Propagation.REQUIRED)
public void updateEmpNameInner(Integer empId, String empName) {
    
    empDao.updateEmpNameById(empId, empName);
}
    
@Transactional(readOnly = false, propagation = Propagation.REQUIRED)
public void updateEmpSalaryInner(Integer empId, Double empSalary) {
    
    empDao.updateEmpSalaryById(empId, empSalary);
}
```

###### [2]创建TopService

service包下

```java
@Service
public class TopService {
    
    // 这里我们只是为了测试事务传播行为，临时在Service中装配另一个Service
    // 实际开发时非常不建议这么做，因为这样会严重破坏项目的结构
    @Autowired
    private EmpService empService;
    
    @Transactional
    public void topTxMethod() {
    
        // 在外层方法中调用两个内层方法
        empService.updateEmpNameInner(2, "aaa");
        
        empService.updateEmpSalaryInner(3, 666.66);
        
    }
    
}
```

#### [3]junit测试方法

```java
@Autowired
private TopService topService;
    
@Test
public void testPropagation() {
    
    // 调用外层方法
    topService.topTxMethod();
    
}
```

###### ②测试 REQUIRED 模式

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 140400.png" style="zoom:67%;" />

效果：内层方法A、内层方法B所做的修改都没有生效，总事务回滚了。

###### ③测试 REQUIRES_NEW 模式

###### [1]修改 EmpService 中内层方法

```java
@Transactional(readOnly = false, propagation = Propagation.REQUIRES_NEW)
public void updateEmpNameInner(Integer empId, String empName) {
    
    empDao.updateEmpNameById(empId, empName);
}
    
@Transactional(readOnly = false, propagation = Propagation.REQUIRES_NEW)
public void updateEmpSalaryInner(Integer empId, Double empSalary) {
    
    empDao.updateEmpSalaryById(empId, empSalary);
}
```

###### [2]执行流程

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 140517.png" style="zoom:67%;" />

##### 4、实际开发情景

###### ①Service方法应用了通知

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 140626.png" style="zoom:67%;" />

###### ②过滤器或拦截器等类似组件

<img src="F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 140655.png" style="zoom:67%;" />

###### ③升华

我们在事务传播行为这里，使用 REQUIRES_NEW 属性，也可以说是让不同事务方法从事务的使用上**解耦合**，不要互相影响。

### 第四节 基于XML的声明式事务

#### 1、加入依赖

相比于基于注解的声明式事务，基于 XML 的声明式事务需要一个额外的依赖：

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>5.3.1</version>
</dependency>
```

#### 2、迁移代码

将上一个基于注解的 module 中的代码转移到新 module。去掉 @Transactional 注解。

#### 3、修改 Spring 配置文件

去掉 tx:annotation-driven 标签，然后加入下面的配置：

```xml
<aop:config>
    <!-- 配置切入点表达式，将事务功能定位到具体方法上 -->
    <aop:pointcut id="txPoincut" expression="execution(* *..*Service.*(..))"/>
    
    <!-- 将事务通知和切入点表达式关联起来 -->
    <aop:advisor advice-ref="txAdvice" pointcut-ref="txPoincut"/>
    
</aop:config>
    
<!-- tx:advice标签：配置事务通知 -->
<!-- id属性：给事务通知标签设置唯一标识，便于引用 -->
<!-- transaction-manager属性：关联事务管理器 -->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <tx:attributes>
    
        <!-- tx:method标签：配置具体的事务方法 -->
        <!-- name属性：指定方法名，可以使用星号代表多个字符 -->
        <tx:method name="get*" read-only="true"/>
        <tx:method name="query*" read-only="true"/>
        <tx:method name="find*" read-only="true"/>
    
        <!-- read-only属性：设置只读属性 -->
        <!-- rollback-for属性：设置回滚的异常 -->
        <!-- no-rollback-for属性：设置不回滚的异常 -->
        <!-- isolation属性：设置事务的隔离级别 -->
        <!-- timeout属性：设置事务的超时属性 -->
        <!-- propagation属性：设置事务的传播行为 -->
        <tx:method name="save*" read-only="false" rollback-for="java.lang.Exception" propagation="REQUIRES_NEW"/>
        <tx:method name="update*" read-only="false" rollback-for="java.lang.Exception" propagation="REQUIRES_NEW"/>
        <tx:method name="delete*" read-only="false" rollback-for="java.lang.Exception" propagation="REQUIRES_NEW"/>
    </tx:attributes>
</tx:advice>
```

> WARNING
>
> 在输入 tx:advice 标签时，需要导入 tx: 名称空间，此时需要注意不要导入错误。我们需要的是以 tx 结尾的名称空间。如下图所示：
>
> ![](F:\LearninginUniversity\2022——自学\笔记\img\img003.bc58e542.png)

#### 4、配置完成后 bean 之间的关系

![](F:\LearninginUniversity\2022——自学\笔记\img\屏幕截图 2022-05-03 141102.png)

#### 5、注意

即使需要事务功能的目标方法已经被切入点表达式涵盖到了，但是如果没有给它配置事务属性，那么这个方法就还是没有事务。所以事务属性必须配置。

## 第四章 Spring5 新特性

### 第一节 JSR305标准相关注解

#### 1、从JSR说起

##### ①JCP

JCP（Java Community Process) 是一个由SUN公司发起的，开放的国际组织。主要由Java开发者以及被授权者组成，负责Java技术规范维护，Java技术发展和更新。

JCP官网地址：https://jcp.org/en/home/index

##### ②JSR

JSR 的全称是：Java Specification Request，意思是 Java 规范提案。谁向谁提案呢？任何人都可以向 JCP (Java Community Process) 提出新增一个标准化技术规范的正式请求。JSR已成为Java界的一个重要标准。登录[ JCP 官网 (opens new window)](https://jcp.org/en/home/index)可以查看[所有 JSR 标准 (opens new window)](https://jcp.org/en/jsr/all)。

#### 2、JSR 305

JSR 305: Annotations for Software Defect Detection

This JSR will work to develop standard annotations (such as @NonNull) that can be applied to Java programs to assist tools that detect software defects.

主要功能：使用注解（例如@NonNull等等）协助开发者侦测软件缺陷。

Spring 从 5.0 版本开始支持了 JSR 305 规范中涉及到的相关注解。

```java
package org.springframework.lang;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

import javax.annotation.Nonnull;
import javax.annotation.meta.TypeQualifierNickname;

/**
 * A common Spring annotation to declare that annotated elements cannot be {@code null}.
 *
 * <p>Leverages JSR-305 meta-annotations to indicate nullability in Java to common
 * tools with JSR-305 support and used by Kotlin to infer nullability of Spring API.
 *
 * <p>Should be used at parameter, return value, and field level. Method overrides should
 * repeat parent {@code @NonNull} annotations unless they behave differently.
 *
 * <p>Use {@code @NonNullApi} (scope = parameters + return values) and/or {@code @NonNullFields}
 * (scope = fields) to set the default behavior to non-nullable in order to avoid annotating
 * your whole codebase with {@code @NonNull}.
 *
 * @author Sebastien Deleuze
 * @author Juergen Hoeller
 * @since 5.0
 * @see NonNullApi
 * @see NonNullFields
 * @see Nullable
 */
@Target({ElementType.METHOD, ElementType.PARAMETER, ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Nonnull
@TypeQualifierNickname
public @interface NonNull {
}
```

#### 3、相关注解

| 注解名称       | 含义                     | 可标记位置                                                   |
| -------------- | ------------------------ | ------------------------------------------------------------ |
| @Nullable      | 可以为空                 | @Target({ElementType.**METHOD**, ElementType.**PARAMETER**, ElementType.**FIELD**}) |
| @NonNull       | 不应为空                 | @Target({ElementType.**METHOD**, ElementType.**PARAMETER**, ElementType.**FIELD**}) |
| @NonNullFields | 在特定包下的字段不应为空 | @Target(ElementType.**PACKAGE**) @TypeQualifierDefault(ElementType.**FIELD**) |
| @NonNullApi    | 参数和方法返回值不应为空 | @Target(ElementType.**PACKAGE**) @TypeQualifierDefault({ElementType.**METHOD**, ElementType.**PARAMETER**}) |

### 第二节 整合junit5

#### 1、导入依赖

在原有环境基础上增加如下依赖：

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.7.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>5.3.1</version>
    <scope>test</scope>
</dependency>
```

#### 2、创建测试类

@ExtendWith(SpringExtension.class) 表示使用 Spring 提供的扩展功能。

@ContextConfiguration(value = {"classpath:spring-context.xml"}) 还是用来指定 Spring 配置文件位置，和整合 junit4 一样。

```java
@ExtendWith(SpringExtension.class)
@ContextConfiguration(value = {"classpath:spring-context.xml"})
public class Junit5IntegrationTest {
    
    @Autowired
    private EmpDao empDao;
    
    @Test
    public void testJunit5() {
        System.out.println("empDao = " + empDao);
    }
    
}
```

#### 3、使用复合注解

@SpringJUnitConfig 注解综合了前面两个注解的功能，此时指定 Spring 配置文件位置即可。但是注意此时需要使用 locations 属性，不是 value 属性了。

```java
@SpringJUnitConfig(locations = {"classpath:spring-context.xml"})
public class Junit5IntegrationTest {
    
    @Autowired
    private EmpDao empDao;
    
    @Test
    public void testJunit5() {
        System.out.println("empDao = " + empDao);
    }
    
}
```