# ModifyLogServiceStatus

You can call this operation to enable or disable log collection in the real-time log analysis feature for a specific domain.

Before you enable log collection, make sure that real-time log analysis has been activated for the WAF instance, and WAF has the permission to save logs to the exclusive Logstore.

For more information, see [Real-time log analysis](~~100503~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=ModifyLogServiceStatus&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyLogServiceStatus|The operation that you want to perform. Set the value to **ModifyLogServiceStatus**. |
|Domain|String|Yes|www.example.com|The domain that has been added to WAF. |
|Enabled|Integer|Yes|1|Specifies whether to enable log collection. Valid values:

 -   **0**: disables log collection
-   **1**: enables log collection |
|InstanceId|String|Yes|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

 You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|ResourceGroupId|String|No|rg-atstuj3rtoptyui|The ID of the resource group to which the queried domain belongs in Resource Management. By default, no value is specified, indicating that the domain belongs to the default resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ModifyLogServiceStatus
&Domain=www.example.com
&Enabled=1
&InstanceId=waf_elasticity-cn-0xldbqtm005
&<Common request parameters>
```

Sample success responses

`JSON` format

```
{
	"RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

`XML` format

```
<RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

