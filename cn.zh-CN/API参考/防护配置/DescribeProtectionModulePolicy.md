# DescribeProtectionModulePolicy {#doc_api_waf-openapi_DescribeProtectionModulePolicy .reference}

调用DescribeProtectionModulePolicy接口查询一个防护功能的防护模式。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=waf-openapi&api=DescribeProtectionModulePolicy)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeProtectionModulePolicy|要执行的操作。取值：**DescribeProtectionModulePolicy**。

 |
|Defense|String|是|antifraud|要操作的防护功能。取值：

 -   **antifraud**：数据风控
-   **waf**：Web攻击防护

 |
|Domain|String|是|www.aliyun.com|要操作的域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|要操作的规则ID。

 **说明：** 您可以调用[DescribeProtectionModuleRules](~~100398~~)接口查看所有规则ID。

 |
|Region|String|否|cn|地域ID。取值：

 -   **cn**：中国大陆地区（默认）
-   **cn-hongkong**：海外地区

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Mode|Integer|1|指定的防护功能的防护模式。取值：

 -   **0**：预警
-   **1**：防护
-   **2**：强拦截

 |
|RequestId|String|66A98669-CC6E-4F3E-80A6-3014697B11AE|当前请求的ID。

 |
|TaskStatus|Integer|123|WAF的请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeProtectionModulePolicy
&Defense=antifraud
&Domain=www.aliyun.com
&InstanceId=waf_elasticity-cn-0xldbqtm005
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeProtectionModulePolicyResponse>
  <code>200</code>
  <data>
    <Mode>1</Mode>
    <TaskStatus>2</TaskStatus>
  </data>
  <requestId>66A98669-CC6E-4F3E-80A6-3014697B11AE</requestId>
  <success>true</success>
</DescribeProtectionModulePolicyResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"data":{
		"TaskStatus":2,
		"Mode":1
	},
	"code":200,
	"success":true
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

