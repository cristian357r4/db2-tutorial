# 介绍

## DB2 简介

IBM DB2 是美国 IBM 公司开发的一套关系型数据库管理系统，它主要的运行环境为 UNIX（包括 IBM 自家的 AIX）、Linux、IBM i（旧称OS/400）、z/OS，以及 Windows 服务器版本。

DB2 主要应用于大型应用系统，具有较好的可伸缩性，可支持从大型机到单用户环境，应用于所有常见的服务器操作系统平台下。 DB2 提供了高层次的数据利用性、完整性、安全性、可恢复性，以及小规模到大规模应用程序的执行能力，具有与平台无关的基本功能和 SQL 命令。DB2 采用了数据分级技术，能够使大型机数据很方便地下载到 LAN 数据库服务器，使得客户机/服务器用户和基于 LAN 的应用程序可以访问大型机数据，并使数据库本地化及远程连接透明化。 DB2 以拥有一个非常完备的查询优化器而著称，其外部连接改善了查询性能，并支持多任务并行查询。 DB2 具有很好的网络支持能力，每个子系统可以连接十几万个分布式用户，可同时激活上千个活动线程，对大型分布式应用系统尤为适用。

DB2 除了可以提供主流的OS/390和VM操作系统，以及中等规模的 AS/400 系统之外，IBM 还提供了跨平台（包括基于 UNIX 的 LINUX，HP-UX，SunSolaris，以及 SCOUnixWare；还有用于个人电脑的 OS/2操作系统，以及微软的 Windows 2000 和其早期的系统）的DB2产品。DB2 数据库可以通过使用微软的开放数据库连接（ODBC）接口，Java 数据库连接（JDBC）接口，或者 CORBA 接口代理被任何的应用程序访问。

## DB2 简史

* 诞生与发展
  * DB2拥有悠久的历史并且被很多人认为是最早使用SQL（同样最早被IBM开发）的数据库产品。
  * 1968:IBM 在 IBM 360 计算机上研制成功了 IMS V1，这是第一个也是最著名的和最为典型的层次型数据库管理系统。至今仍然还有企业在使用呢
  * 1970:这是数据库历史上划时代的一年，IBM公司的研究员E.F.Codd 发表了业界第一篇关于关系数据库理论的论文"A Relational Model of Data for Large Shared Data Banks"，首次提出了关系模型的概念。这篇论文是计算机科学史上最重要的论文之一，奠定了Codd博士"关系数据库之父"的地位。
  * 1973:IBM研究中心启动了 System R 项目，研究多用户与大量数据下关系型数据库的可行性，它为 DB2 的诞生打下了良好基础。由此取得了一大批对数据库技术发展具有关键性作用的成果，该项目于1988年被授予ACM软件系统奖。
  * 1974:IBM研究员Don Chamberlin 和 Ray Boyce 通过 System R 项目的实践，发表了论文"SEQUEL：A Structured English Query Language"，提出了 SEQUEL 语言，此即 SQL 语言的原型。
  * 1975:IBM研究员Don Chamberlin 和 Morton Astrahan的论文 "Implentation of a Structured English Query Language"，在 SEQUEL 的基础上 描述了 SQL 语言的第一个实现方案。这也是 System R 项目得出的重大成果之一。
  * 1976:IBM System R 项目组发表了论文"A System R: Relational Approach to Database Management"，描述了一个关系型数据库的原型。IBM 的研究员Jim Gray 发表了名为"Granularity of Locks and Degrees of Consistency in a Shared DataBase"的论文，正式定义了数据库事务的概念和数据一致性的机制。
  * 1977:System R 原型在3个客户处进行了安装，这 3 个客户分别是：波音公 司、Pratt & Whitney 公司和 Upjohn 药业。这标志着 System R 从技术上已经是 一个比较成熟的数据库系统，能够支撑重要的商业应用了。
  * 1979:IBM研究员Pat Selinger在她的论文"Access Path Selection in a Relational Database Management System"中描述了业界第一个关系查询优化器。
  * 1980:IBM发布了 S/38 系统，该系统中集成了一个以 System R 为原型的数据库服务器。为了方便应用程序的移植，它的 API 与 S/3、S/32 的 API 一致。
  * 1981:由于发明了关系型数据库模型，IBM 的研究员E.F.Codd 接受了ACM 图灵奖，这是计算机科学界的最高荣誉。Codd 博士也是继查尔斯.巴赫曼（Charles W. Bachman） 之后，又一位由于在数据库领域做出巨大贡献而获此殊荣的计算机科学家。
  * 1982:IBMPC 的出现标志着 PC 产业开始孕育发展。在以后相当长的一段时间内，在各种品牌的个人电脑上标记着的"IBM PC Compatible"字样都见证着 IBM 在 这个领域的辉煌。
  * 1982:IBM发布了 SQL/DS for VSE and VM 。这是业界第一个以 SQL 作为接口的商用数据库管理系统。该系统也是基于 System R 原型所设计的。
  * 1983:IBM发布了DATABASE 2（DB2）for MVS（内部代号为"Eagle"）。
  * 1986:System/38 V7 发布，该系统首次配置了查询优化器，能够对应用程序的存取计划进行优化。
  * 1987:IBM发布带有关系型数据库能力的 OS/2 V1.0扩展版，这是IBM第一次把关系型数据库处理能力扩展到微机系统。这也是 DB2 for OS/2、Unix and Window 的雏形。
  * 1988:IBM发布了SQL/400，为集成了关系型数据库管理系统的AS/400服务器提供了SQL支持。IDUG（国际DB2用户组织）组织成立。
  * 1989:IBM定义了 Common SQL 和 IBM 分布式关系数据库架构（DRDA），并在 IBM 所有的关系数据库管理系统上加以实现。 第一届 IDUG北美大会在美国芝加哥召开。
* 走向全球化
  * 1992:第一届 IDUG欧洲大会在瑞士日内瓦召开。这标志着 DB2 应用的全球化。
  * 1993:
    * 1.IBM发布了DB2 for OS/2 V1（DB2 for OS/2 可以被简写为DB2/2）和 DB2 forRS/6000V1（DB2 for RS/6000 可以被简写为DB2/6000），这是 DB2 第 一次在Intel 和Unix 平台上出现。
    * 2.Louis V. Gerstner 入主 IBM。
  * 1994:
    * 1.DB2 For MVS V4 通过并行 Sysplex 技术的实现在主机上引入了分布式计算（数据共享）。
    * 2.IBM发布了运行在 RS/6000 SP2 上的 DB2 并行版 V1，DB2 从此有了能够适应大型数据仓库和复杂查询任务的可扩展架构。IBM 将 DB2 Common Server 扩展到 HP-UX 和 Sun Solaris 上。DB2 开始支持其他公司开发的 UNIX 平台。 DB2/400 集成在 OS/400 V3.1中发布，并且引入了并行机制、存储过程和参照完整性等机制。同时，IBM 宣布在 OS/2 和 AIX 平台上的 DB2 产品能够对多媒体数据和面向对象应用程序提供支持。
  * 1995:
    * 1.IBM发布了 DB2 Common Server V2，这是第一个能够在多个平台上运行的"对象-关系型数据库"(ORDB)产品，并能够对 Web 提供充分支持。DataJoiner for AIX 也诞生在这一年，该产品赋予了 DB2 对异构数据库的支持能力。DB2 在 Windows NT 和 SINIX平台上的第一个版本（DB2 V2）发布。
    * 2.IBM发布了在 AIX 和 MVS 平台上的数据挖掘技术，用于管理大文本、图像、音频、视频和指纹信息的扩展器（Extender）以及可以对数据仓库进行可视化构造和管理的Visual Warehouse。
    * 3.IBM发布了 DB2 WWW Connection V1 for OS/2 and AIX（该产品后来被更名为Net.Data）。该产品可以将数据库中的数据快速发布到 Web。第一届 IDUG 亚太区大会在澳大利亚悉尼召开。这年IBM 并购了 Lotus Development Corp。
  * 1996:
    * 1.IBM发布 DB2 V2.1.2 ，这是第一个真正支持 JAVA 和 JDBC 的数据库产品。
    * 2.DataJoiner 开始支持对非关系型数据库（比如 IMS 和 VSAM）的存取。
    * 3.IBM发布了 Intelligent Miner，该产品可以对基于 DB2 的数据源实施数据挖掘。
    * 4.IBM并购 Tivoli。 IBM 将 DB2 更名为 DB2 Universal Database，这是第一个能够对多媒体和 Web 进行支持的RDBMS。该系统具有很好的伸缩性，可以从桌面系统扩展到大型企业，适应单处理器、 SMP 和 MPP 计算环境，并可以运行在所有主流操作系统和硬件平台上。 DB2 V5 是以前的两个产品的合并：DB2 Common Server V 2.1.2 和 DB2 并行版 1.2。
    * 5.IBM发布了数字图书馆产品，这是一个多媒体资产管理产品，也是 IBM Content Manager 的前身。
    * 6.DB2 Magzine 第一期发布，DB2 有了自己专门的技术刊物。
  * 1997:
    * 1.IBM发布了可以支持 Web 的 DB2 for OS/390 V5，这是当时唯一能够支持64, 000个并发用户和百 TB 级别的数据库产品。
    * 2.IBM发布了DB2 UDB for UNIX、Windows and OS/2，该产品支持 ROLLUP 和 CUBE 函数，对联机分析处理（OLAP）具有重要意义。
    * 3.IDUG 第一次技术论坛在加拿大多伦多召开。
    * 4.IBM发布了用于企业级内容管理的 EDMSuite，该产品包含了用于管理计算机生成报表的 OnDemand 和 管理图像的 ImagePlus VisualInfo。
    * 5.IBM基于 RS/6000 SP 架构的超级计算机"深蓝"在国际象棋的 6 番棋对抗中战胜了世界棋王卡斯帕罗夫。
  * 1998:
    * 1.IBM发布了 DB2 OLAP Server，这是一个基于 DB2 的完整的 OLAP Solution。这个产品是和 Arbor Software（Hyperion的前身）合作开发的。
    * 2.IBM发布了 DB2 Data Links 技术，该技术可使 DB2 对外部文件进行管理。
    * 3.DB2的 shared-nothing集群技术扩展到 Windows 和 Solaris 平台。
    * 4.IBM发布了 DB2 Spatial Extender，这是与ESRI公司在DataJoiner基础 上联合开发的，该产品赋予了DB2 对地理信息数据的存取能力。
    * 5.IBM发布了 ContentConnect，该产品是 Enterprise Information Portal（EIP）的前身。
    * 6.DB2 对 SCO UnixWare 平台提供支持。
    * 7.DB2 UDB V5.2 增加了对 SQLJ、Java 存储过程和用户自定义函数的支持。
    * 8.IBM发布 DB2 UDB for AS/400，使 AS/400 成为充分支持电子商务的机 型。
  * 1999:
    * 1.IBM为了对移动计算提供支持，发布了DB2 UDB 卫星版和DB2 Everywhere（这是一个适用于手持设备的微型关系数据库管理系统，后称为DB2 Everyplace）。
    * 2.IBM发布了 Enterprise Information Portal，该产品可以跨数字图书 馆和 EDMSuite 提供一个统一的联合检索功能。
    * 3.DB2增加了能够识别 XML 语言的文本检索功能，从而引入了 XML 支 持，并启动了DB2 XML Extender 的 beta 计划。
    * 4.IBM发布了 Intel 平台上的 DB2 UDB for Linux。
    * 5.IBM 研究机构将 DB2 的联邦（federation）功能和 Garlic 技术（Garlic的目标是使能大规模多媒体信息系统，集成到生命科学解决方案DiscoveryLink 中  
  * 2000:
    * 1.IBM发布了 DB2 XML Extender，成为在业界第一个为数据库提供内置 XML 支持的厂商。
    * 2.IBM将 Visual Warehouse 集成到 DB2 中，为DB2 提供了内置的数据仓库管理功能。
    * 3.DB2对Linux 的支持进一步增强，能够支持基于 Intel 的 Linux集群、 发布了可以运行在主机上的 DB2 UDB for Linux和可以运行在嵌入式Linux上的 DB2 Everyplace。
    * 4.DB2开始支持 NUMA-Q 平台，可以运行在该平台上的类 UNIX操作系统DYNIX/PTX 上。
    * 5.DB2通过 Net.Search Extender 提供了 in-memory 高速文本检索功能。
    * 6.IBM启动了数据库管理工具业务，起初着重于为主机上的 IMS 和 DB2 提供高效管理工具，最终这项业务扩展到 UNIX、Linux 和 Windows 平台。 Informix数据库产品也在支持之列。
    * 7.IBM开始通过在DB2中集成 DataJoiner 来提供数据联邦（federation）功能 。
    * 8.IBM发布了用于管理数字资产的Content Manager。IBM 数字图书馆和 EDMSuite 产品都被包含在一个单一的架构中来提供多媒体资产管理和企业内 容管理。荷兰国家图书馆、梵蒂冈图书馆都是最早的用户。
    * 9.DB2在主机上销售出了它的第10000个许可证。
  * 2001:
    * 1.IBM以 10 亿美金收购了 Informix 的数据库业务，这次收购扩大了IBM 的分布式数据库业务。
    * 2.DB2 OLAP Server中增添了数据挖掘功能。
    * 3.IBM发布了第一个能够支持多种平台的 DB2 工具。
    * 4.DB2提供了基于 SOAP 的 Web 服务的支持。DB2 XML Extender和存储过程可以使DB2成为 Web 服务的提供者。
    * 5.IBM科学家在纳米碳管晶体管技术领域取得突破。IBM 用纳米碳管制造出了世界上第一批纳米晶体管--由直径 10 个原子大小的碳原子组成的小圆柱结 构，比当今基于硅的晶体管小 500 倍。
    * 6.DB2 拓宽了其数据联邦（federation）的能力，可以对WebSphere MQ消息队列和生命科学领域特定格式的文件提供支持。
    * 7.IBM发布了 DB2 UDB for OS/390。
  * 2002:
    * 1.IBM发布了 Xperanto，这是一个基于标准的信息集成中间件的演示版， 可以用来优化对分散数据源的存取。这个演示版本使用了XML、Xquery、Web 服 务、数据联邦（federation）和全文检索等先进技术。
    * 2.IBM宣布计划收购 Rational Software Corp，从而使得 IBM软件能够 支持从设计、开发、部署到管理和维护的完整过程。
    * 3.DB2通过基于 SOAP 的 Web 服务扩展了数据联邦（federation）的能力。并可以作为 Web 服务的使用者出现在 Web 服务架构中。
    * 4.DB2 OLAP Server中添加了hybrid（多维和关系）分析能力。
    * 5.作为IBM 自主运算策略的一部分，SMART（自我管理和资源调节）技术 在 DB2 UDB V8.1 中首次正式应用。
    * 6.IBM并购 Tarian Sotware，从而加强了Content Manager 中记录管理组 件的功能。
  * 2003:
    * 1.IBM将数据管理产品统一更名为信息管理产品，旨在改变很多用户对于 DB2 家族产品只能完成单一的数据管理的印象，强调了 DB2 家族在信息的处理与集成方面的能力。
    2.DYNIX/ptxDB2 发布了 DB2 Information Integrator（该产品由以 前的 DB2 DataJoiner和 Enterprise Information Portal演化而来），该款软件旨在帮助客户即时访问、集成、管理和分析存储于企业内外任何平台上的各类信息。
  * 2004:IBM DB2 在TPC 的两项测试中屡次刷新该测试的新纪录，在计算领 域的历史上树立了新的里程碑。其中在TPC-C 的测试中，它创造了计算速度领域新的世界记录，彻底粉碎了在该测试中每分钟三百万次交易的极限。
  * 2005:经过长达5年的开发，IBM DB2 9将传统的高性能、易用性与自描述、灵活的XML相结合，转变成为交互式、充满活力的数据服务器。
  * 2006:IBM发布DB2 9，将数据库领域带入XML时代。IT建设业已进入SOA（Service-Oriented Architecture）时代。实现SOA，其核心难点是顺畅解决不同应用间的数据交换问题。XML以其可扩展性、 与平台无关性和层次结构等特性，成为构建SOA时不同应用间进行数据交换的主流语言。而如何存储和管理几何量级的XML数据、直接支持原生XML文档成为SOA构建效率和质量的关键。在这这种情况下，IBM推出了全面支持Original XML的DB2 9，使XML数据的存储问题迎刃而解，开创了一个新的XML数据库时代。同年1月30日，IBM发布了一个DB2免费版本DB2Express-C。

  
## DB2 版本

本文仅关注该产品组合中的基础产品 - DB2 for Linux, Unix, and Windows 数据库家族，在 10.5 版本中包括 含 6 个付费版本、一个单独付费的特性和一个免费包:


* Advanced Enterprise Server Edition：专为中型到非常大的企业服务器而设计
* Advanced Workgroup Server Edition：适合您的所有部门级工作负载需求的一流产品
* Workgroup Server Edition：需要考虑高可用性的部门级工作负载的最佳选择
* Express Edition：简单、安全而又廉价，目标用户是需要小型但强大的事务数据库的中小企业 (SMB) 和 ISV。
* Express-C：一个可免费用于构建、开发和分发的程序包，是开发人员和中小型部署、学术团体等的完美选择。
* Advanced Recovery Feature：是一个新的单独付费的 DB2 10.5 特性。它恰好也是 DB2 10.5 惟一的附加特性。此特性实际上是一个高级数据库备份、恢复和数据提取工具包，可帮助企业改善数据可用性、减轻风险和加速关键管理任务，节省宝贵的时间。
* DB2 Developer Edition：这是一个减价的产品，提供了出于应用程序开发、培训、演示和测试用途而访问大部分 DB2 功能和版本以及 DB2 Connect 的能力，用于任何非生产环境。


![](http://www.ibm.com/developerworks/cn/data/library/techarticle/dm-1311whichdb2edition/figure1-DB2editions.png)

可以看到免费的 DB2 Express-C Edition 是最核心的功能，而其他版本都是在此版本之前提供附加的功能，这样你从 Express-C 升级到其他版本就不会有障碍。

## 共同功能

以下功能是所有 DB2 10.5 版本（包括 DB2 Express-C）中都可找到的共同功能的例子：

* **Oracle 数据库兼容性**：
DB2 支持无痛地迁移应用程序，不仅支持在 DB2 版本之间进行迁移，还支持从 Oracle 数据库迁移。98% 的 PL/SQL 兼容性水平支持您灵活、快速地迁移到 DB2，无需重写您的应用程序。
* **XML 和 NoSQL 支持**：
DB2 是对传统关系数据以及特殊用途的非关系数据类型（比如 XML 和 RDF）的高性能存储和检索的理想选择。
* **基于时间的查询**：
DB2 时态表可用于轻松地找到数据在之前的任何时间点或未来的状态。过去需要花数天时间还原备份镜像才能回答的审计问题，现在使用一个简单查询片刻即可解决。“未来会怎样” 查询同样可以轻松得到处理。
* **同类联盟**：
此功能使您的应用程序能够将所有 DB2 和 Informix 数据库视为单个 DB2 数据库。再辅以一个可单独购买的 DB2 Connect 版本，您还可以为 DB2 for z 和 DB2 for i 数据库建立联盟。
* **备份压缩**：
通过缩小 DB2 数据库备份镜像的大小来降低存储成本。
此外，DB2 提供了两个 Complete Enterprise Option (CEO) 服务产品，它们在设计中充分考虑到了部署灵活性。您可以在必要时部署该集合中的任何组件，以满足您的应用程序需求。这使得应用程序开发人员和安装人员能够为应用程序选择最佳的架构，请求对 IBM 产品的企业级承诺。
* **IBM DB2 CEO**：
此服务产品提供了应用程序的 DB2 基础，在企业资源规划、客户关系管理、B2B 商务和销售力量自动化方面提供了竞争优势。其中的组件包括 DB2 Workgroup Server Edition、DB2 Enterprise Server Edition、DB2 Developer Edition 和 DB2 Connect Enterprise Edition。
* **IBM Advanced DB2 CEO**：
此服务产品通过为您宝贵的信息资产提供一个安全的、富有弹性的信息管理系统，解决如今企业的需求。它提供了丰富的 DB2 数据服务器功能，其中包括 DB2 Advanced Enterprise Server Edition、DB2 Enterprise Server Edition、DB2 Workgroup Server Edition、DB2 Developer Edition 和 DB2 Connect Enterprise Edition。


## 为啥选择 DB2 Express-C

正如上面所述， DB2 Express-C 具有所有版本一样的核心功能，且免费，用来学习 DB2 足够了。本书所演示的例子，也是基于 Express-C 。

## 参考引用

* <http://baike.baidu.com/link?url=srUJcL7gekEhnI5HTYD4bON3KFWV38aIIl4TTK3WaAy7CsinkeUjAGeEfyhrA6Lo2O6P4c7pCwbJxuAGcJyKaa>
* [DB2 版本: 哪个 DB2 10.5 发行版适合您？](http://www.ibm.com/developerworks/cn/data/library/techarticle/dm-1311whichdb2edition/)
