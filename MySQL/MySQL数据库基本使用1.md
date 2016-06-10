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
