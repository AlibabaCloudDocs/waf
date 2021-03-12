# DescribeWafSourceIpSegment

Queries DescribeWafSourceIpSegment CIDR blocks of the WAF instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DescribeWafSourceIpSegment&type=RPC&version=2018-01-17)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|DescribeWafSourceIpSegment|The operation that you want to perform. Valid values: **DescribeWafSourceIpSegment**. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call [DescribePayInfo](~~86651~~) to view your WAF instance ID. |
|Region|String|Yes|cn|The ID of the region to which the WAF instance belongs. Set the value to:

-   **cn**: mainland China \(default\)
-   **cn-hongkong**: outside mainland China |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Ips|String|121.43.18.0/24,120.25.115.0/24,101.200.106.0/24|The CIDR blocks used by WAF. Separate the CIDR blocks with commas \(,\). |
|RequestId|String|9087 ADDC-9047-4D02-82A7-33021B58083C|The ID of the request. |

## Samples

Sample request

```

https://wafopenapi.cn-hangzhou.aliyuncs.com/? Action=DescribeWafSourceIpSegment
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Region=cn
& <Common request parameters>

```

Sample success responses

`XML` format

```
<DescribeWafSourceIpSegmentResponse>
     <Ips>121.43.18.0/24,120.25.115.0/24,101.200.106.0/24</Ips>
     <RequestId>9087ADDC-9047-4D02-82A7-33021B58083C</RequestId>
</DescribeWafSourceIpSegmentResponse>
```

`JSON` format

```
{
	"RequestId":"9087ADDC-9047-4D02-82A7-33021B58083C",
	"Ips":"121.43.18.0/24,120.25.115.0/24,101.200.106.0/24"
}
```

## Error codes.

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

