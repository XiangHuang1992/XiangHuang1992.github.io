---
title: Hibernate学习教程（二）----ORM 概述
description: <blockquote class="blockquote-center">Hibernate是一个ORM框架，这里主要介绍了一下ORM的必要性以及ORM的一些相关概念</blockquote>
date: 2017-03-17 17:52:32
tags: [Hibernate,ORM框架,javaweb]
categories: Hibernate
keywords: Hibernate,ORM,JavaWEB
---


### 什么是JDBC

* JDBC:Java Database Connectivity，提供一组Java API，用于java程序中访问关系数据库。通过这些API，Java程序能够执行SQL语句并与任何SQL兼容的数据库进行交互。

* JDBC提供了一种灵活的架构，可以编写一个独立于数据库的应用程序，该应用程序可以在不同的平台上并与不同的DBMS进行修改。

### JDBC的优点和缺点

|优点	|缺点	|
|---|---|
| 简洁的SQL处理	| 用于大型应用程序时比较复杂	|
| 处理大量数据有着良好的性能	| 资源占用开销比较大	|
| 非常适用于小型应用程序	| 没有进行封装抽象	|
| 语法简单，学习成本较低	| 很难用于MVC模式开发	|
|	|只能用于DBMS查询	|

### 为什么要进行ORM关系映射(Object Relational Mapping)
当我们使用面向对象的系统时，对象模型与关系数据库之间存在不匹配。RDBMS以表格形式表示数据，而面向对象的语言（如Java和C#）将其表现为对象的互联图。如下所示：

```java
public class Employee {
   private int id;
   private String first_name; 
   private String last_name;   
   private int salary;  

   public Employee() {}
   public Employee(String fname, String lname, int salary) {
      this.first_name = fname;
      this.last_name = lname;
      this.salary = salary;
   }
   public int getId() {
      return id;
   }
   public String getFirstName() {
      return first_name;
   }
   public String getLastName() {
      return last_name;
   }
   public int getSalary() {
      return salary;
   }
}
```

上面的对象需要被存储和检索到下面的RDBMS表：

```SQL
create table EMPLOYEE (
   id INT NOT NULL auto_increment,
   first_name VARCHAR(20) default NULL,
   last_name  VARCHAR(20) default NULL,
   salary     INT  default NULL,
   PRIMARY KEY (id)
);
```
那么就会存在以下两个问题：
* 如果我们需要在开发了几个页面之后或在应用程序中修改数据库的设计时，应该怎么处理？
* 在关系数据库加载和存储对象会暴露以下不匹配问题：

|不匹配问题	|描述	|
|---|---|
|Granularity（粒度）	|有时，您将有一个对象模型，它具有比数据库中对应表数量更多的类。	|
|Inheritance（继承）	|RDBMS不定义类似于继承的任何东西，它是面向对象编程语言中的自然范例。	|
|Identity（对象同一性）	|RDBMS正好定义了“同一性”的一个概念：主键。然而，Java定义了对象标识（a == b）和对象相等（a.equals（b））	|
|Associations	|面向对象语言使用对象引用表示Associations，RDBMS使用外键列表示	|
|Navigation	|在Java和RDBMS中访问对象的方式是完全不同的	|

对象关系映射（ORM）是处理所有上述不匹配问题的解决方案。

#### 粒度问题
* 粒度：是指你正在使用的类型的大小。

#### 继承（子类型问题）
* 在Java中，使用超类(superclass)和子类(subclass)来实现继承模型。
* 在Java中，继承是类型继承(type Inheritance)，而数据库表并不是一种类型。
* 数据库产品一般不实现类型或者表继承。而且即使实现了，我们也会遇到数据完整性的问题（对可更新视图的有限完整性规则）。
* 一旦把继承进入到模型当中，就有了`多态(polymorphism)`的可能。SQL数据库缺乏一种明显的表示多态关联的方式，一个外键约束精确的引用一张目标表，定义一个引用多表的外键并不容易。必须编写一个程序化的约束来加强这种完整性规则。

**子类型的这种不匹配的结果是：模型中的继承结构必须在一个不提供继承策略的SQL数据库中被持久化。**

### 对象同一性
如果当我们需要检查两个对象是否为同一个对象的时候。解决方法有三种：
* 在java中：
	* 对象同一性（粗略等同于内存位置，用a==b检查）
	* 等同性，通过equals()方法（也成为值等同）的实现来确定。

* 数据库的同一性用主键值来表达。如果使用java中的方法来判断，那么主键值必然会不相等。
### 什么是ORM

ORM（对象关系映射），是一种用于关系数据库和面向对象编程语言（如Java、C#）之间转换数据的编程技术。相对于JDBC，ORM具有以下优点：

|序号	|优点	|
|---|---|
|1	|允许业务逻辑代码访问对象而不是数据库表	|
|2	|从面向对象的角度考虑隐藏SQL查询的详细信息	|
|3	|底层基于JDBC	|
|4	|无需处理数据库实现	|
|5	|基于业务概念而不是数据库结构的实体	|
|6	|事务管理和秘钥自动生成	|
|7	|应用快速开发	|

ORM解决方案由以下四个模块组成：

|序号	|解决方案	|
|---|---|
|1	|用于对持久化类的对象进行基本CRUD操作的API	|
|2	|用于指定引用类的类和属性的查询的语言或API	|
|3	|用于指定映射元数据的可配置工具	|
|4	|用于实现ORM的一项技术，与事务对象交互，执行脏检查、延迟关联抓取以及其它优化功能	|

### Java中的ORM框架
Java中有几个持久化框架和ORM选项。持久化框架是一种将对象存储和检索到关系数据库中的ORM服务。

* Enterprise JavaBeans Entity Beans
* Java Data Objects
* Castor
* TopLink
* Spring DAO
* Hibernate
* ……. etc.

### ORM和Hibernate的一些好处
#### 生产力
与持久化相关的代码可能会是java中最冗长的一部分代码，Hibernate除去了许多琐碎的工作，让我们可以把更多的精力集中于业务问题的处理上。
无论我们喜欢哪一种应用程序开发策略——自上而下，从一个领域模型开始；或者自底而上，从一个现有的数据库Schema开始——Hibernate与适当的工具一起使用，将明显减少开发时间。

#### 可维护性
更少的代码行使得系统更易于理解，因为它强调业务逻辑甚于那些费力的基础性工作。更重要的是，系统包含的代码越少则越利于重构。自动的对象/关系持久化充分减少了代码行。

Hibernate更易于维护还有其它原因，在手工编码的持久化系统中，关系表示法和对象模型实现领域之间存在一种必然的压力。改变一个，通常都要改变另一个，并且一个表示法设计通常需要妥协以便适应另一个的存在。ORM提供了两个模型之间的一个缓冲，允许面向对象在Java方面进行更优雅的利用，并且每个模型的微小变化都不会传递到另一个模型。

#### 性能
手工编码的持久化和自动的持久化相比总是可以一样快，并且经常更快。这是事实。但是在实际开发中，会受到时间和预算的约束。

在有限时间的项目中，手工编码的持久化通常允许你进行一些优化；Hibernate始终允许使用更多的优化。

自动的持久化能够大大提高开发人员的工作效率，使得开发人员能够花更多的时间对其它少数瓶颈进行手工优化。

实现ORM框架的人，可能在性能优化方面比我们做的更好。

#### 供应商独立性
ORM从底层的SQL数据库和SQL方言中把应用程序抽象出来。如果这个工具支持不同的数据库，这会给我们的应用程序带来一定程度的可移植性。可以帮我们减少一些被供应商锁定的风险。

数据库的独立性使得我们可以在开发时选择一些轻量级的数据库，在部署时，将实际的产品部署在不同的数据库上。