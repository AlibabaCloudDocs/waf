# ModifyProtectionRuleStatus {#doc_api_waf-openapi_ModifyProtectionRuleStatus .reference}

调用ModifyProtectionRuleStatus接口启用或关闭指定的网站防篡改规则。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=waf-openapi&api=ModifyProtectionRuleStatus)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyProtectionRuleStatus|要执行的操作。取值：**ModifyProtectionRuleStatus**。

 |
|Defense|String|是|tamperproof|要操作的防护功能。取值：**tamperproof**。

 |
|Domain|String|是|www.aliyun.com|要操作的域名名称。

 |
|Id|Long|是|111|要操作的规则ID。调用[DescribeProtectionModuleRules](~~100398~~)接口可以查询到所有规则ID。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 |
|LockVersion|Long|是|0|并发锁版本。

 |
|RuleStatus|Integer|是|1|是否启用规则。取值：

 -   **0**：关闭
-   **1**：启用

 |
|Region|String|否|cn|地域ID。取值：

 -   **cn**：中国大陆地区（默认）
-   **cn-hongkong**：海外地区

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|66A98669-CC6E-4F3E-80A6-3014697B11AE|当前请求的ID。

 |
|TaskStatus|Integer|2|当前请求的执行状态：

 -   **0**：等待执行。
-   **1**：正在执行中。
-   **2**：已执行完成。

 |
|WafTaskId|Integer|1232|WAF的请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=ModifyProtectionRuleStatus
&Region=cn
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Domain=www.aliyun.com
&Defense=tamperproof
&Id=111
&RuleStatus=1
&LockVersion=0
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyProtectionRuleStatusResponse>
  <code>200</code>
  <data>
    <TaskStatus>2</TaskStatus>
    <WafTaskId>1232</WafTaskId>
  </data>
  <requestId>66A98669-CC6E-4F3E-80A6-3014697B11AE</requestId>
  <success>true</success>
</ModifyProtectionRuleStatusResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"data":{
		"TaskStatus":2,
		"WafTaskId":1232
	},
	"code":200,
	"success":true
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

