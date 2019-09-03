# oracle sqlplus command

## 查找表

* select table_name from user_tables;   //查找当前用户的表名

* select table_name from all_tables;  //查找所有用户的表名



## 用户

### 查找用户

* select * from all_users;  //查找所有用户
* select * from dba_users;  //查找所有dba用户

### 创建用户

* create user brooksj 

  identified by pasabrooksj 

  default tablespace brooksj_TS

  temporary tablespace brooksj_TMP

  profile default;

```sql
-- Grant/Revoke role privileges 
grant connect to brooksj;
grant datapump_exp_full_database to brooksj;
grant datapump_imp_full_database to brooksj;
grant dba to brooksj;
grant exp_full_database to brooksj;
grant imp_full_database to brooksj;
grant resource to brooksj;
-- Grant/Revoke system privileges 
grant alter_user to brooksj;
grant comment any table to brooksj;
grant create any view to brooksj;
grant create session to brooksj;
grant create user to brooksj;
grant delete any table to brooksj;
grant drop user to brooksj;
grant export full database to brooksj;
grant unlimited tablespace to brooksj;
```

### 删除用户

* drop user brooksj cascade;



## 表空间

### 查找表空间

* select tablespace_name from user_tablespaces;  //查找用户表空间名

* select * from v$tablespace;  //查看所有表空间基本信息(限sysdba用户使用)

* desc dba_data_files;   //查看存储表空间信息的表的表结构(限sysdba用户使用)

* select file_name,tablespace_name from dba_data_files;    //查看表空间对应的数据文件路径名(限sysdba用户使用，涉及dba_data_files的都限sysdba用户访问)

### 创建表空间

* create tablespace brooksj ==datafile== '/home/oracle/app/oradata/orcl/brooksj.dbf' size 1G     //创建1G大小的表空间并指明数据文件存储位置
* create undo tablespace  undo1 ==datafile== '/ora10/product/oradata/ora10/undobrooksj.dbf' size 1000m;    //创建1000m大小的undo类型的表空间(Undo 类型的表空间，当你对一张表或一条记录进行修改的时候，它会对修改之前的信息进行保存，这样可以保证数据的回滚。Undo 只包含undo类型的对象，不能包含任何其他对象，只适合于数据文件和区间管理。)
* 创建临时表空间用tempfile
```sql
create temporary tablespace  starnettemp 
tempfile '/home/oracle/app/oradata/orcl/starnet_temp.dbf' 
size 500m  
autoextend on
next 50m maxsize 2048m
extent management local uniform; 
```
//创建20m大小的临时表空间(临时表空间，相当于一个临时的垃圾场。用于排序操作，比如你要做一次大数据量的查询，但在内存无法存储这么大量的数据，然后会在磁盘上建立一个临时的表空间用记存放这些数据。Oracle就会用这个临时表空间做排序，存储中间结果。一个全局的临时表空间，可以由多个用户共享，谁需要谁使用。但它只能存放临时的数据，不能包含任何永久性对象。 建议用本地管理方式创建这个表空间。)

### 删除表空间

* drop tablespace tsname including contents and datafiles cascade constraints;

> 删除表空间，使用命令drop tablespace ‘表空间名’  但是有3个选项需要注意： 
>
> INCLUDING CONTENTS：指删除表空间中的segments； 
>
> INCLUDING CONTENTS AND DATAFILES：指删除segments和datafiles； 
>
> CASCADE CONSTRAINTS：删除所有与该空间相关的完整性约束条件。 



## 目录directory

### 创建目录

* create directory data_pump_file as '\home\oracle\pumpfile';    //创建oracle逻辑目录data_dump_file并制定物理路径

### 查看目录

* desc dba_directories;   //查看目录表结构
* select directory_name, directory_path from dba_directories;   //查看oracle目录名及其对应路径

### 修改目录

* create or replace directory data_pump_file as '/home';   //修改目录对应路径，不存在则创建

### 删除目录

* drop directory data_pump_file;







