## 1. 接口描述
 
本接口(EmrDestroyCluster)用于销毁一个创建好的emr集群。

接口请求域名：<font style="color:red">emr.api.qcloud.com</font>


## 2. 输入参数
 以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见<a href="/doc/api/372/4153" title="公共请求参数">公共请求参数</a>页面。其中，此接口的Action字段为EmrDestroyCluster。

| 参数名称 | 是否必选  | 类型 | 描述 |
|---------|---------|---------|---------|
| ClusterId | 是 | string | emr集群ID，emr-xxxx格式 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| code | Int | 公共错误码, 0表示成功，其他值表示失败。详见错误码页面的<a href="/doc/api/372/%E9%94%99%E8%AF%AF%E7%A0%81#1.E3.80.81.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="公共错误码">公共错误码</a>。|
| message | String | 模块错误信息描述，与接口相关。|

## 4. 示例
 
输入
<pre>
  http://emr.api.qcloud.com/v2/index.php?Action=EmrDestroyCluster
  &<<a href="/doc/api/229/6976">公共请求参数</a>>
  &ClusterId=emr-rowyenms

</pre>

输出
```
{
    "code": 0,
    "message": ""
}
```
