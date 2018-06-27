## 1 背景说明

1. 脏字指云通信为APP配置的敏感词，如果检查的内容包含脏字，将拒绝请求，并返回[80001错误](/doc/product/269/错误码#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)；
2. 脏字检查的内容包括群组消息（只检查文本消息[TIMTextElem](/doc/product/269/消息格式描述#2.1-.E6.96.87.E6.9C.AC.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0)，不支持对自定义消息[TIMCustomElem](/doc/product/269/消息格式描述#2.4-.E8.87.AA.E5.AE.9A.E4.B9.89.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0)的过滤）、群组资料（群名称、群简介、群公告）和群名片；
3. 云通信的脏字集中已经涵盖了一批默认脏字（政治、色情等领域）；
4. 如果APP有除默认脏字集之外的自定义脏字需求，可以通过脏字管理的REST API进行配置。

## 2 功能说明 

1. APP管理员可以通过该接口查询已设置的自定义脏字。 
 
## 3 接口调用说明 

### 3.1 请求URL
```
http://console.tim.qq.com/v4/openim_dirty_words/get?usersig=xxx&identifier=admin&sdkappid=88888888&random=99999999&contenttype=json 
```

### 3.2 请求参数 

URL中各参数的含义以及填写方式参见[REST API简介](/doc/product/269/REST API简介)。 

### 3.3 最高调用频率 

100次/秒。如需提升调用频率，请根据[工单模板](/doc/product/269/云通信配置变更需求工单#2.15-rest-api.E8.B0.83.E7.94.A8.E9.A2.91.E7.8E.87.E8.B0.83.E6.95.B4)提交工单申请处理。 

### 3.4 HTTP请求方式 

POST 

### 3.5 HTTP请求包体格式 

JSON 

### 3.6 请求包示例

查询已经对APP设置的自定义脏字。 

### 3.7 应答包体示例

```
{
    "ActionStatus": "OK", 
    "ErrorInfo": "", 
    "ErrorCode": 0,
    "DirtyWordsList": [
        "回收金币",
        "代刷人气",
        "抽奖"
    ]
}
```

### 3.8 应答包字段说明 

| 字段 | 类型 | 说明 |
|---------|---------|---------|
| ActionStatus | String | 请求处理的结果，“OK”表示处理成功，“FAIL”表示失败。 |
| ErrorCode | Integer | 错误码。  |
| DirtyWordsList | Array  | 返回结果是已经设置的自定义脏字。  |

### 3.9 错误码说明 

除非发生网络错误（例如502错误），该接口的HTTP返回码均为200。真正的错误码、错误信息是通过应答包体中的ErrorCode、ErrorInfo来表示的。 
公共错误码（60000到79999）参见[REST API公共错误码](/doc/product/269/错误码#rest-api.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。 
本API私有错误码如下： 

| 错误码 | 含义说明| 
|---------|---------|
| 10002 | 系统错误，请再次尝试或联系技术客服。 | 
| 10003 | 请求命令非法，请再次尝试或联系技术客服。 | 
| 10007 | 操作权限不足。请确认操作者是否是[APP管理员](/doc/product/269/账号登录集成说明#3.4-app.E7.AE.A1.E7.90.86.E5.91.98)。| 

## 4 接口调试工具 

### 4.1 Web调试工具 

通过[REST API在线调试工具](http://avc.qcloud.com/im/APITester/APITester.html#v4/openim_dirty_words/get)调试本接口。 

### 4.2 Server调试工具 

无。
更多调试工具参见[REST API调试工具](/doc/product/269/REST%20API简介#5-rest-api.E8.B0.83.E8.AF.95.E5.B7.A5.E5.85.B7)。

## 5 API集成 

### 5.1 PHP集成 

无。

## 6 可能触发的回调 

无 。

## 7 参考 

REST API：添加APP的自定义脏字（[v4/openim_dirty_words/add](/doc/product/269/添加APP自定义脏字)）； 
REST API：删除APP的自定义脏字（[v4/openim_dirty_words/delete](/doc/product/269/删除APP自定义脏字)）。 


