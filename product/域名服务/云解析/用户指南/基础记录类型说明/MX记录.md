### 什么情况下会用到MX记录？

如果需要设置邮箱，让邮箱能收到邮件，就需要添加MX记录。


### MX记录的添加方式

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/static/img/a498e4a9209d03b91489e15f83758585/MX-1.png)

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/static/img/93545943591cdad40248edf7db3ccfe7/MX-2.png)

![](http://imgcache.tcecqpoc.fsphere.cn/image/mccdn.qcloud.com/static/img/ced0a3421c498044c16a2219e3967bbf/MX-3.png)

1. 主机记录处填子域名（一般情况下是要做xxx@123.com的邮箱，所以主机记录一般是留空的；如果主机记录填mail，邮箱地址会变为xxx@mail.123.com）。

2. 记录类型为MX。

3. 线路类型（默认为必填项，否则会导致部分用户无法解析，邮件无法收取；MX一般不需要做智能解析，直接默认即可）。

4. 记录值可以是域名，也可以是一个ip地址。

如果是域名的话，指向的域名必须有A记录（如上图的mail.123.com），记录生成后会自动在域名后面补一个“.”，这是正常现象；
如果是ip的话，直接填写邮件服务器ip即可，记录生成后同样会自动补一个“.”。

5. TTL不需要填写，添加时系统会自动生成，默认为600秒（TTL为缓存时间，数值越小，修改记录各地生效时间越快）

6. MX优先级的数值越低，优先级别就越高（如上图，邮件会先尝试发送到MX优先级为5的1.1.1.1，如果尝试失败，才会发送到MX优先级为10的mail.123.com）。