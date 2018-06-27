## 1.接口描述
本接口（QueryCfsRule）用于查询权限组规则列表。
接口请求域名：**cfs.api.qcloud.com**
## 2.输入参数
|       参数      |  必填 |  类型  |                               描述                           |
|-----------------|------|--------|--------------------------------------------------------------|
|PGroupId    |   是  | string | 权限组ID |

## 3.输出参数
| 参数名称 | 子参数 | 类型 | 描述 |
|----------|------  |----- | ---- |
|RuleList |         |  array  |权限组规则列表 |
|          | RuleId |   string |规则ID |
|          | ClientIp |  string |允许访问的客户端IP |
|          | RWPermission|  string |读写权限, ro为只读，rw为读写 |
|          | UserPermission   | string |用户权限。其中root_squash为所有访问用户都会被映射为匿名用户或用户组；no_all_squash为访问用户会先与本机用户匹配，匹配失败后再映射为匿名用户或用户组；root_squash为将来访的root用户映射为匿名用户或用户组；no_root_squash为来访的root用户保持root帐号权限。 |
|          | Priority|  int    |规则优先级，1-100。 其中 1 为最高，100为最低|


## 4.示例 

### 输入


```
<pre>
  http://cfs.test.api.qcloud.com/v2/index.php?Action=QueryCfsRule
  &Uin=2779000000
  &AppId=12500000000
  &PGroupId=pgroup-atutdqup
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
        "RuleList": [
            {
                "RuleId": "rule-9c93j63j",
                "ClientIp": "10.15.21.100",
                "RWPermission": "rw",
                "UserPermission": "root_squash",
                "Priority": 7
            }
        ]
    }
}

```


