---
title: Hibernate教程（一）---Hibernate简介
description: <blockquote class="blockquote-center">Hibernate是一个java对象映射关系的解决方案的ORM（Object-Relational Mapping）框架，是一个开源持久框架，由`Gavin King`于2001年创建。</blockquote>
date: 2017-03-17 11:14:02
tags: [hibernate,ORM框架,javaweb]
categories: Hibernate
keywords: hibernate教程,JavaWeb框架
---

## Hibernate简介

* Hibernate是一个Java对象映射关系的解决方案的ORM（Object-Relational Mapping）框架，是一个开源持久框架，由`Gavin King`于2001年创建。为Java应用提供强大的、高性能对象持久化和查询服务。

* Hibernate将Java类映射到数据库表，将Java数据类型映射到SQL数据类型，减轻了开发人员95%的数据持久性相关的编程任务。

* Hibernate位于传统的Java对象和数据库服务器之间，基于适当的`O/R机制和模式`来处理持久化这些对象的所有工作。

![Hibernate-position](http://7xt7l1.com1.z0.glb.clouddn.com/hibernate_position.jpg)


### Hibernate的优势

* Hibernate通过XML配置文件将Java类映射到数据库表，而不需要编写任何代码。
* 提供简单的API,用于直接存储和检索数据库中的Java对象。
* 如果数据库或任何表中有更改，只需要修改XML文件。
* 提取我们不熟悉的SQL类型，并提供我们熟悉的Java对象。
* Hibernate不需要应用府服务器来操作。
* 操作复杂关联的数据库对象。
* 使用智能抓取策略简化数据库操作。
* 提供简单的数据查询。

### Hibernate支持的数据库

Hibernate几乎支持所有的关系型数据库管理系统(RDBMS),支持的数据库如下所示：
* HSQL Database Engine
* DB2/NT
* MySQL
* PostgreSQL
* FrontBase
* Oracle
* Microsoft SQL Server Database
* Sybase SQL Server
* nformix Dynamic Server

### Hibernate架构

Hibernate架构是分层的，所以我们不需要知道底层的API，Hibernate利用数据库和配置数据向我们的应用程序提供持久性服务（和持久性对象）。

下图是Hibernate应用结构体系简要视图：
![Hibernate-hign-level](http://7xt7l1.com1.z0.glb.clouddn.com/hibernate_high_level.jpg)

下图是Hibernate应用结构体系详细视图，包含了几个重要的核心类：
![Hibernate架构](http://7xt7l1.com1.z0.glb.clouddn.com/hibernate_architecture.jpg)

* Hibernate使用各种现有的Java API，如`JDBC`,`JTA`,`JNDI`。
> `JDBC`提供了关系数据库通用的功能抽象层，所有具有`JDBC`驱动程序的数据库都被`Hibernate`支持。
> `JTA`和`JNDI`允许`Hibernate`与J2EE服务器集成。

## Hibernate应用结构体系主要类对象

### Configuration Object

`Configuration Object`是我们在Hibernate应用程序中创建的第一个Hibernate对象，通常在应用程序初始化时且只创建一次。它是Hibernate所需要的配置和属性文件。Configuration对象提供两个关键组件：
* **Database Connection:**通过Hibernate支持的一个或多个配置文件来处理。`hibernate.properties`,`hibernate.cfg.xml`。
* **Class Mapping Setup:**这个组件用于Java类和数据库表之间创建连接。

### SessionFactory Object
`Configuration Object`用于创建一个`SessionFactory Obejct`，该对象使用提供的配置文件为应用程序配置`Hibernate`，并允许实例化一个`Session`对象。`SessionFactory`是`线程安全对象`,供应用程序的所有线程使用。

`SessionFactory`是重量级对象。因此通常在应用程序启动期间创建并保留供以后使用。

每个数据库都需要使用一个单独的配置文件创建一个`SessionFactory`对象。如果使用多个数据库，则必须创建多个`SessionFactory`对象。

### Session(会话) Object
`Session（会话）`用于获取与数据库的物理连接，Session对象是轻量级的，并且是每当需要与数据库进行交互时才会被实例化。持久化对象通过Session对象进行保存和检索。

Session对象不应该长时间保持打开，因为他们通常不是线程安全的，所以应该根据业务需求创建和销毁它们。

### Transaction（事务） Object
事务`Transaction`代表与数据库的工作单元，大多数关系型数据库都支持事务功能。Hibernate中的事务由底层事务管理器和事务（来自JDBC和JTA）处理。

这是一个可选对象，Hibernate应用程序可以选择不使用此接口，而选择在自己的应用程序代码中管理事务。

### Query Object

查询`Query`对象使用SQL或者Hibernate查询语言(`Hibernate Query Language,HQL`)字符串从数据库检索数据并创建对象。Query实例用于绑定查询参数，限制查询返回的结果数量，最后执行查询。

### Criteria Object

条件对象用于创建和执行面向对象的标准查询以检索对象。

## Hibernate 环境配置

该章主要介绍如何安装Hibernate以及其它相关包来为Hibernate应用程序准备一个开发环境。本文将使用Mysql数据库来演示Hibernate实例。

### Hibernate下载

* 在windows上下载`.zip`文件，在Unix上下载`.tz`文件。
* 从[http://www.hibernate.org/downloads](http://www.hibernate.org/downloads "hibernate下载链接")下载最新版的Hibernate。
* 下载完成之后进行解压。

### 安装Hibernate

下载完Hibernate之后，只需要执行以下两个简单的步骤即可。请确保正确的配置了`CLASSPATH`环境变量，否则在编译应用程序时会出现问题。


### Hibernate的依赖包

|S.N.	|Packages/Libraries	|
|---|---|
|1	|dom4j - XML parsing www.dom4j.org/	|
|2	|Xalan - XSLT Processor http://xml.apache.org/xalan-j/	|
|3	|Xerces - The Xerces Java Parser http://xml.apache.org/xerces-j/	|
|4	|cglib - Appropriate changes to Java classes at runtime http://cglib.sourceforge.net/	|
|5	|log4j - Logging Faremwork http://logging.apache.org/log4j	|
|6	|Commons - Logging, Email etc. http://jakarta.apache.org/commons	|
|7	|SLF4J - Logging Facade for Java http://www.slf4j.org	|

### Hibernate配置

Hibernate需要提前知道在哪里可以找到定义的Java类和数据库表相关联的映射信息。Hibernate还需要一组与数据库和其它相关参数相关的配置设置。所有这些信息通常作为标准java属性文件`hibernate.properties`或者名为`hibernate.cfg.xml`的XML文件提供。

### Hibernate属性

以下是在独立情况下为一个数据库配置所需要的重要属性列表：

|S.N.	|Properties and Description	|
|---|---|
|1	|`hibernate.dialect`:此属性使Hibernate为选定的数据库生成适当的SQL	|
|2	|`hibernate.connection.driver_class`:JDBC驱动程序类	|
|3	|`hibernate.connection.url`:数据库实例的JDBC URL	|
|4	|`hibernate.connection.username`:数据库用户名	|
|5	|`hibernate.connection.password`:数据库密码	|
|6	|`hibernate.connection.pool_size`:限制在Hibernate数据库连接池中的等待连接数	|
|7	|`hibernate.connection.autocommit`:允许JDBC连接自动提交	|

如果随着应用服务器和JNDI使用同一个服务器，则还需要配置以下属性：

|S.N.	|Properties and Description	|
|---|---|
|1	|`hibernate.connection.datasource`:在应用服务器中定义的JNDI名称	|
|2	|`hibernate.jndi.class`:JNDI的InitialContext类	|
|3	|`hibernate.jndi.<JNDIpropertyname>`:	|
|4	|`hibernate.jndi.url`:提供JNDI的url	|
|5	|`hibernate.connection.username`:数据库用户名	|
|6	|`hibernate.connection.password`:数据库密码	|
### Hibernate和Mysql数据库

`MySQL`是目前最流行的开源数据库系统之一，下面我们创建一个`hibernate.cfg.xml`配置文件，并将其放置于应用程序类路径的根目录下，必须确保已经安装`MySQL` 并保证已经保证创建了可用的测试数据库。
XML配置文件必须符合Hibernate 3 Configuration DTD，该文件可从http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd获得。
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-configuration SYSTEM 
"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
   <session-factory>
   <property name="hibernate.dialect">
      org.hibernate.dialect.MySQLDialect
   </property>
   <property name="hibernate.connection.driver_class">
      com.mysql.jdbc.Driver
   </property>

   <!-- Assume test is the database name -->
   <property name="hibernate.connection.url">
      jdbc:mysql://localhost/test
   </property>
   <property name="hibernate.connection.username">
      root
   </property>
   <property name="hibernate.connection.password">
      root123
   </property>

   <!-- List of XML mapping files -->
   <mapping resource="Employee.hbm.xml"/>

</session-factory>
</hibernate-configuration>
```

下表是各类数据库的属性类型(`Dialect Property`)列表：

|Database	|Dialect Property	|
|---|---|
|DB2	|org.hibernate.dialect.DB2Dialect	|
|HSQLDB	|org.hibernate.dialect.HSQLDialect	|
|HypersonicSQL	|org.hibernate.dialect.HSQLDialect	|
|Informix	|org.hibernate.dialect.InformixDialect	|
|Ingres	|org.hibernate.dialect.IngresDialect	|
|Interbase	|org.hibernate.dialect.InterbaseDialect	|
|Microsoft SQL Server 2000		|org.hibernate.dialect.SQLServerDialect	|
|Microsoft SQL Server 2005		|org.hibernate.dialect.SQLServer2005Dialect	|
|Microsoft SQL Server 2008		|org.hibernate.dialect.SQLServer2008Dialect	|
|MySQL	|	org.hibernate.dialect.MySQLDialect	|
|Oracle (any version)		|org.hibernate.dialect.OracleDialect	|
|Oracle 11g	|org.hibernate.dialect.Oracle10gDialect	|
|Oracle 10g	|org.hibernate.dialect.Oracle10gDialect	|
|Oracle 9i	|org.hibernate.dialect.Oracle9iDialect	|
|PostgreSQL	|org.hibernate.dialect.PostgreSQLDialect	|
|Progress	|org.hibernate.dialect.ProgressDialect	|
|SAP DB		|org.hibernate.dialect.SAPDBDialect	|
|Sybase	|org.hibernate.dialect.SybaseDialect	|
|Sybase Anywhere		|org.hibernate.dialect.SybaseAnywhereDialect	|


## Hibernate实例

### 创建POJO类
* 首先，我们创建`Java POJO类`，这取决于将被持久化到数据库的应用程序，生成`getXXX()`和`setXXX()`方法，使其成为`JavaBeans`兼容类。
* POJO（java普通对象）是一种java对象，它不扩展或实现一些EJB框架分别需要的一些专门的类或接口。所有正常的Java对象都是POJO。
* 当你设计一个要被Hibernate持久化的类时，提供符合JavaBeans的代码以及一个在Employee类中像id属性一样用作索引的属性很重要。

```java
public class Employee {
   private int id;
   private String firstName; 
   private String lastName;   
   private int salary;  

   public Employee() {}
   public Employee(String fname, String lname, int salary) {
      this.firstName = fname;
      this.lastName = lname;
      this.salary = salary;
   }
   public int getId() {
      return id;
   }
   public void setId( int id ) {
      this.id = id;
   }
   public String getFirstName() {
      return firstName;
   }
   public void setFirstName( String first_name ) {
      this.firstName = first_name;
   }
   public String getLastName() {
      return lastName;
   }
   public void setLastName( String last_name ) {
      this.lastName = last_name;
   }
   public int getSalary() {
      return salary;
   }
   public void setSalary( int salary ) {
      this.salary = salary;
   }
}
```

### 创建数据库表
第二步，我们需要在数据库中创建一张表，将表对应我们需要持久化的每一个对象，根据上面的java类我们创建下面这样一个表“

```SQL
create table EMPLOYEE (
   id INT NOT NULL auto_increment,
   first_name VARCHAR(20) default NULL,
   last_name  VARCHAR(20) default NULL,
   salary     INT  default NULL,
   PRIMARY KEY (id)
);
```

### 创建配置映射文件

接下来我们需要创建一个配置文件，说明Hibernate如何将定义的类映射至数据库表。

```XML
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
 "-//Hibernate/Hibernate Mapping DTD//EN"
 "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd"> 

<hibernate-mapping>
   <class name="Employee" table="EMPLOYEE">
      <meta attribute="class-description">
         This class contains the employee detail. 
      </meta>
      <id name="id" type="int" column="id">
         <generator class="native"/>
      </id>
      <property name="firstName" column="first_name" type="string"/>
      <property name="lastName" column="last_name" type="string"/>
      <property name="salary" column="salary" type="int"/>
   </class>
</hibernate-mapping>
```
我们应该把映射文件保存为`<classname>.hbm.xml`格式的文件。上面文件保存为`Employee.hbm.xml`。
* 映射文件是一个XML格式的文档。`<hibernate-mapping>`作为包含所有`<class>`元素的根元素。
* `<class>`元素用于定义从java类到数据库表的特定映射。`java类名称`使用使用类元素的`name属性`指定，并且使用`table`属性指定数据库表名称。
* `<meta>`元素是可选元素，用于创建类描述。
* `<id>`是将类中的唯一ID元素映射到数据库表的主键。id元素中的name属性引用类中的属性，cloumn属性引用数据库表中的列。type属性保存hibernate映射类型，此映射类型将从Java转换成SQL数据类型。
* id元素中的`<generator>`属性用于自动生成主键值，设置class的属性值为`native`，让hibernate选择`identity`，`sequence`,`hilo`算法来创建主键，这取决于底层数据库的能力。
* `<property>`元素用于将Java类属性映射到数据库表中的列。元素的name属性引用类中的属性，cloumn属性引用数据库表中的列。type属性保存hibernate映射类型，此映射类型将从Java类型转换成SQL数据类型。

### 创建应用类(java class)

完成了以上步骤后，我们来创建一个应用文件来测试一下我们的配置。

```java
import java.util.List; 
import java.util.Date;
import java.util.Iterator; 
 
import org.hibernate.HibernateException; 
import org.hibernate.Session; 
import org.hibernate.Transaction;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class ManageEmployee {
   private static SessionFactory factory; 
   public static void main(String[] args) {
      try{
         factory = new Configuration().configure().buildSessionFactory();
      }catch (Throwable ex) { 
         System.err.println("Failed to create sessionFactory object." + ex);
         throw new ExceptionInInitializerError(ex); 
      }
      ManageEmployee ME = new ManageEmployee();

      /* 添加一些employee对象到数据库表中*/
      Integer empID1 = ME.addEmployee("Zara", "Ali", 1000);
      Integer empID2 = ME.addEmployee("Daisy", "Das", 5000);
      Integer empID3 = ME.addEmployee("John", "Paul", 10000);

      /* 列出所有employee对象 */
      ME.listEmployees();

      /* 修改 */
      ME.updateEmployee(empID1, 5000);

      /* 从数据库中删除 */
      ME.deleteEmployee(empID2);

      /* 列出所有对象s */
      ME.listEmployees();
   }
   /* 向数据库中添加employee对象的方法 */
   public Integer addEmployee(String fname, String lname, int salary){
      Session session = factory.openSession();
      Transaction tx = null;
      Integer employeeID = null;
      try{
         tx = session.beginTransaction();
         Employee employee = new Employee(fname, lname, salary);
         employeeID = (Integer) session.save(employee); 
         tx.commit();
      }catch (HibernateException e) {
         if (tx!=null) tx.rollback();
         e.printStackTrace(); 
      }finally {
         session.close(); 
      }
      return employeeID;
   }
   /* 列出所有employee对象的方法 */
   public void listEmployees( ){
      Session session = factory.openSession();
      Transaction tx = null;
      try{
         tx = session.beginTransaction();
         List employees = session.createQuery("FROM Employee").list(); 
         for (Iterator iterator = 
                           employees.iterator(); iterator.hasNext();){
            Employee employee = (Employee) iterator.next(); 
            System.out.print("First Name: " + employee.getFirstName()); 
            System.out.print("  Last Name: " + employee.getLastName()); 
            System.out.println("  Salary: " + employee.getSalary()); 
         }
         tx.commit();
      }catch (HibernateException e) {
         if (tx!=null) tx.rollback();
         e.printStackTrace(); 
      }finally {
         session.close(); 
      }
   }
   /* 修改employee对象的方法 */
   public void updateEmployee(Integer EmployeeID, int salary ){
      Session session = factory.openSession();
      Transaction tx = null;
      try{
         tx = session.beginTransaction();
         Employee employee = 
                    (Employee)session.get(Employee.class, EmployeeID); 
         employee.setSalary( salary );
		 session.update(employee); 
         tx.commit();
      }catch (HibernateException e) {
         if (tx!=null) tx.rollback();
         e.printStackTrace(); 
      }finally {
         session.close(); 
      }
   }
   /* 删除employee对象的方法 */
   public void deleteEmployee(Integer EmployeeID){
      Session session = factory.openSession();
      Transaction tx = null;
      try{
         tx = session.beginTransaction();
         Employee employee = 
                   (Employee)session.get(Employee.class, EmployeeID); 
         session.delete(employee); 
         tx.commit();
      }catch (HibernateException e) {
         if (tx!=null) tx.rollback();
         e.printStackTrace(); 
      }finally {
         session.close(); 
      }
   }
}
```

### 编译和执行

编译和执行的步骤（请确保正确配置了环境变量）：

* 创建`hibernate.cfg.xml`配置文件。
* 创建`Employee.hbm.xml`映射文件。
* 创建`Employee.java`文件，并编译它。
* 创建如上所示的`ManageEmployee.java`文件，并执行编译。
* 执行`ManageEmployee.class`文件，运行程序。