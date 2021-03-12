# DescribeDomainNames

You can call this operation to obtain a list of domains that have been added to a specified WAF instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DescribeDomainNames&type=RPC&version=2018-01-17)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|DescribeDomainNames|The operation that you want to perform. Set the value to **DescribeDomainNames**. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call [DescribePayInfo](~~86651~~) to view your WAF instance ID. |
|Region|String|Yes|cn|The ID of the region to which the WAF instance belongs. Set the value to:

-   **cn**: mainland China \(default\)
-   **cn-hongkong**: outside mainland China |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|Cost|The ID of the request. |
|Result| |rstest.cdn.com|The returned result. The structure is described as follows:

-   **DomainNames** A list of domain names that have been added. It is a string array. |
|DomainNames| | |The returned result. The structure is described as follows:

-   **DomainNames** A list of domain names that have been added. It is a string array. |

## Samples

Sample request

```

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeDomainNames
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Common request parameters

```

Sample success responses

`XML` format

```
<DescribeDomainNamesResponse>
      <RequestId>56B40D30-4960-4F19-B7D5-2B1F0EE6CB70</RequestId>
      <Result>
            <DomainNames>rstest.cdn.com</DomainNames>
            <DomainNames>rstest1.cdn.com</DomainNames>
            <DomainNames>rstest2.cdn.com</DomainNames>
            <DomainNames>rstest3.cdn.com</DomainNames>
      </Result>
</DescribeDomainNamesResponse>
```

`JSON` format

```
{
	"Result":{
		"DomainNames":[
			"rstest.cdn.com",
			"rstest1.cdn.com",
			"rstest2.cdn.com",
			"rstest3.cdn.com"
		]
	},
	"RequestId":"56B40D30-4960-4F19-B7D5-2B1F0EE6CB70"
}
```

## Error codes.

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

