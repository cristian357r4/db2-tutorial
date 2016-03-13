# 备份与还原

## 备份

使用Backup命令，可以把整个数据库备份副本。该备份副本包括数据库系统文件，数据文件，日志文件，控制信息等。

可以备份脱机工作时或在线。


### 脱机备份

脱机表示当您执行您的操作时，没有其他的用户连接到数据库。
所以在备份前，要确保没有用户连接到数据库

语法：[列出活动的应用/数据库]

    db2 list application  
    
若有，则需要强制到一个实例的所有数据库的所有连接

语法：[使用的应用程序强制应用程序。处理ID]

    db2  force application (39)


或者  

    db2 force applications all
    
输出
    
```
D:\Program Files\IBM\SQLLIB\BIN> db2 force applications all
DB20000I  FORCE APPLICATION 命令成功完成。
DB21024I  此命令为异步的，可能未能立即生效。
```


语法：[终止数据库连接]

    db2 terminate  

语法：[关闭数据库]

    db2 deactivate database newdb   

语法：[执行备份文件]

    db2 backup db <db_name> [to <path>]

    
示例：

    db2 backup db newdb to d:\
  
输出

```
D:\Program Files\IBM\SQLLIB\BIN>db2 backup db newdb to d:\

备份成功。此备份映像的时间戳记是：20160313173948
```

查看备份的历史记录

示例：

```
D:\Program Files\IBM\SQLLIB\BIN>db2 list history backup all for newdb

                    列示 newdb 的历史记录文件

匹配的文件条目数 = 1


 Op Obj 时间戳记+序列     类型 设备 最早日志    当前日志     备份标识
 -- --- ------------------ ---- --- ------------ ------------ --------------
  B  D  20160313173948001   F    D  S0000000.LOG S0000000.LOG
 ----------------------------------------------------------------------------
  包含 3 表空间：

 00001 SYSCATSPACE
 00002 USERSPACE1
 00003 SYSTOOLSPACE
 ----------------------------------------------------------------------------
    Comment: DB2 BACKUP NEWDB OFFLINE
 开始时间：20160313173948
   结束时间：20160313173958
     状态：A
 ----------------------------------------------------------------------------
  EID：2 位置：d:
```   

### 在线备份


在脱机备份的基础上，加上 online 关键字，

示例：


    db2 backup db newdb online to d:\


## 从备份中还原数据库

语法：

    db2 restore db <db_name> from <location> taken at <timestamp>    
    
示例：

    db2 restore db newdb from d:\ taken at 20160313173948
    
输出：

```
D:\Program Files\IBM\SQLLIB\BIN>db2 restore db newdb from d:\ taken at 201603131
73948
SQL2539W  要复原的备份映像的指定名称与目标数据库的名称相同。复原到与备份映像数据

库相同的现有数据库时，会导致备份版本覆盖当前数据库。
想要继续吗？（y/n） y
DB20000I  RESTORE DATABASE 命令成功完成。
```