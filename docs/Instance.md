# 实例

## 基本概念

实例是 DB2 数据库管理器中的逻辑环境。使用实例可以管理数据库。根据我们的要求，可以在一台物理机器创建多个实例。实例目录的内容是：

* 数据库管理器配置
* 文件系统数据库目录
* 节点目录
* 节点配置文件 [db2nodes.cfg]
* 调试文件，转储文件

对于 DB2 数据库服务器，默认情况下是“DB2”。这不可以在创建后更改实例目录的位置。一个实例可以管理多个数据库。在一个实例，每个数据库都有一个唯一的名称，它自己的一套目录表，配置文件，权限和特权认证。



## 基本操作

### 列出所有在您的服务器上的实例

    db2ilist

创建一个名为 newinst 的新实例
语法:

    db2icrt=<instance_name> 
    
示例：
    db2icrt newinst

### 切换到 newinst 实例，并验证它确实是您的当前实例。然后启动它。

语法:

    set db2instance=<instance_name> 
    
示例：

    set db2instance=newinst 
    
注意，等号=前后不能有空格

确证了 newinst 就是当前实例

    db2 get instance 

输出：

    当前数据库管理器实例是：NEWINST
    
### 启动一个实例。在此之前，需要运行“set instance”：

    db2start

输出：

    SQL1063N  DB2START 处理成功。

### 停止当前实例 newinst

    db2stop

### 删除实例 newinst

    db2idrop newinst
