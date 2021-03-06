## 迁移过程
| 源实例 | 迁移的源实例 |
|---------|---------|
| 目标实例 | 迁移的目标实例，即用户购买的云平台 MongoDB |
| 所在服务器 | 迁移的源实例所在的服务器 |

#### 迁移注意事项
1.	为保障迁移效率，CVM 自建实例迁移不支持跨地域迁移；
2.	外网实例迁移时，请确保源实例服务在外网环境下可访问；
3.	迁移成功时，由业务侧验证数据后，可断开源实例连接，将连接切换到目标实例。
4.	[特别提醒]如果自建实例是单节点的，由于单节点无 oplog，所以不支持在线迁移

## 迁移过程
#### 新建迁移任务
进入“迁移任务列表”后，请按如下步骤新建迁移任务：
a.	选择目标实例所在地域；
b.	点击“新建实例迁移任务”，进入创建迁移任务页；
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/164c0ebdd2ce7a9a171c9be0727b6cb3/1.1.png)

#### 填写基本信息
以下以云主机 CVM 上的 MongoDB 实例为例说明，外网实例迁移下同

| 字段 | 描述 | 用途 | 必填 |
|---------|---------|---------|---------|
| 任务名称 | 迁移任务的名称 |方便用户管理任务 | 是 |
| 云服务器 ID | 源 MongoDB 实例所在的云平台主机 ID |迁移任务会根据 CVM 实例 ID，检查云主机运行情况。如果是外网迁移可不填写 | 是 |
| MongoDB IP |源 MongoDB 实例所在的云平台主机的内网 IP |迁移任务会检查 CVM 内网 IP | 是 |
| 端口 | 源实例端口号 |迁移任务会访问源实例服务 | 是 |
| 密码 | 源实例密码 |访问源实例服务时有鉴权 | 是 |
| 目标库-实例 | 目标实例 ID |同步数据到目标实例 | 是 |
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/6db68ed9a974aae89e26700b2b0bec9e/image.png)

#### 选择迁移对象
目前支持库级别的迁移能力，勾选要迁移的库。点击保持来创建任务
 ![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/f4df377f4a08b92dbd875bcd2063775a/image.png)


任务创建成功，会在任务列表中显示一条任务
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/346f74a2a400e9ef851d35412cb8dfb4/5.png)

#### 启动迁移任务
任务创建成功后，任务还处于未启动状态。点击启动，启动任务后，任务会做一次参数校验
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/188aace20bea6af2363b6b170409bb4a/6.png)

参数校验成功后，才能进行迁移，否则无法进行。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/417733549ad60a3fbcbec475663f762f/7.png)
特别注意：如果网络不可达，请检查源实例所在服务的安全组，需要将安全组放通全部端口

#### 迁移过程
点击弹框中的启动按钮，正式启动迁移。
迁移过程一共分为 3 步
1.数据同步
2.索引创建
3.oplog 同步
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/4e72afb7a91729bbcc47e9424bc6ff65/8.png)

#### 断开同步
当 oplog 追到一定时间状态的时候，点击完成任务，确定，即可完成数据同步操作，完成任务会终止 oplog 的同步标记任务成功。(断开同步前，可以在目标实例上验证数据，如果验证无误，即可断开同步。)
若迁移过程中，想中断迁移，可以点击中止任务，中止任务会把已经同步的操作全部做回滚标记任务失败。

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/d4f8a746fb7be7c172088ce808d13fc1/9.png)

![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/e56d0392b9e0fc287eec5ee1e8fcfd12/10.png)
