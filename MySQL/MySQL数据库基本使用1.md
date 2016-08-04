# MySQL的创建相关知识

# 登录到MySQL

`mysql -h hostname -P hostport -u username -p`

- -h 指定希望连接的主机，可以用来连接远程主机上的MySQL，如果忽略默认登录本机数据库
- -P 指定所连接主机开放的MySQL端口，如果忽略此项默认使用3306端口登录
- -u 指定连接数据库时使用的用户名称，如果忽略此项默认使用你的本机用户名
- -p 告诉服务器会使用密码来连接数据库，如果忽略此项使用无密码登录


使用密码登入时，会出现以下响应

```
Enter password:
```

输入密码后成功登录会得到以下响应

```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 4
Server version: 5.7.12 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

# 创建数据库

每个程序都需要数据库，可以在MySQL命令提示符下输入：    
```
mysql> create database dbname;
```
创建成功后，可以得到以下响应:   

```
Query OK, 1 row affected (0.00 sec)
```

# 设置用户和权限
一个MySQL可能有许多用户，而且不同的用户有不同的权限。

最少权限原则：一个用户（或者一个进程）应该拥有能够执行分配给他的任务的最低级别的权限

`GRANT`和`REVOKE`分别用来授予和取消MySQL用户的权限   

权限分为四个级别：
- 全局
- 数据库
- 表
- 列

## 权限的类型和级别
MySQL权限有3个基本类型：
- 适用于一般用户的权限
- 适用于赋予管理员的权限
- 几个特定的权限

**用户的权限**
从系统的安全性方面考虑，适于常规用户的权限大多数是相对无害的。
| 权限   | 应用于     | 描述                       |
|:-------|:-----------|:---------------------------|
| SELECT | 表，列     | 允许用户从表中选择行       |
| INSERT | 表，列     | 允许用户在表中插入行       |
| DELETE | 表，列     | 允许用户修改现存表中的行   |
| INDEX  | 表         | 允许用户删除现存表的行     |
| ALTER  | 表         | 允许用户修改现存表的结构   |
| CREATE | 数据库，表 | 允许用户创建新的数据库或表 |
| DROP   | 数据库，表 | 允许用户删除数据库或表     |

**管理员权限**
这些权限都可以授予非管理员用户，但是必须非常小心

FILE权限有些不同，对普通用户非常有用，可以将数据从文件载入数据库，否则必须把数据输入数据库，非常浪费时间。
但是必须注意，可能会载入其他用户数据库和潜在的密码文件，授予权限时必须非常小心，或者管理员载入数据

| 权限                    | 应用于                                   |
|:------------------------|:-----------------------------------------|
| CREATE TEMPORARY TABLES | 允许管理员创建临时表                     |
| FILE                    | 允许数据从文件读入表，或从表读入文件     |
| LOCK TABLES             | 允许使用LOCK TABLES语句                  |
| PROCESS                 | 允许管理员查看属于所有用户的服务器进程   |
| REPLICATION CLIENT      | 允许在复制主机和从机上使用SHOW STATUS    |
| REPLICATION SLAVE       | 允许复制从服务器连接到主服务器           |
| SHOW DATABASES          | 允许使用SHOW DATABASES查看所有数据库列表 |
| SHUTDOWN                | 允许管理员关闭MySQL服务器                |
| SUPER                   | 允许管理员关闭属于任何用户的线程         |

**特别的权限**
| 权限  | 应用于                                                                                     |
|:------|:-------------------------------------------------------------------------------------------|
| ALL   | 授予用户和管理员表的所有权限                                                               |
| USAGE | 不授予权限。这将创建一个用户并允许他登录，但是不允许进行任何操作，通常在以后授予更多的权限 |

## GRANT命令
`GRANT`命令用来创建用户并赋予权限，常见形式是

```
GRANT privileges [columns]
ON item
TO username [IDENTIFIED BY 'password']
[REQUIRE ssl_options]
[WITH [GRANT OPTION | limit_options]]
```

- 占位符columns是可选的，可以用于对每个列指定权限，也可以使用单列的名称或者逗号分开的一组列的名称

- 占位符item是新权限所应用于的数据库或表。如果没有使用在任何特定数据库，可以使用`*`赋予全局权限。
更常见的是，以`dbname.*`的形式指定数据库中所有表，以`dbname.tablename`的形式指定单个表，或者
通过指定tablename来指定特定的列。这些分别表示其他3个可以利用的权限：数据库、表、列。
如果在输入命令的时候正在使用一个数据库，tablename本身被解释为当前数据库的一个表

- username应该是用户登录数据库的用户名。用户名可以包含一个主机名，可以用来区分如fred@localhost、fred@someip.com。这样可以区分来自不同域的相同用户名的用户。

- password应该是用户登录数据库的密码

- REQUIRE子句允许指定用户是否必须通过加密套接字连接，或者指定其他SSL选项。更多的参考MySQL手册

- WITH GRANT OPTION选项，如果指定，表示允许指定的用户向别人授予自己拥有的权限。
> 还可以指定如下所示的WITH选项:
> - `MAX_QUERIES_PER_HOUR n`: 用户每小时执行的查询数量上限
> - `MAX_UPDATES_PER_HOUR n`: 用户每小时执行的更新数量上限
> - `MAX_CONNECTIONS_PER_HOUR n`: 用户每小时连接的数量

## REVOKE命令
与`GRANT`相反的命令是`REVOKE`，用来从一个用户收回权限，语法与GRANT类似

```
REVOKE privileges [(columns)]
ON item
FROM username
```

如果已经给出WITH GRANT OPTION子句，可以用下面方式撤销（以及其他所有权限）
```
REVOKE ALL PRIVILEGES, GRANT
FROM username
```

## 使用GRANT和REVOKE的例子

1. 管理员的创建和撤销
创建一个管理员，可以输入如下所示命令：  
命令授予了一个用户名zhao，密码为secret的用户使用所有数据库的所有权限，并允许他向其他人授予这些权限
```
grant all
on *
to zhao identified by 'secret'
with grant option;
```
如果不希望用户在系统中存在，可以按照以下方式撤销：
```
revoke all privileges, grant
from zhao
```

2. 创建基本用户和授予权限
创建一个没有任何权限的普通用户zhao：
```
grant USAGE
on test.*
to zhao identified by 'secret';
```
在跟用户zhao沟通之后，授予一些适当的权限:
```
grant select, insert, update, delete, index, alter, create, drop
on test.*
from zhao;
```
如果我们认为zhao的权限过高，可以按照下面方式减少一些权限
```
revoke alter, create, drop
on test.*
from zhao;
```
后来，当这个用户不需要使用数据库时，按照下面方式撤销所有权限
```
revoke all
on test.*
from zhao;
```

# 创建用户
在上面权限的介绍中插入一些关于创建用户时的权限基本知识，也了解一个数据库用户是如何创建的。
在许多web应用中，用户只需要SELECT,INSERT,DELETE,UPDATE的权限。因此可以按照如下方式设定权限：
```
grant select, insert, delete, update
on test.*
to lily indetified by 'secret';
```

# 使用正确的数据库

如果开始使用MySQL，登录之后，要做的第一件事就是指定要使用的数据库。可以输入以下命令完成：
```
use dbname
```

也可以在登录时候指定数据库而避免选择数据库,如下所示
```
mysql -D dbname -h hostname -u username -p
```

例子：
我们使用一个名为books的数据库：
`use books;`
输入命令后，MySQL应该给出如下所示的响应:
`Database changed`
如果开始工作前没有选择数据库，MySQL会给出如下所示错误信息：
`ERROR 1046 (3D000): No database selected`

# 创建数据库表
创建数据库之后，就是创建实际的表。创建表的命令是`CREATE TABLE`,常见形式如下：
`create table tablename(columns)`

假如我们要创建一个订单的表单，orders(customerid, name, address, amount, date)
创建orders表，数据类型后面再详细说明，这里的比较简单：
```
create table orders
(
    customerid int unsigned not null auto_increment primary key,
    name char(50) not null,
    address char(100) not null,
    amount float(6, 2),
    date date not null
);
```

## 理解关键字的意思
not null的意思是表中所有行此属性必须有一个值。如果没有指定，该列可以是（NULL）

auto_increment 是一个特殊的MySQL特性，可以在整数列中使用。意思是再插入行的时候，如果该字段为空，
那么MySQL自动产生一个唯一标示符。该值比本列中现存的最大值更大。在每个列中只能有这样一个值。
指定auto_increment的列必须是索引列

primary key,这个只用于单列主键。如果需要多列合并为主键需要使用primary key(prop1, prop2)

整数类型后面unsigned意思是这一列只能是0或者一个正数

## 理解列的类型
创建一个表的时候，需要确定列的数据类型。根据orders表分析一下。

- customerid：主键，数据类型是一个正数，并且是无符号的，自动增长      
- name：char类型，并且分配50个字符的空间，也可以使用varchar类型，虽然varchar可以根据需要分配空间，但是char数据速度更快    
- amount：float类型，指定了显示宽度和小数点后位数   
- date：date类型，日期

更多的的类型可以查看MySQL手册

## 用SHOW和DESCRIBE来查看数据库
登录到MySQL并且使用数据库之后，输入`show tables;`可以查看所有表。    
MySQL将显示数据库中所有的表单：
```
+-----------------+
| Tables_in_blog  |
+-----------------+
| migrations      |
| password_resets |
| posts           |
| users           |
+-----------------+
```

也可以使用`show databases;`来查看数据库列表:
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| blog               |
| books              |
| dbname             |
| homestead          |
| mysql              |
| performance_schema |
| sys                |
| test               |
+--------------------+
```

如果没有show databases权限，将只能看到权限范围内的数据库

要查看某个表的详细信息，可以使用describe命令：`describe table_name;`或者`desc table_name`

MySQL将显示你创建表时提供的信息,提供一个例子，我的博客数据库posts表单的设计：
```
+--------------+------------------+------+-----+---------+----------------+
| Field        | Type             | Null | Key | Default | Extra          |
+--------------+------------------+------+-----+---------+----------------+
| id           | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| slug         | varchar(255)     | NO   |     | NULL    |                |
| title        | varchar(255)     | NO   |     | NULL    |                |
| content      | text             | NO   |     | NULL    |                |
| published_at | timestamp        | NO   |     | NULL    |                |
| created_at   | timestamp        | YES  |     | NULL    |                |
| updated_at   | timestamp        | YES  |     | NULL    |                |
+--------------+------------------+------+-----+---------+----------------+
7 rows in set (0.00 sec)
```

## 创建索引
设计主键时将在这些列上面创建索引。

MySQL新用户可能面临一个常见的问题，数据库性能低下。但这个问题经常在数据库上没有创建任何索引的情况下发生。

要开始创建索引，可以使用自动创建的索引。如果发现需要对一个不是主键的列运行许多查询，可以在该列上添加索引来改善性能

创建索引的语法是`create index`:
```
create [UNIQUE | FULLTEXT] INDEX index_name
ON table_name (index_column_name [(length) [ASC | DESC], ...])
```

FULLTEXT索引用来索引文本字段，length字段允许指定该字段的前length个字符被索引，ASC｜DESC可以指定索引的排序为升序或降序


# 理解MySQL的标示符
在MySQL中有5种类型的标识符: `Database`,`Table`,`Column`,`index`和`Alias`

| 类型     | 最大长度 | 是否区分大小写 | 允许的字符                                       |
|:---------|:---------|:---------------|:-------------------------------------------------|
| Database | 64       | 与操作系统相同 | 操作系统目录名允许出现的字符，不包含 "\","/","." |
| Table    | 64       | 与操作系统相同 | 操作系统目录名允许出现的字符，不包含 "/","."     |
| Column   | 64       | 否             | 任何字符                                         |
| index    | 64       | 否             | 任何字符                                         |
| Alias    | 255      | 否             | 任何字符                                         |


# 选择列数据类型
MySQL中3种基本的列数据类型：数字、日期和时间、字符串。

## 数字类型
数字类型分为：整型和浮点型   
对于浮点型，可以指定小数点后数字的位数。可以指定为最大值30或者最大显示长度－2    
对于整型，可以指定为无符号型    
对于所有数字类型，可以指定zerofill属性。当显示zerofill字段中的值时，空余部分用前导0来补充。如果将一个字段指定为zerofill，将自动成为unsigned数据类型

整数数据类型

| 类型         | 取值范围                       | 存储空间（单位：字节） | 描述          |
|:-------------|:-------------------------------|:-----------------------|:--------------|
| tinyint      | -127～128或0～255              | 1                      | 非常小的整数  |
| bit          | -127～128或0～255              | 1                      | tinyint同义词 |
| Bool         | -127～128或0～255              | 1                      | tinyint同义词 |
| smallint     | －32768～32767或0～65535       | 2                      | 小型整数      |
| mediumint    | -8388608～8388607或0～16777215 | 3                      | 中型整数      |
| int(Integer) | -2^31~2^32-1或0～2^32-1        | 4                      | 一般整数      |
| bigint       | -2^63~2^63-1或0~2^64-1         | 8                      | 大型整数      |

浮点数据类型

| 类型              | 取值范围                                                                                                                          | 存储空间（单位：字节） | 描述                                        |
|:------------------|:----------------------------------------------------------------------------------------------------------------------------------|:-----------------------|:--------------------------------------------|
| float(精度)       | 取决于精度                                                                                                                        | 可变                   | 可用于指定单精度和双精度浮点数              |
| float[(M, D)]     | (-3.402 823 466 E+38，1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38)                                        | 4                      | 单精度浮点数，相当于float(4),指定宽度和小数 |
| double[(M, D)]    | (1.797 693 134 862 315 7 E+308，2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 8                      | 双精度浮点数，相当于float(8),指定宽度和小数 |
| double            | 同上                                                                                                                              | 8                      | double[(M, D)] 同义                         |
| precision[(M, D)] | 同上                                                                                                                              | 8                      | double[(M, D)] 同义                         |
| real[(M, D)]      | 同上                                                                                                                              | 8                      | double[(M, D)] 同义                         |
| decimal[(M[, D])] | 可变                                                                                                                              | M+2                    | 浮点数，以char存储，范围取决于宽度M         |
| numeric[(M, D)]   | 同上                                                                                                                              | M+2                    | decimal的同义词                             |
| dec[(M, D)]       | 同上                                                                                                                              | M+2                    | decimal的同义词                             |
| fixed[(M, D)]     | 同上                                                                                                                              | M+2                    | decimal的同义词                             |

## 日期和时间类型

MySQL支持多种日期和时间类型，使用这些类型，可以以字符串或数字格式输入数据。如果不手动设置，特定行的timestamp列将被设置为最近修改改行的日期和时间

日期和时间数据类型

| 类型           | 取值范围                                              | 描述                                              |
|:---------------|:------------------------------------------------------|:--------------------------------------------------|
| date           | 1000-01-01~9999-12-31                                 | 一个日期，以yyyy-mm-dd格式                        |
| time           | -838:59:59~838:59:59                                  | 一个时间，以hh:mm:ss形式显示                      |
| datetime       | 1000-01-01 00:00:00~9999-12-31 23:59:59               | 日期和时间，以yyyy-mm-dd hh:mm:ss格式显示         |
| timestamp[(M)] | 1970-01-01 00:00:00～2037年某个时间（取决于UNIX限制） | 时间标签，在处理报告中有意义。显示格式取决于M的值 |
| year           | 70-69（1970～2069） ／ 1901～2155                     | 年份。可以指定2位数字或4位数字的格式              |

timestamp显示类型

| 指定类型      | 显示           | 指定类型     | 显示     |
|:--------------|:---------------|:-------------|:---------|
| timestamp     | YYYYMMDDHHMMSS | timestamp(8) | YYYYMMDD |
| timestamp(14) | YYYYMMDDHHMMSS | timestamp(6) | YYMMDD   |
| timestamp(12) | YYMMDDHHMMSS   | timestamp(4) | YYMM     |
| timestamp(10) | YYMMDDHHMM     | timestamp(2) | YY       |

## 字符串类型

字符串类型为3类：普通字符串，text和blob类型，特殊类型

普通字符串，即小段文本，包括char类型和varchar类型。可以指定每种类型宽度。无论数据大小是多少，char类型的列都会用空格填补空白，
但是varchar列宽随数据大小变化。MySQL获取char和varchar数据的时候，将会过滤多余的空格。这两种类型都有速度与存储空间的问题。

text和blob类型。这些类型大小可变，他们分别适用于长文本或二进制数据。blob全称为大二进制对象，支持任何数据，例如图像或声音数据

两种特殊类型，set和enum。set类型用来指定列中的值必须来自一个特定集合中的指定值。列值可以包含来自该集合的多个值。
在指定的集合中，最大可以有64个元素

enum就是枚举，与set类型相似，但是该类型的列可以只有一个指定集合中的值或者null，在枚举中最大还可以有65535个元素

常规字符串类型

| 类型                                     | 取值范围     | 描述                                                                                                                                                                                          |
|:-----------------------------------------|:-------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [National]char(M) [Binary/Ascii/Unicode] | 0~255个字符  | 固定长度为M的字符串，其中M的取值范围0～255.National关键字指定了应使用的默认字符集。Binary关键字指定了数据是否区分大小写。Ascii关键字指定了在该列使用lation1字符集。Unicode指定了使用Ucs字符集 |
| char                                     | 0~255个字符  | char(1)的同义词                                                                                                                                                                               |
| [National]varchar(M) [Binary]            | 1～255个字符 | 出了可变长度，其他与上一项相同                                                                                                                                                                |

text和blob类型

| 类型       | 最大长度（字符数） | 描述                     |
|:-----------|:-------------------|:-------------------------|
| tinyblob   | 255                | 小二进制大对象(blob)字段 |
| tinytext   | 255                | 小text字段               |
| blob       | 65535              | 常规大小blob字段         |
| text       | 65535              | 常规大小text字段         |
| mediumblob | 2^24-1(16777215)   | 中型大小blob字段         |
| mediumtext | 2^24-1(16777215)   | 中型大小text字段         |
| longblob   | 2^32-1(4294967295) | 长blob字段               |
| longtext   | 2^32-1(4294967295) | 长text字段               |

set和enum类型

| 类型                         | 集合最大值 | 描述                                   |
|:-----------------------------|:-----------|:---------------------------------------|
| enum('value1','value2',... ) | 65535      | 该类型的列只可以容纳所列值之一或者null |
| set('value','value',...)     | 64         | 该类型的列可以容纳一组值或者null       |
