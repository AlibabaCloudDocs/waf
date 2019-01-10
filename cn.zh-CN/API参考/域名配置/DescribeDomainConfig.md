# DescribeDomainConfig {#doc_api_908424 .reference}

调用DescribeDomainConfig接口获取指定域名的转发配置信息。

## 调试 {#apiExplorer .section}

单击[这里](https://api.aliyun.com/#product=waf-openapi&api=DescribeDomainConfig)在OpenAPI Explorer中进行可视化调试，并生成SDK代码示例。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Domain|String|是|rstest.cdn.com|已添加的域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以通过调用[DescribePayInfo](~~86651~~)接口查看您当前WAF实例ID。

 |
|Region|String|否|cn|WAF实例所在的地域。取值：

 -   **cn**：表示中国大陆地区。
-   **cn-hongkong**：表示海外地区。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|56B40D30-4960-4F19-B7D5-2B1F0EE6CB70|请求ID。

 |
|Result| | |返回结果。

 |
|└DomainConfig| | |域名配置结构体。

 |
|└Cname|String|xxxxxxxxxxxxxx.fakewaf.com|WAF实例分配的CNAME。

 |
|└ProtocolType|Integer|2|协议类型：

 -   **0**：表示支持HTTP协议。
-   **1**：表示支持HTTPS协议。
-   **2**：表示同时支持HTTP和HTTPS协议。

 |
|└SourceIps|String|1.1.1.1|源站IP。

 |
|└Status|Integer|2|请求执行状态：

 -   **0**：表示该请求等待执行。
-   **1**：表示该请求正在执行中。
-   **2**：表示该请求已执行完成。

 |
|└WafTaskId|String|aliyun.waf.20180712180229702.Y6re3d|WAF的请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeDomainConfig
&Domain=www.aliyun.com
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDomainConfigResponse>
  <RequestId>56B40D30-4960-4F19-B7D5-2B1F0EE6CB70</RequestId>
  <Result>
    <Status>2</Status>
    <DomainConfig>
      <ProtocolType>2</ProtocolType>
      <SourceIps>x.x.x.x</SourceIps>
      <SourceIps>x.x.x.x</SourceIps>
      <Cname>xxxxxxxxxxxxxx.fakewaf.com</Cname>
    </DomainConfig>
    <WafTaskId>aliyun.waf.20180712180229702.Y6re3d</WafTaskId>
  </Result>
</DescribeDomainConfigResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Result":{
		"Status":2,
		"WafTaskId":"aliyun.waf.20180712180229702.Y6re3d",
		"DomainConfig":{
			"Cname":"xxxxxxxxxxxxx.fakewaf.com",
			"ProtocolType":2,
			"SourceIps":[
				"x.x.x.x",
				"x.x.x.x"
			]
		}
	},
	"RequestId":"56B40D30-4960-4F19-B7D5-2B1F0EE6CB70"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

