## 监控面板配置

用户可以通过查看不同的监控面板，来快速了解各种云资源的运行状况。

- 所有的监控视图都需创建在监控面板之上，故可以将监控面板理解为监控视图的集合
- 通过创建不同的监控面板，可区分不同分组下的云资源

每个开发商最多可创建20个监控面板。

###  创建监控面板

1. 登录云平台云监控控制台 [Dashbaord](http://console.tcecqpoc.fsphere.cn/monitor/dashboard) 页面。
2. 单击【+】图标，即新建监控面板按钮。
3. 自定义监控面板名称，单击【确定】后完成创建面板。
   ![3](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/389f555ee1ffb844fb00f8c61822c38b/image.png)

### 重命名&删除面板

用户可通过面板中的菜单栏，对面板进行重命名和删除操作。单击面板右侧的【...】图标即可进行操作。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/affd539eaf50e0d41a4a4e3dc42573bc/image.png)

### 调整面板排序

点击面板标签并拖动到目的位置，即可调整面板排序。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/87c038ba833c3e612dc5a3ab6d3664aa/image.png)

## 监控视图配置

通过在监控面板中创建不同的监控视图，可灵活满足用户在不同监控场景查看资源性能状况的需求。不同的视图类别、视图联动、视图拖拽放大等功能特性，为用户查看监控数据带来更多便利。

### 视图种类

Dashboard目前提供了折线图、面积图、柱状图三种监控视图供用户选择。

- 折线图：最常见、最通用的视图，能满足绝大部分时序性监控数据的查阅需求。
- 柱状图：适用于磁盘使用率等指标，有利于用户查看目前消耗资源的比值。

### 创建折线图

折线图包含明细视图与聚合视图。

- 明细视图：在一个图里展示多台资源同个指标的多条曲线。
- 聚合视图：在一个图里展示多台资源同个指标汇聚数据的曲线，支持同时展示两个同单位指标的汇聚数据。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/67c54615dc83ed2bb92b1e4684ed9d44/image.png)

#### 创建流程

1. 点击dashbaord中的【添加监控图表】。
   ![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/846763f78af542e795b211cac8d63e61/image.png)

2. 在弹窗中进行图表配置操作。
   ![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/fc99d01f2c0671e40d66b127e8eaf318/image.png)

3. 完成后单击【确定】按钮，即完成视图创建。
   - 若面板中无视图，新建视图将默认由左上至右下的次序依次建立在面板中。
   - 若面板中已有视图，新建的视图将默认由左上至右下的次序跟随在面板最下方视图后。

> **注意：**
> 
> 在一次新建图表过程中，支持批量创建同一批对象多个指标的多个图表，为用户免去重复选择监控对象的繁琐流程。
>
> 若用户选择的实例数量超出单张曲线图容纳上限，将默认按对象列表顺序批量创建图表，避免用户多次重复新建图表配置。
>
> 实力列表支持资源列表的筛选、搜索、一键全选以及按shift多选功能。友好的批量操作为用户大批量选取资源带来便利，提升配置效率。

### 创建柱状图

1. 柱状图的创建流程与折线图一致。
2. 当用户选择的指标为“云服务器—磁盘使用率”时，图表样式将自动切换为柱状图。

