# DescribeWafSourceIpSegment

Queries the back-to-origin CIDR blocks that are used by a WAF instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DescribeWafSourceIpSegment&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeWafSourceIpSegment|The operation that you want to perform. Set the value to **DescribeWafSourceIpSegment**. |
|InstanceId|String|Yes|waf-cn-zz11sr5\*\*\*\*|The ID of the WAF instance.

**Note:** You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|ResourceGroupId|String|No|rg-acfm2pz25js\*\*\*\*|The ID of the resource group to which the WAF instance belongs in Resource Management. By default, no value is specified, indicating that the domain name belongs to the default resource group.

For more information about resource groups, see [Create a resource group](~~94485~~). |

All Alibaba Cloud API operations must include common request parameters. For more information about common request parameters, see [Common parameters](~~162719~~).

For more information about sample requests, see the **"Examples"** section of this topic.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IpV6s|String|39.XXX.XXX.0/24,……,2408:400a:XXXX:XXXX::/56|The back-to-origin IPv6 CIDR blocks that are used by the WAF instance. |
|Ips|String|47.XXX.XXX.192/26,……,47.XXX.XXX.0/24|The back-to-origin IPv4 CIDR blocks that are used by the WAF instance. |
|RequestId|String|AB2F5E31-EE96-4FD7-9560-45FF5D5377FF|The ID of the request. |

## Examples

Sample request

```
http(s)://[Endpoint]/? Action=DescribeWafSourceIpSegment
&InstanceId=waf-cn-zz11sr5****
&<Common request parameters>
```

Sample responses

`XML` format

```
<DescribeWafSourceIpSegmentResponse>
      <RequestId>AB2F5E31-EE96-4FD7-9560-45FF5D5377FF</RequestId>
      <IpV6s>39.XXX.XXX.0/24,……,2408:400a:XXXX:XXXX::/56</IpV6s>
      <Ips>47.XXX.XXX.192/26,……,47.XXX.XXX.0/24</Ips>
</DescribeWafSourceIpSegmentResponse>
```

`JSON` format

```
{
    "RequestId": "AB2F5E31-EE96-4FD7-9560-45FF5D5377FF",
    "IpV6s": "39.XXX.XXX.0/24,……,2408:400a:XXXX:XXXX::/56",
    "Ips": "47.XXX.XXX.192/26,……,47.XXX.XXX.0/24"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

