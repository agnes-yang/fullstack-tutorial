# MySQL

[TOC]
<!-- TOC -->

- [MySQL](#mysql)
    - [1. 什么是事务](#1-什么是事务)
        - [AUTOCOMMIT](#autocommit)
    - [2. 数据库ACID？ 【阿里面经OneNote】](#2-数据库acid-阿里面经onenote)
        - [1. 原子性（Atomicity）](#1-原子性atomicity)
        - [2. 一致性（Consistency）](#2-一致性consistency)
        - [3. 隔离性（Isolation）](#3-隔离性isolation)
        - [4. 持久性（Durability）](#4-持久性durability)
    - [3. 数据库中的范式有哪些？ 【阿里面经OneNote】](#3-数据库中的范式有哪些-阿里面经onenote)
    - [4. 脏读、不可重复读和幻读 【阿里面经OneNote】](#4-脏读不可重复读和幻读-阿里面经onenote)
        - [脏读](#脏读)
        - [不可重复读](#不可重复读)
        - [幻读](#幻读)
    - [5. 事务隔离级别 【阿里面经OneNote】](#5-事务隔离级别-阿里面经onenote)
    - [6. MySQL存储引擎选择](#6-mysql存储引擎选择)
        - [存储引擎简介](#存储引擎简介)
        - [1. MyISAM](#1-myisam)
        - [2. InnoDB](#2-innodb)
            - [补充：独立表空间和系统表空间应该如何抉择呢？](#补充独立表空间和系统表空间应该如何抉择呢)
        - [3. CSV](#3-csv)
        - [4. Archive](#4-archive)
        - [5. Memory](#5-memory)
        - [6. Federated](#6-federated)
        - [★思考题](#★思考题)
            - [1. 如何选择存储引擎？](#1-如何选择存储引擎)
            - [2. MyISAM和InnoDB引擎的区别？](#2-myisam和innodb引擎的区别)
            - [3. 为什么不建议innodb使用亿级大表](#3-为什么不建议innodb使用亿级大表)
    - [7. MySQL数据类型](#7-mysql数据类型)
        - [整型](#整型)
        - [浮点数](#浮点数)
        - [字符串](#字符串)
        - [时间和日期](#时间和日期)
            - [1. DATATIME](#1-datatime)
            - [2. TIMESTAMP](#2-timestamp)
    - [8. 索引](#8-索引)
        - [（1）索引使用的场景](#1索引使用的场景)
        - [（2）B Tree 原理](#2b-tree-原理)
            - [1. B-Tree](#1-b-tree)
            - [2. B+Tree](#2-btree)
            - [3. 顺序访问指针](#3-顺序访问指针)
            - [4. 优势](#4-优势)
        - [（3）索引分类](#3索引分类)
            - [1. B+Tree 索引](#1-btree-索引)
            - [2. 哈希索引](#2-哈希索引)
            - [3. 全文索引](#3-全文索引)
            - [4. 空间数据索引（R-Tree）](#4-空间数据索引r-tree)
        - [（4）索引的特点](#4索引的特点)
        - [（5）索引的优点](#5索引的优点)
        - [（6）索引的缺点](#6索引的缺点)
        - [（7）索引失效](#7索引失效)
        - [（8）在什么情况下适合建立索引？](#8在什么情况下适合建立索引)
    - [9. 数据库中的分页查询语句怎么写？【阿里面经OneNote】](#9-数据库中的分页查询语句怎么写阿里面经onenote)
    - [10. 常用的数据库有哪些？Redis用过吗？【阿里面经OneNote】](#10-常用的数据库有哪些redis用过吗阿里面经onenote)
    - [11. Redis的存储结构，或者说如何工作的，与mysql的区别？有哪些数据类型？ 【阿里面经OneNote】](#11-redis的存储结构或者说如何工作的与mysql的区别有哪些数据类型-阿里面经onenote)
    - [12. 分库分表](#12-分库分表)
        - [1. 垂直切分](#1-垂直切分)
            - [（1）垂直切分的优点如下：](#1垂直切分的优点如下)
            - [（2）垂直切分的缺点如下：](#2垂直切分的缺点如下)
        - [2. 水平切分](#2-水平切分)
            - [（1）水平切分的优点如下：](#1水平切分的优点如下)
            - [（2）水平切分的缺点如下：](#2水平切分的缺点如下)
            - [（3）综上所述，垂直切分和水平切分的共同点如下：](#3综上所述垂直切分和水平切分的共同点如下)
        - [Sharding 策略](#sharding-策略)
        - [Sharding 存在的问题及解决方案](#sharding-存在的问题及解决方案)
            - [1. 事务问题](#1-事务问题)
            - [2. JOIN](#2-join)
            - [3. ID 唯一性](#3-id-唯一性)
    - [13. 主从复制与读写分离](#13-主从复制与读写分离)
        - [主从复制](#主从复制)
        - [读写分离](#读写分离)
    - [14. 查询性能优化](#14-查询性能优化)
        - [（1）使用 Explain 进行分析](#1使用-explain-进行分析)
        - [（2）优化数据访问](#2优化数据访问)
            - [1. 减少请求的数据量](#1-减少请求的数据量)
            - [2. 减少服务器端扫描的行数](#2-减少服务器端扫描的行数)
        - [（3）重构查询方式](#3重构查询方式)
            - [1. 切分大查询](#1-切分大查询)
            - [2. 分解大连接查询](#2-分解大连接查询)
- [实践问题](#实践问题)
    - [1. 如何解决秒杀的性能问题和超卖的讨论](#1-如何解决秒杀的性能问题和超卖的讨论)
            - [解决方案1：](#解决方案1)
            - [解决方案2：](#解决方案2)
            - [解决方案3：](#解决方案3)
    - [2. 数据库主从不一致，怎么解？](#2-数据库主从不一致怎么解)
- [附录：参考资料](#附录参考资料)

<!-- /TOC -->


## 1. 什么是事务

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/185b9c49-4c13-4241-a848-fbff85c03a64.png)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/185b9c49-4c13-4241-a848-fbff85c03a64.png)

 

事务指的是满足 ACID 特性的一组操作，可以通过 Commit 提交一个事务，也可以使用 Rollback 进行回滚。

### AUTOCOMMIT

MySQL 默认采用自动提交模式。也就是说，如果不显式使用`START TRANSACTION`语句来开始一个事务，那么每个查询都会被当做一个事务自动提交



## 2. 数据库ACID？ 【阿里面经OneNote】

### 1. 原子性（Atomicity）

事务被视为不可分割的最小单元，事务的所有操作要么全部提交成功，要么全部失败回滚。

回滚可以用日志来实现，日志记录着事务所执行的修改操作，在回滚时反向执行这些修改操作即可。

### 2. 一致性（Consistency）

数据库在事务执行前后都保持一致性状态。

在一致性状态下，所有事务对一个数据的读取结果都是相同的。

### 3. 隔离性（Isolation）

一个事务所做的修改在最终提交以前，对其它事务是不可见的。

### 4. 持久性（Durability）

一旦事务提交，则其所做的修改将会永远保存到数据库中。即使系统发生崩溃，事务执行的结果也不能丢失。

可以通过数据库备份和恢复来实现，在系统发生奔溃时，使用备份的数据库进行数据恢复。



事务的 ACID 特性概念简单，但不是很好理解，主要是因为这几个特性不是一种平级关系：

- 只有满足一致性，事务的执行结果才是正确的。
- 在无并发的情况下，事务串行执行，隔离性一定能够满足。此时要只要能满足原子性，就一定能满足一致性。
- 在并发的情况下，多个事务并发执行，事务不仅要满足原子性，还需要满足隔离性，才能满足一致性。
- 事务满足持久化是为了能应对数据库奔溃的情况。

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/35650b4b-efa1-49ba-9680-19837027cfc9.png)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/35650b4b-efa1-49ba-9680-19837027cfc9.png)

## 3. 数据库中的范式有哪些？ 【阿里面经OneNote】

目前关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式（5NF，又称完美范式）。满足最低要求的范式是第一范式（1NF）。在第一范式的基础上进一步满足更多规范要求的称为第二范式（2NF），其余范式以次类推。一般说来，数据库只需满足第三范式(3NF）就行了。 

范式的包含关系。一个数据库设计如果符合第二范式，一定也符合第一范式。如果符合第三范式，一定也符合第二范式… 

- 1NF ：符合1NF的关系中的每个属性都不可再分 
- 2NF：属性完全依赖于主键 [消除部分子函数依赖] 
- 3NF：属性不依赖于其它非主属性[消除传递依赖] 
- BCNF：在1NF基础上，任何非主属性不能对主键子集依赖[在3NF基础上消除对主码子集的依赖] 
- 4NF：要求把同一表内的多对多关系删除。 
- 5NF：从最终结构重新建立原始结构。 



范式理论是为了解决以上提到四种异常。

高级别范式的依赖于低级别的范式，1NF 是最低级别的范式。

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/c2d343f7-604c-4856-9a3c-c71d6f67fecc.png)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/c2d343f7-604c-4856-9a3c-c71d6f67fecc.png)

 

## 4. 脏读、不可重复读和幻读 【阿里面经OneNote】

### 脏读

 （针对未提交数据）如果一个事务中对数据进行了更新，但**事务还没有提交**，另一个事务可以“看到”该事务没有提交的更新结果，这样造成的问题就是，如果第一个事务回滚，那么，第二个事务在此之前所“看到”的数据就是一笔脏数据。 **（脏读又称无效数据读出。一个事务读取另外一个事务还没有提交的数据叫脏读。 ）**

 e.g.

​	Mary的原工资为1000, 财务人员将Mary的工资改为了8000(但未提交事务)

​	Mary读取自己的工资 ,发现自己的工资变为了8000，欢天喜地！

​	而财务发现操作有误，回滚了事务,Mary的工资又变为了1000

​	像这样,Mary记取的工资数8000是一个脏数据。

解决办法：把数据库的事务隔离级别调整到READ_COMMITTED



### 不可重复读

是指在一个事务内，多次读同一数据。在这个事务还没有结束时，另外一个事务也访问该同一数据。那么，在第一个事务中的两次读数据之间，由于第二个事务的修改，那么第一个事务两次读到的的数据可能是不一样的。这样在一个事务内两次读到的数据是不一样的，因此称为是不可重复读。**（同时操作，事务一分别读取事务二操作时和提交后的数据，读取的记录内容不一致。不可重复读是指在同一个事务内，两个相同的查询返回了不同的结果。 ）**

**例子：**

（1）在事务1中，Mary 读取了自己的工资为1000，操作并没有完成   

```sql
con1 = getConnection();  
select salary from employee empId ="Mary"; 
```

（2）在事务2中，这时财务人员修改了Mary的工资为2000,并提交了事务. 

```sql
con2 = getConnection();  
update employee set salary = 2000;  
con2.commit();  
```

（3）在事务1中，Mary 再次读取自己的工资时，工资变为了2000 

```sql
//con1  
select salary from employee empId ="Mary";  
```

在一个事务中前后两次读取的结果并不致，导致了不可重复读。

**解决办法**：如果只有在修改事务完全提交之后才可以读取数据，则可以避免该问题。把数据库的事务隔离级别调整到REPEATABLE_READ



### 幻读

事务T1读取一条指定的Where子句所返回的结果集，然后T2事务新插入一行记录，这行记录恰好可以满足T1所使用的查询条件。然后T1再次对表进行检索，但又看到了T2插入的数据。 **（和可重复读类似，但是事务T2的数据操作仅仅是插入和删除，不是修改数据，读取的记录数量前后不一致）** 



幻读的重点在于新增或者删除 (数据条数变化)

同样的条件, 第1次和第2次读出来的记录数不一样

**例子：**

目前工资为1000的员工有10人。 
（1）事务1，读取所有工资为1000的员工（共读取10条记录 ）

```sql
con1 = getConnection();  
Select * from employee where salary =1000;  
```

（2）这时另一个事务向employee表插入了一条员工记录，工资也为1000  

```sql
con2 = getConnection();  
Insert into employee(empId,salary) values("Lili",1000);  
con2.commit();  
```

事务1再次读取所有工资为1000的员工（共读取到了11条记录，这就像产生了幻读）

```sql
//con1  
select * from employee where salary =1000;  
```

**解决办法：**如果在操作事务完成数据处理之前，任何其他事务都不可以添加新数据，则可避免该问题。把数据库的事务隔离级别调整到SERIALIZABLE_READ  





## 5. 事务隔离级别 【阿里面经OneNote】

- **串行化(Serializable)**：所有事务一个接着一个的执行，这样可以避免幻读(phantom read),对于基于锁来实现并发控制的数据库来说，串行化要求在执行范围查询的时候，需要获取范围锁，如果不是基于锁实现并发控制的数据库，则检查到有违反串行操作的事务时，需回滚该事务。 
- **可重复读(Repeated Read)**：所有被Select获取的数据都不能被修改，这样就可以避免一个事务前后读取不一致的情况。但是没有办法控制幻读，因为这个时候其他事务不能更改所选的数据，但是可以增加数据，因为强恶意事务没有范围锁 
- **读已提交(Read Committed)**：被读取的数据可以被其他事务修改，这样可能导致不可重复读。也就是说，事务读取的时候获取读锁，但是在读完之后立即释放(不需要等事务结束)，而写锁则是事务提交之后才释放，释放读锁之后，就可能被其他事务修改数据。该等级也是SQL Server默认的隔离等级 
- **读未提交(Read Uncommitted)**：最低的隔离等级，允许其他事务看到没有提交的数据，会导致脏读
- 总结
  - 四个级别逐渐增强，每个级别解决一个问题，每个级别解决一个问题，事务级别遇到，性能越差，大多数环境(Read committed 就可以用了) 

| 隔离级别     | 脏读   | 不可重复读 | 幻读    |
| ------------ | ------ | ---------- | ------- |
| 串行化       | NO     | NO         | NO      |
| 可重复读     | NO     | NO         | YES     |
| **读已提交** | **NO** | **YES**    | **YES** |
| 读未提交     | YES    | YES        | YES     |



## 6. MySQL存储引擎选择

对于初学者来说我们通常不关注存储引擎，但是 MySQL 提供了多个存储引擎，包括处理事务安全表的引擎和处理非事务安全表的引擎。在 MySQL 中，不需要在整个服务器中使用同一种存储引擎，针对具体的要求，可以对每一个表使用不同的存储引擎。 

### 存储引擎简介

MySQL中的数据用各种不同的技术存储在文件(或者内存)中。这些技术中的每一种技术都使用不同的存储机制、索引技巧、锁定水平并且最终提供广泛的不同的功能和能力。通过选择不同的技术，你能够获得额外的速度或者功能，从而改善你的应用的整体功能。 存储引擎说白了就是如何存储数据、如何为存储的数据建立索引和如何更新、查询数据等技术的实现方法。

例如，如果你在研究大量的临时数据，你也许需要使用内存存储引擎。内存存储引擎能够在内存中存储所有的表格数据。又或者，你也许需要一个支持事务处理的数据库(以确保事务处理不成功时数据的回退能力)。



> 在MySQL中有很多存储引擎，每种存储引擎大相径庭，那么又改如何选择呢？


`MySQL 5.5`以前的默认存储引擎是`MyISAM`, `MySQL 5.5`之后的默认存储引擎是`InnoDB`

不同存储引起都有各自的特点，为适应不同的需求，需要选择不同的存储引擎，所以首先考虑这些存储引擎各自的功能和兼容。




### 1. MyISAM
MySQL 5.5版本之前的默认存储引擎，在`5.0`以前最大表存储空间最大`4G`，`5.0`以后最大`256TB`。


Myisam存储引擎由`.myd`（数据）和 `.myi`（索引文件）组成，`.frm`文件存储表结构（所以存储引擎都有）

**特性**

- 并发性和锁级别 （对于读写混合的操作不好，为表级锁，写入和读互斥）
- 表损坏修复
- myisam表支持的索引类型（全文索引）
- myisam支持表压缩（压缩后，此表为只读，不可以写入。使用myisampack压缩）

**应用场景**

- 没有事务
- 只读类应用（插入不频繁，查询非常频繁）
- 空间类应用（唯一支持空间函数的引擎）
- 做很多count 的计算




### 2. InnoDB
MySQL 5.5及之后版本的默认存储引擎

**特性**

- Innodb为事务性存储引擎
- 完全支持事物的ACID特性
- Redo log （实现事务的持久性） 和Undo log（为了实现事务的原子性，存储未完成事务log，用于回滚）
- Innodb支持行级锁
- 行级锁可以最大程度的支持并发
- 行级锁是由存储引擎层实现的

**应用场景**

- 可靠性要求比较高，或者要求事务
- 表更新和查询都相当的频繁，并且行锁定的机会比较大的情况。



#### 补充：独立表空间和系统表空间应该如何抉择呢？

**两者比较**

- 系统表空间：无法简单的收缩大小（这很恐怖，会导致ibdata1一直增大，即使删除了数据也不会变小）
- 独立表空间：可以通过optimize table 命令收缩系统文件
- 系统表空间：会产生I/O瓶颈（因为只有一个文件）
- 独立表空间：可以向多个文件刷新数据

**总结**  
强烈建议：对Innodb引擎使用独立表空间（mysql5.6版本以后默认是独立表空间）

**系统表转移为独立表的步骤（非常繁琐）**

- 使用mysqldump导出所有数据库表数据
- 停止mysql服务，修改参数，并且删除Innodb相关文件
- 重启mysql服务，重建mysql系统表空间
- 重新导入数据




### 3. CSV

**文件系统存储特点**

- 数据以文本方式存储在文件中
- `.csv`文件存储表内容
- `.csm`文件存储表的元数据，如表状态和数据量
- `.frm`存储表的结构



**CSV存储引擎特点**

- 以CSV格式进行数据存储
- 所有列必须都是不能为NULL
- 不支持索引
- 可以对数据文件直接编辑（其他引擎是二进制存储，不可编辑）



**引用场景**

- 作为数据交换的中间表

  

### 4. Archive

**特性**

- 以zlib对表数据进行压缩，磁盘I/O更少
- 数据存储在ARZ为后缀的文件中（表文件为`a.arz`，`a.frm`）
- 只支持insert 和 select 操作（不可以delete 和update，会提示没有这个功能）
- 只允许在自增ID列上加索引

**应用场景**

- 日志和数据采集类应用




### 5. Memory

特性

- 也称为HEAP存储引擎，所以数据保存在内存中（数据库重启后会导致数据丢失）

- 支持HASH索引（等值查找应选择HASH）和BTree索引（范围查找应选择）
- 所有字段都为固定长度，varchar(10) == char(10)
- 不支持BLOG和TEXT等大字段
- Memory存储使用表级锁（性能可能不如innodb） 
- 最大大小由`max_heap_table_size`参数决定
- Memory存储引擎默认表大小只有`16M`，可以通过调整`max_heap_table_size`参数

应用场景

- 用于查找或是映射表，例如右边和地区的对应表
- 用于保存数据分析中产生的中间表
- 用于缓存周期性聚合数据的结果表


**注意：** Memory数据易丢失，所以要求数据可再生




### 6. Federated
**特性**

- 提供了访问远程mysql服务器上表的方法
- 本地不存储数据，数据全部放在远程服务器上

**使用 Federated**

默认是禁止的。如果需要启用，需要在启动时增加Federated参数







### ★思考题

#### 1. 如何选择存储引擎？

**参考条件：**  

- 是否需要事务
- 是否可以热备份
- 崩溃恢复
- 存储引擎的特有特性  


**重要一点：** 不要混合使用存储引擎   
**强烈推荐：** Innodb



#### 2. MyISAM和InnoDB引擎的区别？

**区别：**

- MyISAM不支持外键，而InnoDB支持
- MyISAM是非事务安全型的，而InnoDB是事务安全型的。
- MyISAM锁的粒度是表级，而InnoDB支持行级锁定。
- MyISAM支持全文类型索引，而InnoDB不支持全文索引。
- MyISAM相对简单，所以在效率上要优于InnoDB，小型应用可以考虑使用MyISAM。
- MyISAM表是保存成文件的形式，在跨平台的数据转移中使用MyISAM存储会省去不少的麻烦。
- InnoDB表比MyISAM表更安全，可以在保证数据不会丢失的情况下，切换非事务表到事务表（alter table tablename type=innodb）。

**应用场景：**

- MyISAM管理非事务表。它提供高速存储和检索，以及全文搜索能力。如果应用中需要执行大量的SELECT查询，那么MyISAM是更好的选择。

- InnoDB用于事务处理应用程序，具有众多特性，包括ACID事务支持。如果应用中需要执行大量的INSERT
  或UPDATE操作，则应该使用InnoDB，这样可以提高多用户并发操作的性能。

  


#### 3. 为什么不建议innodb使用亿级大表
[为什么不建议innodb使用亿级大表 | 峰云就她了](http://xiaorui.cc/2016/12/08/%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E5%BB%BA%E8%AE%AEinnodb%E4%BD%BF%E7%94%A8%E4%BA%BF%E7%BA%A7%E5%A4%A7%E8%A1%A8/)





## 7. MySQL数据类型

### 整型

TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT 分别使用 8, 16, 24, 32, 64 位存储空间，一般情况下越小的列越好。

INT(11) 中的数字只是规定了交互工具显示字符的个数，对于存储和计算来说是没有意义的。

### 浮点数

FLOAT 和 DOUBLE 为浮点类型，DECIMAL 为高精度小数类型。CPU 原生支持浮点运算，但是不支持 DECIMAl 类型的计算，因此 DECIMAL 的计算比浮点类型需要更高的代价。

FLOAT、DOUBLE 和 DECIMAL 都可以指定列宽，例如 DECIMAL(18, 9) 表示总共 18 位，取 9 位存储小数部分，剩下 9 位存储整数部分。

### 字符串

主要有 CHAR 和 VARCHAR 两种类型，一种是定长的，一种是变长的。

VARCHAR 这种变长类型能够节省空间，因为只需要存储必要的内容。但是在执行 UPDATE 时可能会使行变得比原来长，当超出一个页所能容纳的大小时，就要执行额外的操作。MyISAM 会将行拆成不同的片段存储，而 InnoDB 则需要分裂页来使行放进页内。

VARCHAR 会保留字符串末尾的空格，而 CHAR 会删除。

### 时间和日期

MySQL 提供了两种相似的日期时间类型：DATATIME 和 TIMESTAMP。

#### 1. DATATIME

能够保存从 1001 年到 9999 年的日期和时间，精度为秒，使用 8 字节的存储空间。

它与时区无关。

默认情况下，MySQL 以一种可排序的、无歧义的格式显示 DATATIME 值，例如“2008-01-16 22:37:08”，这是 ANSI 标准定义的日期和时间表示方法。

#### 2. TIMESTAMP

和 UNIX 时间戳相同，保存从 1970 年 1 月 1 日午夜（格林威治时间）以来的秒数，使用 4 个字节，只能表示从 1970 年 到 2038 年。

它和时区有关，也就是说一个时间戳在不同的时区所代表的具体时间是不同的。

MySQL 提供了 FROM_UNIXTIME() 函数把 UNIX 时间戳转换为日期，并提供了 UNIX_TIMESTAMP() 函数把日期转换为 UNIX 时间戳。

默认情况下，如果插入时没有指定 TIMESTAMP 列的值，会将这个值设置为当前时间。

应该尽量使用 TIMESTAMP，因为它比 DATETIME 空间效率更高。





## 8. 索引

### （1）索引使用的场景

索引能够轻易将查询性能提升几个数量级。

（1）对于非常小的表、大部分情况下简单的全表扫描比建立索引更高效。（2）对于中到大型的表，索引就非常有效。（3）但是对于特大型的表，建立和维护索引的代价将会随之增长。这种情况下，需要用到一种技术可以直接区分出需要查询的一组数据，而不是一条记录一条记录地匹配，例如可以使用分区技术。

索引是在存储引擎层实现的，而不是在服务器层实现的，所以不同存储引擎具有不同的索引类型和实现。



### （2）B Tree 原理

#### 1. B-Tree

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/06976908-98ab-46e9-a632-f0c2760ec46c.png)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/06976908-98ab-46e9-a632-f0c2760ec46c.png)

 

定义一条数据记录为一个二元组 [key, data]，B-Tree 是满足下列条件的数据结构：

- 所有叶节点具有相同的深度，也就是说 B-Tree 是平衡的；
- 一个节点中的 key 从左到右非递减排列；
- 如果某个指针的左右相邻 key 分别是 keyi 和 keyi+1，且不为 null，则该指针指向节点的（所有 key ≥ keyi） 且（key ≤ keyi+1）。

查找算法：首先在根节点进行二分查找，如果找到则返回对应节点的 data，否则在相应区间的指针指向的节点递归进行查找。

由于插入删除新的数据记录会破坏 B-Tree 的性质，因此在插入删除时，需要对树进行一个分裂、合并、旋转等操作以保持 B-Tree 性质。

#### 2. B+Tree

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/7299afd2-9114-44e6-9d5e-4025d0b2a541.png)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/7299afd2-9114-44e6-9d5e-4025d0b2a541.png)

 

与 B-Tree 相比，B+Tree 有以下不同点：

- 每个节点的指针上限为 2d 而不是 2d+1（d 为节点的出度）；
- 内节点不存储 data，只存储 key；
- 叶子节点不存储指针。

#### 3. 顺序访问指针

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/061c88c1-572f-424f-b580-9cbce903a3fe.png)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/061c88c1-572f-424f-b580-9cbce903a3fe.png)

 

一般在数据库系统或文件系统中使用的 B+Tree 结构都在经典 B+Tree 基础上进行了优化，在叶子节点增加了顺序访问指针，做这个优化的目的是为了提高区间访问的性能。



#### 4. 优势

红黑树等平衡树也可以用来实现索引，但是文件系统及数据库系统普遍采用 B Tree 作为索引结构，主要有以下两个原因：

**（一）更少的检索次数**

平衡树检索数据的时间复杂度等于树高 h，而树高大致为 O(h)=O(logdN)，其中 d 为每个节点的出度。

红黑树的出度为 2，而 B Tree 的出度一般都非常大。红黑树的树高 h 很明显比 B Tree 大非常多，因此检索的次数也就更多。

B+Tree 相比于 B-Tree 更适合外存索引，因为 B+Tree 内节点去掉了 data 域，因此可以拥有更大的出度，检索效率会更高。

**（二）利用计算机预读特性**

为了减少磁盘 I/O，磁盘往往不是严格按需读取，而是每次都会预读。这样做的理论依据是计算机科学中著名的局部性原理：当一个数据被用到时，其附近的数据也通常会马上被使用。预读过程中，磁盘进行顺序读取，顺序读取不需要进行磁盘寻道，并且只需要很短的旋转时间，因此速度会非常快。

操作系统一般将内存和磁盘分割成固态大小的块，每一块称为一页，内存与磁盘以页为单位交换数据。数据库系统将索引的一个节点的大小设置为页的大小，使得一次 I/O 就能完全载入一个节点，并且可以利用预读特性，相邻的节点也能够被预先载入。

更多内容请参考：[MySQL 索引背后的数据结构及算法原理](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)



### （3）索引分类

| 特性                        | InnoDB | MyISAM | MEMORY |
| --------------------------- | ------ | ------ | ------ |
| B树索引(B-tree indexes)     | √      | √      | √      |
| R树索引(R-tree indexes)     |        | √      |        |
| 哈希索引(Hash indexes)      | √      |        | √      |
| 全文索引(Full-text indexes) | √      | √      |        |

#### 1. B+Tree 索引

B+Tree 索引是大多数 MySQL 存储引擎的默认索引类型。

因为不再需要进行全表扫描，只需要对树进行搜索即可，因此查找速度快很多。除了用于查找，还可以用于排序和分组。

可以指定多个列作为索引列，多个索引列共同组成键。

B+Tree 索引适用于全键值、键值范围和键前缀查找，其中键前缀查找只适用于最左前缀查找。

如果不是按照索引列的顺序进行查找，则无法使用索引。

InnoDB 的 B+Tree 索引分为**主索引**和**辅助索引**。

主索引的叶子节点 data 域记录着完整的数据记录，这种索引方式被称为聚簇索引。因为无法把数据行存放在两个不同的地方，所以一个表只能有一个聚簇索引。

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/c28c6fbc-2bc1-47d9-9b2e-cf3d4034f877.jpg)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/c28c6fbc-2bc1-47d9-9b2e-cf3d4034f877.jpg)

 

辅助索引的叶子节点的 data 域记录着主键的值，因此在使用辅助索引进行查找时，需要先查找到主键值，然后再到主索引中进行查找。

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/7ab8ca28-2a41-4adf-9502-cc0a21e63b51.jpg)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/7ab8ca28-2a41-4adf-9502-cc0a21e63b51.jpg)

 

#### 2. 哈希索引

InnoDB 引擎有一个特殊的功能叫“自适应哈希索引”，当某个索引值被使用的非常频繁时，会在 B+Tree 索引之上再创建一个哈希索引，这样就让 B+Tree 索引具有哈希索引的一些优点，比如快速的哈希查找。

哈希索引能以 O(1) 时间进行查找，但是失去了有序性，它具有以下限制：

- 无法用于排序与分组；
- 只支持精确查找，无法用于部分查找和范围查找；

#### 3. 全文索引

MyISAM 存储引擎支持全文索引，用于查找文本中的关键词，而不是直接比较是否相等。查找条件使用 MATCH AGAINST，而不是普通的 WHERE。

全文索引一般使用倒排索引实现，它记录着关键词到其所在文档的映射。

InnoDB 存储引擎在 MySQL 5.6.4 版本中也开始支持全文索引。

#### 4. 空间数据索引（R-Tree）

MyISAM 存储引擎支持空间数据索引，可以用于地理数据存储。空间数据索引会从所有维度来索引数据，可以有效地使用任意维度来进行组合查询。

必须使用 GIS 相关的函数来维护数据。



### （4）索引的特点 

- 可以加快数据库的检索速度 
- 降低数据库插入、修改、删除等维护的速度 
- 只能创建在表上，不能创建到视图上 
- 既可以直接创建又可以间接创建 
- 可以在优化隐藏中使用索引 
- 使用查询处理器执行SQL语句，在一个表上，一次只能使用一个索引 



### （5）索引的优点 

- 创建唯一性索引，保证数据库表中每一行数据的唯一性 
- 大大加快数据的检索速度，这是创建索引的最主要的原因 
- 加速数据库表之间的连接，特别是在实现数据的参考完整性方面特别有意义 
- 在使用分组和排序子句进行数据检索时，同样可以显著减少查询中分组和排序的时间 
- 通过使用索引，可以在查询中使用优化隐藏器，提高系统的性能 



### （6）索引的缺点 

- 创建索引和维护索引要耗费时间，这种时间随着数据量的增加而增加 
- 索引需要占用物理空间，除了数据表占用数据空间之外，每一个索引还要占一定的物理空间，如果建立聚簇索引，那么需要的空间就会更大 
- 当对表中的数据进行增加、删除和修改的时候，索引也需要维护，降低数据维护的速度 



### （7）索引失效 

- 如果条件中有or，即使其中有条件带索引也不会使用(这就是问什么尽量少使用or的原因) 
- 对于多列索引，不是使用的第一部分，则不会使用索引 
- like查询是以%开头 
- 如果列类型是字符串，那一定要在条件中使用引号引起来，否则不会使用索引 
- 如果MySQL估计使用全表扫秒比使用索引快，则不适用索引。 



### （8）在什么情况下适合建立索引？

- 为经常出现在关键字order by、group by、distinct后面的字段，建立索引。 
- 在union等集合操作的结果集字段上，建立索引。其建立索引的目的同上。 
- 为经常用作查询选择的字段，建立索引。 
- 在经常用作表连接的属性上，建立索引。 
- 考虑使用索引覆盖。对数据很少被更新的表，如果用户经常只查询其中的几个字段，可以考虑在这几个字段上建立索引，从而将表的扫描改变为索引的扫描。 





## 9. 数据库中的分页查询语句怎么写？【阿里面经OneNote】

- Mysql的limit用法 
  - SELECT * FROM table LIMIT [offset,] rows | rows OFFSET offset 
  - LIMIT 接受一个或两个数字参数。参数必须是一个整数常量。如果给定两个参数，第一个参数指定第一个返回记录行的偏移量，第二个参数指定返回记录行的最大数目。初始记录行的偏移量是 0(而不是 1) 
- 最基本的分页方式：SELECT ... FROM ... WHERE ... ORDER BY ... LIMIT ...  



## 10. 常用的数据库有哪些？Redis用过吗？【阿里面经OneNote】

- 常用的数据库有哪些？Redis用过吗？ 
  - 常用的数据库 
    - MySQL
    - SQLServer 
  - Redis
    - Redis是一个速度非常快的非关系型数据库，他可以存储键(key)与5种不同类型的值（value）之间的映射，可以将存储在内存中的键值对数据持久化到硬盘中。 
    - 与Memcached相比 
      - 两者都可用于存储键值映射，彼此性能也相差无几 
      - Redis能够自动以两种不同的方式将数据写入硬盘 
      - Redis除了能存储普通的字符串键之外，还可以存储其他4种数据结构，memcached只能存储字符串键 
      - Redis既能用作主数据库，由可以作为其他存储系统的辅助数据库 
  - Redis应用场景
    - 缓存、任务队列、应用排行榜、网站访问统计、数据过期处理、分布式集群架构中的session分离
  - Redis特点
    - （1）高并发读写；（2）海量数据的高效存储和访问；（3）高可扩展性和高可用性



## 11. Redis的存储结构，或者说如何工作的，与mysql的区别？有哪些数据类型？ 【阿里面经OneNote】

- Redis的数据结构 
  - STRING：可以是字符串、整数或者浮点数 
  - LIST：一个链表，链表上的每个节点都包含了一个字符串 
  - SET：包含字符串的无序收集器（unordered collection），并且被包含的每个字符串都是独一无二、各不相同的 
  - HAST：包含键值对的无序散列表 
  - ZSET：字符串成员（member）与浮点数分值（score）之间的有序映射，元素的排列顺序由分值的大小决定 



## 12. 分库分表

简单来说，数据的切分就是通过某种特定的条件，将我们存放在同一个数据库中的数据分散存放到多个数据库（主机）中，以达到分散单台设备负载的效果，即分库分表。

数据的切分根据其切分规则的类型，可以分为如下两种切分模式。

- 垂直（纵向）切分：把单一的表拆分成多个表，并分散到不同的数据库（主机）上。
- 水平（横向）切分：根据表中数据的逻辑关系，将同一个表中的数据按照某种条件拆分到多台数据库（主机）上。

### 1. 垂直切分

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/e130e5b8-b19a-4f1e-b860-223040525cf6.jpg)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/e130e5b8-b19a-4f1e-b860-223040525cf6.jpg)

 

垂直切分是将一张表按列切分成多个表，通常是按照列的关系密集程度进行切分，也可以利用垂直切分将经常被使用的列和不经常被使用的列切分到不同的表中。

在数据库的层面使用垂直切分将按数据库中表的密集程度部署到不同的库中，例如将原来的电商数据库垂直切分成商品数据库 payDB、用户数据库 userBD 等。



#### （1）垂直切分的优点如下：

- 拆分后业务清晰，拆分规则明确

- 系统之间进行整合或扩展很容易

- 按照成本、应用的等级、应用的类型等将表放到不同的机器上，便于管理

- 便于实现**动静分离**、**冷热分离**的数据库表的设计模式

- 数据维护简单

  

#### （2）垂直切分的缺点如下：

- 部分业务表无法关联（Join），只能通过接口方式解决，提高了系统的复杂度
- 受每种业务的不同限制，存在单库性能瓶颈，不易进行数据扩展和提升性能
- 事务处理复杂



### 2. 水平切分

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/63c2909f-0c5f-496f-9fe5-ee9176b31aba.jpg)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/63c2909f-0c5f-496f-9fe5-ee9176b31aba.jpg)

 

水平切分又称为 Sharding，它是将同一个表中的记录拆分到多个结构相同的表中。

当一个表的数据不断增多时，Sharding 是必然的选择，它可以将数据分布到集群的不同节点上，从而缓存单个数据库的压力。



#### （1）水平切分的优点如下：

- 单库单表的数据保持在一定的量级，有助于性能的提高
- 切分的表的结构相同，应用层改造较少，只需要增加路由规则即可
- 提高了系统的稳定性和负载能力



#### （2）水平切分的缺点如下：

- 切分后，数据是分散的，很难利用数据库的Join操作，跨库Join性能较差
- 拆分规则难以抽象
- 分片事务的一致性难以解决
- 数据扩容的难度和维护量极大



#### （3）综上所述，垂直切分和水平切分的共同点如下：

- 存在分布式事务的问题
- 存在跨节点Join的问题
- 存在跨节点合并排序、分页的问题
- 存在多数据源管理的问题



### Sharding 策略

- 哈希取模：hash(key) % NUM_DB

  - 比如按照 userId mod 64.将数据分布在64个服务器上

- 范围：可以是 ID 范围也可以是时间范围

  - 比如每台服务器计划存放一个亿的数据,先将数据写入服务器A.一旦服务器A写满,则将数据写入服务器B,以此类推. 这种方式的好处是扩展方便.数据在各个服务器上分布均匀.  

- 映射表：使用单独的一个数据库来存储映射关系

  

### Sharding 存在的问题及解决方案

#### 1. 事务问题

使用分布式事务来解决，比如 XA 接口。

#### 2. JOIN

可以将原来的 JOIN 查询分解成多个单表查询，然后在用户程序中进行 JOIN。

#### 3. ID 唯一性

- 使用全局唯一 ID：GUID。
- 为每个分片指定一个 ID 范围。
- 分布式 ID 生成器 (如 Twitter 的 Snowflake 算法)。



## 13. 主从复制与读写分离

### 主从复制

主要涉及三个线程：binlog 线程、I/O 线程和 SQL 线程。

- **binlog 线程** ：负责将主服务器上的数据更改写入二进制文件（binlog）中。
- **I/O 线程** ：负责从主服务器上读取二进制日志文件，并写入从服务器的中继日志中。
- **SQL 线程** ：负责读取中继日志并重放其中的 SQL 语句。

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/master-slave.png)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/master-slave.png)

 

### 读写分离

主服务器用来处理写操作以及实时性要求比较高的读操作，而从服务器用来处理读操作。

读写分离常用代理方式来实现，代理服务器接收应用层传来的读写请求，然后决定转发到哪个服务器。

MySQL 读写分离能提高性能的原因在于：

- 主从服务器负责各自的读和写，极大程度缓解了锁的争用；
- 从服务器可以配置 MyISAM 引擎，提升查询性能以及节约系统开销；
- 增加冗余，提高可用性。

[![img](https://github.com/CyC2018/Interview-Notebook/raw/master/pics/master-slave-proxy.png)](https://github.com/CyC2018/Interview-Notebook/blob/master/pics/master-slave-proxy.png)



## 14. 查询性能优化

### （1）使用 Explain 进行分析

Explain 用来分析 SELECT 查询语句，开发人员可以通过分析 Explain 结果来优化查询语句。

比较重要的字段有：

- **select_type** : 查询类型，有简单查询、联合查询、子查询等
- **key** : 使用的索引
- **rows** : 扫描的行数

```sql
mysql> explain select * from user_info where id = 2\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: user_info
   partitions: NULL
         type: const
possible_keys: PRIMARY
          key: PRIMARY
      key_len: 8
          ref: const
         rows: 1
     filtered: 100.00
        Extra: NULL
1 row in set, 1 warning (0.00 sec)
```

更多内容请参考：[MySQL 性能优化神器 Explain 使用分析](https://segmentfault.com/a/1190000008131735)



### （2）优化数据访问

#### 1. 减少请求的数据量

（一）只返回必要的列

最好不要使用 SELECT * 语句。

（二）只返回必要的行

使用 WHERE 语句进行查询过滤，有时候也需要使用 LIMIT 语句来限制返回的数据。

（三）缓存重复查询的数据

使用缓存可以避免在数据库中进行查询，特别要查询的数据经常被重复查询，缓存可以带来的查询性能提升将会是非常明显的。

#### 2. 减少服务器端扫描的行数

最有效的方式是使用索引来覆盖查询。



### （3）重构查询方式

#### 1. 切分大查询

一个大查询如果一次性执行的话，可能一次锁住很多数据、占满整个事务日志、耗尽系统资源、阻塞很多小的但重要的查询。

```sql
DELEFT FROM messages WHERE create < DATE_SUB(NOW(), INTERVAL 3 MONTH);
```

```sql
rows_affected = 0
do {
    rows_affected = do_query(
    "DELETE FROM messages WHERE create  < DATE_SUB(NOW(), INTERVAL 3 MONTH) LIMIT 10000")
} while rows_affected > 0
```



#### 2. 分解大连接查询

将一个大连接查询（JOIN）分解成对每一个表进行一次单表查询，然后将结果在应用程序中进行关联，这样做的好处有：

- 让缓存更高效。对于连接查询，如果其中一个表发生变化，那么整个查询缓存就无法使用。而分解后的多个查询，即使其中一个表发生变化，对其它表的查询缓存依然可以使用。
- 分解成多个单表查询，这些单表查询的缓存结果更可能被其它查询使用到，从而减少冗余记录的查询。
- 减少锁竞争；
- 在应用层进行连接，可以更容易对数据库进行拆分，从而更容易做到高性能和可扩展。
- 查询本身效率也可能会有所提升。例如下面的例子中，使用 IN() 代替连接查询，可以让 MySQL 按照 ID 顺序进行查询，这可能比随机的连接要更高效。

```sql
SELECT * FROM tab
JOIN tag_post ON tag_post.tag_id=tag.id
JOIN post ON tag_post.post_id=post.id
WHERE tag.tag='mysql';
SELECT * FROM tag WHERE tag='mysql';
SELECT * FROM tag_post WHERE tag_id=1234;
SELECT * FROM post WHERE post.id IN (123,456,567,9098,8904);
```















# 实践问题

## 1. 如何解决秒杀的性能问题和超卖的讨论

抢订单环节一般会带来2个问题：

　　1、高并发

　　比较火热的秒杀在线人数都是10w起的，如此之高的在线人数对于网站架构从前到后都是一种考验。

　　2、超卖

　　任何商品都会有数量上限，如何避免成功下订单买到商品的人数不超过商品数量的上限，这是每个抢购活动都要面临的难题。





#### 解决方案1：

　　将存库从MySQL前移到Redis中，所有的写操作放到内存中，由于Redis中不存在锁故不会出现互相等待，并且由于Redis的写性能和读性能都远高于MySQL，这就解决了高并发下的性能问题。然后通过队列等异步手段，将变化的数据异步写入到DB中。

　　优点：解决性能问题

　　缺点：没有解决超卖问题，同时由于异步写入DB，存在某一时刻DB和Redis中数据不一致的风险。



#### 解决方案2：

　　**引入队列，然后将所有写DB操作在单队列中排队，完全串行处理。当达到库存阀值的时候就不在消费队列，并关闭购买功能。这就解决了超卖问题。**

　　优点：解决超卖问题，略微提升性能。

　　缺点：性能受限于队列处理机处理性能和DB的写入性能中最短的那个，另外多商品同时抢购的时候需要准备多条队列。



#### 解决方案3：

　　**将提交操作变成两段式，先申请后确认。然后利用Redis的原子自增操作（相比较MySQL的自增来说没有空洞），同时利用Redis的事务特性来发号，保证拿到小于等于库存阀值的号的人都可以成功提交订单。**然后数据异步更新到DB中。

　　优点：解决超卖问题，库存读写都在内存中，故同时解决性能问题。

　　缺点：由于异步写入DB，可能存在数据不一致。另可能存在少买，也就是如果拿到号的人不真正下订单，可能库存减为0，但是订单数并没有达到库存阀值。



https://mp.weixin.qq.com/s/waGRvyhab2z8b-BIw9bJeA

[如何解决秒杀的性能问题和超卖的讨论 - CSDN博客](https://blog.csdn.net/zhoudaxia/article/details/38067003)



## 2. 数据库主从不一致，怎么解？

数据库主库和从库不一致，常见有这么几种优化方案：

（1）业务可以接受，系统不优化

（2）强制读主，高可用主库，用缓存提高读性能

（3）在cache里记录哪些记录发生过写请求，来路由读主还是读从



**详细请参考：**

- https://mp.weixin.qq.com/s/5JYtta9aMGcic7o_ejna-A





# 附录：参考资料

- [视频：MySQL 事务的隔离级别与锁-极客学院](http://www.jikexueyuan.com/course/1524.html)
- [mysql-tutorial/3.5.md at master · jaywcjlove/mysql-tutorial](https://github.com/jaywcjlove/mysql-tutorial/blob/master/chapter3/3.5.md)
- [大神带你剖析Mysql索引底层数据结构_哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/video/av17252271?from=search&seid=3701018912873961528)
- [大众点评订单系统分库分表实践](https://tech.meituan.com/dianping_order_db_sharding.html)
- [库存扣减还有这么多方案？ | 架构师之路](https://mp.weixin.qq.com/s/Lfy7ek-vArVBTaUYfl64Bg)
- [关于分库分表，这有一套大而全的轻量级架构设计思路（蚂蚁金服技术专家）](https://www.toutiao.com/a6545626478447428103/?tt_from=weixin&article_category=stock&timestamp=1524029012&app=news_article&iid=26214166927&wxshare_count=1)
- [Java大型互联网架构-快速搞定大型互联网网站分库分表方案_哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/video/av20966672?from=search&seid=6900253656657206494)
- [MySQL分库分表_ITPUB博客](http://blog.itpub.net/29254281/viewspace-1819422/)