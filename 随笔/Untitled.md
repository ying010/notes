| 父级节点 | 子级节点 | 深度 | 级别 | 是否子账户 |
| -------- | -------- | ---- | ---- | ---------- |
|          |          |      |      |            |



ALTER TABLE `mambike_dealer`.`t_bind_user_car` 
ADD COLUMN `qualification` varchar(100) NULL COMMENT '合格证编码' AFTER `name`;

ALTER TABLE `mambike_mammoth`.`t_bind_vehicle` 
ADD `use_start_time` varchar(30) NULL COMMENT '租期开始时间' AFTER `qualification`;

| 自提补录订单添加签约校验            |
| ----------------------------------- |
| 根据手机号查询C端签约信息           |
| 定时器校验签约,失败的7天轮询        |
| 签约导致补贴失败的钉钉推送          |
| 录入订单是C端解绑电池监控           |
| 换电站耗电查询统计                  |
| 绑定/解绑换电柜时统计时间段内耗电量 |
| 自助换电记录C端同步掌柜             |
| 换电记录查询                        |
| 实用工具车辆信息查询                |
| leads列表查询添加来源项筛选         |







总行驶里程

租赁时间

租期截至时间

合格证

详细地址

告警需要合格证





- [ ] 获取租期截至时间

- [ ] 退租

- [ ] 绑定车辆要把信息同步给驿站小程序
  - t_vehicle 保存车辆信息
  - t_merchants_vehicle  车辆与商户的关系
  - t_bind_vehicle  用户绑车记录
    - 字段
      - 合格证
      - 租赁时间
      - 租期截至时间
      - 车架号
      - 姓名
      - 电话
      - 电池SN

- [ ] 车辆监控
  - 车辆状态
  - 电池电量
  - 位置信息
  - 行驶里程

- [ ] 行驶里程7\30统计
- [ ] 总里程统计
- [x] 告警信息  mongodb  me_alarm_notice
- [ ] 实时坐标转为地址  





t_vehicle:

vehicle_code

vehicle_status

t_bind_vehicle:

vehicle_code

battery_sn

user_name

phone

user_id

bind_time

unbind_time

bind_status

del_flag

qualification



修改订单状态

?发放佣金

修改小猪cms

核销优惠券

修改客户信息

同步leads信息

创建租电白名单













ALTER TABLE `mambike_dealer`.`t_door_site` 
ADD COLUMN `service_workday_time` varchar(15) NOT NULL DEFAULT '' COMMENT '站点工作日营业时间' AFTER `contact_name`,
ADD COLUMN `service_holiday_time` varchar(15) NOT NULL DEFAULT '' COMMENT '站点非工作日营业时间' AFTER `service_workday_time`;





















| 表名                            | 注释                               |
| ------------------------------- | ---------------------------------- |
| t_bind_user_car                 | 用户绑车信息表                     |
| t_customer                      | 客户管理信息                       |
| t_customer_contact_record       | 客户联系记录                       |
| t_customer_set                  | 门店客户分配规则                   |
| t_d2d_door_electronic_fence     | 上门服务电子围栏表                 |
| t_d2d_door_setting              | 上门时间配置表                     |
| t_d2d_door_time                 | 上门时间段表                       |
| t_d2d_order                     | 上门服务信息                       |
| t_d2d_order_forward             | 转派记录表                         |
| t_d2d_order_material            | 上门服务收费信息                   |
| t_d2d_repair_order              | 上门维保订单信息                   |
| t_d2d_repair_order_material     | 上门维保耗材收费信息               |
| t_data_extract_plan             | 提货计划表                         |
| t_dealer                        | 一网二网信息表                     |
| t_dealer_account                | 掌柜端统一账号表                   |
| t_dealer_battery_bl             |                                    |
| t_dealer_battery_bl_op_record   |                                    |
| t_dealer_image_info             | 商户图片信息表                     |
| t_dealer_login_record           | 掌柜端账号登录记录表               |
| t_ding_after_sale_parts_record  | 钉钉电动售后退回部件跟踪记录       |
| t_ding_electricity_sales_record | 钉钉电动销售记录                   |
| t_discount                      | 优惠券核销记录表                   |
| t_door                          | 门店信息                           |
| t_door_read_protocol            | 租电补贴协议通知读取               |
| t_door_site                     | 门店设备站点                       |
| t_door_site_image               | 换电站图片                         |
| t_door_update                   | 门店修改信息                       |
| t_door_whitelist                | 门店白名单                         |
| t_electric_exchange_battery     | 换电流通电池表                     |
| t_electric_exchange_blank_list  | 换电黑名单列表                     |
| t_electric_exchange_record      | 门店设备换电记录表                 |
| t_equipment_bind_record         | 门店设备绑定记录表                 |
| t_equipment_store               | 门店设备关联表                     |
| t_erp_chejia                    | ERP车架数据表                      |
| t_erp_customer                  | e10视图客户表                      |
| t_erp_item                      | e10物料                            |
| t_erp_xsck                      | e10出库信息                        |
| t_exchange_electric_setting     | 换电套餐配置表                     |
| t_favour_option                 | 产品偏好表                         |
| t_favour_option_platform        | 产品偏好表                         |
| t_favour_option_sub             | 产品偏好子表                       |
| t_file_md5                      | 上传文件MD5                        |
| t_firstyear_flowpackage_reset   | 首年免费流量包重                   |
| t_flow_pack                     | 车型流量包表                       |
| t_fresh_deposit_expand          | 新品预定定金膨胀记录表             |
| t_fresh_deposit_expand_rule     | 新品预定助力金规则表               |
| t_functive                      | 功能项表                           |
| t_functive_grade                | 功能项版本对应关系表               |
| t_functive_plan                 | 功能项方案表                       |
| t_functive_use                  | 车型可用功能表                     |
| t_goods_sku                     | 商品SKU                            |
| t_goods_sku_pig                 | 商品SKU与小猪商品对应表            |
| t_in_goods                      | 入库信息                           |
| t_in_products                   | 入库产品信息                       |
| t_installment_set               | 电池分期套餐                       |
| t_installment_whitelist         | 分期购白名单                       |
| t_inventory_entering            | 门店盘点，车架号、电池SN号录入接口 |
| t_inventory_entering_batch      | 录入车架批次                       |





设备绑定、解绑保存

提供设备解绑处理接口









魔岩:

![image-20210507110427676](source/Untitled.assets/image-20210507110427676.png)

- 消息提醒是否已取消;是否影响掌柜

- 退租是否影响掌柜

  ![image-20210507110820794](source/Untitled.assets/image-20210507110820794.png)

**车辆监控**

​	**C端需要提供接口:**

- 车辆状态统计(传车架号列表)

- 车辆列表剩余电量、当前位置、车辆状态(传车架号列表)

- 车辆详情的剩余电量、当前位置、车辆状态、总里程(传单个车架号)

​	**数据组接口**

- 查询截至昨日的总里程
- 7日/30日各天的里程

**车辆告警**

- Kafka接收遥测上报数据保存mongo



进销存调拨

- [ ] 获取门店列表

- [ ] 商品调拨
- [x] 调拨记录查询



