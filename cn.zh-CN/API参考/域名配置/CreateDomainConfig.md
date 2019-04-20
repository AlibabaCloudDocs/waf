# CreateDomainConfig {#doc_api_waf-openapi_CreateDomainConfig .reference}

调用CreateDomainConfig接口添加域名配置信息。

**通过调用API接口，将您的域名接入WAF实例实现Web安全防护，建议您参考以下步骤：**

1. 调用[CreateDomainConfig](~~86412~~)接口添加域名配置信息。

2. 根据返回结果中的**WafTaskId**值，调用[DescribeAsyncTaskStatus](~~86725~~)接口查看添加域名配置任务的执行进度。当该任务已完成时，说明域名配置信息已成功添加。

3. 调用[DescribeDomainConfigStatus](~~86404~~)接口确认该域名配置是否生效。

**说明：** 只有当返回结果显示配置已经生效后，您才可以将业务流量切换至WAF实例。

4. 调用[DescribeDomainConfig](~~86389~~)接口查看WAF实例为该域名分配的CNAME。

5. 在域名DNS解析服务提供商处，修改该域名的解析记录，将业务流量切换至WAF。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=waf-openapi&api=CreateDomainConfig)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDomainConfig|要执行的操作。取值：**CreateDomainConfig**。

 |
|Domain|String|是|rstest.cdn.com|域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以通过调用[DescribePayInfo](~~86651~~)接口查看您当前WAF实例ID。

 |
|Protocols|String|是|\["http"\]|该域名所支持的访问协议，取值：

 -   **http**：表示支持HTTP协议。
-   **https**：表示支持HTTPS协议。
-   **http,https**：同时支持HTTP、HTTPS协议。

 |
|SourceIps|String|是|\[1.1.1.1\]|源站IP，支持指定多个IP。示例值：`["1.1.1.1"]`。

 |
|HttpPort|String|否|\[80\]|HTTP协议配置的端口。指定多个HTTP端口时，使用“,”进行分隔。示例值：`[80]`。

 **说明：** 配置协议为HTTP时，该参数为必填项。默认值为**80**。**HttpPort**与**HttpsPort**两个请求参数至少需要填一个。

 |
|HttpToUserIp|Integer|否|0|是否开启HTTPS访问请求通过HTTP协议转发回源站，取值：

 -   **0**：表示关闭 （默认）
-   **1**：表示开启

 **说明：** 如果您的网站不支持HTTPS回源，开启HTTP回源（默认回源端口是80端口）功能项，即可通过WAF实现HTTPS访问。

 |
|HttpsPort|String|否|\[443\]|HTTPS协议配置的端口。指定多个HTTPS端口时，使用“,”进行分隔。示例值：`[443]`。

 **说明：** 配置协议为HTTPS时，该参数为必填项。默认值为**443**。**HttpPort**与**HttpsPort**两个请求参数至少需要填一个。

 |
|HttpsRedirect|Integer|否|0|是否开启HTTPS强制跳转，取值：

 -   **0**：表示关闭 （默认）
-   **1**：表示开启

 **说明：** 仅使用HTTPS访问协议时需填写该请求参数。开启强制跳转后HTTP请求将显示为HTTPS，默认跳转至443端口。

 |
|IsAccessProduct|Integer|否|0|该域名在WAF前是否配置有七层代理（例如，高防、CDN等），取值：

 -   **0**：表示无。
-   **1**：表示有。

 |
|LoadBalancing|Integer|否|0|回源负载均衡策略，取值：

 -   **0**：表示IP Hash方式。
-   **1**：表示轮询方式。

 |
|Region|String|否|cn|WAF实例所在的地域。取值：

 -   **cn**：表示中国大陆地区（默认）
-   **cn-hongkong**：表示海外地区

 |
|RsType|Integer|否|0|该域名的回源地址类型，取值：

 -   **0**：表示回源到IP。
-   **1**：表示回源到域名。

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

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=CreateDomainConfig
&Domain=www.aliyun.com
&SourceIps=["x.x.x.x","x.x.x.x"]
&Protocols=["http","https"]
&HttpPort=[80]
&HttpsPort=[443]
&RsType=0
&IsAccessProduct=0
&LoadBalancing=0
&HttpsRedirect=1
&HttpToUserIp=0
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateDomainConfigResponse>
  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
  <Result>
    <Status>2</Status>
    <WafTaskId>aliyun.waf.20180712214032277.qmxI9a</WafTaskId>
  </Result>
</CreateDomainConfigResponse>

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

