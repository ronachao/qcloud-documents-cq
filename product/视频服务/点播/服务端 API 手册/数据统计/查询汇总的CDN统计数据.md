## 接口名称
DescribeCdnStat

## 功能说明
用于查询指定域名在某一时间区间的累计的CDN统计数据。如果查询流量、请求数，返回的是这段时间累计的总流量、总请求数，如果查询是的是带宽数据，返回的是这段时间的峰值带宽数据。

### 详细说明
1. 流量的单位是byte(字节），带宽的单位是bps(比特每秒)
2.  可以查询最近90天的数据。

*本接口只支持点播4.0*

## 事件通知
无

## 请求方式

### 请求域名
vod.api.qcloud.com

### 最高调用频率
100次/分钟

### 参数说明
| 参数名称      | 必填 | 类型   | 说明                                                                                                           |
| ------------- | ---- | ------ | -------------------------------------------------------------------------------------------------------------- |
| hosts         | 否   | Array  | 域名列表，一次最多查询20个域名，如果为空。将查询用户的所有点播域名的统计数据（如果域名数超过20个，则返回错误） |
| startDate     | 是   | string | 起始时间，格式为yyyy-MM-dd HH:mm:ss如 2018-03-20 00:00:00                                                      |
| endDate       | 是   | string | 结束时间，格式为yyyy-MM-dd HH:mm:ss如 2018-03-23 23:55:00                                                      |
| statType      | 是   | string | CDN统计数据类型， flux表示总流量， bandwidth表示峰值带宽，requests表示总请求数，cache表示平均请求命中率        |
| COMMON_PARAMS | 是   |        | 参见[公共参数](/document/product/266/7782#.E5.85.AC.E5.85.B1.E5.8F.82.E6.95.B0)                                |

### 请求示例
```
http://vod.api.qcloud.com/v2/index.php?Action=DescribeCdnStat&hosts.0=123.vod2.myqcloud.com&startDate=2017-03-20 00:00:00&endDate=2017-03-26:23:55:00&statType=flux
&hosts.0=123.vod2.myqcloud.com&COMMON_PARAMS
```
## 接口应答

### 参数说明
| 参数名称       | 类型    | 说明                                   |
| -------------- | ------- | -------------------------------------- |
| code           | Integer | 错误码, 0: 成功, 其他值: 失败          |
| message        | String  | 错误信息                               |
| data           | Object  | 结果数据                               |
| data.hostDatas | Array   | 域名的统计数据列表，见HostStatData说明 |

#### HostStatData
| 参数名称     | 类型    | 说明                                          |
| ------------ | ------- | --------------------------------------------- |
| host         | String  | 域名                                          |
| value        | Integer | 国内CDN节点的统计数据，如流量大小或者峰值带宽 |
| overseaValue | Integer | 海外CDN节点的统计数据，如流量大小或者峰值带宽 |

### 错误码说明
| 错误码    | 含义说明                                     |
| --------- | -------------------------------------------- |
| 4000-7000 | 参见[公共错误码](/document/product/266/7783) |
| 1         | 内部错误                                     |
| 1000      | 无效参数                                     |
| 1001      | 内部错误                                     |
| 1003      | 内部错误                                     |
| 2000      | 内部错误                                     |
| 10022     | 内部错误                                     |

### 应答示例
```javascript
{
	"code": 0,
	"message": "",
	"data": {
		"hostDatas": [{
			"host": "123.vod2.myqcloud.com",
			"value": 13659874512,
			"oveaseaValue": 654859
		}]
	}
}
```
