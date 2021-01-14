# CreateDomain

Adds a domain name to a WAF instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=CreateDomain&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDomain|The operation that you want to perform. Set the value to **CreateDomain**. |
|Domain|String|Yes|www.example.com|The domain name that you want to add. |
|InstanceId|String|Yes|waf\_elasticity-cn-0xldbqt\*\*\*\*|The ID of the WAF instance.

**Note:** You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|IsAccessProduct|Integer|Yes|0|Specifies whether to configure a Layer 7 proxy, such as Anti-DDoS Pro, Anti-DDoS Premium, or CDN, to filter inbound traffic before the traffic is forwarded to the WAF instance. Valid values:

-   **0**: A Layer 7 proxy is not configured.
-   **1**: A Layer 7 proxy is configured. |
|SourceIps|String|No|\["1.1.1.1", "2.2.2.2"\]|The IP addresses of the origin servers or a back-to-origin domain name.

**Note:** You cannot specify the IP addresses of the origin servers and a back-to-origin domain name at the same time.

-   You can specify a maximum of maximum of 20 IP addresses. Separate more than one IP address with commas \(,\).
-   You can specify only one back-to-origin domain name. |
|LoadBalancing|Integer|No|0|The load balancing algorithm that is used to forward requests to the origin servers. Valid values:

-   **0**: IP hash
-   **1**: round robin |
|LogHeaders|String|No|\[\{"k":"wafmark","v":"test"\}\]|The key-value pair that is used to mark the inbound requests that pass through the WAF instance.

The value is in the `[{"k":"_key_","v":"_value_"}]` format. `_key_` specifies a custom header field. `_value_` specifies the value of the header field.

WAF automatically adds the custom field and value to the headers of these requests. This way, the requests that pass through WAF are marked.

**Note:** If the headers of requests contain the custom field, WAF overwrites the original value of the field with the specified value. |
|HttpPort|String|No|\[80\]|The HTTP ports. Separate more than one port with commas \(,\).

**Note:** Set this parameter only when you want to use HTTP. You must configure at least one of the **HttpPort** and **HttpsPort** parameters. |
|HttpsPort|String|No|\[443\]|The HTTPS ports. Separate more than one port with commas \(,\).

**Note:** Set this parameter only when you want to use HTTPS. You must configure at least one of the **HttpPort** and **HttpsPort** parameters. |
|Http2Port|String|No|\[443\]|The HTTP/2 ports. Separate more than one port with commas \(,\). |
|HttpToUserIp|Integer|No|0|Specifies whether to enable the HTTP back-to-origin feature. After this feature is enabled, WAF uses HTTP to forward HTTPS requests to the origin servers. By default, port 80 is used. Valid values:

-   **0**: disabled. This is the default value.
-   **1**: enabled.

**Note:** If your website does not support HTTPS access, you can enable the HTTP back-to-origin feature to allow HTTPS access by using WAF. |
|HttpsRedirect|Integer|No|0|Specifies whether to enable the feature of redirecting HTTP requests to HTTPS requests. Valid values:

-   **0**: disabled. This is the default value.
-   **1**: enabled.

**Note:** This parameter must be specified only when the domain name uses HTTPS. After you enable this feature, HTTP requests are redirected to HTTPS requests on port 443. |
|ClusterType|Integer|No|0|The type of the cluster to which the WAF instance belongs. Valid values:

-   **0**: shared cluster. This is the default value.
-   **1**: exclusive cluster. |
|ResourceGroupId|String|No|rg-atstuj3rtop\*\*\*\*|The ID of the resource group to which the domain name belongs in Resource Management. By default, no value is specified, indicating that the domain name belongs to the default resource group. |
|ConnectionTime|Integer|No|5|The connection timeout period for WAF exclusive clusters. Unit: seconds.

**Note:** You can specify this parameter when you use exclusive clusters to protect resources. |
|ReadTime|Integer|No|120|The read timeout period for WAF exclusive clusters.

**Note:** You can specify this parameter when you use exclusive clusters to protect resources. |
|WriteTime|Integer|No|120|The write timeout period for WAF exclusive clusters.

**Note:** You can specify this parameter when you use exclusive clusters to protect resources. |
|AccessType|String|No|waf-cloud-dns|The mode that you use to add your website.

Valid values:

-   **waf-cloud-dns**: CNAME access mode. This is the default value.
-   **waf-cloud-native**: transparent access mode. |
|CloudNativeInstances|String|No|\[ \{"InstanceId":"i-2vc4k6vbs3f\*\*\*\*", "Port":80\}, \{"InstanceId":"lb-2zent2qvovb6\*\*\*\*", "Port":8080\} \]|The WAF instances to which websites are added in transparent access mode. This parameter takes effect only when the **AcessType** parameter is set to `waf-cloud-native`.

The value is a JSON string that contains the following fields:

-   **InstanceId**: the ID of the WAF instance.
-   **Port**: the port that is used for forwarding traffic. |
|IpFollowStatus|Integer|No|1|Specifies whether to enable the feature of using the same protocol. WAF forwards requests to the origin servers based on the protocol in the requests.

Valid values:

-   **0**: disabled. This is the default value.
-   **1**: enabled. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Cname|String|xxxxxx.yundunwaf3.com|The CNAME that is assigned by the WAF instance to the domain name that you added. |
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=CreateDomain
&Domain=www.example.com
&InstanceId=waf_elasticity-cn-0xldbqt****
&IsAccessProduct=0
&SourceIps=["1.1.1.1", "2.2.2.2"]
&HttpPort=[80]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateDomainResponse>
      <Cname>xxxxxx.yundunwaf3.com</Cname>
      <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
</CreateDomainResponse>
```

`JSON` format

```
{
    "Cname": "xxxxxx.yundunwaf3.com",
    "RequestId": "D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

