# CreateDomainConfig

Adds CreateDomainConfig domain name configuration information.

**To ensure Web application security when you add your domain name to WAF, perform the following steps:**

1. Call [CreateDomainConfig](~~86412~~) to add domain name configuration information.

2. Based on the information in the returned result**WafTaskId** value, call [DescribeAsyncTaskStatus](~~86725~~) to view the execution progress of the configuration task for adding a domain name. When the task is completed, the domain name configuration information is added.

3. Call [DescribeDomainConfigStatus](~~86404~~) to check whether the domain name configuration takes effect.

**Note:** In the returned result, you can switch the business traffic to the WAF instance only after the configurations take effect.

4. Call [DescribeDomainConfig](~~86389~~) to view the WAF CNAME address.

5. In the domain name DNS resolution service provider, modify the parsing records of the domain name, switch the business traffic to WAF.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=CreateDomainConfig&type=RPC&version=2018-01-17)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|CreateDomainConfig|The operation that you want to perform. Valid values: **CreateDomainConfig**. |
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
|SourceIps|String|Yes|\["1.1.1.1"\]|The origin IP address. Multiple IP addresses can be specified. Array type. Example values: `["1.1.1.1"]`. |
|HttpPort|String|Yes|\[80\]|The HTTP ports. When multiple HTTP ports are specified, separate them with commas \(,\). Example value: `[80]`.

**Note:** This parameter is required if the Protocols parameter is set to http. Default value: **80**.**HttpPort** and**HttpsPort** fill in at least one of the two request parameters. |
|HttpsPort|String|Yes|\[443\]|The HTTPS ports. When multiple HTTPS ports are specified, separate them with commas \(,\). Example value: `[443]`.

**Note:** This parameter is required if the Protocols parameter is set to https. Default value: **443**.**HttpPort** and**HttpsPort** fill in at least one of the two request parameters. |
|Region|String|Yes|cn|The ID of the region to which the WAF instance belongs. Set the value to:

-   **cn**: mainland China \(default\)
-   **cn-hongkong**: areas outside mainland China |
|LoadBalancing|String|Optional|0|The back-to-source SLB policy. Valid values:

-   **0**: represents IP Hash mode.
-   **1**: Round robin |
|HttpToUserIp|String|Optional|0|Indicates whether to enable HTTP-based back-to-origin for HTTPS requests. Valid values:

-   **0**: Disabled \(default\)
-   **1**: indicates enabled

**Note:** If your website does not support HTTPS back-to-origin, enable the HTTP back-to-origin feature \(port 80 is selected by default\) to enable HTTPS access through WAF. |
|HttpsRedirect|String|Optional|0|Specifies whether to redirect HTTP requests as HTTPS requests. Valid values:

-   **0**: Disabled \(default\)
-   **1**: indicates enabled

**Note:** You need to specify this request parameter only if the Protocols parameter is set to https. After you enable this feature, HTTP requests are redirected to HTTPS port 443. |
|RsType|String|Optional|0|The origin address type of the domain name. Valid values:

-   **0**: indicates a back-to-origin IP address.
-   **1**Indicates the back-to-origin domain name. |
|ResourceGroupId|String|Yes|rs1234|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|The ID of the request. |
|Result|Struct| |The returned result. |
|WafTaskId|String|aliyun.waf.20180712214032277.qmxI9a|The ID of the WAF request. |
|Status|Integer|2|Request execution status:

-   **0**: indicates that the request is pending execution.
-   **1**: indicates that the request is being executed.
-   **2**: indicates that the request has been completed. |

## Samples

Sample request

```
https://wafopenapi.cn-hangzhou.aliyuncs.com/? Action=CreateDomainConfig
&Domain=www.aliyun.com
&SourceIps=["x.x.x.x","x.x.x.x"]
&Protocols=["http","https"]
&HttpPort=[80]
&HttpsPort=[443]
&RsType=0
&IsAccessProduct=0
&LoadBalancing=0
&HttpsRedirect=1
&HttpToUserIp=0
&Common request parameters
```

Sample success responses

`XML` format

```
<CreateDomainConfigResponse>
      <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
      <Result>
            <Status>2</Status>
            <WafTaskId>aliyun.waf.20180712214032277.qmxI9a</WafTaskId>
      </Result>
</CreateDomainConfigResponse>
```

`JSON` format

```
{
    "RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0", 
    "Result":{
        "Status":2,
        "WafTaskId":"aliyun.waf.20180712214032277.qmxI9a"
    } 
}
```

## Error codes.

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

