# MySQL 存储过程

##  1、数据库简单的创建存储过程

    --创建存储过程
     delimiter //
     create procedure px(p int)
     begin
          set @x = 0;
          set @sum = 0;
	  -- 循环
          repeat
          set @x = @x+1;
          set @sum=@sum+ @x;
	  -- until 是循环条件
          until @x = p end repeat;
     end//
     
     delimiter //
     create procedure sx(s int)
     begin 
	 -- 定义变量
          declare x int;
          set x = 0;
          set @z = 1;
          repeat set x = x +1;
          if(x%3=0) and (x%9 <> 0)then
               @z = @z * x;
          end if;
          until x >=s end repeat;
     end//


## 2、MyBatis 获取存储过程的信息
	
### 1、通过 id 获取所有的子类 id

	delimiter //

	-- in 是入参 out 是出参数
	create procedure getChildList(in id char(32), out oTemp varchar(4000))
	begin
		
		-- 定义局部变量
    		declare oTempChild VARCHAR(4000);
    		-- declare oTemp VARCHAR(4000);
    		-- cast 类型转换
    		set oTempChild = cast(id AS CHAR);
    		set oTemp = '';
		
		-- 循环获取子类的 id
    		while oTempChild is not null
    		do
		-- 判断 oTemp 是否为空
    		if oTemp != '' then

			-- 如果不是空就两个字符进行向拼接
        		set oTemp = CONCAT(oTemp, ',', oTempChild);
    		else
			
        		set oTemp = oTempChild;
    		end if;
		-- 如果 corporation_parent_id 修改为 corporation_id 就是搜索父类 id
		-- 并且 FIND_IN_SET 要修改为 corporation_parent_id
    		select GROUP_CONCAT(corporation_parent_id) INTO oTempChild
   		from pms_corporation

	    	-- find_in_set 是全表扫描的,find_in_set 是精确匹配，字段值以英文”,”分隔
		-- 搜索 corporation_id 
    		where FIND_IN_SET(corporation_id, oTempChild) > 0;
    		end while;
	end //
	
	
	-- 在数据库测试一下 @x 是否发生改变
	set @x = "adfadfa" ;
	call getChildList("4F67D5E1F1BE4DFA95F49396CD14EC7F", @x);
	select @x;

### 2、MyBatis 获取到存储过程返回的值

	<!-- 接收存储过程返回的值 -->
    	<parameterMap id="resultMap" type="java.util.Map">
        	<!-- 入参 -->
        	<parameter property="id" javaType="java.lang.String" mode="IN"/>
        	<!-- 出参 -->
        	<parameter property="oTemp" javaType="java.lang.String" mode="OUT"/>
    	</parameterMap>
	
	<!-- 查询存储过程 -->
	<select id="getChild" parameterMap="resultMap" resultType="java.lang.String" statementType="CALLABLE">
	    	
		<!-- call 调用存储过程 -->
            
		{call getChildList(#{map.id, jdbcType=CHAR, mode=IN}, #{map.oTemp, jdbcType=VARCHAR, mode=OUT})}

    	</select>




