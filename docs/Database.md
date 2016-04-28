#  数据库

## 基本概念
数据库是表，模式，缓冲池，日志，存储组和表空间合作有效地处理数据库操作的集合。

![](http://www.yiibai.com/uploads/allimg/141215/091I54530-0.png)

## 基本操作

### 列出当前实例可用的数据库目录列表

语法:

	db2 list db directory 


### 创建数据库

语法:

	db2 create db <db_name>
 
示例：

	db2 create db newdb

输出：

	DB20000I  CREATE DATABASE 命令成功完成。
	
可以查看到当前数据库的目录

```
D:\Program Files\IBM\SQLLIB\BIN>db2 list db directory

 系统数据库目录

 目录中的条目数 = 1

数据库 1 条目：

 数据库别名                      = NEWDB
 数据库名称                               = NEWDB
 本地数据库目录                  = D:
 数据库发行版级别                = 10.00
 注释                            =
 目录条目类型                    = 间接
 目录数据库分区号                  = 0
 备用服务器主机名                =
 备用服务器端口号                =
```

### 删除数据库

语法：

    db2 drop db <db_name>
	
示例：

    [db2inst@localhost ~]$ db2 drop db sample
    DB20000I  The DROP DATABASE command completed successfully.


### 激活数据库

该命令启动了所有必要的服务，为特定的数据库，这样的数据库是可用的应用程序。

语法:

	db2 activate db <db_name> 
	
示例: 

	db2 activate db newdb  
	
### 停用数据库

使用此命令，可以停止数据库服务。

语法:

	db2 deactivate db <db_name>
	
示例: 

	db2 deactivate db newdb
	
### 连接到数据库

创建一个数据库，把它投入使用后，需要连接或启动数据库。

语法:

	db2 connect to <database name> 
	
示例: 

	db2 connect to newdb 

输出：

```
D:\Program Files\IBM\SQLLIB\BIN>db2 connect to newdb

   数据库连接信息

 数据库服务器         = DB2/NT64 10.5.5
 SQL 授权标识         = ADMIN
 本地数据库别名       = NEWDB
```

## 用用户名和密码远程连接到数据库

语法：

	db2 connect to <db_name> user <userid> using <password>   

示例：

	db2 connect to newdb user db2admin using 123abc   

输出：

```
D:\Program Files\IBM\SQLLIB\BIN>db2 connect to newdb user db2admin using 123abc


   数据库连接信息

 数据库服务器         = DB2/NT64 10.5.5
 SQL 授权标识         = DB2ADMIN
 本地数据库别名       = NEWDB
```

## 验证数据库的权限

语法：

```
db2 "select substr(authority,1,25) as authority, d_user, d_group, d_public, role_user, role_group, role_public,d_role from table( sysproc.auth_list_authorities_for_authid ('public','g'))as t order by authority"  
```
   