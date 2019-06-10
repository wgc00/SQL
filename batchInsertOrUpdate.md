#### 批量插入

	<insert id="batchAddOrder" parameterType="java.util.List">
		insert into cs_order(good_id,
		user_id,
		menu_id,
		order_status,
		order_Total_price,
		order_payment,
		order_quantity,
		order_created_time,
		order_number,
		order_updated_time)
		values
		<foreach collection="list" item="item" separator=",">
			(#{item.good.id},#{item.user.id},#{item.menu.id},
			#{item.status}, #{item.totalPrice},
			#{item.payment}, #{item.quantity},
			#{item.createdTime},#{item.number},#{item.updatedTime})
		</foreach>
	</insert>
					
### 批量更新	

	<update id="batchModifyOrderByStatus" parameterType="java.util.List">
        	<foreach collection="list" item="item" index="index" close=";" open="" separator=";">
            	 update `cs_order`
           	 <set>
                	<if test="item.status >= 0">
                  	`order_status` = #{item.status, jdbcType=TINYINT},
                	</if>
              		`order_updated_time` = #{item.updatedTime, jdbcType=TIMESTAMP},
            	</set>
           	<where>
               		`order_Recipient` = #{item.recipient, jdbcType=INTEGER}
                	and `order_id` = #{item.id, jdbcType=INTEGER}
            	</where>
        	</foreach>
    </update>
