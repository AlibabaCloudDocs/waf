# ModifyDomainConfig

You can call this operation to modify the configuration of a specified domain name.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=ModifyDomainConfig&type=RPC&version=2018-01-17)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|ModifyDomainConfig|The operation that you want to perform. Valid values: **ModifyDomainConfig**. |
|Domain|String|No|rstest.cdn.com|The domain that you want to add to WAF. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call [DescribePayInfo](~~86651~~) to view your WAF instance ID. |
|IsAccessProduct|Integer|Yes|0|Indicates whether a layer -7 proxy, such as anti-DDoS pro or CDN, has been configured for the domain name in front of the WAF instance. Valid values:

-   **0**: indicates none.
-   **1**: indicates yes. |
|Protocols|String|No|\["http"\]|The access protocol supported by the domain name. Valid values:

-   **HTTP**: indicates that HTTP is supported.
-   **HTTPS**: indicates that HTTPS is supported.
-   **http,https**: supports both HTTP and HTTPS. |
|HttpPort|String|Yes|\[80\]|The HTTP ports. When multiple HTTP ports are specified, separate them with commas \(,\). Example value: `[80]`.

**Note:** This parameter is required if the Protocols parameter is set to http. Default value: **80**.**HttpPort** and**HttpsPort** fill in at least one of the two request parameters. |
|HttpToUserIp|String|Optional|0|Indicates whether to enable HTTP-based back-to-origin for HTTPS requests. Valid values:

-   **0**: Disabled \(default\)
-   **1**: indicates enabled

**Note:** If your website does not support HTTPS back-to-origin, enable the HTTP back-to-origin feature \(port 80 is selected by default\) to enable HTTPS access through WAF. |
|HttpsPort|String|Yes|\[443\]|The HTTPS ports. When multiple HTTPS ports are specified, separate them with commas \(,\). Example value: `[443]`.

**Note:** This parameter is required if the Protocols parameter is set to https. Default value: **443**.**HttpPort** and**HttpsPort** fill in at least one of the two request parameters. |
|HttpsRedirect|String|Optional|1|The Https status. Set the value to:

-   **1:** Log backup is enabled.
-   **0**: Off \(default\) |
|LoadBalancing|String|Optional|0|The load balancing method. Valid values:

-   **0**:IP hash
-   **1**: Polling |
|Region|String|Yes|cn|The ID of the region to which the WAF instance belongs. Set the value to:

-   **cn**: mainland China \(default\)
-   **cn-hongkong**: areas outside mainland China |
|SourceIps|String|Yes|\["1.1.1.1"\]|The origin IP address. Multiple IP addresses can be specified. Example: `["1.1.1.1"]`. |

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

https://wafopenapi.cn-hangzhou.aliyuncs.com/? Action=ModifyDomainConfig
&Domain=www.aliyun.com
&SourceIps=["x.x.x.x","x.x.x.x"]
&Protocols=["http","https"]
&HttpPort=[80]
&HttpsPort=[443]
&IsAccessProduct=0
&HttpsRedirect=1
&HttpToUserIp=0
&Common request parameters

```

Sample success responses

`XML` format

```
<ModifyDomainConfigResponse>
      <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
      <Result>
            <Status>2</Status>
            <WafTaskId>aliyun.waf.20180712214032277.qmxI9a</WafTaskId>
      </Result>
</ModifyDomainConfigResponse>
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

