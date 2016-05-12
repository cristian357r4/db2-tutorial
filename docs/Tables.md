表
====

使用前先连接到数据

列出所有表


用法：

    db2 list tables for schema <schema name>

示例：


```
db2inst@db1:~> db2 list tables for schema db2inst

Table/View                      Schema          Type  Creation time             
------------------------------- --------------- ----- --------------------------
WHITE_PAPER                     DB2INST         T     2014-11-14-15.26.13.447709
WHITE_PAPER_SEASON              DB2INST         T     2014-11-14-15.26.14.410808

  2 record(s) selected.

db2inst@db1:~> 

```