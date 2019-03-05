# SQL
一些比较遗忘的SQL语句


     -- 连接sql   
     select concat("insert into ge_policy_raw() values('" , crawl_url, "')") from  ge_policy_raw;
     
     
     --一、创建用户要切换到mysql数据


     --允许本地 IP 访问 localhost, 127.0.0.1
     --'123456'表示密码
     create user '用户名'@'localhost' identified by '123456';

     --允许外网 IP 访问
     create user '用户名'@'%' identified by '123456';

     --查看表结构
     desc 表名;
     show columns from 表名;
     describe 表名;
     show create table 表名;


     --创建存储过程
     create procedure px(p int)
     begin
          set @x = 0;
          set @sum = 0;
          repeat
          set @x = @x+1;
          set @sum=@sum+ @x;
          until @x = p end repeat;
     end

     create procedure sx(s int)
     begin 
          declare x int;
          set x = 0;
          set @z = 1;
          repeat set x = x +1;
          if(x%3=0) and (x%9 <> 0)then
               @z = @z * x;

          end if;
          until x >=s end repeat;
     end





     1.外键的平凡的添加会导致开发时的难度，会出现一些列的表频繁检查的问题；
     2.不添加外键可以提高性能、操作简单、方便管理
     3.我们既要提高性能同时就应该想到安全方面的问题，所以安全要自己控制。

     char 
     varchar


     -- 创建一个表，
     drop table randString;
     create table randString(
       id int,
       stringName varchar(225)
     );

     delimiter //
     -- 创建一个随机字符串的函数
     drop function if exists randStrs;
     create function randStrs(n int)
       returns varchar(225) charset 'utf8'
       begin
         declare char_str varchar(100) default 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
         declare return_str varchar(225) default '';
         declare i int default 0;
         while i < n do
           set return_str = concat(return_str, substring(char_str, floor(1 + rand() * 62), 1));
           set i = i + 1;
         end while ;
         return return_str;
       end //

     delimiter //

     drop procedure if exists proc_randString;

     create procedure proc_randString(num int)
       begin
         -- declare char_str varchar(100) default 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
         declare init_data int default 0;
         declare rand_str varchar(225);
         while init_data < num do
           set init_data = init_data + 1;
           set rand_str = substring('abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789', floor(1 + rand() * 62));
           insert into randString(id,stringName) values (init_data , rand_str);
         end while ;
       end
     //

     -- 删除进入死循环的表
     -- select count(*) from randString;

     set autocommit = 0;

     delete  from randString;

     commit ;


     select * from randString;




     Statement、PreparedStatement、CallbelStatement三者的关系和区别

     关系：PreparedStatement类继承了 Statement类，CallbelStatement继承了PreparedStatement类。
           Statement（是爷爷）、PreparedStatement（儿子）、CallbelStatement（孙子）。

     区别：Statement类可以写sql，但有sql注入
           PreparedStatement类是在Statement类的基础加了预编译，设置参数。
           CallbelStatement类是在PreparedStatement的基础继承了他预编译，可以设置参数和获取参数，用于执行存储过程。


