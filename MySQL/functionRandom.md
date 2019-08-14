# MySQl 创建函数

## 1、使用函数创建随机数
	-- 创建一个表，
     	drop table randString;
     	create table randString(
       		id int,
       		stringName varchar(225)
     	);
     
     	-- 切换结尾字符
     	delimiter //
     	-- 创建一个随机字符串的函数
     	drop function if exists randStrs;
     	create function randStrs(n int)
       	returns varchar(225) charset 'utf8'
       	begin
		-- 定义局部变量， 给予默认值
         	declare char_str varchar(100) default 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
	
         	declare return_str varchar(225) default '';
        	declare i int default 0;
		
		-- 循环         
		while i < n do
	
           		set return_str = concat(return_str, substring(char_str, floor(1 + rand() * 62), 1));
           		set i = i + 1;
         	end while ;
		-- 返回值         	
		return return_str;
       	 end //

    

## 2、使用存储过程创建随机数
	
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
           	-- 插入到表中
		insert into randString(id,stringName) values (init_data , rand_str);
         	end while ;
       	end//

     -- 删除进入死循环的表
     -- select count(*) from randString;

   	-- 关闭事务
     	set autocommit = 0;

     	delete  from randString;
	
	-- 提交事务
     	commit ;


     	select * from randString;

