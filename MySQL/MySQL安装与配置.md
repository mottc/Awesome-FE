MySQL的安装方式分为两种  
- MSI安装  
- ZIP安装  

----------


# MSI安装方式
1.官网下载MSI安装文件(http://dev.mysql.com/downloads/mysql/)  
2.双击安装    
3.选择Typical（典型）安装   
4.一路next  
5.选择安装路径下bin目录中的MySQLInstanceConfig.exe  
6.选择标准配置  
7.安装为Windows服务，配置环境变量  
8.设置密码  
9.选择安装路径下my.ini文件修改编码方式  
```
[mysql]
default-character-set=utf8
[mysqld]
character-set-server=utf8
```
10.运行数据库cmd->mysql -uroot -p   
# ZIP安装方式
1.官网下载ZIP包(http://dev.mysql.com/downloads/mysql/)  
2.下载完成后解压到D:\Program Files下，打开解压目录  
3.复制一个my-default.ini文件，并改为my.ini，用以下代码覆盖文件内容：  
```
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8 
[mysqld]
#设置3306端口
port = 3306 
# 设置mysql的安装目录(根据安装路径修改路径，修改x.x.xx为你的版本号！！！)
basedir=D:\Program Files\mysql-x.x.xx
# 设置mysql数据库的数据的存放目录(根据安装路径修改路径，修改x.x.xx为你的版本号！！！)
datadir=D:\Program Files\mysql-x.x.xx\data
# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB 
#或者是这个default-storage-engine=MYISAM
```
4.管理员身份运行CMD  
5.目录切换到你解压文件的bin目录,再输入mysqld install，再输入net start mysql 启动服务。
  如果服务无法启动，可能是mysql安装目录下没有data这个目录，打开cmd命令窗口，并且进入到mysql安装目录的bin目录下。然后输入命令：
```
mysqld --initialize-insecure --user=mysql
```
6.在环境变量path中加入D:\mysql\mysql-x.x.xx-winx64\bin;  
7.运行数据库cmd->mysql -uroot -p    
8.如果遇到1055错误，把sql_mode=NO_ENGINE_SUBSTITUTION这句也加到my.ini里面  
