# MySQL

1、sql、DB、DBMS分别是什么，他们之间的关系？
DB：
DataBase（数据库，数据库实际上在硬盘上以文件的形式存在）

```
DBMS：
	DataBase Management System（数据库管理系统，常见的有：MySQL Oracle DB2 Sybase SqlServer……）

SQL：
	结构化查询语言，是一门标准通用的语言。标准的sql适合于所有的数据库产品。
SQL属于高级语言。
SQL语句在执行的时候，实际上内部也会先进行编译，然后再执行sql。（SQL语句的编译由DBMS完成。）

DBMS负责执行sql语句，通过执行sql语句来操作DB当中的数据。
DBMS -(执行)-> SQL--(操作)-> DB
```

2、每一个字段包括哪些属性？
字段名、数据类型、相关约束

3、学习MySQL主要还是学习通用的SQL语句，SQL语句包括增删改查
SQL语句分类：
DQL（数据查询语言）：查询语句，凡是select语句都是DQL。
DML（数据操作语言）：insert delete update，对表当中的数据进行增删改。
DDL（数据定义语言）：creat drop alter，对表的结构进行增删改。
TCL（事务控制语言）：commit提交事务，rollback回滚事务。（TCL中的T是Transaction）
DCL（数据控制语言）：grant授权、revoke撤销权限等。

4、导入数据
第一步：登录mysql数据库管理系统
dos命令窗口：
mysql -uroot -p密码;

```
 第二步：查看有哪些数据库
 	show databases;（这个不是SQL语句，属于MySQL的命令）

 第三步：创建属于我们自己的数据库
 	create database tzwtable;（这个不是SQL语句，属于MySQL的命令）

 第四步：使用tzwtable数据
 	use tzwtable;（这个不是SQL语句，属于MySQL的命令）

 第五步：查看当前使用的数据库中有哪些表？
 	show tables;（这个不是SQL语句，属于MySQL的命令）

 第六步：初始化数据
 	mysql>文件路径.sql
```

5、tzwtable.sql，这个文件以sql结尾，这样的文件被称为"sql脚本"。什么是sql脚本呢？
当一个文件的扩展名是.sql，并且该文件中编写了大量的sql语句，我们称这样的文件为sql脚本。

注意：直接使用source命令可以执行sql脚本。
sql脚本中的数据量太大的时候，无法打开，请使用source命令完成初始化。

6、删除数据库：drop database 数据库名;

7、简单的查询语句（SQL）

语法格式：
select 字段名1,字段名2,字段名3 from 表名;

```
注意：
1、任何一条sql语句都以 ";" 结尾。
2、sql语句不区分大小写。
3、标准sql语句中要求字符串使用单引号括起来。
4、as关键字可以省略。
```

8、条件查询格式：
select 字段1,字段2 from 表名 where 条件 order by ...;
执行顺序：先from，然后where，再select，最后order by。

```
注意：
   between ... and ..是闭区间。（必须左小右大）
   between ... and ...也可以用在字符串方面，此时变为左闭右开。
   在数据库中，null不是一个值，代表什么也没有，是一个空。（不是空值）
   空必须使用is null 或者 is not null。
   在使用not in()时，小括号里面要排除NULL。
```

9、模糊查询like
在模糊查询中，必须掌握两个特殊的符号，一个是%，一个是_
%代表任意多个字符，_代表任意1个字符。
\是转义字符，比如说要找出一个名字中带有_的人：where name like '%_%';

10、排序
order by；（默认升序）
（asc表示升序，desc表示降序）

```
注意：多个字段排序，如果前面字段相等时，后面的排序字段才会启用。
	  eg：order by score desc,name asc;
      按照成绩降序排，当成绩相同时，按照名字升序排。
```

11、分组函数（多行处理函数）
count 计数
sum 求和
avg 平均值
max 最大值
min 最小值

```
注意： 分组函数自动忽略NULL。
      所有的分组函数都是对"某一组"数据进行操作的。
      如果参与运算的字段有null，那么结果一定是null。
      where后面不能直接用分组函数。（得用having）
```

11.1、count(*)和count(具体的某个字段)，他们有什么区别？
count(*)：不是统计某个字段中的数据，而是统计总记录条数。（和某个字段无关）
count(具体的某个字段)：表示统计字段中不为NULL的数据总数量。

11.2、分组函数也能组合起来用。

12、ifnull() 空处理函数
ifnull(可能为NULL的数据，被当作什么处理)：属于单行处理函数。

13、group by 和 having

```
group by：按照某个字段或者某些字段进行分组。
having：having是对分组之后的数据进行再次过滤。（只能出现在group by后面）

注意：分组函数一般都会和group by联合使用，并且任何一个分组函数(count avg sum max min)都是在group by语句执行结束后才会执行的。
      当一条sql语句内有group by的话，整张表的数据会自成一组。
      当一条语句中有group by的话，select后面只能跟分组函数和参与分组的字段。
```

14、 select   5
...
from     1
...
where    2
...
group by 3
...
having   4
...
order by 6
...

15、查询去重复
select distinct job from table;  对工作岗位去重复。
注意：distinct只能出现在所有字段的最前面。

16、连接查询

16.1、什么是连接查询？
在实际开发中，大部分的情况下都不是从单表中查询数据，一般都是多张表联合查询取出最终的结果。
在实际开发中，一般一个业务都会对应多张表。

16.2、分类

```
内连接：
    等值连接
    非等值连接
    自连接   
 
 外连接：
    左外连接（左连接）
    右外连接（右连接）
```

16.3、避免笛卡尔积现象，会减少记录的匹配次数吗？
不会，次数还是一样的，只是显示的是有效记录。

16.4、内等值连接格式
select
s.name,a.address
from
student s
//inner可以省略
inner join
address a
on
s.name = a.name;(连接条件)
where
...

16.5、内非等值连接
select
s.name,a.address
from
student s
//inner可以省略
inner join
address a
on
s.age between s.age and a.age;(连接条件)
where
...

16.6、自连接
格式一样，主要是找到两张表的共同字段，然后连接起来(某一个表的字段包含另一个表的某个字段)

16.7、外连接
什么是外连接?和内连接有什么区别？

```
内连接：
   假设A表和B表进行连接，使用内连接的话，凡是A表和B表能够匹配上的记录查询出来，这就是内连接。
   AB两张表没有主副之分，两张表是平等的。（不能匹配上的记录会被忽略）

外连接：
   假设A和B表进行连接，使用外连接的话，AB两张表中有一张表是主表，一张表是副表，主要查询主表中的数据，捎带查询副表中的数据，当副表中的数据没有和主表中相匹配的数据，副表自动模拟处NULL与之匹配。
```

17、子查询
select语句当中嵌套select语句，被嵌套的select语句都是子查询。

```
可以出现在：
	select
	   ...(select).
	from
	   ...(select).
	where
	   ...(select).
```

18、union（可以将查询结果集相加）
注意：必须要保证列数一致，列数不一致会报错。
eg：
select name from student
union
select book from books;
(可以将没有联系的两张表的结果结合在一起显示)

19、limit

19.1、取结果中的部分数据

19.2、语法机制：
limit startIndex,length
startIndex 表示起始位置（下标从0开始）
length 表示取几个

19.3、limit是sql语句最后执行的一个环节。

19.4、limit每页显示多少条记录公式：
limit (pageNo - 1) * pageSize,pageSize;
pageNo是页码，pageSize是每页显示多少条。

20、关于MySQL当中字段的常用数据类型
int        整数型
bigint     长整型
float      浮点型
char       定长字符串
varchar    可变长字符串
date       日期类型
BLOB       二进制大对象（存储图片、视频等流媒体信息）
CLOB       字符大对象（存储较大文本）

```
（1，ASCII码：一个英文字母（不分大小写）占一个字节的空间，一个中文汉字占两个字节的空间。

  2，UTF-8编码：一个英文字符等于一个字节，一个中文（含繁体）等于三个字节。中文标点占三个字节，英文标点占一个字节。

  3，Unicode编码：一个英文等于两个字节，一个中文（含繁体）等于两个字节。中文标点占两个字节，英文标点占两个字节。）
```

21、外键约束

顺序要求：
删除数据的时候，先删除子表，再删除父表。
添加数据的时候，先添加父表，再添加子表。
创建表的时候，先创建父表，再创建子表。
删除表的时候，先删除子表，再删除父表。

添加外键约束公式：
foreign key(添加外键的字段) references 被引用表名(被引用字段);

注意：外键字段引用其它表的某个字段的时候，被引用的字段不一定是主键，但至少具有unique约束。
（被引用字段要具有唯一性）

22、事务（要想保证多条DML语句同时成功或同时失败，就需要用"事务机制"）

```
22.1、和事务相关的语句只有：DML语句。（insert delete update）
      因为这三条语句都是和数据库表当中的"数据"相关的。
  
22.2、事务的存在是为了保证数据的完整性，安全性。

22.3、如果一条SQL语句就能完成的事，不需要用到事务。

22.4、事务的特性
	事务的提醒包括四大特性：ACID
A：原子性：事务是最小的工作单元，不可再分。
C：一致性：事务必须保证多条DML语句同时成功或同时失败。
I：隔离性：事务A与事务B之间具有隔离。
D：持久性：最终数据必须持久化到硬盘中，事务才算成功的结束。

22.5、关于事务之间的隔离性
	事务隔离性存在隔离级别，理论上隔离级别分为4个：
    第一级别：读未提交（read uncommitted）
    	对方事务还没有提交，我们当前事务可以读取到对方未提交的数据。
	读未提交存在脏读（Dirty Read）现象：表示读到了脏的数据。
        第二级别：读已提交（read committed）
    	对方事务提交后的数据我方可以读取到。
	这种隔离级别解决了：脏读。
	读已提交存在的问题是：不可重复读。
    第三种级别：可重复度（repeatable read）
    	这种隔离级别解决了：不可重复度问题。
	这种隔离级别存在的问题是：读取到的数据是幻想。
	   （即别人已经修改了数据，而自己这边显示的还是自己未提交的数据）
    第四种级别：序列化/串行化读：
    	解决了所有问题。
	但是效率低，需要排队。

    oracle数据库默认的隔离级别是：读已提交。
    mysql数据库默认的隔离级别是：可重复度。

22.6、设置事务的全局隔离级别：
			set global transaction isolation level 事务级别;
  查看事务的全局隔离级别：
  		select @@global.tx isolation;
```

23、索引

23.1、什么是索引？有什么用？
索引就相当于一本书的目录，通过目录可以快速的找到对应的资源。
在数据库方面，查询一张表的时候有两种检索方式：
第一种：全表扫描
第二种：根据索引检索（效率很高）

```
 索引为什么可以提高检索效率呢？
   其实最根本的原理是缩小了扫描范围。

 索引虽然可以提高检索效率，但是不能随意的添加索引，因为索引也是数据库当中
 的对象，也需要数据库不断的维护。是有维护成本的。
 比如：表中的数据经常被修改，这样就不适合添加索引，因为数据一旦修改，索引需要
 重新排序，进行维护。
```

23.2、创建索引对象：
create index 索引名称 on 字段名;
删除索引对象：
drop index 索引名称 on 表名;

23.3、什么时候考虑给字段添加索引？（满足什么条件）
（1）数据量庞大。（根据客户的需求，根据线上环境）
（2）该字段很少DML操作。（因为字段进行修改操作，索引也需要维护）
（3）该字段经常出现在where子句中。（经常根据哪个字段查询）

23.4、注意：主键和具有unique约束的字段会自动添加索引。
根据主键查询效率较高。尽量根据主键检索。

23.5、查看sql语句的执行计划：
explain select ** from ** where **;

23.6、索引底层采用的数据结构是：B + Tree

23.7、索引的实现原理
通过B Tree缩小扫描范围，底层索引进行了排序，分区，索引会携带数据在表中的"物理地址"，
最终通过索引检索到数据之后，获取到关联的物理地址，通过物理地址定位表中的数据，效率
是最高的。
select name from student where name = 'zhangsan';
通过索引转换为：
select name from student where 物理地址 = 0x123;

23.8、索引的分类
单一索引：给单个字段添加索引
复合索引：给多个字段联合起来添加1个索引
主键索引：主键上会自动添加索引
唯一索引：有unique约束的字段上会自动添加索引。
.....

23.9、索引什么时候失效？
select name from student where name like '%z%';
模糊查询的时候，第一个通配符使用的是%，这个时候索引是失效的。

30、数据库设计三范式

```
1、什么是设计范式？
    设计表的依据。按照这个三范式设计的表不会出现数据冗余。

2、三范式都是哪些？
    
    第一范式：任何一张表都应该有主键，并且每一个字段原子性不可再分。

    第二范式：建立在第一范式的基础上，所有非主键字段完全依赖主键，不能产生部份依赖。
		（多对多，三张表，关系表，两外键）
    
    第三范式：建立在第二范式的基础上，所有非主键字段直接依赖主键，不能产生传递依赖。
    		（一对多，三张表，关系表，加外键）

    提醒：在实际开发中，以满足客户的需求为主，有的时候会拿冗余换取执行速度。

3、一对一怎么设计？
	
	主键共享（主键外键为同一个字段）

	外键唯一（外键加上unique）
```

31、在mysql当中怎么计算两个日期的"年差"，差了多少年？
TimeStampDiff(间隔类型，前一个日期，后一个日期)

```
timestampdiff(YEAR,date,now());

间隔类型有：
	FRAC_SECOND 表示间隔是毫秒，
	SECOND 秒，
	MINUTE 分钟，
	HOUR 小时，
	DAY 天，
	WEEK 星期
	MONTH 月，
	QUARTER 季度，
	YEAR 年；
```

32、在select后面加for update语句，表示行级锁，不能修改这一行的数据
（通常在where条件后面加）又被称为悲观锁。

```
添加主键约束：

alter table 表名 add constraint 主键 （形如：PK_表名） primary key 表名(主键字段);

添加外键约束：

alter table 从表 add constraint 外键（形如：FK_从表_主表） foreign key 从表(外键字段) references 主表(主键字段);

删除主键约束：

alter table 表名 drop primary key;

删除外键约束：

alter table 表名 drop foreign key 外键（区分大小写）;

添加列：

alter table 表名 add column 列名 varchar(30);

删除列：

alter table 表名 drop column 列名;

修改列名：

alter table 表名 change oldcolname newcolname int;

修改列属性：

alter table 表名 modify 列名 varchar(22);
```
