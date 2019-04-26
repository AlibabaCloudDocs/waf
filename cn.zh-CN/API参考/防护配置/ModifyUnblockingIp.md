# ModifyUnblockingIp {#doc_api_waf-openapi_ModifyUnblockingIp .reference}

调用ModifyUnblockingIp接口一键解除当前被封禁的IP。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=waf-openapi&api=ModifyUnblockingIp)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyUnblockingIp|要执行的操作。取值：**ModifyUnblockingIp**。

 |
|Defense|String|是|block\_ip|要操作的防护功能。取值：

 -   **block\_dirscan**：目录遍历防护
-   **block\_ip**：高频Web攻击IP自动封禁

 |
|Domain|String|是|www.aliyun.com|要操作的域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以调用[DescribePayInfo](~~86651~~)接口查看当前WAF实例ID。

 |
|Region|String|否|cn|地域ID。取值：

 -   **cn**：中国大陆地区（默认）
-   **cn-hongkong**：海外地区

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1FA7FDD9-6F78-484C-AD13-DC5F1C1AC408|当前请求的ID。

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

http(s)://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=ModifyUnblockingIp
&Defense=block_ip
&Domain=www.aliyun.com
&InstanceId=waf_elasticity-cn-0xldbqtm005
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyUnblockingIpResponse>
  <code>200</code>
  <requestId>1FA7FDD9-6F78-484C-AD13-DC5F1C1AC408</requestId>
  <success>true</success>
</ModifyUnblockingIpResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"1FA7FDD9-6F78-484C-AD13-DC5F1C1AC408",
	"code":200,
	"success":true
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

