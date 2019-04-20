# DescribePayInfo {#doc_api_waf-openapi_DescribePayInfo .reference}

调用DescribePayInfo接口获取指定地域的WAF实例当前信息。

**说明：** 请求该API接口时，无需指定**InstanceId**公共请求参数。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=waf-openapi&api=DescribePayInfo)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribePayInfo|要执行的操作。取值：**DescribePayInfo**。

 |
|InstanceSource|String|否|waf-cloud|实例来源。默认值：**waf-cloud**。

 |
|Region|String|否|cn|地域ID，取值：

 -   **cn**：表示中国大陆地区（默认）
-   **cn-hongkong**：表示海外地区

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|276D7566-31C9-4192-9DD1-51B10DAC29D2|请求ID。

 |
|Result| | |返回结果。

 |
|└EndDate|Long|1512921600|实例到期时间。

 **说明：** 对于按量付费实例，表示试用版到期时间。

 |
|└InDebt|Integer|1|当前实例是否欠费：

 -   **0**：表示已欠费。
-   **1**：表示正常。

 **说明：** 该参数按量计费WAF实例有意义。

 |
|└InstanceId|String|waf\_elasticity-cn-0xldbqtm005|实例ID。

 |
|└PayType|Integer|2|WAF实例类型：

 -   **0**：表示未购买或未开通。
-   **1**：表示包年包月实例。
-   **2**：表示按量付费实例。

 |
|└Region|String|cn|所属地域：

 -   **cn**：表示中国大陆地区。
-   **cn-hongkong**：表示海外地区。

 |
|└RemainDay|Integer|0|试用版WAF实例剩余可用天数。

 **说明：** 该参数仅对按量计费WAF实例有意义。

 |
|└Status|Integer|0|WAF实例当前状态：

 -   **0**：表示已到期。
-   **1**：表示正常。

 **说明：** 该参数仅对包年包月WAF实例有意义。

 |
|└Trial|Integer|0|是否试用版WAF实例：

 -   **0**：表示否。
-   **1**：表示是。

 **说明：** 该参数仅对按量计费WAF实例有意义。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribePayInfo
&Region=cn
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribePayInfoResponse>
  <RequestId>56B40D30-4960-4F19-B7D5-2B1F0EE6CB70</RequestId>
  <Result>
    <Status>1</Status>
    <Trial>0</Trial>
    <InstanceId>waf_elasticity-cn-0xldbqtm005</InstanceId>
    <InDebt>1</InDebt>
    <Region>cn</Region>
    <RemainDay>0</RemainDay>
    <PayType>2</PayType>
    <EndDate>1512921600</EndDate>
  </Result>
</DescribePayInfoResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Result":{
		"Status":1,
		"EndDate":1512921600,
		"Region":"cn",
		"InDebt":1,
		"Trial":0,
		"InstanceId":"waf_elasticity-cn-0xldbqtm005",
		"RemainDay":0,
		"PayType":2
	},
	"RequestId":"276D7566-31C9-4192-9DD1-51B10DAC29D2"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

