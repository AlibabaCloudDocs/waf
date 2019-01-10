# ModifyDomainConfig {#doc_api_908421 .reference}

调用ModifyDomainConfig接口修改指定域名配置信息。

## 调试 {#apiExplorer .section}

单击[这里](https://api.aliyun.com/#product=waf-openapi&api=ModifyDomainConfig)在OpenAPI Explorer中进行可视化调试，并生成SDK代码示例。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Domain|String|是|rstest.cdn.com|域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以通过调用[DescribePayInfo](~~86651~~)接口查看您当前WAF实例ID。

 |
|IsAccessProduct|Integer|是|0|该域名在WAF前是否配置有七层代理（例如，高防、CDN等），取值：

 -   **0**：表示无。
-   **1**：表示有。

 |
|HttpPort|String|否|80|HTTP协议配置的端口。指定多个HTTP端口时，使用“,”进行分隔。

 **说明：** 配置协议为HTTP时，该参数为必填项。默认值为**80**。**HttpPort**与**HttpsPort**两个请求参数至少需要填一个。

 |
|HttpToUserIp|Integer|否|0|是否开启HTTPS访问请求通过HTTP协议转发回源站，取值：

 -   **0**：表示关闭 （默认）
-   **1**：表示开启

 **说明：** 如果您的网站不支持HTTPS回源，开启HTTP回源（默认回源端口是80端口）功能项，即可通过WAF实现HTTPS访问。

 |
|HttpsPort|String|否|443|HTTPS协议配置的端口。指定多个HTTPS端口时，使用“,”进行分隔。

 **说明：** 配置协议为HTTPS时，该参数为必填项。默认值为**443**。**HttpPort**与**HttpsPort**两个请求参数至少需要填一个。

 |
|LoadBalancing|Integer|否|0|负载均衡的方式，取值：

 -   **0**：IP hash
-   **1**：轮询

 |
|Protocols|String|否|http|该域名所支持的访问协议，取值：

 -   **http**：表示支持HTTP协议。
-   **https**：表示支持HTTPS协议。
-   **http,https**：同时支持HTTP、HTTPS协议。

 |
|Region|String|否|cn|WAF实例所在的地域。取值：

 -   **cn**：表示中国大陆地区。
-   **cn-hongkong**：表示海外地区。

 |
|SourceIps|String|否|1.1.1.1|源站IP，支持指定多个IP。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|请求ID。

 |
|Result| | |返回结果。

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

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=ModifyDomainConfig
&Domain=www.aliyun.com
&SourceIps=["x.x.x.x","x.x.x.x"]
&Protocols=["http","https"]
&HttpPort=[80]
&HttpsPort=[443]
&IsAccessProduct=0
&HttpsRedirect=1
&HttpToUserIp=0
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDomainConfigResponse>
  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
  <Result>
    <Status>2</Status>
    <WafTaskId>aliyun.waf.20180712214032277.qmxI9a</WafTaskId>
  </Result>
</ModifyDomainConfigResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Result":{
		"Status":2,
		"WafTaskId":"aliyun.waf.20180712214032277.qmxI9a"
	},
	"RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

