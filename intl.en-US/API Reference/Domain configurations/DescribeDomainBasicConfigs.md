# DescribeDomainBasicConfigs

You can call this operation to query the protection settings in domain configuration records.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DescribeDomainBasicConfigs&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDomainBasicConfigs|The operation that you want to perform. Set the value to **DescribeDomainBasicConfigs**. |
|InstanceId|String|Yes|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|DomainKey|String|No|example|A domain keyword. Specify a keyword to query the configuration records of domains that contain the keywords.

**Note:** By default, no value is specified, indicating that the configuration records of all domains added to WAF are queried. |
|PageNumber|Integer|No|1|The number of the page to return. Default value: 1 |
|PageSize|Integer|No|10|The number of domain configuration records to return on each page. Default value: 10 |
|ResourceGroupId|String|No|rg-atstuj3rtoptyui|The ID of the resource group to which the queried domains belong in Resource Management. By default, no value is specified, indicating that the domains that belong to the default resource group are queried. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DomainConfigs| | |The protection settings of the queried domains. |
|AclStatus|Integer|1|The status of the HTTP ACL policy feature. Valid values:

-   **0**: disabled
-   **1**: enabled |
|CcMode|Integer|0|The mode of HTTP flood protection. Valid values:

-   **0**: normal
-   **1**: emergency |
|CcStatus|Integer|1|The status of the HTTP flood protection feature. Valid values:

-   **0**: disabled
-   **1**: enabled |
|Domain|String|www.example.com|The domain name. |
|Owner|String|WAF|The source of a domain configuration record:

-   **Anti-Bot**: The domain configuration record was created in Anti-Bot Service.
-   **WAF**: The domain configuration record was created in WAF. |
|Status|Integer|1|The status of a domain configuration record. Valid values:

-   **0**: invalid or deleted
-   **1**: valid
-   **10**: creating
-   **11**: creation failed
-   **20**: deleting |
|Version|Long|0|The system data identifier that is used to control optimistic locking. |
|WafMode|Integer|0|The mode of Web application protection. Valid values:

-   **0**: prevention mode
-   **1**: detection mode |
|WafStatus|Integer|1|The status of Web application protection. Valid values:

-   **0**: disabled
-   **1**: enabled |
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|The ID of the request. |
|TotalCount|Integer|1|The number of records returned. |

## Examples

Sample requests

```

http(s)://[Endpoint]/? Action=DescribeDomainBasicConfigs
&InstanceId=waf_elasticity-cn-0xldbqtm005
&<Common request parameters>

```

Sample success responses

`XML` format

```
<TotalCount>1</TotalCount>
<DomainConfigs>
    <Owner>WAF</Owner>
    <AclStatus>1</AclStatus>
    <Version>0</Version>
    <CcStatus>1</CcStatus>
    <WafMode>0</WafMode>
    <WafStatus>1</WafStatus>
    <Domain>www.example.com</Domain>
    <CcMode>0</CcMode>
</DomainConfigs>
<RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
```

`JSON` format

```
{
	"TotalCount":1,
	"RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0",
	"DomainConfigs":[
		{
			"WafStatus":1,
			"Owner":"WAF",
			"AclStatus":1,
			"Domain":"www.example.com",
			"WafMode":0,
			"CcStatus":1,
			"CcMode":0,
			"Version":0
		}
	]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

