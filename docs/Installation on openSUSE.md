# 在 openSUSE 上安装 DB2 服务器

## 环境

本机演示的环境为：

* 操作系统：  [openSUSE Leap 42.1](https://software.opensuse.org/421/us_EN)
* 处理器:	英特尔 第三代酷睿 i3-3110M @ 2.40GHz 双核
* 内存	: 4 GB 
* DB2: Express-C 10.5（64-bit）

## 下载 DB2 Express-C

DB2 Express-C 具有 DB2 所有版本一样的核心功能，且免费，用来学习 DB2 足够了。

下载地址：<http://www-01.ibm.com/software/data/db2/express-c/download.html>

本例安装包为：v10.5_linuxx64_expc.tar.gz

**注：** 下载前，需要提供 IBM 账号，可以免费注册。

## 解压、检查环境

### 解压 

    tar –zxvf v10.5_linuxx64_expc.tar.gz

生成了 `expc` 目录，切换到该目录下，执行相关命令


### 检查环境

检查该环境是否满足安装的需求，这里的安装包的版本是 `10.5.0.7`

    /home/software/expc/db2prereqcheck -v 10.5.0.7

如果检查出，环境不满足，则需要安装相应的包，比如：

```
Requirement not matched for DB2 database "Server" with pureScale feature . Version: "10.5.0.7". 
Summary of prerequisites that are not met on the current system: 
DBT3507E  The db2prereqcheck utility failed to find the following package or file: "kernel-source". 


DBT3507E  The db2prereqcheck utility failed to find the following package or file: "gcc-c++". 


DBT3507E  The db2prereqcheck utility failed to find the following package or file: "cpp". 
```

上面提示 kernel-source、gcc-c++、cpp 不满足安装条件，先安装上述软件

```
zypper install kernel-source
zypper install gcc-c++
zypper install cpp
```

安装完成，再执行 db2prereqcheck 检查，最终输出如下，才能执行安装

```
DBT3533I  The db2prereqcheck utility has confirmed that all installation prerequisites were met.
```

## 创建用户和组

### 创建用户和组

需用具有 root 用户权限手动创建下列用户和组:

用户	| 示例用户名	| 示例组名
---- | ---- | ----
实例所有者	| db2inst1	| db2iadm1
受防护的用户	| db2fenc1	| db2fsdm1
DB2 管理服务器用户	| dasusr1 | dasadm1

输入下列命令：

```
groupadd -g 999 db2iadm1
groupadd -g 998 db2fsdm1
groupadd -g 997 dasadm1
```

为每个组创建用户：

```
useradd -u 1004 -g db2iadm1 -m -d /home/db2inst1 db2inst1
useradd -u 1003 -g db2fsdm1 -m -d /home/db2fenc1 db2fenc1 
useradd -u 1002 -g dasadm1 -m -d /home/dasusr1 dasusr1
```

设置初始密码：

```
passwd db2inst1
passwd db2fenc1
passwd dasusr1
```

### 解释：

* Instance owner(实例所有者)：DB2 实例 被 Instance owner 创建在 home 目录。这个 用户 ID 控制所有 DB2 进程、拥有的所有文件系统和包含在实例的数据库使用的设备。默认用户名称是 db2inst1 和默认分组是 db2iadm1。
* Fenced user(受防护的用户)：主要负责用户自定义函数（user defined function）和存储过程（stored precedure）。创建这个用户的好处是，当一个自定义函数发生内存泄漏的问题，至多影响到这些自定义函数和存储过程。而影响不到整个数据库管理系统。所以，如果你不需要过多的安全需要，比如在测试环境，可以将 Instance owner 用户作为 Fenced user。 如果你的系统有很多自定义函数或者存储过程的话，最好创建一个跟实例名不是同名的，这里默认创建一个名叫 db2fenc1 的用户，默认分组 db2fadm1
* DB2 administration server user(DB2 管理服务器用户)：DB2 管理服务器用户的用户标识用于在系统上运行 DB2 管理服务器 (DAS)。缺省用户为 dasusr1，缺省组为 dasadm1。每台计算机上只能有一个 DAS。一个 DAS 维护一个或多个数据库实例，包括属于不同安装的数据库实例。DAS 可以维护其发行版级别低于 DAS 发行版级别的数据库实例。但是，对于其发行版级别高于 DAS 发行版级别的数据库实例，DAS 必须迁移到更高级别。DAS 发行版级别必须不低于所维护的任何数据库实例的发行版级别。注意， [V9.7 中已经不推荐使用 DAS
](http://www.ibm.com/support/knowledgecenter/SSEPGG_9.7.0/com.ibm.db2.luw.wn.doc/doc/i0059276.html)，在以后的发行版中可能会将其除去。推荐使用 IBM® Data Studio 和 IBM Optim™ 工具来代替控制中心工具。有关详细信息，请参阅 不推荐使用控制中心工具。推荐使用采用安全 shell (SSH) 协议的软件程序进行远程管理。例如，可以在 Data Studio 配置工作台以运行 SQL 语句、实用程序和命令，或使用安全 shell (SHH) 协议来浏览和访问远程服务器上的文件。


### 用户标识限制

用户标识具有下列限制和要求：
* 必须具有除 guests、admins、users 和 local 之外的主组
* 可以包含小写字母 (a-z)、数字 (0-9) 和下划线字符 ( _ )
* 长度不能超过八个字符
* 不能以 IBM、SYS、SQL 或数字开头
* 不能是 DB2 保留字（USERS、ADMINS、GUESTS、PUBLIC 或 LOCAL）或 SQL 保留字
* 不能使用任何具有 root 用户特权的用户标识作为 DB2 实例标识、DAS 标识或受防护标识
* 不能包含重音字符
* 如果已指定现有用户标识，而不是创建新用户标识，那么确保该用户标识：
    * 未锁定
    * 不具有到期的密码





## 执行 db2_install 安装 DB2

执行安装

```
linux-rrkj:/home/software/expc/db2_install

DBI1324W  Support of the db2_install command is deprecated.

Default directory for installation of products - /opt/ibm/db2/V10.5

***********************************************************
Install into default directory (/opt/ibm/db2/V10.5) ? [yes/no] 
```

期间需要确认安装位置，输入 yes 继续

安装完成后，输出如下：

```
The execution completed successfully.

For more information see the DB2 installation log at
"/tmp/db2_install.log.26071".
```

默认安装目录为 /opt/ibm/db2/V10.5 ，该 tmp 目录下，存储的是日志文件

## 安装 license

license 文件在解压包目录 /home/software/expc/db2/license/db2expc_uw.lic

安装 license，命令如下：
 
```
linux-rrkj:~ # /opt/ibm/db2/V10.5/adm/db2licm -a /home/software/expc/db2/license/db2expc_uw.lic

LIC1402I  License added successfully.


LIC1426I  This product is now licensed for use as outlined in your License Agreement.  USE OF THE PRODUCT CONSTITUTES ACCEPTANCE OF THE TERMS OF THE IBM LICENSE AGREEMENT, LOCATED IN THE FOLLOWING DIRECTORY: "/opt/ibm/db2/V10.5/license/en_US.iso88591"
```

查看授权信息

```
linux-rrkj:~ # /opt/ibm/db2/V10.5/adm/db2licm -l
Product name:                     "DB2 Express-C"
License type:                     "Unwarranted"
Expiry date:                      "Permanent"
Product identifier:               "db2expc"
Version information:              "10.5"
Max number of CPUs:               "2"
Max amount of memory (GB):        "16"
Enforcement policy:               "Soft Stop"
```

## 使用 db2icrt 创建实例

/opt/IBM/db2/V10.5/instance/db2icrt -p 50001 -u db2fenc1 db2inst1

其中，-p 制定了服务器端口号，不指定默认是 50000。

```
waylau:~ # /opt/ibm/db2/V10.5/instance/db2icrt -p 50001 -u db2fenc1 db2inst1
DBI1446I  The db2icrt command is running.


DB2 installation is being initialized.

 Total number of tasks to be performed: 4 
Total estimated time for all tasks to be performed: 309 second(s) 

Task #1 start
Description: Setting default global profile registry variables 
Estimated time 1 second(s) 
Task #1 end 

Task #2 start
Description: Initializing instance list 
Estimated time 5 second(s) 
Task #2 end 

Task #3 start
Description: Configuring DB2 instances 
Estimated time 300 second(s) 
Task #3 end 

Task #4 start
Description: Updating global profile registry 
Estimated time 3 second(s) 
Task #4 end 

The execution completed successfully.

For more information see the DB2 installation log at "/tmp/db2icrt.log.3207".
DBI1070I  Program db2icrt completed successfully.

```

### 问题处理

可能会出现如下问题：
```
linux-rrkj:~ # /opt/ibm/db2/V10.5/instance/db2icrt -p 50001 -u db2fenc1 db2inst1
DBI1446I  The db2icrt command is running.


DB2 installation is being initialized.

 The host name "linux-rrkj" is invalid. Specify a valid host name.

A major error occurred during the execution that caused this program to
terminate prematurely. If the problem persists, contact your technical service
representative.

For more information see the DB2 installation log at "/tmp/db2icrt.log.21212".
DBI1264E  This program failed. Errors encountered during execution were
      written to the installation log file. Program name:
      db2icrt. Log file name: /tmp/db2icrt.log.21212.

Explanation: 

This message is returned when some processes and operations have failed.
Detailed information about the error was written to the log file.

User response: 

Contact IBM support to get assistance in resolving this issue. Keep the
log file intact as this file is an important reference for IBM support.
```

解决方法：

设置主机名称，比如，本例为 waylau.com

    linux-rrkj:~ # hostname waylau.com
    linux-rrkj:~ # vi /etc/hosts

在 hosts 中添加一个 

    127.0.0.1 waylau.com
    ::1       waylau.com
    
修改 HOSTNAME 为 waylau.com

    linux-rrkj:~ # vi /etc/HOSTNAME
 

### 设置数据库实例自动启动

设置数据库实例 db2inst1 自动启动，执行 

    waylau:~ # /opt/ibm/db2/V10.5/instance/db2iauto -on db2inst1

## 验证安装

1. 作为具有 SYSADM 权限的用户登录系统（这里指 db2inst1）。
2. 输入 db2start 命令来启动数据库管理器。
3. 输入 db2sampl 命令来创建 SAMPLE 数据库。
处理此命令可能要花几分钟。没有完成消息；当返回命令提示符时，该过程完成。
创建 SAMPLE 数据库时，该数据库自动以数据库别名 SAMPLE 进行编目。

4. 连接至 SAMPLE 数据库，检索所有在部门 20 工作的职员的列表，然后重置数据库连接。从命令行处理器 (CLP) 中输入下列命令：

```
connect to sample
select * from staff where dept = 20
connect reset
```

输出应该类似于以下内容：

```
db2inst1@waylau:~> db2
(c) Copyright IBM Corporation 1993,2007
Command Line Processor for DB2 Client 10.5.7

You can issue database manager commands and SQL statements from the command 
prompt. For example:
    db2 => connect to sample
    db2 => bind sample.bnd

For general help, type: ?.
For command help, type: ? command, where command can be
the first few keywords of a database manager command. For example:
 ? CATALOG DATABASE for help on the CATALOG DATABASE command
 ? CATALOG          for help on all of the CATALOG commands.

To exit db2 interactive mode, type QUIT at the command prompt. Outside 
interactive mode, all commands must be prefixed with 'db2'.
To list the current command option settings, type LIST COMMAND OPTIONS.

For more detailed help, refer to the Online Reference Manual.

db2 => connect to sample

   Database Connection Information

 Database server        = DB2/LINUXX8664 10.5.7
 SQL authorization ID   = DB2INST1
 Local database alias   = SAMPLE

db2 => select * from staff where dept = 20

ID     NAME      DEPT   JOB   YEARS  SALARY    COMM     
------ --------- ------ ----- ------ --------- ---------
    10 Sanders       20 Mgr        7  98357.50         -
    20 Pernal        20 Sales      8  78171.25    612.45
    80 James         20 Clerk      -  43504.60    128.20
   190 Sneider       20 Clerk      8  34252.75    126.50

  4 record(s) selected.

db2 => connect reset
DB20000I  The SQL command completed successfully.
db2 => terminate
DB20000I  The TERMINATE command completed successfully.
db2 => quit
DB20000I  The QUIT command completed successfully.

```

停止数据库

    db2inst1@waylau:~> db2stop
    SQL1064N  DB2STOP processing was successful.


## 参考引用

* [Installing DB2 Servers](http://public.dhe.ibm.com/ps/products/db2/info/vr105/pdf/en_US/DB2InstallingServers-db2ise1051.pdf)