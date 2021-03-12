# DescribeAsyncTaskStatus

You can call this operation to query the DescribeAsyncTaskStatus of a WAF task.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DescribeAsyncTaskStatus&type=RPC&version=2018-01-17)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|DescribeAsyncTaskStatus|The operation that you want to perform. Valid values: **DescribeAsyncTaskStatus**. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call [DescribePayInfo](~~86651~~) to view your WAF instance ID. |
|WafRequestId|String|No|aliyun.waf.20180719140433783.SvaZeY|The ID of the WAF task. |
|Region|String|Yes|cn|The ID of the region to which the WAF instance belongs. Set the value to:

-   **cn**: mainland China \(default\)
-   **cn-hongkong**: areas outside mainland China |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|12EF3845-CCEB-4B84-AE60-2B49B2FF1EE5|The ID of the request. |
|Result| | |Responses |
|AsyncTaskStatus|String|env|Asynchronous task execution status:

-   **0**: indicates that the request is pending execution.
-   **1**: indicates that the request is being executed.
-   **2**: indicates that the request has been completed. |
|Data|String|xx|The business data returned by asynchronous tasks. |
|ErrCode|String|400|Error code.

**Note:** This parameter is only returned when an error occurs during request execution. |
|ErrMsg|String|xx|The description of the error message.

**Note:** This parameter is only returned when an error occurs during request execution. |
|Progress|Integer|90|The progress of the asynchronous task. Unit: percentage. |

## Samples

Sample request

```

https://wafopenapi.cn-hangzhou.aliyuncs.com/? Action=DescribeAsyncTaskStatus
&InstanceId=waf_elasticity-cn-0xldbqtm005
&WafRequestId=aliyun.waf.20180719140433783.SvaZeY
&Common request parameters

```

Sample success responses

`XML` format

```
<DescribeAsyncTaskStatusResponse>
      <RequestId>12EF3845-CCEB-4B84-AE60-2B49B2FF1EE5</RequestId>
      <Result>
            <DomainConfig>
                  <Progress>100</Progress>
                  <AsyncTaskStatus>2</AsyncTaskStatus>
            </DomainConfig>
      </Result>
</DescribeAsyncTaskStatusResponse>
```

`JSON` format

```
{
	"Result":{
		"DomainConfig":{
			"AsyncTaskStatus":2,
			"Progress":100
		}
	},
	"RequestId":"12EF3845-CCEB-4B84-AE60-2B49B2FF1EE5"
}
```

## Errors

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

