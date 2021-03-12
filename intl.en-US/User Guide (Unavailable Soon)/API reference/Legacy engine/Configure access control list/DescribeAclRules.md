# DescribeAclRules

You can call this operation to query the list of precise access control rules for a specified domain name.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DescribeAclRules&type=RPC&version=2018-01-17)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|DescribeAclRules|The operation that you want to perform. Valid values: **DescribeAclRules**. |
|CurrentPage|Integer|Yes|1|The number of the page to return. For example, to query the returned results on the first page, enter **1**. |
|Domain|String|No|www.aliyun.com|The domain that you want to add to WAF. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call [DescribePayInfo](~~86651~~) to view your WAF instance ID. |
|PageSize|Integer|Yes|10|The number of entries returned per page. |
|Region|String|Yes|cn|The ID of the region to which the WAF instance belongs. Set the value to:

-   **cn**: mainland China \(default\)
-   **cn-hongkong**: areas outside mainland China |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|The ID of the request. |
|Result| | |The returned result. |
|AclRules| | |The list of HTTP-based ACL rules. Each ACL rule is described as a sub-parameter of AclRule. The AclRule sub-parameter is a JSON string. |
|AclRule| | |The list of HTTP-based ACL rules. Each ACL rule is described as a sub-parameter of AclRule. The AclRule sub-parameter is a JSON string. |
|Action|Integer|1|The matching action of the rule. Valid values:

-   **0**: indicates blocking, that is, the access request is blocked if the matching condition of the rule is met.
-   **1**: allows the access request to pass, that is, the access request that meets the matching condition of the rule.
-   **2**: indicates an alert. That is, when the matched condition of the rule is matched, the access request is allowed, but the request is recorded and an alert is generated. |
|Conditions| | |The structure of rule matching conditions. |
|condition| | |The structure of rule matching conditions. |
|Contain|String|1|Logical operator:

-   **0**: indicates that the rule is not included.
-   **1**: indicates include.
-   **2**: indicates that it does not exist.
-   **10**: indicates a value that is not equal to the passed value.
-   **11**: indicates equal to.
-   **20**: indicates that the length is less than the specified value.
-   **21**: indicates a character with a length equal to the value of
-   **22**: indicates that the length is greater than.
-   **30**: indicates that the value is less than.
-   **31**: indicates that the value is equal to.
-   **32**: indicates a value greater than. |
|Key|String|url|The matching field. Valid values: IP, URL, Referer, User-Agent, Params, Cookie, Content-Type, X-Forwarded-For, Content-Length, Post-Body, Http-Method, and Header.

**Note:** Note: WAF instances of different versions support different fields. You can view the supported fields in the Web Application Firewall console. |
|Value|String|login.|The matching content. |
|ContinueBlockGeo|Integer|1|Indicates whether to continue region blocking. Valid values:

-   **0**: false
-   **1**: true |
|ContinueCc|Integer|1|Indicates whether to proceed with the HTTP flood detection. Valid values:

-   **0**: false
-   **1**: true |
|ContinueDataRiskControl|Integer|1|Indicates whether to continue data risk control protection. Valid values:

-   **0**: false
-   **1**: true |
|ContinueSA|Integer|1|Indicates whether to perform the smart protection engine rule check. Valid values:

-   **0**: false
-   **1**: true |
|ContinueSdk|Integer|1|Indicates whether to continue SDK protection. Valid values:

-   **0**: no
-   **1**: true |
|ContinueWaf|Integer|1|Indicates whether to proceed with the Web attack protection rule detection. Valid values:

-   **0**: false
-   **1**: true |
|Id|Long|1111|The ID of the ACL rule. |
|IsDefault|Integer|1|Indicates whether the rule is a default rule. Valid values:

-   **0**: false
-   **1**: true |
|Name|String|test|The name of the rule. |
|Order|Integer|1|The order of the rules.

**Note:** Note: the greater the value, the higher the priority of the rule. |
|Total|Interger|1|The total number of rules. |

## Samples

Sample request

```

https://wafopenapi.cn-hangzhou.aliyuncs.com/? Action=DescribeAclRules
&Domain=www.aliyun.com
&CurrentPage=1
&PageSize=50
&Common request parameters

```

Sample success responses

`XML` format

```
<DescribeAclRulesResponse>
      <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
      <Result>
            <AclRules>
                  <AclRule>
                        <IsDefault>1</IsDefault>
                        <Order>0</Order>
                        <ContinueBlockGeo>1</ContinueBlockGeo>
                        <Action>1</Action>
                        <ContinueWaf>1</ContinueWaf>
                        <ContinueSdk>0</ContinueSdk>
                        <Id>16572</Id>
                        <ContinueCc>1</ContinueCc>
                        <Conditions>
                              <condition>
                                    <key>URL</key>
                                    <contain>1</contain>
                                    <value>asfas</value>
                              </condition>
                        </Conditions>
                        <Name>default</Name>
                        <ContinueDataRiskControl>1</ContinueDataRiskControl>
                        <ContinueSA>1</ContinueSA>
                   </AclRule>
            </AclRules>
            <Total>1</Total>
      </Result>
</DescribeAclRulesResponse>
```

`JSON` format

```
{
	"Result":{
		"AclRules":{
			"AclRule":[
				{
					"Name":"default",
					"Conditions":{
						"condition":[
							{
								"contain":1,
								"value":"asfas",
								"key":"URL"
							}
						]
					},
					"ContinueDataRiskControl":1,
					"Action":1,
					"ContinueSdk":0,
					"ContinueWaf":1,
					"IsDefault":1,
					"Order":0,
					"Id":16572,
					"ContinueCc":1,
					"ContinueSA":1,
					"ContinueBlockGeo":1
				}
			]
		},
		"Total":1
	},
	"RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## Error codes.

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

