## 功能描述
ApplyIps 用于申请黑石私有网络子网IP。

接口请求域名：bmvpc.api.qcloud.com


## 请求

### 请求示例
```
GET http://bmvpc.api.qcloud.com/v2/index.php?Action=ApplyIps
    &<公共请求参数>
    &unVpcId=<VPC网络唯一ID>
	&unSubnetId=<子网唯一ID>
	&count=<申请IP个数>
    &ipClass=<IP类型>
```
### 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见<a href="/doc/api/372/4153" title="公共请求参数">公共请求参数</a>页面。其中，此接口的Action字段为ApplyIps。

| 参数名称 |描述 | 类型 | 必选  | 
|---------|---------|---------|---------|
| unVpcId |系统分配的私有网络ID，例如：vpc-kd7d06of。可通过DescribeBmVpcEx接口查询返回的unVpcId值。 | String |  是 |
| unSubnetId |  系统分配的私有网络子网ID，例如：subnet-k20jbhp0。可通过DescribeBmSubnetEx接口查询返回的unSubnetId值。 |String | 是 |
| count |申请IP个数，默认为1，取值范围1-20。 | Int |  否 |
| ipClass | IP类型，0为物理机IP，1为虚拟机类型IP，2为托管类型IP。默认传1 | Int | 否 |


## 响应

### 响应示例
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": [
        "10.6.100.40"
    ],
    "count": 1
}
```
### 响应参数

| 参数名称 | 描述 | 类型 |
|---------|---------|---------|
| code | 公共错误码, 0表示成功，其他值表示失败。详见错误码页面的<a href="/doc/api/372/%E9%94%99%E8%AF%AF%E7%A0%81#1.E3.80.81.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="公共错误码">公共错误码</a>。| Int |
| message | 模块错误信息描述，与接口相关。| String |
| count |申请成功的IP个数。| Int | 
| data.n | 申请成功的IP数组。| Array |

## 错误码

| 错误代码 |英文提示| 描述 |
|---------|---------|---------|
| -3047 |InvalidBmVpc.NotFound| 无效的VPC,VPC资源不存在，请再次核实您输入的资源信息是否正确。 |
| -3030  |InvalidBmSubnet.NotFound| 无效的子网,子网资源不存在，请再次核实您输入的资源信息是否正确。 |
| -3031 |AvailableIpUseUp| 没有可用的IP可以分配。 |
| -3001| InvalidInputParams|参数不合法


## 实际案例
### 输入
```
GET http://bmvpc.api.qcloud.com/v2/index.php?
	Action=ApplyIps
	&SecretId=AKIDlfdHxN0ntSVt4KPH0xXWnGl21UUFNoO5
    &Nonce=6791
    &Timestamp=1507777243
    &Region=bj
    &Signature=RLfmJ0mnkm2Fla4zbTGABkRA%2Ft4%3D
	&unVpcId=vpc-2ari9m7h
	&unSubnetId=subnet-keqt3oty
	&count=1
	&ipClass=1
```

### 输出
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": [
        "10.6.100.40"
    ],
    "count": 1
}
```
