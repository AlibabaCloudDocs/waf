# DescribeProtectionModuleCodeConfig {#doc_api_waf-openapi_DescribeProtectionModuleCodeConfig .reference}

调用DescribeProtectionModuleCodeConfig接口获取防护模块支持的code列表，如区域封禁地理信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=waf-openapi&api=DescribeProtectionModuleCodeConfig)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeProtectionModuleCodeConfig|要执行的操作。取值：**DescribeProtectionModuleCodeConfig**。

 |
|CodeType|Integer|是|14|Code类型，取值：

 -   **14**：区域封禁地理信息

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以调用[DescribePayInfo](~~86651~~)接口查看当前WAF实例ID。

 |
|CodeValue|Integer|否|0|要查看的code的值。区域封禁地理信息的取值：

 -   **0**：国内省地理信息码全集
-   **1**：海外国家短码全集

 |
|Region|String|否|cn|地域ID。取值：

 -   **cn**：中国大陆地区（默认）
-   **cn-hongkong**：海外地区

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|CodeConfigs|String|详见返回示例|code列表信息。区域封禁地理信息的具体结构如下：

 -   **code**，Interger类型，code的值。取值：
    -   **0**：国内省地理信息码
    -   **1**：海外国家短码
-   **name**，String类型，支持的code列表。

 |
|RequestId|String|66A98669-CC6E-4F3E-80A6-3014697B11AE|当前请求的ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeProtectionModuleCodeConfig
&CodeType=14
&InstanceId=waf_elasticity-cn-0xldbqtm005
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeProtectionModuleCodeConfigResponse>
  <code>200</code>
  <data>
    <CodeConfig>
      <element>
        <code>0</code>
        <name>310000,530000,150000,110000,TW_01,220000,510000,120000,640000,340000,370000,140000,440000,450000,650000,320000,360000,130000,410000,330000,460000,420000,430000,MO_01,620000,350000,540000,520000,210000,500000,610000,630000,HK_01,230000</name>
      </element>
      <element>
        <code>1</code>
        <name>JP,KR,US,AU,MY</name>
      </element>
    </CodeConfig>
  </data>
  <requestId>66A98669-CC6E-4F3E-80A6-3014697B11AE</requestId>
  <success>true</success>
</DescribeProtectionModuleCodeConfigResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"data":{
		"CodeConfig":[
			{
				"name":"310000,530000,150000,110000,TW_01,220000,510000,120000,640000,340000,370000,140000,440000,450000,650000,320000,360000,130000,410000,330000,460000,420000,430000,MO_01,620000,350000,540000,520000,210000,500000,610000,630000,HK_01,230000",
				"code":0
			},
			{
				"name":"JP,KR,US,AU,MY",
				"code":1
			}
		]
	},
	"code":200,
	"success":true
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

