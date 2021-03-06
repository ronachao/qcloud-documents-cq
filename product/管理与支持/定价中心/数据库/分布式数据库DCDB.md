## 分布式数据库 DCDB 定价

DCDB for TDSQL或于2017年2月开始按需售卖模式（即内存和硬盘单独计价的售卖方式），具体请参见云平台官网公告。

云平台DCDB for TDSQL采用实例包年包月付费方式。

实例总价=分片价格\*分片数量=（分片内存\*单价+分片磁盘*单价）\*数量

### 华北地区(北京)、华东地区(上海)、华南地区(广州)定价

#### 分片规格费用信息
|节点配置类型|实例版本|实例规格|包月价/元/月|
|:--:|:--:|:--:|:--:|
|高IO版|标准版（一主一备）|内存1GB|178|
|高IO版|标准版（一主一备）|内存2GB|356|
|高IO版|标准版（一主一备）|内存4GB|712|
|高IO版|标准版（一主一备）|内存8GB|1424|
|高IO版|标准版（一主一备）|内存16GB|2848|
|高IO版|标准版（一主一备）|内存32GB|5696|
|高IO版|标准版（一主一备）|内存48GB|8544|
|高IO版|标准版（一主一备）|内存64GB|10592|
|高IO版|标准版（一主一备）|内存96GB|14688|
|高IO版|标准版（一主一备）|内存120GB|17760|
|高IO版|标准版（一主一备）|内存156GB|22368|
|高IO版|标准版（一主一备）|内存180GB|25440|
|高IO版|标准版（一主一备）|内存240GB|33120|
|高IO版|标准版（一主一备）|内存480GB|63840|

#### 存储空间费用信息

**标准版（一主一备）**存储空间 **0.8元/GB/月**

### 金融专区定价

#### 分片规格费用信息

|节点配置类型|实例版本|实例规格|包月价/元/月|
|:--:|:--:|:--:|:--:|
|高IO版|金融定制（一主一备）|内存1GB|284.8|
|高IO版|金融定制（一主一备）|内存2GB|569.6|
|高IO版|金融定制（一主一备）|内存4GB|1139.2|
|高IO版|金融定制（一主一备）|内存8GB|2278.4|
|高IO版|金融定制（一主一备）|内存16GB|4556.8|
|高IO版|金融定制（一主一备）|内存32GB|9113.6|
|高IO版|金融定制（一主一备）|内存48GB|13670.4|
|高IO版|金融定制（一主一备）|内存64GB|16947.2|
|高IO版|金融定制（一主一备）|内存96GB|23500.8|
|高IO版|金融定制（一主一备）|内存120GB|28416|
|高IO版|金融定制（一主一备）|内存156GB|35788.8|
|高IO版|金融定制（一主一备）|内存180GB|40704|
|高IO版|金融定制（一主一备）|内存240GB|52992|
|高IO版|金融定制（一主一备）|内存480GB|102144|

#### 存储空间费用信息

**金融定制（一主一备）**存储空间 **1.28元/GB/月**

### 备份空间定价

备份与日志空间：简称“备份空间”，免费赠送实例容量的50%。从2015年12月31起超过免费容量部分0元优惠，优惠取消时间待定。

备份空间主要存储TDSQL运行过程中的关键日志和备份文件，日志包括错事务日志（Binlog）、错误日志、慢日志等。

### 增值服务定价

除常规的数据库服务外，DCDB for TDSQL还为用户提供多种增值服务。

- 数据库审计：又名数据库安全审计，主要用于监视并记录对数据库服务器的各类操作行为，实时地、智能地解析对数据库服务器的各种操作，并记入审计数据库中以便日后进行查询、分析、过滤，实现对目标数据库系统的用户操作的监控和审计。**从2016年08月31起CDB for TDSQL数据库审计功能0元优惠，优惠取消时间待定。**

### 带宽/流量定价

公网流量：只收取实例往客户端发送的公网流量费用，目前DCDB for TDSQL公网流量0元优惠，优惠取消时间待定。

## 购买指导

直接点击云平台产品售卖页面选择购买。页面实例最多一次性购买10个分片，超过10个分片的请多次重复购买。

说明：实例购买后，需初始化实例方可正常运行。

### 地域选择帮助

**公有云：**
云平台目前提供多个可选地域，TDSQL支持在中国公有云机房部署。


**金融云：**
针对金融行业监管要求定制的合规专区，具有高安全，高隔离性的特点；已认证通过的金融行业客户可提工单申请使用专区，详见[金融专区介绍](/doc/product/304/%E9%87%91%E8%9E%8D%E4%BA%91%E7%AE%80%E4%BB%8B)

## 升级指导

实例升级操作指将现有TDSQL实例的规格升级到更高规格，升级过程中会发生1次秒级闪断，建议您在业务低峰期升级。

- 升级流程开始后，不能被中断
- 管理中心暂不支持降级操作，如有需要请提工单

1、在【管理中心-分布式数据库-TDSQL】 中选择选择相应的实例，点击【升级】，弹出升级弹窗。

2、根据需要选择目标规格，并支付响应费用，成功后系统将自动升级实例规格
 
**升级费用=（目标规格单价-原规格单价）x剩余到期时间**

## 续费指导

续费操作指延长SCDB for TDSQL实例的使用时长，通常可以支持：

- 在【管理中心—分布式数据库—TDSQL—更多操作-批量续费】中选择选择相应的实例，点击【续费】、【批量续费】、【设置自动续费】。

- 在【用户中心-续费管理-分布式数据库TDSQL】待续费项，选择选择相应的实例，点击【续费】或【批量续费】。

- 在【用户中心-续费管理-分布式数据库TDSQL】自动续费。

【注意事项】

- 自动续费的会在到期当日会执行自动续费，需账户费用保障充足。若自动续费不成功，不再自动重试。

## 续费定价

续费费用=实例月单价x续费时间（月）+(实例月单价/30 x 续费时间（天）)

说明：不足整月的部分，我们将按照月价折算您续费天数的价格。例如，4月5日到期的资源，月价格为60元，需要调整到期日为每月20日，续费至5月20日，您需要支付的金额为90元（60+60÷30×15）。

## 到期提醒

正式计费前，您可以选择提交工单，申请免费续期（每次最长2个月）。

1、云服务资源到期前七天，系统会开始给用户发送续费提醒通知。[提醒规则](/document/product/555/7438)

2、到期后，七天内，云服务还可以继续使用，需要尽快续费，系统将发送云服务到期提醒。

3、到期超过七天的云服务资源将被系统回收，数据将会被清除，不可恢复。

