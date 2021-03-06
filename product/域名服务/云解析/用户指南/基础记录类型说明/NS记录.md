### 什么情况下会用到NS记录？

如果需要把子域名交给其他DNS服务商解析，就需要添加NS记录.

### NS记录的添加方式

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/static/img/937b1357daaa2ad3266bec04d3950514/Ns-1.png)

1. 主机记录处填子域名（比如需要将 www.123.com 的解析授权给其他DNS服务器，只需要在主机记录处填写www即可，主机记录“@”不能做NS记录，授权出去的子域名不会影响其他子域名的正常解析）。

2. 记录类型为NS。

3. 线路类型（默认为必填项，否则会导致部分用户无法解析）。

4. 记录值为要授权的DNS服务器域名，记录生成后会自动在域名后面补一个“.”，这是正常现象。

5. TTL不需要填写，添加时系统会自动生成，默认为600秒（TTL为缓存时间，数值越小，修改记录各地生效时间越快）。

6. MX优先级不需要填写。