# ModifyAclRule

Modifies a specified ACL rule.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=ModifyAclRule&type=RPC&version=2018-01-17)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|ModifyAclRule|The operation that you want to perform. Valid values: **ModifyAclRule**. |
|Domain|String|No|rstest.cdn.com|The domain that you want to add to WAF. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call [DescribePayInfo](~~86651~~) to view your WAF instance ID. |
|Rules|String|No|\{"conditions":\[\{"key":"URL","contain":1,"value":"asfas"\}\],"continueComponent":\{"post\_action\_cc":1,"post\_action\_waf":1,"post\_action\_sa":1,"post\_action\_block\_geo":"0","post\_action\_data\_risk\_control":"1"\},"action":"1","name":"lei123","id":65899\}|The details of the HTTP-based ACL rule, in JSON format. The following table describes the structure.

-   **Id** the ID of the rule. Required. The ID is of the Long type.
-   **Name**: the name of the rule. This parameter is required and of String type.
-   **Action** the matching action of the rule. This parameter is required and of Integer type. Valid values:
    -   **0**: indicates blocking, that is, the access request is blocked if the matching condition of the rule is met.
    -   **1**: allows the access request to pass, that is, the access request that meets the matching condition of the rule.
    -   **2**: indicates an alert. That is, when the matched condition of the rule is matched, the access request is allowed, but the request is recorded and an alert is generated.
-   **ContinueComponent**: Optional. The String type. This parameter specifies whether to run other WAF protection policies in JSON format. The following table describes the structure.
    -   **post\_action\_cc**\(Optional\) The Integer type. Specifies whether to proceed with the HTTP flood detection. Valid values:
        -   **0**: false
        -   **1**: true
    -   **post\_action\_waf**\(Optional\) The Integer type. It indicates whether to proceed with the detection of Web attack protection rules. Valid values:
        -   **0**: false
        -   **1**: true
    -   **post\_action\_sa**\(Optional\) The Integer type. Specifies whether to proceed with intelligent protection rule detection. Valid values:
        -   **0**: false
        -   **1**: true
    -   **post\_action\_block\_geo** optional. The Integer type. Specifies whether to resume the regional block. Valid values:
        -   **0**: false
        -   **1**: true
    -   **post\_action\_data\_risk\_control** optional. The Integer type. Specifies whether to proceed with data risk control. Valid values:
        -   **0**: false
        -   **1**: true
    -   **post\_action\_sdk** optional. The Integer type. It indicates whether to continue SDK protection. Valid values:
        -   **0**: false
        -   **1**: true
-   **Conditions** optional. The Array type is required. The Array is required as described in the following table.
    -   **Key** the matching field. This parameter is required and of String Type. Valid values: IP, URL, Referer, User-Agent, Params, Cookie, Content-Type, X-Forwarded-For, Content-Length, Post-Body, http-Method and headers. WAF instances of different versions support different fields. You can view the supported fields in the Web Application Firewall console.
    -   **Contain**, required. The logical operator. The type is Integer. Valid values:
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
        -   **32**: indicates a value greater than.
    -   **Value** String type. Required. The matching content. |
|Region|String|Yes|cn|The ID of the region to which the WAF instance belongs. Set the value to:

-   **cn**: mainland China \(default\)
-   **cn-hongkong**: areas outside mainland China |

Specifies the mapping between a field and logical operators.

|Field

|Logical operator |
|-------|------------------|
|IP

|Belongs to, does not belong to |
|Referer

|Contains, does not contain, is equal to, is not equal to, is less than, length is equal to, and length is greater than |
|User-Agent

|Contains, does not contain, is equal to, is not equal to, is less than, length is equal to, and length is greater than |
|Param

|Contains, does not contain, is equal to, is not equal to, is less than, length is equal to, and length is greater than |
|Cookie

|Contains, does not contain, is equal to, is not equal to, is less than, has a length of, is greater than, and does not exist |
|Content-Type

|Contains, does not contain, is equal to, is not equal to, is less than, length is equal to, and length is greater than |
|X-Forwarded-For

|Contains, does not contain, is equal to, is not equal to, is less than, has a length of, is greater than, and does not exist |
|Content-Length

|Value less than, value equal to, and value greater than |
|Post-Body

|Contains, does not contain, equals, is not equal to |
|Http-Method

|Equal to, not equal to |
|Header

|Contains, does not contain, is equal to, is not equal to, is less than, has a length of, is greater than, and does not exist |

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
https://wafopenapi.cn-hangzhou.aliyuncs.com/? Action=ModifyAclRule
&Domain=www.aliyun.com
&ServiceOn=1
&Rules={...}
&Common request parameters
```

Sample success responses

`XML` format

```
<ModifyAclRuleResponse>
      <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
      <Result>
            <Status>2</Status>
            <WafTaskId>aliyun.waf.20180712214032277.qmxI9a</WafTaskId>
      </Result>
</ModifyAclRuleResponse>
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

