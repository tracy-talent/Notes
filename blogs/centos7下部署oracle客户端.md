# centos7下部署oracle客户端

## 下载安装包

* 去oracle官网下载下面三个软件包:

  1. oracle-instantclient12.1-sqlplus-12.1.0.2.0-1.x86_64.rpm
  2. oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
  3. oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm

  **下载链接**: <a href="https://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html" rel="nofollow" target="_blank">oracle-instantclient</a>



## 安装oracle客户端

* 使用rpm -qpl命令查看oracle client默认安装路径：

```shell
[liujian@master03 downloads]$ rpm -qpl oracle-instantclient12.1-sqlplus-12.1.0.2.0-1.x86_64.rpm
/usr/bin/sqlplus64
/usr/lib/oracle/12.1/client64/bin/sqlplus
/usr/lib/oracle/12.1/client64/lib/glogin.sql
/usr/lib/oracle/12.1/client64/lib/libsqlplus.so
/usr/lib/oracle/12.1/client64/lib/libsqlplusic.so
```

由上面的查询结果可知oracle client默认安装在/usr/lib目录下，其他两个.rpm包也是安装在/usr/lib下，如果想让oracle client安装在自己指定的目录下，可以使用rpm -ivh –relocate重定向默认安装路径的前缀，例如：

```shell
rpm -ivh –relocate /usr=/oracle oracle-instantclient12.1-sqlplus-12.1.0.2.0-1.x86_64.rpm
```

这样就使得oracle client被安装到/oracle/lib下面，这里我使用了默认的安装路径/usr/lib.

* 使用mkdir -p创建/usr/lib/oracle/12.1/client64/network/admin目录，并使用scp命令把server端/home/oracle/app/oracle/product/11.2.0/dbhome_1/network/admin/tnanames.ora复制到client端/usr/lib/oracle/12.1/client64/network/admin下

* 配置环境变量：

  <div align="center">
      <img src="https://raw.githubusercontent.com/tracy-talent/Notes/master/imgs/oraclerc_client.png">
  </div>

* 测试

```shell
[liujian@slave101 admin]$ sqlplus scott@orcl

SQL*Plus: Release 12.1.0.2.0 Production on Thu Sep 27 01:10:47 2018

Copyright (c) 1982, 2014, Oracle.  All rights reserved.

Enter password:

Connected to:
Oracle Database 11g Enterprise Edition Release 11.2.0.1.0 - 64bit Production
With the Partitioning, OLAP, Data Mining and Real Application Testing options

SQL>
```

> attention: 如果没有在环境变量中指定ORACLE_SID，那么在使用sqlplus连接远程数据库的时候需要@远程数据库的SID，由于客户端系统用户不属于远程oracle数据库的SYSOPER和SYSDBA，所以不能使用sys登录而只能使用数据库普通用户登录，其中scott是使用dbca创建第一个数据库时提供的一个可选用户。



==END==