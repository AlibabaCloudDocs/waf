# DescribeDomainConfigStatus {#doc_api_908422 .reference}

调用DescribeDomainConfigStatus接口查询指定域名的转发配置是否生效。

## 调试 {#apiExplorer .section}

单击[这里](https://api.aliyun.com/#product=waf-openapi&api=DescribeDomainConfigStatus)在OpenAPI Explorer中进行可视化调试，并生成SDK代码示例。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以通过调用[DescribePayInfo](~~86651~~)接口查看您当前WAF实例ID。

 |
|Domain|String|否|rstest.cdn.com|已添加的域名名称。

 |
|Region|String|否|cn|WAF实例所在的地域。取值：

 -   **cn**：表示中国大陆地区。
-   **cn-hongkong**：表示海外地区。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|请求ID。

 |
|Result| | |返回结果。

 |
|└DomainConfig| | |域名转发配置结构体。

 |
|└ConfigStatus|String|1|域名转发配置生效状态：

 -   **0**：表示未生效。
-   **1**：表示已生效。
-   **2**：表示尚未检测完成。

 |
|└Status|Integer|2|请求执行状态：

 -   **0**：表示该请求等待执行。
-   **1**：表示该请求正在执行中。
-   **2**：表示该请求已执行完成。

 |
|└WafTaskId|String|aliyun.waf.20180712214032277.qmxI9a|WAF的请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeDomainConfigStatus
&Domain=www.aliyun.com
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDomainConfigStatusResponse>
  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
  <Result>
    <Status>2</Status>
    <DomainConfig>
      <ConfigStatus>2</ConfigStatus>
    </DomainConfig>
    <WafTaskId>aliyun.waf.20180712214032277.qmxI9a</WafTaskId>
  </Result>
</DescribeDomainConfigStatusResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Result":{
		"Status":2,
		"WafTaskId":"aliyun.waf.20180712214032277.qmxI9a",
		"DomainConfig":{
			"ConfigStatus":2
		}
	},
	"RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

