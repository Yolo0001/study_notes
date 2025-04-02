# IoC容器

## Spring IoC容器和Bean简介

对象仅通过构造参数、工厂方法的参数来定义其依赖关系，然后容器在创建Bean时注入这些依赖关系。这样和平常直接构建Bean的过程相逆，因此被称为控制反转。

IoC容器通过`BeanFactory`和`ApplicationContext`创建，`ApplicationContext`是`BeanFactory`的超集，增加了更多特定的企业功能。

## 容器概述

容器通过读取配置元数据来获得关于要实例化、配置和组装哪些对象的指示。

`ApplicationContext`提供了两个实现：

`ClassPathXmlApplicationContext`(通过读取类路径下的 XML 格式的配置文件创建 IOC 容器对象)

`FileSystemXmlApplicationContext`(通过文件系统路径读取 XML 格式的配置文件创建 IOC 容器对象)

### 配置元数据

基于注解的配置

基于XML的配置

### 实例化一个容器

### 使用容器

`T getBean(String name, Class<T> requiredType)`来检索Bean的实例，但一般不用，而是通过autowiring注解来对特定的Bean产生依赖。

## Bean的概览

