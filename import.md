

# mysql 导入导出的命令


## 一、导出命令

### 1.1 整个数据库都导出
       
        mysqldump -uroot -p123456 databaseName > fileName.sql
        

### 1.2 导出数据库中单表和多表


        mysqldump -uroot -p123456 databaseName tableName > fileName.sql
        
        mysqldump -uroot -p12345  databaseName tableName1 tableName2 > fileName.sql
        
## 二、导入数据库命令

### 2.1 导入整个数据库

        mysql -uroot -p12345 < fileName.sql
        
### 2.2 往数据库中导入一个表

        -- 打开数据库
        mysql -uroot -p123456 
        
        -- 切换到要导入的数据库
        use databaseName;
        
        -- 导入一个文件中的表
        source /home/wgc/sql.sql
        
#   通过 sql 查询某一个时间段的信息

         -- 查询某一个时间段的信息
       select *
       from cs_good as g
       -- 要查询的字段
       WHERE STR_TO_DATE(g.good_created_time, '%Y-%m-%d')
       -- 开始时间
       BETWEEN STR_TO_DATE("2019-05-13", '%Y-%m-%d') 
       -- 结束时间
       AND STR_TO_DATE("2019-05-19", '%Y-%m-%d')
       -- 进行升序
       ORDER BY STR_TO_DATE(g.good_created_time, '%Y-%m-%d') DESC;
