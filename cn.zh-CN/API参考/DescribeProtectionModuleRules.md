# DescribeProtectionModuleRules {#reference_xxl_skw_dgb .reference}

调用DescribeProtectionModuleRules接口查询所有网站防篡改规则的信息。

## 请求参数 {#section_pbv_hlw_dgb .section}

|名称|类型|是否必须|描述|
|--|--|----|--|
|Action|String|是|要执行的操作。取值：DescribeProtectionModuleRules

|
|Region|String|是|地域ID。取值：-   cn：中国大陆地区。
-   cn-hongkong：海外地区。

|
|InstanceId|String|是|WAF实例ID。|
|Domain|String|是|要操作的域名名称。|
|Defense|String|是|要操作的防护功能。取值：tamperproof

|
|CurrentPage|Integer|否|列表的页码。默认值：1|
|PageSize|Integer|否|每页的行数。默认值：10|

## 返回参数 {#section_blm_3lw_dgb .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|当前请求的ID。|
|success|Boolen|是否成功完成当前请求。|
|TaskStatus|Integer|当前请求的执行状态：-   0：等待执行。
-   1：正在执行中。
-   2：已执行完成。

|
|Total|Integer|网站防篡改规则的总数。|
|ModuleRules|Sturct|网站防篡改规则的详情。具体结构描述见[ModuleRule](#)。|

|名称|类型|描述|
|:-|:-|:-|
|Version|String|并发锁版本号。|
|Content|Struct|规则内容。具体结构描述见[Content](#)。|
|Time|Long|创建时间。|
|Id|Long|该规则的ID。|

|名称|类型|描述|
|:-|:-|:-|
|name|String|规则名称。|
|uri|String|该规则所防护的URI。|
|status|Boolen|该规则是否启用。|

## 示例 {#section_p1w_3lw_dgb .section}

**请求示例**

```
https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=ModifyProtectionRuleCacheStatus
&Region=cn
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Domain=www.aliyun.com
&Defense=tamperproof
&CurrentPage=1
&PageSize=10
```

**返回示例**

```
{
	"code": 200,
	"data": {
        "ModuleRules":[{
			"Version":1,
			"Content":{
				"name":"test123",
				"uri":"http://xx11.aliyun.com/example/",
				"status":1
			},
			"Time":0,
			"Id":149
		}]
       "TaskStatus": 2,
       "Total":111
	},
	"requestId": "66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"success": true
}
```

