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

	<update id="updateByPrimaryKey" parameterType="com.cateringsystem.entity.order.Order">
		update cs_order
		<set>
			order_status = #{record.status},
			order_payment = #{record.payment},
			order_quantity = #{record.quantity},
			order_Total_price = #{record.totalPrice},
			<if test="record.sendTime != null">
				order_send_time = #{record.sendTime},
			</if>
			<if test="record.eneTime != null">
				order_ene_time = #{record.eneTime},
			</if>
			order_updated_time = #{record.updatedTime}
		</set>
		<where>
			user_id = #{record.user.id} or order_Recipient = #{record.recipient}
		</where>
	</update>
