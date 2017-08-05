# 目录

[TOC]

---



# 概念

Java SE，用于桌面开发，如，一些单机类的程序；
Java EE，用于Web开发，即网站开发，如，淘宝网；会使用一些成熟的框架；

java 基础包含的技术：
	面向对象，集合，界面，线程，文件流，网络；(而servlet，jsp，struts都是以java基础延伸的，)

jsp, 是JavaEE的核心技术的一种，

Java EE 程序员必须要掌握的基本技术是：java，servlet，jsp；
技术路线：java > servlet > jsp

java 本身不支持web开发，servlet 相当于对java的一个扩展，使java可以进行web开发，而servlet 做界面比较困难，所以出现了jsp技术；



## Java Servlet

> Java Servlet 是运行在Web 服务器或应用服务器上的程序，它是作为来自 Web 浏览器或其他 HTTP 客户端的请求和 HTTP 服务器上的数据库或应用程序之间的中间层。
>
> 使用 Servlet，您可以收集来自网页表单的用户输入，呈现来自数据库或者其他源的记录，还可以动态创建网页”。Servlet 是 sun 公司提供的一门用于开发动态 web 资源的技术。其实，"Servlet"本来是指 Java语言实现的一个接口（狭义的Servlet），但更多的也更普遍的情况是：我们把任何实现了 Servlet 接口的类都叫作 "Servlet"。Servlet 的作用主要是对 Request 的请求数据进行解析、按照业务逻辑处理并将结果封装成 Response 返回我的理解就是“读-计算-写”，像数学计算器一样，输入操作数、操作符按"等于"就显示出结果；也像人的脑神经元一样“接受刺激-信号处理-作出响应”。



struts 框架 + hibernate框架 + spring 框架 就形成了 ssh 框架组合架构；


JavaEE的学习路线：
java基础技术 > jdbc(java 的数据库编程) > oracle/mysql/sqlserver > html+css+javascript 网页设计> xml 

struts 是一个web框架，用来管理jsp/action/actionfrom；处于web层；

hibernate 是一个ORM框架，即对象和关系映射的框架 ，处于持久层；

spring 是一个容器框架，用于配置bean并维护bean之间关系的；此处的bean



# 01. Java 基础技术

## 面向对象





## 集合



## 多线程



## 文件及IO流



## XML



## 网络





# Java 的应用场景

### 1.企业级应用开发

大到全国联网的系统，小到中小企业的应用解决方案，JAVA都占有极为重要的地位 .

### 2.网站平台开发

JSP+Servlet+JavaBean，一直以来都相当流行模式.

### 3.移动领域

典型的应用是手机游戏（国内主要是这方面），大量使用到了J2ME 。

### 4.移动android APP开发

[Android](http://lib.csdn.net/base/android) 开发只用到了JAVA的语法和[Java SE](http://lib.csdn.net/base/javase)的一小部分API.

### 5.一般学习哪些阶段

![这里写图片描述](http://img.blog.csdn.net/20160625235149057) 
其中JavaSE部分的学习内容就非常的多.

### 6.薪资情况

如果有2-3年Java平台开发经验的,工资一般都是10-16K左右的.属于中等偏上水平.

------



---



# 02. MySQL

使用MySQL数据库之前要先安装和配置好MySQL；

运行：`services.msc`  检查MySQL 服务是否开启，如果没有开启则手动开启；

## 常用命令

`mysql> show variables; `  展示环境变量；

`mysql> show variables like "char%"`  根据条件来展示环境变量；

## MySQL 中文乱码问题



## 使用 sql 脚本进行MySQL 编程

将SQL语句写在 sql 脚本中，命名规范为：`xxx.sql`

在MySQL数据库中使用 sql 脚本：

`mysql> source sql文件的路径`，回车即可执行该 sql 脚本； 

---
# 03. JDBC 数据库编程

### 简介

```markdown
使用JDBC 开发数据库应用。
Java8 支持 JDBC 4.2 标准。
JDBC（Java Data Base Connectivity,java数据库连接）是一种用于执行SQL语句的Java API，可以为多种关系数据库提供统一访问，它由一组用Java语言编写的类和接口组成。JDBC提供了一种基准，据此可以构建更高级的工具和接口，使数据库开发人员能够编写数据库应用程序。
```

```markdown
Sun 公司提供的JDBC可以完成 3 个基本工作：
	1. 建立与数据库的连接；
	2、执行 SQL 语句；
	3、获得 SQL 语句的执行结果。
```



### 一、配置 JDBC 的开发环境

使用eclipse 进行 JDBC 编程，首先要配置开发环境：

1、要添加`Referenced Libraries` 来注册驱动，然后才能在代码中注册驱动。
​	将`mysql-connector-java-5.1.30-bin.jar`添加到项目的lib目录下，然后`Add to Buildpath`即可添加为`Referenced Libraries`。

这一步就相当于将 MySQL数据库驱动添加到windows系统的 CLASSPATH 环境变量中。

2、然后就可以查询 JDK API，进行代码**加载驱动** 和随后的JDBC编程。



### 二、API

> API 的学习参照：“JDK_API_1_6_zh_CN.chm” 和 “Java Platform SE 8.chm”。勤查 API.



## java 连接 MYSQL 案例

### 案例1

**需求**：编写一个程序，这个程序从 user 表中读取数据，并打印在命令行窗口中。

**实现**：

开发环境：

Eclipse-Java EE，MYSQL;

#### 1、搭建实验环境：
##### 1.1、  MYSQL 

> 在 MYSQL 中创建一个数据库，并创建 student 表和插入表的数据

​	创建一个使用utf8字符集的std_db 数据库：

```mysql
create database std_db character set utf8;
```

​	使用std_db 数据库：

```mysql
use std_db;
```

​	创建student表：

```mysql
create table student(
  id int(4) not null primary key auto_increment,
  name char(20) not null,
  age char(20) not null
);
```

​	查看表结构：

```mysql
desc student;
```

​	向`student`表中插入记录：

```mysql
insert into student values(1, 'Lucy', '22'), (2, 'Lily', '8');
```

​	查询`student`表的所有行：

```mysql
select * from student;
```

##### 1.2、给Java Project 添加数据库驱动软件包
New一个`Java Project`,并导入MYSQL数据库驱动`mysql-connector-java-x.x.x-bin.jar`(在项目目录下创建lib目录，copy驱动到lib中，然后‘add to build path’)；

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
```



#### 2、编写java程序，在程序中加载数据库驱动；
```java
//使用反射来注册驱动
Class.forName("com.mysql.jdbc.Driver");
```

#### 3、建立连接
`Connection conn = DriverManager.getConnection(url, username, password);`
数据库的Url 用于标识数据库的位置，程序员通过ur告诉JDBC 程序连接哪个数据库，
Url 的写法为：
`协议:子协议//主机:端口号/数据库名?参数名:参数值`
`jdbc:mysql://localhost:3306/student`  或者简写为`jdbc:mysql:///std_db`
```java
//和数据库建立连接
conn = DriverManager.getConnection("jdbc:mysql:///std_db", "root", "123");
```

####4、创建用于向数据库发送SQL的 Statement 对象，并发送sql
```java
//创建一个Statement用来发送sql语句
Statement st = conn.createStatement();
//sql语句
String sql = "select * from student";
//执行查询操作,结果集中就包含了从数据库查询到的结果
ResultSet rs = st.excuteQuery(sql);
```

#### 5、从结果集 ResultSet 中取出数据，打印到命令行窗口
```java
//next把光标移动至下一行，取出下一行的数据
while(rs.next()) {
  String name = rs.getString("name");
  String age = rs.getString("age");
  System.out.println(name +":" + age);
}
```

#### 6、断开与数据库的连接，并释放相关资源
```java
finally {
  if(rs != null){
    rs.close();
  }
  if(st != null) {
    st.close();
  }
  if(conn != null) {
    conn.close();
  }
}
```

### 真实项目



---

# 04. servlet

## 学习的站点

[Servlet 的使用-CSDN]( http://blog.csdn.net/a_running_wolf/article/details/51377550) 

[Servlets Tutorial](https://www.tutorialspoint.com/servlets/index.htm)



## What are Servlets?

Java Servlets are programs that run on a Web or Application server and act as a middle layer(中间层) between a request coming from a Web browser or other HTTP client and databases or applications on the HTTP server.

Using Servlets, you can collect input from users through web page forms, present records from a database or another source, and create web pages dynamically.

Java Servlets often serve the same purpose as programs implemented using the Common Gateway Interface (CGI，通用网管接口). But Servlets offer several advantages in comparison with the CGI.

- Performance is significantly better.
- Servlets execute within the address space of a Web server. It is not necessary to create a separate process to handle each client request.
- Servlets are platform-independent because they are written in Java.
- Java security manager on the server enforces a set of restrictions to protect the resources on a server machine. So servlets are trusted.
- The full functionality of the Java class libraries is available to a servlet. It can communicate with applets, databases, or other software via the sockets and RMI mechanisms that you have seen already.

## Servlets Architecture:

Following diagram shows the position of Servelts in a Web Application.

![Servlets Architecture](https://www.tutorialspoint.com/servlets/images/servlet-arch.jpg)

## Servlets Tasks:

Servlets perform the following major tasks:

- Read the explicit data sent by the clients (browsers). This includes an HTML form on a Web page or it could also come from an applet or a custom HTTP client program.
- Read the implicit HTTP request data sent by the clients (browsers). This includes cookies, media types and compression schemes the browser understands, and so forth.
- Process the data and generate the results. This process may require talking to a database, executing an RMI or CORBA call, invoking a Web service, or computing the response directly.
- Send the explicit data (i.e., the document) to the clients (browsers). This document can be sent in a variety of formats, including text (HTML or XML), binary (GIF images), Excel, etc.
- Send the implicit HTTP response to the clients (browsers). This includes telling the browsers or other clients what type of document is being returned (e.g., HTML), setting cookies and caching parameters, and other such tasks.

## Servlets Packages:

Java Servlets are Java classes run by a web server that has an interpreter that supports the Java Servlet specification.

Servlets can be created using the **javax.servlet** and **javax.servlet.http** packages, which are a standard part of the Java's enterprise edition, an expanded version of the Java class library that supports large-scale development projects.

These classes implement the Java Servlet and JSP specifications. At the time of writing this tutorial, the versions are Java Servlet 2.5 and JSP 2.1.

Java servlets have been created and compiled just like any other Java class. After you install the servlet packages and add them to your computer's Classpath, you can compile servlets with the JDK's Java compiler or any other current compiler.

## What is Next?

I would take you step by step to set up your environment to start with Servlets. So fasten your belt for a nice drive with Servlets. I'm sure you are going to enjoy this tutorial very much.





---
# 05. jsp



