# DescribeDomainConfig

You can call this operation to query the forwarding configurations of a specified domain name.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DescribeDomainConfig&type=RPC&version=2018-01-17)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|DescribeDomainConfig|The operation that you want to perform. Valid values: **DescribeDomainConfig**. |
|Domain|String|No|rstest.cdn.com|The domain name that has been added to WAF. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call [DescribePayInfo](~~86651~~) to view your WAF instance ID. |
|Region|String|Yes|cn|The ID of the region to which the WAF instance belongs. Set the value to:

-   **cn**: mainland China \(default\)
-   **cn-hongkong**: areas outside mainland China |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|Cost|The ID of the request. |
|Result| | |The returned result. |
|DomainConfig| | |Domain name configuration structure. |
|Cname|String|xxxxxxxxxxxxxx.fakewaf.com|The WAF CNAME address. |
|ProtocolType|Integer|env|Protocol type:

-   **0**: indicates that HTTP is supported.
-   **1**: indicates that HTTPS is supported.
-   **2**: indicates that both HTTP and HTTPS are supported. |
|SourceIps|String|1.1.1.1|The IP address of the origin server. |
|Status|Integer|env|Request execution status:

-   **0**: indicates that the request is pending execution.
-   **1**: indicates that the request is being executed.
-   **2**: indicates that the request has been completed. |
|WafTaskId|String|aliyun.waf.20180712180229702.Y6re3d|The ID of the WAF request. |

## Samples

Sample request

```

https://wafopenapi.cn-hangzhou.aliyuncs.com/? Action=DescribeDomainConfig
&Domain=www.aliyun.com
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Common request parameters

```

Sample success responses

`XML` format

```
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

`JSON` format

```
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

## Error codes.

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

