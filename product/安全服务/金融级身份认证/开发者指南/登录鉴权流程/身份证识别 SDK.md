<!--- 身份识别 SDK -->
## 整体登录鉴权流程
### 第一步：Access Token 获取
- Access Token 有效期 7200 秒，建议合作方缓存在服务器，必须在临近过期和使用中失效时重新获取。获取方式见 [Access Token 获取](/document/product/655/13813)。

### 第二步：SDK 登录鉴权
- NONCE ticket 有效期 120 秒，且仅一次性有效。
- 在用户登录流程中，获取 API ticket 请求的 user_id 为必填参数，type 为 NONCE。获取方式见 [NONCE ticket 获取](/document/product/655/13816)。

### 第三步：返回结果服务端验证
- SIGN ticket 有效期 3600 秒，建议合作方缓存在服务器，必须在临近过期和使用中失效时重新获取。流程中，获取 API ticket 请求的 type 为 SIGN。获取方式见 [SIGN ticket 获取](/document/product/655/13815)。现有以下两种方式返回结果验证：
- 方式一：签名验证
  合作伙伴 App 端调用其服务后台验证签名，验证成功后即可信任前端的返回结果。
- 方式二：服务端查询结果
  合伙伙伴 App 端调用其服务后台查询识别结果，由 OCR 识别服务端鉴权并返回最终结果。

具体接入开发指南见：[**身份证识别 SDK 接入**](/document/product/655/13846)
## 流程图示
 ![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/757aebd7592edcc02fa967a875dc70c4/ID+card+OCR.png)



更多产品鉴权流程：[登录鉴权概览](/document/product/655/13663)
