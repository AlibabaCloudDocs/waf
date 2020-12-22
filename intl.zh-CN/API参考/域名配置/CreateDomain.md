# CreateDomain

调用CreateDomain接口添加域名配置信息，将您的域名接入WAF实例进行防护。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=CreateDomain&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDomain|要执行的操作。取值：**CreateDomain**。 |
|Domain|String|是|www.example.com|域名名称。 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqt\*\*\*\*|WAF实例ID。

 **说明：** 您可以通过调用[DescribeInstanceInfo](~~140857~~)接口查看当前WAF实例ID。 |
|IsAccessProduct|Integer|是|0|该域名在WAF前是否配置有七层代理（例如，高防、CDN等），即客户端访问流量到WAF前是否有经过其它七层代理转发，取值：

 -   **0**：表示否。
-   **1**：表示是。 |
|SourceIps|String|否|\["1.1.1.1", "2.2.2.2"\]|域名对应的源站服务器IP或服务器回源域名。

 **说明：** 您只能选择填写源站服务器IP或服务器回源域名中的一种。

 -   填写源站服务器IP时，支持添加最多20个源站服务器IP实现负载均衡，IP间以英文逗号（,）分隔。
-   填写服务器回源域名时，只能填写一个域名地址。 |
|LoadBalancing|Integer|否|0|回源时采用的负载均衡算法，取值：

 -   **0**：表示IP Hash方式。
-   **1**：表示轮询方式。 |
|LogHeaders|String|否|\[\{"k":"wafmark","v":"test"\}\]|域名的流量标记字段和值，用于标记经过WAF的流量。

 该参数值的样式为`[{"k":"_key_","v":"_value_"}]`。其中，`_key_`表示所指定的自定义请求头部字段，`_value_`表示为该字段设定的值。

 通过指定自定义请求头部字段和对应的值，当域名的访问流量经过WAF时，系统将自动在请求头部中添加所设定的自定义字段值作为流量标记，便于后端服务统计相关信息。

 **说明：** 如果请求中已存在该自定义头部字段，系统将用所设定的流量标记值覆盖请求中该自定义字段的值。 |
|HttpPort|String|否|\[80\]|HTTP协议配置的端口。指定多个HTTP端口时，使用英文逗号（,）分隔。

 **说明：** 填写该参数值即表示使用HTTP访问协议，且**HttpPort**与**HttpsPort**两个请求参数至少有一个不为空。 |
|HttpsPort|String|否|\[443\]|HTTPS协议配置的端口。当指定多个HTTPS端口时，使用英文逗号（,）分隔。

 **说明：** 填写该参数值即表示使用HTTPS访问协议，且**HttpPort**与**HttpsPort**两个请求参数至少有一个不为空。 |
|Http2Port|String|否|\[443\]|HTTP 2.0协议配置的端口。当指定多个HTTP 2.0端口时，使用英文逗号（,）分隔。 |
|HttpToUserIp|Integer|否|0|是否开启HTTP回源功能，开启后HTTPS访问请求将通过HTTP协议转发回源站，默认回源端口为80端口，取值：

 -   **0**：表示关闭（默认）。
-   **1**：表示开启。

 **说明：** 如果您的网站不支持HTTPS回源，开启HTTP回源功能可通过WAF支持HTTPS访问。 |
|HttpsRedirect|Integer|否|0|是否开启HTTPS强制跳转，取值：

 -   **0**：表示关闭（默认）。
-   **1**：表示开启。

 **说明：** 只有当域名使用HTTPS访问协议时，需填写该请求参数。开启强制跳转后HTTP请求将显示为HTTPS，默认跳转至443端口。 |
|ClusterType|Integer|否|0|WAF实例的集群类别，取值：

 -   **0**：表示物理集群（默认）。
-   **1**：表示虚拟集群，即WAF独享集群。 |
|ResourceGroupId|String|否|rg-atstuj3rtop\*\*\*\*|域名在资源管理产品中所属的资源组ID。默认为空，即属于默认资源组。 |
|ConnectionTime|Integer|否|5|WAF独享集群连接超时时长，单位：秒。

 **说明：** 使用独享集群防护资源时，可以配置该参数。 |
|ReadTime|Integer|否|120|WAF独享集群读连接超时时长，单位：秒。

 **说明：** 使用独享集群防护资源时，可以配置该参数。 |
|WriteTime|Integer|否|120|WAF独享集群写连接超时时长，单位：秒。

 **说明：** 使用独享集群防护资源时，可以配置该参数。 |
|AccessType|String|否|waf-cloud-dns|网站接入WAF的方式。

 取值：

 -   **waf-cloud-dns**：CNAME接入（默认）。
-   **waf-cloud-native**：透明接入。 |
|CloudNativeInstances|String|否|\[ \{"InstanceId":"i-2vc4k6vbs3f\*\*\*\*", "Port":80\}, \{"InstanceId":"lb-2zent2qvovb6\*\*\*\*", "Port":8080\} \]|透明接入的实例的信息列表。仅当**AcessType**取值为`waf-cloud-native`时，本参数有效。

 本字段为符合JSON规范的字符串，包含以下字符：

 -   InstanceId：实例ID。
-   Port：透明接入配置的端口，即引流端口。 |
|IpFollowStatus|Integer|否|1|回源地址为IPv4或IPv6地址时，是否开启协议跟随回源。即访问的网站地址为IPv4地址时，WAF回源的源站地址也为IPv4地址。

 取值：

 -   0：表示关闭（默认）。
-   1：表示开启。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Cname|String|xxxxxx.yundunwaf3.com|WAF实例为该域名配置记录所分配的CNAME。 |
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateDomain
&Domain=www.example.com
&InstanceId=waf_elasticity-cn-0xldbqt****
&IsAccessProduct=0
&SourceIps=["1.1.1.1", "2.2.2.2"]
&HttpPort=[80]
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateDomainResponse>
	  <Cname>xxxxxx.yundunwaf3.com</Cname>
	  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
</CreateDomainResponse>
```

`JSON` 格式

```
{
	"Cname": "xxxxxx.yundunwaf3.com",
	"RequestId": "D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/waf-openapi)查看更多错误码。

