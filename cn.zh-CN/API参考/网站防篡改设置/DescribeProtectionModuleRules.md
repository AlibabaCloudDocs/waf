# DescribeProtectionModuleRules {#doc_api_916756 .reference}

调用DescribeProtectionModuleRules接口查询所有网站防篡改规则的信息。

## 调试 {#apiExplorer .section}

单击[这里](https://api.aliyun.com/#product=waf-openapi&api=DescribeProtectionModuleRules)在OpenAPI Explorer中进行可视化调试，并生成SDK代码示例。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Defense|String|是|tamperproof|要操作的防护功能。取值： **tamperproof**

 |
|Domain|String|是|www.aliyun.com|要操作的域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 |
|CurrentPage|Integer|否|1|列表的页码。默认值：**1**

 |
|PageSize|Integer|否|10|每页的行数。默认值：**10**

 |
|Region|String|否|cn|地域ID。取值：

 -   **cn**：中国大陆地区。
-   **cn-hongkong**：海外地区。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ModuleRules| | |网站防篡改规则的详情。具体结构描述见ModuleRule。

 |
|└Content|String|xx|规则内容。具体结构描述如下：

 -   **name**：String类型，规则名称。
-   **uri**：String类型，该规则所防护的URI。
-   **status**：Boolen类型，该规则是否启用。

 |
|└Id|Long|149|该规则的ID。

 |
|└Time|Long|0|创建时间。

 |
|└Version|Long|1|并发锁版本号。

 |
|RequestId|String|66A98669-CC6E-4F3E-80A6-3014697B11AE|当前请求的ID。

 |
|TaskStatus|Integer|2|当前请求的执行状态：

 -   **0**：等待执行。
-   **1**：正在执行中。
-   **2**：已执行完成。

 |
|Total|Integer|1|网站防篡改规则的总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=ModifyProtectionRuleCacheStatus
&Region=cn
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Domain=www.aliyun.com
&Defense=tamperproof
&CurrentPage=1
&PageSize=10

```

正常返回示例

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"data":{
		"ModuleRules":[
			{
				"Time":0,
				"Id":149,
				"Content":{
					"status":1,
					"name":"test123",
					"uri":"http://xx11.aliyun.com/example/"
				},
				"Version":1
			}
		],
		"TaskStatus":2,
		"Total":111
	},
	"code":200
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

