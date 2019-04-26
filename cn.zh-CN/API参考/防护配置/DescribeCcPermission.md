# DescribeCcPermission {#doc_api_waf-openapi_DescribeCcPermission .reference}

调用DescribeCcPermission接口查询是否启用CC安全防护。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=waf-openapi&api=DescribeCcPermission)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeCcPermission|要执行的操作。取值：**DescribeCcPermission**。

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
|Allowed|Integer|1|CC安全防护的启用状态。取值：

 -   **1**：允许
-   **0**：不允许

 |
|RequestId|String|66A98669-CC6E-4F3E-80A6-3014697B11AE|当前请求的ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeCcPermission
&Domain=www.aliyun.com
&InstanceId=waf_elasticity-cn-0xldbqtm005
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeCcPermissionResponse>
  <code>200</code>
  <data>
    <Allowed>1</Allowed>
  </data>
  <requestId>66A98669-CC6E-4F3E-80A6-3014697B11AE</requestId>
  <success>true</success>
</DescribeCcPermissionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"data":{
		"Allowed":1
	},
	"code":200,
	"success":true
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

