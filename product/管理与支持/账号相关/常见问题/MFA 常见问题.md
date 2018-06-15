### 什么是 MFA 设备？
MFA (Multi-FactorAuthentication)即多因子认证，是一种简单有效的安全认证方法，它能够实现在用户名和密码之外再增加一层保护。MFA 设备（又叫动态口令卡或 token 卡）是提供这种安全认证方法的设备。目前云平台提供两种MFA设备： 硬件 MFA 设备 和 虚拟 MFA 设备 。

### 如何绑定虚拟 MFA 设备？
1. 登录云平台控制台，进入安全设置，在 MFA 设备那一栏上，单击【绑定】。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/63c17fdf2fc1913927ad669c86dcafcd/image.png)
2. 在弹出来的页面中，单击【发送验证码】，收到验证码后，将6位数字验证码输入框内。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/48f47db0b56e5e114569f069813a3a26/image.png)
3. 在弹出来的页面中，依次按照图片中的步骤进行操作。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/0e9169e02f094677636e0cd4943f8cc0/image.png)
4. 将手机中的应用程序出现的连续的安全码输入到框内，安全码每 30 秒更新一次。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/cfaf0d3ccd26fa60c792e476780d3e64/image.png)
5. 选择您想启用的范围，您可以选择登录保护，也可以选择操作保护，只需要在你想选择的范围前面勾选出来即可，可多选。选择完之后，单击【提交】。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/2848c64ff4752ae458ab3eb579ebf945/image.png)

### 如何绑定 MFA 设备？
目前云平台提供的硬件 MFA设备为“云平台安全令牌”，也叫动态口令卡或 token 卡，首批 token 卡采用内测的形式发放给客户，照片如图所示（不同版本可能在外观上有差异）
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/a12ed49934d347fdd059e0d74784f32b/image.png)
主要有以下几个步骤：
1. 进入用户中心>账户信息>安全设置，单击【绑定】按钮。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/4f5a99eade8a87c651669e8d4d156345/image.png)
2. 弹出身份验证框，输入手机中收到的6位数验证码，单击【确定】按钮。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/3742fd7d9f94c24808ad8608423250e4/image.png)
3. 在绑定 MFA 设备页中选择“硬件 MFA 设备”，根据提示输入 token 卡背面的序列码（SN 码），和 token 卡正面的 6 位数动态安全码。
启用范围可勾选也可以不勾选：不勾选则默认您的账户不开启安全保护；勾选登陆保护则登陆后需要验证 token 卡上的安全码。

勾选操作保护则在账户中进行删除云主机，修改安全资料，查看云 API 密钥等敏感操作前需要验证 token 卡上的安全码;
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/85a7a9ecd595b223a8207f56443a1849/image.png)
信息输入无误后，点击【确认】则绑定完成，绑定成功，并开启登录保护和操作保护的状态如下图所示。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/ba1e533f52a4cee0dbcae8f623c07347/image.png)

### 什么是登录保护？
目前云平台提供两种登录保护，普通用户采用 QQ 安全中心口令验证方式，内测版用户采用 MFA 口令验证方式（Multi-FactorAuthentication多因子认证）；

开启登录保护后，在登录云平台官方网站时需要验证身份。这样即使他人盗取您的密码，也无法登录您的帐号，能够最大限度地保证您的帐号安全。
- 普通用户采用 QQ 安全中心口令验证，输入 QQ 安全中心工具栏顶部的 6 位动态安全码即可完成身份验证。
- 内测用户采用 MFA 口令验证，输入对应帐号的 MFA 设备上的 6 位动态安全码即可完成身份验证。

开启登陆保护后，即使密码泄漏，也能最大限度的保证您的帐号安全。

### 如果账号绑定了 MFA，手机丢失后如何登录账号？
您好，如果您没有完成账号实名制认证 无法操作解绑。
如果您已完成账号的实名制认证，您可以到官网提交投诉与反馈，提供如下信息进行申请解绑：
**个人：** 
账号：QQ、邮箱、微信和微信公众号注册的(填写微信和微信公众号账号)、绑定手机号、姓名、证件号码（申请人须与实名认证信息一致)，上传手持身份证照片、可以联系到客户的手机号。
**企业：** 
账号：QQ、邮箱、微信和微信公众号注册的(填写微信和微信公众号账号)、绑定手机号、企业名称、证件号码、公司营业执照证件照片或者彩色扫描件、申请人手持身份证照片。
