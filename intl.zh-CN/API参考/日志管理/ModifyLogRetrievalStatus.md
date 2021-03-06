# ModifyLogRetrievalStatus

调用ModifyLogRetrievalStatus接口开启或关闭指定域名配置的日志检索功能。

**说明：** 只有为域名开启日志检索功能，WAF的全量日志功能才会记录该域名的访问请求日志。如果您关闭日志检索功能，则处于关闭状态期间的访问请求日志不会被记录；即使重新开启日志检索功能，您也无法查询到停用期间的访问请求日志。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=ModifyLogRetrievalStatus&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyLogRetrievalStatus|要执行的操作。取值：**ModifyLogRetrievalStatus**。 |
|Domain|String|是|www.example.com|已添加的域名名称。 |
|Enabled|Integer|是|1|是否开启日志检索功能，取值：

 -   **0**：关闭
-   **1**：开启 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqt\*\*\*\*|WAF实例ID。

 **说明：** 您可以通过调用[DescribeInstanceInfo](~~140857~~)接口查看当前WAF实例ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ModifyLogRetrievalStatus
&Domain=www.example.com
&Enabled=1
&InstanceId=waf_elasticity-cn-0xldbqt****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyLogRetrievalStatusResponse>
	  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
</ModifyLogRetrievalStatusResponse>
```

`JSON` 格式

```
{
    "RequestId": "D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/waf-openapi)查看更多错误码。

