# ModifyProtectionRuleCacheStatus {#doc_api_waf-openapi_ModifyProtectionRuleCacheStatus .reference}

调用ModifyProtectionRuleCacheStatus接口更新指定网站防篡改规则所防护的页面的缓存。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=ModifyProtectionRuleCacheStatus&type=RPC&version=2018-01-17)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyProtectionRuleCacheStatus|要执行的操作。取值：**ModifyProtectionRuleCacheStatus**。

 |
|Defense|String|是|tamperproof|要操作的防护功能。取值：**tamperproof**。

 |
|Domain|String|是|www.aliyun.com|要操作的域名名称。

 |
|Id|Long|是|111|要操作的规则ID。调用[DescribeProtectionModuleRules](~~100398~~)接口可以查询到所有规则ID。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 |
|Region|String|否|cn|地域ID。取值：

 -   **cn**：中国大陆地区（默认）
-   **cn-hongkong**：海外地区

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|66A98669-CC6E-4F3E-80A6-3014697B11AE|当前请求的ID。

 |
|TaskStatus|Integer|2|当前请求的执行状态：

 -   **0**：等待执行。
-   **1**：正在执行中。
-   **2**：已执行完成。

 |
|WafTaskId|Integer|123|WAF的请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=ModifyProtectionRuleCacheStatus
&Region=cn
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Domain=www.aliyun.com
&Defense=tamperproof
&Id=111
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyProtectionRuleCacheStatusResponse>
     <code>200</code>
     <data>
          <TaskStatus>2</TaskStatus>
          <WafTaskId>123</WafTaskId>
     </data>
     <requestId>66A98669-CC6E-4F3E-80A6-3014697B11AE</requestId>
</ModifyProtectionRuleCacheStatusResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"data":{
		"TaskStatus":2,
		"WafTaskId":123
	},
	"code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/waf-openapi)查看更多错误码。

