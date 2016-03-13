# 安装服务器

## 环境

本机演示的环境为：

* 操作系统： Windows 7 旗舰版 64位 SP1
* 处理器:	英特尔 第三代酷睿 i3-3110M @ 2.40GHz 双核
* 内存	: 4 GB 
* DB2: Express-C 10.5（64-bit）

## 下载 Express-C

链接：<http://www-01.ibm.com/software/data/db2/express-c/download.html>

**注：** 下载前，需要提供 IBM 账号，可以免费注册。

## 安装

1. 下载完成后，会有一个类似于 `v10.5_win64_expc.exe`可执行文件，双击运行。
2. 点击 Unzip 按钮进行解压。
3. 解压完成后，会弹出“DB2 安装启动板”，选择“安装产品”，并点击“安装新产品”。
4. 点击“下一步”
5. 选择“我接受IBM条款也接受非IBM条款”，点击“下一步”
6. 选择“典型安装”，点击“下一步”
7. 选择一个安装目录，点击“下一步”
8. 选择一个 SSH 安装目录，选择“不自动启动 IBM SSH Server”，这样就需要手动来启动该服务，点击“下一步”
9. 点击“下一步”
10. 配置用户信息，默认会创建一个“db2admin”用户，输入密码，点击“下一步”
11. 此时会自动默认配置一个数据库实例，点击“下一步”
12. 点击“完成”即可，程序就开始自动安装了

下面是完整的配置信息：
                                        
```
要安装的产品：                          	DB2 Express-C - DB2COPY1

安装类型：                              	典型

                                        

DB2 副本名称：                          	DB2COPY1

设置为缺省 DB2 副本：                   	是

设置为缺省 IBM 数据库客户机接口副本：   	是

                                        

所选功能部件：                          

    基本应用程序开发工具                	

    基本客户机支持                      	

    管理工具                            	

    IBM 数据服务器 .NET 提供程序        	

    第一步                              	

    Spatial Extender 客户机             	

    DB2 更新服务                        	

    JDBC 支持                           	

    DB2 LDAP 支持                       	

    ODBC 支持                           	

    OLE DB 支持                         	

    样本数据库源                        	

    SQLJ 支持                           	

    IBM Secure Shell Server for Windows 	

    DB2 WMI 提供程序                    	

                                        

语言：                                  

    英语                                	

    简体中文                            	

                                        

目标目录：                              	D:\Program Files\IBM\SQLLIB

                                        

需要的空间：                            	945MB

特定于安装的驱动程序详细信息            

用于 ODBC 和 CLI 的 IBM 数据服务器驱动程序的名称：	IBM DB2 ODBC DRIVER - DB2COPY1

OLE DB 提供程序 GUID：                  	{9C7900DE-39B5-4C45-ABB7-25EB8B96085C}

                                        

新建实例：                              

    实例名：                            	DB2

        重新引导时启动实例：            	是

        TCP/IP 配置：                   	

            服务名称：                  	db2c_DB2

            端口号：                    	50001

        实例用户信息：                  	

            用户名：                    	db2admin

                                        

DB2 管理服务器：                        

    实例用户信息：                      	

        用户名：                        	db2admin

                                        

                                        

IBM Secure Shell Server for Windows：   

                                        

        IBM SSH Server 目标目录：       	D:\Program Files\IBM\IBM SSH Server\

        IBM SSH Server 服务启动类型：   	手动

                                        

响应文件名：                            	C:\Users\admin\Documents\PROD_EXPC.rsp
```


安装完成后，会填出“DB2 第一步”的导航界面，这个小应用程序概述了几种不同的选择让您开始使用 DB2，如创建默认的示例数据库（适当命名
的 SAMPLE） 或创建您自己的新的数据库。如果您不想要探索通过第一步的 DB2 在这个时候，您可以关闭该窗口，并在稍后时间调用。

要手动启动 Windows DB2 的第一步， 选择“开始” ->“程序” - > “IBM DB2” -> “DB2COPY1”（默认） -> “设置了工具” - > “第一步骤” 或运行命令，从命令提示符 db2fs。

## 验证安装

需要验证下安装是否正确。可以从DB2 命令窗口（DB2 Command Window）（适用于 Windows）或从终端（适用于 Linux）上，运行三个命令来验证您的安装状态良好：

* **db2level**： 此命令显示有关的 DB2 安装的产品，修订包的水平，和其他详细信息。
* **db2licm -l**： 此命令会列出您所安装的 DB2 信息。
* **db2val**：它会验证您所安装的拷贝的核心功能。它会验证您所创建的实例是一致的，并验证数据库的创建及数据库连接。

完整的命令执行和输出如下：

```
D:\Program Files\IBM\SQLLIB\BIN>db2level
DB21085I  此实例或安装（适用的实例名："DB2"）使用 "64" 位和级别标识为 "0606010E"

的 DB2 代码发行版 "SQL10055"。
参考标记为 "DB2 v10.5.500.107"、"s141128" 和 "IP23628"，修订包为 "5"。
产品使用 DB2 副本名 "DB2COPY1" 安装在 "D:\PROGRA~1\IBM\SQLLIB" 中。

D:\Program Files\IBM\SQLLIB\BIN>db2licm -l
产品名：                          "DB2 Express-C"
许可证类型：                     "无担保"
到期日期：                        "永久"
产品标识：                       "db2expc"
版本信息：                        "10.5"
最大 CPU 数目：                  "2"
最大内存量 (GB)：               "16"
强制策略：                        "软停止"

D:\Program Files\IBM\SQLLIB\BIN>db2val


DBI1379I  db2val 命令正在运行。这可能要花几分钟才能完成。

DBI1333I  验证 DB2 副本 DB2COPY1 的安装文件成功。

DBI1339I  验证实例 DB2 成功。

DBI1343I  成功完成了 db2val 命令。有关详细信息，请参阅日志文件 C:\Users\admin\DO
CUME~1\DB2LOG\db2val-Sun Mar 13 13_57_52 2016.log。
```

