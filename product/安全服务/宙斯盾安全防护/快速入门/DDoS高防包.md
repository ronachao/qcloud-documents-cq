# 快速入门DDoS高防包 #
云平台宙斯盾 DDoS 高防包防护流程图如下：
![](http://imgcache.tcecqpoc.fsphere.cn/image/main.qcloudimg.com/raw/26e2bab63e6df5395036522b50b3cfd4.png)
## 一、准备与选型 
1. 注册云平台账号
新用户需在 [云平台官网](/) 进行【注册】然后购买宙斯盾安全防护服务，详情可参见 [注册云平台](/document/product/378/9603) 操作指引和宙斯盾安全防护 [购买指导]()。
2. 确定高防包区域
 - 区域选择原则
DDoS 高防包只能为同区域的云平台公网 IP 提供高防服务，请务必选择与您云平台源站服务器同区域的高防包。
3. 确定高防 IP 配置方案
 - 防护范围
 可以选择单IP或多IP。单IP模式高防包可以绑定一个云平台公网IP地址，该IP独享防护峰值。多IP模式高防包可以绑定多个云平台公网IP地址，多IP共享防护峰值。当多IP同时遭受DDoS攻击时，若叠加峰值超过防护峰值时，会从攻击流量最大的IP地址开始封堵。
 - 保底防护峰值
 保底防护峰值为包年包月预付费。建议以历史攻击流量的平均值为参考，配置保底防护峰值高于平均值，以使保底防护峰值足够防御大部分攻击事件。
 - 弹性防护峰值
 弹性防护峰值为按使用量计费，每日结算。建议以历史攻击流量最高值为参考，配置弹性防护峰值略高于历史最高峰值，以便发生大流量攻击时有足够的容量可以防御，避免超过防护峰值IP被封堵。同时弹性按月用量付费，未使用时不付费，可以大量节省成本。

## 二、添加防护 IP
DDoS 高防包购买完成后，在 DDoS 高防包管理页面列表中即可以看到分配的高防包资源。高防包可以直接对云平台公网 IP 地址提升 DDoS 防护能力.
本部分介绍添加 IP 的配置方法。
1. 在宙斯盾安全防护产品控制台，在左侧目录中选择【DDoS 高防包】 即可以进入 DDoS 高防包管理页；
 ![](http://imgcache.tcecqpoc.fsphere.cn/image/i.imgur.com/EyS5666.jpg)
2. 在高防包列表中，单击【绑定 IP 数】列的 IP 数量，即可接入防护 IP 列表；
 ![](http://imgcache.tcecqpoc.fsphere.cn/image/i.imgur.com/SWyyKSx.jpg)
3. 在防护 IP 列表下，单击【添加 IP】，并选取需要添加到高防包中防护的 IP 地址；
 ![](http://imgcache.tcecqpoc.fsphere.cn/image/i.imgur.com/nPTbOqg.jpg)
 ![](http://imgcache.tcecqpoc.fsphere.cn/image/i.imgur.com/itOyZcR.jpg)
4. 完成添加后，该 IP 地址即可以得到宙斯盾安全防护系统的保护了。
![](http://imgcache.tcecqpoc.fsphere.cn/image/i.imgur.com/7wzmM0D.jpg)
