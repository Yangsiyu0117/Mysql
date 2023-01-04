# Mysql

[TOC]

## <u>文档标识</u>

| 文档名称 | Mysql    |
| -------- | -------- |
| 版本号   | <V1.0.0> |

## <u>文档修订历史</u>

| 版本   | 日期       | 描述   | 文档所有者 |
| ------ | ---------- | ------ | ---------- |
| V1.0.0 | 2022.11.23 | create | 杨丝雨     |
|        |            |        |            |
|        |            |        |            |

## <u>路径规划</u>

| 路径                | 描述       | 文件名     | remarks |
| ------------------- | ---------- | ---------- | ------- |
| /var/lib/mysql      | 数据库目录 |            |         |
| /var/log/mysqld.log | 安装日志   | mysqld.log |         |
|                     |            |            |         |

## <u>端口规划</u>

| 端口 | 协议 | remrks   |
| ---- | ---- | -------- |
| 3306 | TCP  | 默认端口 |
|      |      |          |

## <u>相关文档参考</u>

[Mysql5.7中文文档]: https://www.docs4dev.com/docs/zh/mysql/5.7/reference/

## 什么是MySQL

​	MySQL是一个小型关系数据库管理系统，与其他大型数据库管理系统（例如Oracle、DB2、SQL Server等）相比，MySQL规模小、功能有限，但是它体积小、速度快、成本低，且提供的功能对稍微复杂的应用来说已经够用，这些特性使得MySQL成为世界上最受欢迎的开放源代码数据库。

## MySQL版本

针对不同用户，MySQL分为两个不同的版本。

MySQL Community Server（社区版）：该版本完全免费，但是官方不提供技术支持。

MySQL Enterprise Server（企业版服务器）：它能够以很高性价比为企业提供数据仓库应用，支持ACID事物处理，提供完整的提交、回滚、崩溃恢复和行级锁定功能。但是该版本需付费使用，官方提供电话技术支持。

> **提示**
>
> MySQL Cluster主要用于架设集群服务器，需要在社区版或企业版的基础上使用。针对不同的操作系统，读者可以在MySQL官方下载页面（http://dev.mysql.com/downloads/）下载相应的安装文件。

## MySQL的优势

MySQL的主要优势如下：

（1）速度：运行速度快。

（2）价格：MySQL对多数个人来说是免费的。

（3）容易使用：与其他大型数据库的设置和管理相比，其复杂程度较低，易于学习。

（4）可移植性：能够工作在众多不同的系统平台上，例如Windows、Linux、UNIX、Mac OS等。

（5）丰富的接口：提供了用于C、C＋＋、Eiffel、Java、Perl、PHP、Python、Ruby和Tcl等语言的API。

（6）支持查询语言：MySQL可以利用标准SQL语法和支持ODBC（开放式数据库连接）的应用程序。

（7）安全性和连接性：十分灵活和安全的权限和密码系统，允许基于主机的验证。连接到服务器时，所有的密码传输均采用加密形式，从而保证了密码安全。并且由于MySQL是网络化的，因此可以在因特网上的任何地方访问，提高数据共享的效率。

## MySQL 5.7的新特性

和MySQL 5.6相比，MySQL 5.7的新功能主要包括以下几个方面。

1．性能大幅度提升

MySQL 5.7在所有负载模型上都有显著的性能改进，并创造了新的基准测试纪录。MySQL 5.7在Point Select查询测试中，测试成绩是MySQL 5.6的3倍多。

2．支持JSON

JSON（JavaScript Object Notation）是一种存储信息的格式，可以很好地替代XML。从MySQL 5.7将支持JSON，而在此版本之前，只能通过strings之类的通用形式来存储JSON文件，这样做的缺陷很明显，就是必须要自行确认和解析数据、解决更新中的困难或在执行插入操作时忍受较慢的速度。

在MySQL 5.7中，新增了一种新的数据类型，用来在MySQL的表中存储JSON格式的数据。原生支持JSON数据类型主要有如下好处：

（1）文档校验：只有符合JSON规范的数据段才能被写入类型为JSON的列中，相当于有了自动JSON语法校验。

（2）高效访问：在JSON类型的列中存储JSON文档时，数据不会被视为纯文本进行存储，而是以一种优化后的二进制格式进行存储，以便可以更快速地访问其对象成员和数组元素。

（3）提升性能：通过在JSON类型的列上创建索引，可以提升数据查询性能。

3．Performance Schema

对于任何数据管理系统而言，监控是必要的。MySQL提供的核心监控策略是Performance Schema。Performance Schema在MySQL 5.7中的改进包括大量新加入的监控项、降低占用空间和负载、通过新的SYS Schema机制显著地提升易用性。

在监控方面，Performance Schema提供了如下新功能：

（1）元数据锁（Metadata Locking）：任何已经开始的事务将一直持有表的元数据锁直到事务提交。由于开始的事务会持有事务关联的所有表的元数据锁，因此任何DDL操作在前面的事务提交前是不能够执行的。

（2）进度跟踪（Stage Tracking）：长时间跟踪操作的进度。

（3）事务：监控服务层和存储引擎层的事务的全部方面。

（4）内存使用：通过统计内存使用的信息，从而了解内存的消耗情况。

（5）预编译语句：通过预编译语句提供聚合统计信息，并且展示服务使用的预编译语句。

4．SYS Schema

MySQL SYS Schema是一个由一系列对象（视图、存储过程、存储方法、表和触发器）组成的数据Schema，主要存储在Performance Schema和INFORMATION_SCHEMA的监测数据资源中。MySQL SYS Schema默认包含在MySQL 5.7中，并提供摘要视图以解决以下问题：

（1）哪些进程占用了数据库的所有资源？

（2）哪些主机对数据库服务器的访问量最大？

（3）数据库实例上的内存都被用到了什么地方？

5．性能和可扩展性

改进InnoDB的可扩展性和临时表的性能，从而实现更快的网络和大数据加载等操作。

6．改进复制以提高可用性的性能

包括多源复制、增强多从线程功能、在线GTIDs和增强的半同步复制。

7．性能模式提供更好的视角

增加了许多新的监控功能，以减少空间和过载，使用新的SYS模式显著提高易用性。

8．提高安全

以安全第一为宗旨，提供了很多新的功能，从而保证数据库的安全。

9．优化

重写了大部分解析器、优化器和成本模型，提高了可维护性、可扩展性和性能。

10．透明的页级别压缩

自MySQL 5.1开始，InnoDB支持表压缩特性。InnoDB页级别的压缩是MySQL5.7的一个新特性，它补充了InnoDB的表级压缩，它们可以在同一个服务实例上并存。用户现在可以选择最适合他们使用场景的压缩方式，甚至基于不同的表选择不同的压缩方式。

对于压缩算法，目前支持Zlib和LZ4。当一个页被写入时，它就被指定的压缩算法压缩。压缩后的数据写到磁盘上，随后“hole punching”机制会在页的末尾处释放空块。如果压缩失败，数据则被原样写入。

InnoDB现在也支持32KB和64KB的页大小设置，这对于页级的压缩来说是一个很好的补充。一般来说，更大的页通常会增加冗余的数据量。MySQL 5.7增加了用户可配置填充因子和页合并抑制的新特性，这样可以让InnoDB更好地使用存储空间。

11．本地分区

在早期版本中，对InnoDB分区的支持依赖于ha_partition处理器，这个处理器可以为每一个分区创建一个新的处理器，当使用很多分区时，这个处理器也相应地浪费了很多资源。

在MySQL 5.7 InnoDB中包含对本地分区的支持，可以使用更少的整体资源。InnoDB的本地分区也为较好地整体分区铺平了道路。这包含并行查询进程、改进分区裁剪、外键支持、全局二级索引和在分区表上的全文本搜索之类的功能。作为这项工作的一部分，也已经从分区处理器类中的特性部分分离出了它自己的分区接口。InnoDB本地分区功能可以明显降低负载，减少多达90%的内存需求。

12．缓存保留

在MySQL 5.7服务器重启时，InnoDB自动保留缓存池中最热的25%的数据。这样的好处是，用户不需要任何预加载或预热数据缓存的工作，也不需要承担MySQL重启带来的性能损失。
MySQL命令行实用程序
MySQL服务器端实用工具程序如下。

（1）mysqld: SQL后台程序（MySQL服务器进程）。必须在该程序运行之后，客户端才能通过连接服务器访问数据库。

（2）mysqld_safe：服务器启动脚本。在UNIX和NetWare中推荐使用mysqld_safe来启动mysqld服务器。mysqld_safe增加了一些安全特性，例如当出现错误时重启服务器并向错误日志文件写入运行时间信息。

（3）mysql.server：服务器启动脚本。在UNIX中的MySQL分发版包括mysql.server脚本。该脚本用于使用包含为特定级别的、运行启动服务的脚本的、运行目录的系统。它调用mysqld_safe来启动MySQL服务器。

（4）mysql_multi：服务器启动脚本，可以启动或停止系统上安装的多个服务器。

（5）myisamchk：用来描述、检查、优化和维护MyISAM表的实用工具。

（6）mysqlbug: MySQL缺陷报告脚本。它可以用来向MySQL邮件系统发送缺陷报告。

（7）mysql_install_db：该脚本用默认权限创建MySQL授权表。通常只是在系统上首次安装MySQL时执行一次。

## MySQL客户端实用工具程序

（1）myisampack：压缩MyISAM表以产生更小的只读表的一个工具。

（2）mysql：交互式输入SQL语句或从文件以批处理模式执行它们的命令行工具。

（3）mysqlaccess：检查访问主机名、用户名和数据库组合的权限的脚本。

（4）mysqladmin：执行管理操作的客户程序，例如创建或删除数据库、重载授权表、将表刷新到硬盘上以及重新打开日志文件。mysqladmin还可以用来检索版本、进程以及服务器的状态信息。

（5）mysqlbinlog：从二进制日志读取语句的工具。在二进制日志文件中包含执行过的语句，可用来帮助系统从崩溃中恢复。

（6）mysqlcheck：检查、修复、分析以及优化表的表维护客户程序。

（7）mysqldump：将MySQL数据库转储到一个文件（例如SQL语句或tab分隔符文本文件）的客户程序。

（8）mysqlhotcopy：当服务器在运行时，快速备份MyISAM或ISAM表的工具。

（9）mysql import：使用LOAD DATA INFILE将文本文件导入相关表的客户程序。

（10）mysqlshow：显示数据库、表、列以及索引相关信息的客户程序。

（11）perror：显示系统或MySQL错误代码含义的工具。

## Mysql5.7安装

> CentOS 7的默认yum仓库中并没有MySQL5.7，我们需要手动添加，好在MySQL官方提供了仓库的地址，所以我们能够比较简单地安装MySQL。

### 1、添加Mysql5.7仓库

```shell
sudo rpm -ivh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
```

### 2、确认Mysql仓库成功添加

```shell
sudo yum repolist all | grep mysql | grep enabled
```

如果展示像下面,则表示成功添加仓库:

```shell
mysql-connectors-community/x86_64  MySQL Connectors Community    enabled:     51
mysql-tools-community/x86_64       MySQL Tools Community         enabled:     63
mysql57-community/x86_64           MySQL 5.7 Community Server    enabled:    267
```

需要import mysql的公钥到RPM的配置中

```shell
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
```

### 3、开始安装Mysql5.7

```shell
sudo yum -y install mysql-community-server
```

### 4、启动Mysql

1、启动

```bash
sudo systemctl start mysqld
```

2、设置系统启动时自动启动

```bash
sudo systemctl enable mysqld
```

3、查看启动状态

```bash
sudo systemctl status mysqld
```

### 5、Mysql的安全设置

CentOS上的root默认密码可以在文件/var/log/mysqld.log找到，通过下面命令可以打印出来

```shell
cat /var/log/mysqld.log | grep -i 'temporary password'
```

执行下面命令进行安全设置，这个命令会进行设置root密码设置，移除匿名用户，禁止root用户远程连接等

```shell
mysql_secure_installation
```

### 6、设置数据库编码为utf8

1、打开配置文件

```
sudo vim /etc/my.cnf
```

2、在[mysqld]，[client]，[mysql]节点下添加编码设置

```shell
[client]
default-character-set=utf8

[mysql]
default-character-set=utf8

[mysqld]
collation-server = utf8_unicode_ci
init-connect='SET NAMES utf8'
character-set-server = utf8
```

3、重启Mysql即可

```shell
sudo systemctl restart mysqld
```

## Msql5.7配置文件详解

```shell
[client]
default-character-set = utf8mb4

[mysql]
#开启 tab 补全
#auto-rehash
default-character-set = utf8mb4

[mysqld]
port=3306
basedir=/data/server/mysql57/
datadir=/data/server/mysql57/data/
socket=/data/server/mysql57/data/mysql.sock
symbolic-links=0
log-error=/data/logs/mysql57/mysqld.log
pid-file=/data/server/mysql57/data/mysqld57.pid

# 禁用主机名解析
skip-name-resolve
# 默认的数据库引擎
default-storage-engine = InnoDB
innodb-file-per-table=1innodb_force_recovery = 1#一些坑
group_concat_max_len = 10240sql_mode=expire_logs_days = 7memlock

### 字符集配置
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
init_connect='SET NAMES utf8mb4'### GTID
server_id = 330759# 为保证 GTID 复制的稳定, 行级日志
binlog_format = row
# 开启 gtid 功能
gtid_mode = on
# 保障 GTID 事务安全
# 当启用enforce_gtid_consistency功能的时候,
# MySQL只允许能够保障事务安全, 并且能够被日志记录的SQL语句被执行,
# 像create table ... select 和 create temporarytable语句, 
# 以及同时更新事务表和非事务表的SQL语句或事务都不允许执行
enforce-gtid-consistency = true# 以下两条配置为主从切换, 数据库高可用的必须配置
# 开启 binlog 日志功能
log_bin = mysql57-bin 
# 开启从库更新 binlog 日志
log-slave-updates = on
#slave复制进程不随mysql启动而启动
skip_slave_start=1### 慢查询日志
# 打开慢查询日志功能
slow_query_log = 1# 超过2秒的查询记录下来
long_query_time = 2# 记录下没有使用索引的查询
log_queries_not_using_indexes = 0slow_query_log_file =/data/logs/mysql57/slow.log
#log=/data/logs/mysql57/all.log
### 自动修复
# 记录 relay.info 到数据表中
relay_log_info_repository = TABLE
# 记录 master.info 到数据表中 
master_info_repository = TABLE
# 启用 relaylog 的自动修复功能
relay_log_recovery = on
# 在 SQL 线程执行完一个 relaylog 后自动删除
relay_log_purge = 1### 数据安全性配置
# wei关闭 master 创建 function 的功能
log_bin_trust_function_creators = on
# 每执行一个事务都强制写入磁盘
sync_binlog = 1# timestamp 列如果没有显式定义为 not null, 则支持null属性
# 设置 timestamp 的列值为 null, 不会被设置为 current timestamp
explicit_defaults_for_timestamp=true### 优化配置
# 优化中文全文模糊索引
ft_min_word_len = 1# 默认库名表名保存为小写, 不区分大小写
lower_case_table_names = 1# 单条记录写入最大的大小限制
# 过小可能会导致写入(导入)数据失败
max_allowed_packet = 256M
# 半同步复制开启
#rpl_semi_sync_master_enabled = 1#rpl_semi_sync_slave_enabled = 1# 半同步复制超时时间设置
#rpl_semi_sync_master_timeout = 1000# 复制模式(保持系统默认)
#rpl_semi_sync_master_wait_point = AFTER_SYNC
# 后端只要有一台收到日志并写入 relaylog 就算成功
#rpl_semi_sync_master_wait_slave_count = 1# 多线程复制
# 基于组提交的并行复制方式
slave_parallel_type = logical_clock
#并行的SQL线程数量，此参数只有设置   1<N的情况下才会才起N个线程进行SQL重做。
#经过测试对比发现， 如果主库的连接线程为M， 只有M < N的情况下， 备库的延迟才可以完全避免。
slave_parallel_workers = 4### 连接数限制
max_connections = 1500# 验证密码超过20次拒绝连接
max_connect_errors = 200# back_log值指出在mysql暂时停止回答新请求之前的短时间内多少个请求可以被存在堆栈中
# 也就是说，如果MySql的连接数达到max_connections时，新来的请求将会被存在堆栈中
# 以等待某一连接释放资源，该堆栈的数量即back_log，如果等待连接的数量超过back_log
# 将不被授予连接资源
back_log = 500open_files_limit = 65535# 服务器关闭交互式连接前等待活动的秒数
interactive_timeout = 3600# 服务器关闭非交互连接之前等待活动的秒数
wait_timeout = 3600### 内存分配
# 指定表高速缓存的大小。每当MySQL访问一个表时，如果在表缓冲区中还有空间
# 该表就被打开并放入其中，这样可以更快地访问表内容
table_open_cache = 1024# 为每个session 分配的内存, 在事务过程中用来存储二进制日志的缓存
binlog_cache_size = 4M
# 在内存的临时表最大大小
tmp_table_size = 128M
# 创建内存表的最大大小(保持系统默认, 不允许创建过大的内存表)
# 如果有需求当做缓存来用, 可以适当调大此值
max_heap_table_size = 16M
# 顺序读, 读入缓冲区大小设置
# 全表扫描次数多的话, 可以调大此值
read_buffer_size = 1M
# 随机读, 读入缓冲区大小设置
read_rnd_buffer_size = 8M
# 高并发的情况下, 需要减小此值到64K-128K
sort_buffer_size = 1M
# 每个查询最大的缓存大小是1M, 最大缓存64M 数据
query_cache_size = 64M
query_cache_limit = 1M
# 提到 join 的效率
join_buffer_size = 16M
# 线程连接重复利用
thread_cache_size = 64### InnoDB 优化
## 内存利用方面的设置
# 数据缓冲区
innodb_buffer_pool_size=2G
## 日志方面设置
# 事务日志大小
innodb_log_file_size = 256M
# 日志缓冲区大小
innodb_log_buffer_size = 4M
# 事务在内存中的缓冲
innodb_log_buffer_size = 3M
# 主库保持系统默认, 事务立即写入磁盘, 不会丢失任何一个事务
innodb_flush_log_at_trx_commit = 1# mysql 的数据文件设置, 初始100, 以10M 自动扩展
#innodb_data_file_path = ibdata1:100M:autoextend
# 为提高性能, MySQL可以以循环方式将日志文件写到多个文件
innodb_log_files_in_group = 3##其他设置
# 如果库里的表特别多的情况，请增加此值
#innodb_open_files = 800# 为每个 InnoDB 表分配单独的表空间
innodb_file_per_table = 1# InnoDB 使用后台线程处理数据页上写 I/O（输入）请求的数量
innodb_write_io_threads = 8# InnoDB 使用后台线程处理数据页上读 I/O（输出）请求的数量
innodb_read_io_threads = 8# 启用单独的线程来回收无用的数据
innodb_purge_threads = 1# 脏数据刷入磁盘(先保持系统默认, swap 过多使用时, 调小此值, 调小后, 与磁盘交互增多, 性能降低)
 innodb_max_dirty_pages_pct = 90# 事务等待获取资源等待的最长时间
innodb_lock_wait_timeout = 120# 开启 InnoDB 严格检查模式, 不警告, 直接报错 1开启 0关闭
innodb_strict_mode=1# 允许列索引最大达到3072
 innodb_large_prefix = on

[mysqldump]
# 开启快速导出
quick
default-character-set = utf8mb4
max_allowed_packet = 256M

```

## 安裝 Docker & Docker-compose

```shell
yum install -y yum-utils
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum update
yum install docker-ce docker-ce-cli containerd.io.
sudo systemctl enable docker
sudo systemctl start docker
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

查找MySQL镜像：

```shell
docker search mysql
```

拉起MySQL镜像(:5.7 表示5.7版本)

```shell
docker pull mysql:5.7
```

运行MySQL容器

```shell
docker run -d -p 3306:3306 --privileged=true -v /docker/mysql/conf/my.cnf:/etc/my.cnf -v /docker/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql mysql:5.7 --character-set-server=utf8mb4 --collation-server=utf8mb4_general_ci
```

参数说明:

- run　run 是运行一个容器
- -d　 表示后台运行
- -p　 表示容器内部端口和服务器端口映射关联
- --privileged=true　设值MySQL 的root用户权限, 否则外部不能使用root用户登陆
- -v /docker/mysql/conf/my.cnf:/etc/my.cnf 将服务器中的my.cnf配置映射到docker中的/docker/mysql/conf/my.cnf配置
- -v /docker/mysql/data:/var/lib/mysql　　同上,映射数据库的数据目录, 避免以后docker删除重新运行MySQL容器时数据丢失
- -e MYSQL_ROOT_PASSWORD=123456　　　设置MySQL数据库root用户的密码
- --name mysql　　　　 设值容器名称为mysql
- mysql:5.7　　表示从docker镜像mysql:5.7中启动一个容器
- --character-set-server=utf8mb4 --collation-server=utf8mb4_general_ci 设值数据库默认编码

进入容器

```shell
docker exec -it mysql bash
```



## 集群架构设计理念

集群在合计时，主要准从三个维度

1. 可用性
2. 扩展性
3. 一致性

### 可用性设计

> 站点高可用，冗余站点
>
> 服务高可用，冗余服务
>
> 数据高可用，冗余数据

保证高可用的方法就是冗余。但是数据冗余带来的问题就是数据一致性问题。
实现高可用的方案有以下几种架构模式

1、主从模式

> 简单灵活，能满足各种需求，。比较主流的用法，但是写操作的高可用需要自行处理

2、双主模式

> 互为主从，有双主双从，双主单从两张方式，建议使用双主单从

### 扩展性设计

扩展性主要围绕着读操作扩展和写操作扩展展开。

如何扩展以提高读性能

> 加从库，简单易操作，方案成熟。
> 从库过多会引发主库性能损耗。建议不要作为长期的扩充方案，应该设法用良好的设计避免持续加从库来缓解读性能问题。

分库分表

> 可以分为垂直拆分和水平拆分，垂直拆分可以缓解部分压力，水平拆分理论上可以无限扩展。

如何扩展以提高写性能

> 分库分表

### 一致性设计

一致性主要考虑集群中各数据库数据同步以及同步延迟问题。可以采用的方案如下：

不使用从库

> 扩展读性能问题需要单独考虑，否则容易出现系统瓶颈。

增加访问路由层

> 可以先得到主从同步最长时间t，在数据发生修改后的t时间内，先访问主库。

## 主从模式

MySQL主从模式是指数据可以从一个MySQL数据库服务器主节点复制到一个或多个从节点。MySQL 默认采用**异步复制**方式，这样从节点不用一直访问主服务器来更新自己的数据，从节点可以复制主数据库中的所有数据库，或者特定的数据库，或者特定的表。

mysql主从复制用途：

> 实时灾备，用于故障切换（高可用）
> 读写分离，提供查询服务（读扩展）
> 数据备份，避免影响业务（高可用）

主从部署必要条件：

> 从库服务器可以连通主库
> 主库开启binlog日志（设置log-bin参数）
> 主从的server-id不同

### 实现原理

![image.png](https://www.rsthe.com/upload/2022/04/image-55c18b914ce14a9f96d356a2d91c820f.png)

主从复制整体分为以下三个步骤：

1. 主库将数据库的变更操作记录到Binlog日志文件中
2. 从库读取主库中的Binlog日志文件信息写入到从库的Relay Log中继日志中
3. 从库读取中继日志信息在从库中进行Replay,更新从库数据信息

在上述三个过程中，涉及了`Master`的**BinlogDump Thread**和`Slave`的**I/O Thread**、**SQL Thread**，它们的作用如下：

> Master服务器对数据库更改操作记录在Binlog中，BinlogDump Thread接到写入请求后，读取Binlog信息推送给Slave的I/O Thread。
>
> Slave的I/O Thread将读取到的Binlog信息写入到本地Relay Log中。
>
> Slave的SQL Thread检测到Relay Log的变更请求，解析relay log中内容在从库上执行。

异步复制时序图

![image.png](https://www.rsthe.com/upload/2022/04/image-62b7b176ef9b426f827c321d57c2a1a4.png)

### 并行复制

MySQL的主从复制延迟一直是受开发者最为关注的问题之一，MySQL从5.6版本开始追加了并行复制功能，目的就是为了改善复制延迟问题，并行复制称为enhanced multi-threaded slave（简称MTS）。
在从库中有两个线程IO Thread和SQL Thread，都是单线程模式工作，因此有了延迟问题，我们可以采用多线程机制来加强，减少从库复制延迟。（IO Thread多线程意义不大，主要指的是SQL Thread多线程）
在MySQL的5.6、5.7、8.0版本上，都是基于上述SQL Thread多线程思想，不断优化，减少复制延迟。

MySQL 5.7并行复制原理

> MySQL 5.7是基于组提交的并行复制，MySQL 5.7才可称为真正的并行复制，这其中最为主要的原因就是slave服务器的回放与master服务器是一致的，即master服务器上是怎么并行执行的slave上就怎样进行并行回放。不再有库的并行复制限制。

MySQL 5.7中组提交的并行复制究竟是如何实现的？

> MySQL 5.7是通过对事务进行分组，当事务提交时，它们将在单个操作中写入到二进制日志中。如果多个事务能同时提交成功，那么它们意味着没有冲突，因此可以在Slave上并行执行，所以通过在主库上的二进制日志中添加组提交信息。
>
> MySQL 5.7的并行复制基于一个前提，即所有已经处于prepare阶段的事务，都是可以并行提交的。这些当然也可以在从库中并行提交，因为处理这个阶段的事务都是没有冲突的。在一个组里提交的事务，一定不会修改同一行。这是一种新的并行复制思路，完全摆脱了原来一直致力于为了防止冲突而做的分发算法，等待策略等复杂的而又效率底下的工作。
>
> InnoDB事务提交采用的是两阶段提交模式。一个阶段是prepare，另一个是commit。
>
> 为了兼容MySQL5.6基于库的并行复制，5.7引入了新的变量slave-parallel-type，其可以配置的值有：DATABASE（默认值，基于库的并行复制方式）、LOGICAL_CLOCK（基于组提交的并行复制方式）。

那么如何知道事务是否在同一组中，生成的Binlog内容如何告诉Slave哪些事务是可以并行复制的？

> 在MySQL 5.7版本中，其设计方式是将组提交的信息存放在GTID中。为了避免用户没有开启GTID功能（gtid_mode=OFF），MySQL 5.7又引入了称之为Anonymous_Gtid的二进制日志event类型ANONYMOUS_GTID_LOG_EVENT。

通过mysqlbinlog工具分析binlog日志，就可以发现组提交的内部信息。
![image.png](https://www.rsthe.com/upload/2022/04/image-fdb17fd396a948ae9c6f8a66c29284dd.png)

可以发现MySQL 5.7二进制日志较之原来的二进制日志内容多了last_committed和sequence_number，last_committed表示事务提交的时候，上次事务提交的编号，如果事务具有相同的last_committed，表示这些事务都在一组内，可以进行并行的回放。

并行复制配置与调优

> binlog_transaction_dependency_history_size
> 用于控制集合变量的大小。

> binlog_transaction_depandency_tracking
> 用于控制binlog文件中事务之间的依赖关系，即last_committed值。
> COMMIT_ORDERE: 基于组提交机制
> WRITESET: 基于写集合机制
> WRITESET_SESSION: 基于写集合，比writeset多了一个约束，同一个session中的事务last_committed按先后顺序递增

> transaction_write_set_extraction
> 用于控制事务的检测算法，参数值为：OFF、 XXHASH64、MURMUR32

> master_info_repository
> 开启MTS功能后，务必将参数master_info_repostitory设置为TABLE，这样性能可以有50%~80%的提升。这是因为并行复制开启后对于元master.info这个文件的更新将会大幅提升，资源的竞争也会变大。

> slave_parallel_workers
> 若将slave_parallel_workers设置为0，则MySQL 5.7退化为原单线程复制，但将slave_parallel_workers设置为1，则SQL线程功能转化为coordinator线程，但是只有1个worker线程进行回放，也是单线程复制。然而，这两种性能却又有一些的区别，因为多了一次coordinator线程的转发，因此slave_parallel_workers=1的性能反而比0还要差。

> slave_preserve_commit_order
> MySQL 5.7后的MTS可以实现更小粒度的并行复制，但需要将slave_parallel_type设置为LOGICAL_CLOCK，但仅仅设置为LOGICAL_CLOCK也会存在问题，因为此时在slave上应用事务的顺序是无序的，和relay log中记录的事务顺序不一样，这样数据一致性是无法保证的，为了保证事务是按照relay log中记录的顺序来回放，就需要开启参数slave_preserve_commit_order。
> 要开启enhanced multi-threaded slave其实很简单，只需根据如下设置：

```
slave-parallel-type=LOGICAL_CLOCK
slave-parallel-workers=16
slave_pending_jobs_size_max = 2147483648
slave_preserve_commit_order=1
master_info_repository=TABLE
relay_log_info_repository=TABLE
relay_log_recovery=ON
```

并行复制监控
在使用了MTS后，复制的监控依旧可以通过SHOW SLAVE STATUS\G，但是MySQL 5.7在performance_schema库中提供了很多元数据表，可以更详细的监控并行复制过程。
![image.png](https://www.rsthe.com/upload/2022/04/image-532f5df8ef9b4e17aa3af167f5bab23f.png)

通过replication_applier_status_by_worker可以看到worker进程的工作情况：

![image.png](https://www.rsthe.com/upload/2022/04/image-f9c4199642374adeafd8eaf10c215115.png)

最后，如果MySQL 5.7要使用MTS功能，建议使用新版本，最少升级到5.7.19版本，修复了很多Bug。

### 读写分离

大多数互联网业务中，往往读多写少，这时候数据库的读会首先成为数据库的瓶颈。如果我们已经优化了SQL，但是读依旧还是瓶颈时，这时就可以选择“读写分离”架构了。
读写分离首先需要将数据库分为主从库，一个主库用于写数据，多个从库完成读数据的操作，主从库之间通过主从复制机制进行数据的同步，如图所示。

![image.png](https://www.rsthe.com/upload/2022/04/image-f2990106b4534fa584e0c39dd74bce21.png)

> 在应用中可以在从库追加多个索引来优化查询，主库这些索引可以不加，用于提升写效率。
> 读写分离架构也能够消除读写锁冲突从而提升数据库的读写性能。使用读写分离架构需要注意：主从同步延迟和读写分配机制问题

主从同步延迟
使用读写分离架构时，数据库主从同步具有延迟性，数据一致性会有影响，对于一些实时性要求比较高的操作，可以采用以下解决方案。

> 写后立刻读
> 在写入数据库后，某个时间段内读操作就去主库，之后读操作访问从库。

> 二次查询
> 先去从库读取数据，找不到时就去主库进行数据读取。该操作容易将读压力返还给主库，为了避免恶意攻击，建议对数据库访问API操作进行封装，有利于安全和低耦合。

> 根据业务特殊处理
> 根据业务特点和重要程度进行调整，比如重要的，实时性要求高的业务数据读写可以放在主库。对于次要的业务，实时性要求不高可以进行读写分离，查询时去从库查询。

读写分离落地
读写路由分配机制是实现读写分离架构最关键的一个环节，就是控制何时去主库写，何时去从库读。目前较为常见的实现方案分为以下两种：

1. 基于编程和配置实现（应用端）

> 程序员在代码中封装数据库的操作，代码中可以根据操作类型进行路由分配，增删改时操作主库，查询时操作从库。这类方法也是目前生产环境下应用最广泛的。优点是实现简单，因为程序在代码中实现，不需要增加额外的硬件开支，缺点是需要开发人员来实现，运维人员无从下手，如果其中一个数据库宕机了，就需要修改配置重启项目。

1. 基于服务器端代理实现（服务器端）

![image.png](https://www.rsthe.com/upload/2022/04/image-674fd0f9410f425a927f471f79df2d63.png)

> 中间件代理一般介于应用服务器和数据库服务器之间，从图中可以看到，应用服务器并不直接进入到master数据库或者slave数据库，而是进入MySQL proxy代理服务器。代理服务器接收到应用服务器的请求后，先进行判断然后转发到后端master和slave数据库。
> 目前有很多性能不错的数据库中间件，常用的有MySQL Proxy、MyCat以及Shardingsphere等等。
>
> MySQL Proxy：是官方提供的MySQL中间件产品可以实现负载平衡、读写分离等。
> MyCat：MyCat是一款基于阿里开源产品Cobar而研发的，基于 Java 语言编写的开源数据库中间件。
> ShardingSphere：ShardingSphere是一套开源的分布式数据库中间件解决方案，它由ShardingJDBC、Sharding-Proxy和Sharding-Sidecar（计划中）这3款相互独立的产品组成。已经在2020年4月16日从Apache孵化器毕业，成为Apache顶级项目。
> Atlas：Atlas是由 Qihoo 360公司Web平台部基础架构团队开发维护的一个数据库中间件。
> Amoeba：变形虫，该开源框架于2008年开始发布一款 Amoeba for MySQL软件。

### 主从复制配置

#### Master配置

```shell
#Server ID，一般设置成IP地址的最后一位
server_id=52
#开启log bin，名字最好有意义用来区分
log-bin=dev-bin
#需要进行复制的数据库，可以指定数据库,这里我注释掉不用
#binlog-do-db=DB_master
#不需要备份的数据库，可以设置多个数据库，一般不会同步mysql这个库
binlog-ignore-db=mysql
binlog-ignore-db=information_schema
binlog-ignore-db=performance_schema
#为每个session 分配的内存，在事务过程中用来存储二进制日志的缓存
 binlog_cache_size=1m
 #二进制日志自动删除/过期的天数。默认值为0，表示不自动删除。
 expire_logs_days=7
# 跳过主从复制中遇到的所有错误或指定类型的错误，避免slave端复制中断。
# 如：1062错误是指一些主键重复，1032错误是因为主从数据库数据不一致
slave_skip_errors=1062
```

```shell
# 登陆mysql，给从服务器授权可以复制的权限
[root@master ~]# mysql -uroot -p
mysql> GRANT REPLICATION SLAVE ON *.* TO 'myslave'@'192.168.245.%' IDENTIFIED BY '123456'; //让从服务器可以复制
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

# 查看主服务器的日志文件和状态点
mysql> show master status;
+-------------------+----------+--------------+------------------+-------------------+
| File              | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+-------------------+----------+--------------+------------------+-------------------+
| master-bin.000001 |      604 |              |                  |                   |
+-------------------+----------+--------------+------------------+-------------------+
1 row in set (0.00 sec)
```

### Slave配置

```shell
server_id=9
#binlog-ignore-db=mydql
#binlog-ignore-db=information_schema
#binlog-ignore-db=performance_schema
#log-bin=dev-slave-bin
binlog_cache_size=1M
binlog_format=mixed
expire_logs_days=7
slave_skip_errors=1062
relay_log=dev-relay-bin
#log_slave_updates=1
read_only=1
```

```shell
# 登陆数据库，设置复制同步的masterip地址，用户名密码和日志文件、状态点
[root@slave1 ~]# mysql -uroot -p
mysql> change master to master_host='192.168.245.204',master_user='myslave',master_password='123456',master_log_file='master-bin.000001',master_log_pos=604;
Query OK, 0 rows affected, 2 warnings (0.02 sec)

mysql> start slave;      <------开启slave
Query OK, 0 rows affected (0.00 sec)

mysql> show slave status \G;    <------查看slave状态
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: 192.168.245.204
                  Master_User: myslave
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: master-bin.000001
          Read_Master_Log_Pos: 604
               Relay_Log_File: relay-log-bin.000002
                Relay_Log_Pos: 321
        Relay_Master_Log_File: master-bin.000001
             Slave_IO_Running: Yes      <------yes为正常状态
            Slave_SQL_Running: Yes      <------yes为正常状态
        
```

### 读写分离配置

> mysql 5.7 Amoeba

## 双主模式

### 适用场景

很多企业刚开始都是使用MySQL主从模式，一主多从、读写分离等。但是单主如果发生单点故障，从库切换成主库还需要作改动。因此，如果是双主或者多主，就会增加MySQL入口，提升了主库的可用性。因此随着业务的发展，数据库架构可以由主从模式演变为双主模式。双主模式是指两台服务器互为主从，任何一台服务器数据变更，都会通过复制应用到另外一方的数据库中。

![image.png](https://www.rsthe.com/upload/2022/04/image-1dcd4645471040ec9e3c2e93c88d1134.png)

使用双主双写还是双主单写？
建议大家使用双主单写，因为双主双写存在以下问题：

1. ID冲突

> 在A主库写入，当A数据未同步到B主库时，对B主库写入，如果采用自动递增容易发生ID主键的冲突。
> 可以采用MySQL自身的自动增长步长来解决，例如A的主键为1,3,5,7…，B的主键为2,4,6,8… ，但是对数据库运维、扩展都不友好。

1. 更新丢失

> 同一条记录在两个主库中进行更新，会发生前面覆盖后面的更新丢失。

高可用架构如下图所示，其中一个Master提供线上服务，另一个Master作为备胎供高可用切换，Master下游挂载Slave承担读请求。

![image.png](https://www.rsthe.com/upload/2022/04/image-86f04b3fddb540bc8b9bc87b5075f28a.png)

随着业务发展，架构会从主从模式演变为双主模式，建议用双主单写，再引入高可用组件，例如Keepalived和MMM等工具，实现主库故障自动切换。

### MMM架构

MMM（Master-Master Replication Manager for MySQL）是一套用来管理和监控双主复制，支持双主故障切换 的第三方软件。MMM 使用Perl语言开发，虽然是双主架构，但是业务上同一时间只允许一个节点进行写入操作。下图是基于MMM实现的双主高可用架构。

![image.png](https://www.rsthe.com/upload/2022/04/image-e78aefa0df3d4d6fba582614b32cd80b.png)

MMM故障处理机制
MMM 包含`writer`和`reader`两类角色，分别对应**写节点**和**读节点**

> 当 writer节点出现故障，程序会自动移除该节点上的VIP
> 写操作切换到 Master2，并将Master2设置为writer

> 将所有Slave节点会指向Master2
> 除了管理双主节点，MMM 也会管理 Slave 节点，在出现宕机、复制延迟或复制错误，MMM 会移除该节点的 VIP，直到节点恢复正常。

MMM监控机制
MMM 包含monitor和agent两类程序，功能如下：

1. monitor：监控集群内数据库的状态，在出现异常时发布切换命令，一般和数据库分开部署。
2. agent：运行在每个 MySQL 服务器上的代理进程，monitor 命令的执行者，完成监控的探针工作和具体服务设置，例如设置 VIP（虚拟IP）、指向新同步节点。

### MHA架构

MHA（Master High Availability）是一套比较成熟的 MySQL 高可用方案，也是一款优秀的故障切换和主从提升的高可用软件。在MySQL故障切换过程中，MHA能做到在30秒之内自动完成数据库的故障切换操作，并且在进行故障切换的过程中，MHA能在最大程度上保证数据的一致性，以达到真正意义上的高可用。MHA还支持在线快速将Master切换到其他主机，通常只需0.5－2秒。
目前MHA主要支持一主多从的架构，要搭建MHA，要求一个复制集群中必须最少有三台数据库服务器。
![image.png](https://www.rsthe.com/upload/2022/04/image-c81278427d08411e9391db61b6f832d4.png)

MHA由两部分组成：`MHA Manager（管理节点）`和`MHA Node（数据节点）`。

> `MHA Manager`可以单独部署在一台独立的机器上管理多个`master-slave`集群，也可以部署在一台slave节点上。负责检测master是否宕机、控制故障转移、检查MySQL复制状况等。
> `MHA Node`运行在每台MySQL服务器上，不管是Master角色，还是Slave角色，都称为`Node`，是被监控管理的对象节点，负责保存和复制master的二进制日志、识别差异的中继日志事件并将其差异的事件应用于其他的slave、清除中继日志。
> `MHA Manager`会定时探测集群中的master节点，当master出现故障时，它可以自动将最新数据的slave提升为新的master，然后将所有其他的slave重新指向新的master，整个故障转移过程对应用程序完全透明。
> MHA故障处理机制：

> 把宕机master的binlog保存下来
> 根据binlog位置点找到最新的slave
> 用最新slave的relay log修复其它slave
> 将保存下来的binlog在最新的slave上恢复
> 将最新的slave提升为master
> 将其它slave重新指向新提升的master，并开启主从复制

MHA优点：

> 自动故障转移快
> 主库崩溃不存在数据一致性问题
> 性能优秀，支持半同步复制和异步复制
> 一个Manager监控节点可以监控多个集群

### 主备切换

主备切换是指将备库变为主库，主库变为备库，有可靠性优先和可用性优先两种策略。

主备延迟问题
主备延迟是由主从数据同步延迟导致的，与数据同步有关的时间点主要包括以下三个：

> 主库 A 执行完成一个事务，写入 binlog，我们把这个时刻记为 T1;
> 之后将binlog传给备库 B，我们把备库 B 接收完 binlog 的时刻记为 T2;
> 备库 B 执行完成这个binlog复制，我们把这个时刻记为 T3。
> 所谓主备延迟，就是同一个事务，在备库执行完成的时间和主库执行完成的时间之间的差值，也就是 T3-T1。
> 在备库上执行show slave status命令，它可以返回结果信息，seconds_behind_master表示当前备库延迟了多少秒。
> 同步延迟主要原因如下：

备库机器性能问题

> 机器性能差，甚至一台机器充当多个主库的备库。

分工问题

> 备库提供了读操作，或者执行一些后台分析处理的操作，消耗大量的CPU资源。

大事务操作

> 大事务耗费的时间比较长，导致主备复制时间长。比如一些大量数据的delete或大表DDL操作都可能会引发大事务。

可靠性优先

> 主备切换过程一般由专门的HA高可用组件完成，但是切换过程中会存在短时间不可用，因为在切换过程中某一时刻主库A和从库B都处于只读状态。如下图所示：
> ![image.png](https://www.rsthe.com/upload/2022/04/image-f414c80f3842423aa0f7ab995903d4d5.png)

主库由A切换到B，切换的具体流程如下：

> 判断从库B的Seconds_Behind_Master值，当小于某个值才继续下一步
> 把主库A改为只读状态（readonly=true）
> 等待从库B的Seconds_Behind_Master值降为 0
> 把从库B改为可读写状态（readonly=false）
> 把业务请求切换至从库B

可用性优先
不等主从同步完成， 直接把业务请求切换至从库B ，并且让 从库B可读写 ，这样几乎不存在不可用时间，但可能会数据不一致。
![image.png](https://www.rsthe.com/upload/2022/04/image-653185114359416e849fcd44de1ce7c1.png)

如上图所示，在A切换到B过程中，执行两个INSERT操作，过程如下：

> 主库A执行完 INSERT c=4 ，得到 (4,4) ，然后开始执行 主从切换
> 主从之间有5S的同步延迟，从库B会先执行 INSERT c=5 ，得到 (4,5)
> 从库B执行主库A传过来的binlog日志 INSERT c=4 ，得到 (5,4)
> 主库A执行从库B传过来的binlog日志 INSERT c=5 ，得到 (5,5)
> 此时主库A和从库B会有 两行 不一致的数据

通过上面介绍了解到，主备切换采用可用性优先策略，由于可能会导致数据不一致，所以大多数情况下，优先选择可靠性优先策略。在满足数据可靠性的前提下，MySQL的可用性依赖于同步延时的大小，同步延时越小，可用性就越高。