DB2 常见问题排查
====

##  备份或者还原未完成

### 问题

执行操作，提示如下：

```
[db2inst@localhost ~]$ db2 deactivate db necc_db
SQL1120N  A connection to or activation of database "NECC_DB" cannot be made 
because a previous backup or restore is incomplete.  SQLSTATE=57019
```

### 排查

根据 <https://www.ibm.com/support/knowledgecenter/SSEPGG_9.7.0/com.ibm.db2.luw.messages.sql.doc/doc/msql01120n.html>
描述：“因为先前备份或复原不完整，所以不能连接或激活数据库 名称。”

### 解决

直接删除了数据，再执行还原该数据库

```
[db2inst@localhost ~]$ db2 drop db necc_db
DB20000I  The DROP DATABASE command completed successfully.
```


## 还原完后不能连接到数据库

### 问题

还原完数据库后，不能连接到数据库

```
[db2inst@localhost ~]$ db2 connect to necc_db
SQL1117N  A connection to or activation of database "NECC_DB" cannot be made 
because of ROLL-FORWARD PENDING.  SQLSTATE=57019
```

### 排查

出现SQL1117N  由于 ROLL-FORWARD PENDING，不能连接或激活数据库 "NECC_DB"。

### 解决

需要执行命令：

```
[db2inst@localhost ~]$ db2 rollforward db necc_db to end of logs and stop

                                 Rollforward Status

 Input database alias                   = necc_db
 Number of members have returned status = 1

 Member ID                              = 0
 Rollforward status                     = not pending
 Next log file to be read               =
 Log files processed                    =  -
 Last committed transaction             = 2016-04-27-09.18.11.000000 UTC

DB20000I  The ROLLFORWARD command completed successfully.

```

## 空间不足不能执行命令

### 问题

执行 db2 语句创建或者删除数据库操作，均出现如下提示

```
SQL1004C  There is not enough storage on the file system to process the command.
```
### 排查

用户的磁盘不够了。增加用户磁盘，或者删除一些数据，来增大用户能使用的空间。

### 解决

删除了没有用的数据库和老旧的数据库备份文件。