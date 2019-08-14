# SQL
一些比较遗忘的SQL语句

## 1、拼接 concat 函数

     -- 连接sql   
     select concat("insert into ge_policy_raw() values('" , crawl_url, "')") from  ge_policy_raw;

## 2、查看 table 结构      

     --查看表结构
     desc 表名;
     show columns from 表名;
     describe 表名;
     show create table 表名;

     1.外键的平凡的添加会导致开发时的难度，会出现一些列的表频繁检查的问题；
     2.不添加外键可以提高性能、操作简单、方便管理
     3.我们既要提高性能同时就应该想到安全方面的问题，所以安全要自己控制。

   

## 3、Statement、PreparedStatement、CallbelStatement三者的关系和区别


     关系：PreparedStatement类继承了 Statement类，CallbelStatement继承了PreparedStatement类。
           Statement（是爷爷）、PreparedStatement（儿子）、CallbelStatement（孙子）。

     区别：Statement类可以写sql，但有sql注入
           PreparedStatement类是在Statement类的基础加了预编译，设置参数。
           CallbelStatement类是在PreparedStatement的基础继承了他预编译，可以设置参数和获取参数，用于执行存储过程。



# 目录：

## MyBatis

[1、批量插入、更新数据] (https://github.com/wgc00/SQL/blob/master/MyBatis/batchOperating.md)

## MySQL
	
[2、MySQL函数创建随机数](https://github.com/wgc00/SQL/blob/master/MySQL/functionRandom.md)
	
[3、存储过程的使用] (https://github.com/wgc00/SQL/blob/master/MySQL/procedure.md)

[4、表的导入导出] (https://github.com/wgc00/SQL/blob/master/MySQL/tableImportAndExport)
	
[5、表名的更新] (https://github.com/wgc00/SQL/blob/master/MySQL/tableNameUpdate.md)

## PostgreSQL
