## 1.接口描述
本接口（DeleteCfsPGroup）用于删除权限组。
接口请求域名：**cfs.api.qcloud.com**
## 2.输入参数
|       参数      | 必填 |  类型  |                               描述                           |
|-----------------|------|--------|--------------------------------------------------------------|
| PGroupId        | 是   | string | 权限组ID|


## 3.输出参数
| 参数名称 |  类型 | 描述 |
|----------|----- | ---- |
|AppId     | int    |用户ID   |
|PGroupId   | string |权限组ID |


## 4.示例 

### 输入


```
<pre>
  http://cfs.test.api.qcloud.com/v2/index.php?Action=DeleteCfsPGroup
  &Uin=27790000000
  &AppId=1250000000
  &PGroupId=pgroup-qa948g7z
  &<<a href="http://www.tce.fsphere.cn/doc/api/229/6976"> 公共请求参数 </a>>
</pre>
```

### 输出

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "PGroupId": "pgroup-qa948g7z",
        "AppId": 1250000000
    }
}

```


