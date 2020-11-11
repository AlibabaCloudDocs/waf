# ModifyLogServiceStatus

调用ModifyLogServiceStatus接口开启或关闭指定域名配置的日志采集功能。

为域名配置开启日志采集功能前请确认WAF实例已开通日志实时查询分析功能并且授权WAF将记录的日志分发到您专属的日志服务Logstore中。

更多详细信息，请参见[日志实时查询分析](~~100503~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=ModifyLogServiceStatus&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyLogServiceStatus|要执行的操作。取值：**ModifyLogServiceStatus**。 |
|Domain|String|是|www.example.com|已添加的域名名称。 |
|Enabled|Integer|是|1|是否开启日志采集功能，取值：

 -   **0**：关闭
-   **1**：开启 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqt\*\*\*\*|WAF实例ID。

 您可以通过调用[DescribeInstanceInfo](~~140857~~)接口查看当前WAF实例ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ModifyLogServiceStatus
&Domain=www.example.com
&Enabled=1
&InstanceId=waf_elasticity-cn-0xldbqt****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyLogServiceStatusResponse>
	  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
</ModifyLogServiceStatusResponse>
```

`JSON` 格式

```
{
    "RequestId": "D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/waf-openapi)查看更多错误码。

访问[错误中心](https://error-center.alibabacloud.com/status/product/waf-openapi)查看更多错误码。

