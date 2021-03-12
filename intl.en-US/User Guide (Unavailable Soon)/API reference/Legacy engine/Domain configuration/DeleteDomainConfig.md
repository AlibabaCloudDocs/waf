# DeleteDomainConfig

You can call this operation to delete the configurations of a specified domain name.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DeleteDomainConfig&type=RPC&version=2018-01-17)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|DeleteDomainConfig|The operation that you want to perform. Valid values: **DeleteDomainConfig**. |
|Domain|String|No|rstest.cdn.com|The domain name that has been added to WAF. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call [DescribePayInfo](~~86651~~) to view your WAF instance ID. |
|Region|String|Yes|cn|The ID of the region to which the WAF instance belongs. Set the value to:

-   **cn**: mainland China \(default\)
-   **cn-hongkong**: outside mainland China |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|The ID of the request. |
|Result| | |The returned result. |
|Status|Integer|env|Request execution status:

-   **0**: indicates that the request is pending execution.
-   **1**: indicates that the request is being executed.
-   **2**: indicates that the request has been completed. |
|WafTaskId|String|aliyun.waf.20180712214032277.qmxI9a|The ID of the WAF request. |

## Samples

Sample request

```

https://wafopenapi.cn-hangzhou.aliyuncs.com/? Action=DeleteDomainConfig
&Domain=www.aliyun.com
&Common request parameters

```

Sample success responses

`XML` format

```
<DeleteDomainConfigResponse>
      <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
      <Result>
            <Status>2</Status>
            <WafTaskId>aliyun.waf.20180712214032277.qmxI9a</WafTaskId>
      </Result>
</DeleteDomainConfigResponse>
```

`JSON` format

```
{
	"Result":{
		"Status":2,
		"WafTaskId":"aliyun.waf.20180712214032277.qmxI9a"
	},
	"RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## Error codes.

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

