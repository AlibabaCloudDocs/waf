# ModifyProtectionModuleStatus

You can call this operation to enable or disable the protection of a specified WAF feature, such as web intrusion prevention, data security, advanced protection, Bot management, and access control or throttling.

You can set the **DefenseType** parameter to specify the protection module. For more information about the values of this parameter, see the description of **DefenseType** in the following section.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=ModifyProtectionModuleStatus&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|ModifyProtectionModuleStatus|The operation that you want to perform. Set the value to **ModifyProtectionModuleStatus**. |
|DefenseType|String|No|waf|The protection module. Valid values:

-   **waf**: the RegEx protection engine
-   **dld**: the big data deep learning engine
-   **tamperproof**: tamper protection
-   **antihijack**: web page anti-hijacking
-   **dlp**: data leakage prevention
-   **normalized**: positive security model
-   **bot\_crawler**: valid crawlers
-   **bot\_intelligence**: Bot Threat Intelligence
-   **antifraud**: data risk control
-   **bot\_algorithm**: intelligent algorithm
-   **bot\_wxbb**: App Protection
-   **bot\_wxbb\_pkg**: version protection in App protection

**Note:** After you enable the version protection function, call [CreateProtectionModuleRule](~~100349~~) to create version protection rules that specify the permitted valid versions.

-   **cc**: HTTP flood protection
-   **ac\_blacklist**: the IP blacklist.
-   **ac\_highfreq**: block high-frequency Web attacks in the scanning protection module
-   **ac\_dirscan**: directory traversal protection
-   **ac\_scantools**: scan tools in the scan protection module are blocked.
-   **ac\_collaborative**: collaborative defense
-   **ac\_custom**: custom protection policies |
|Domain|String|No|www.example.com|The domain name that has been added to WAF. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|ModuleStatus|Integer|Yes|1|The status of the specified protection module. Valid values:

-   **0**: disables the feature
-   **1**: enables protection |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|The ID of the request. |

## Samples

Sample request

```
http(s)://[Endpoint]/? Action=ModifyProtectionModuleStatus
&DefenseType=waf
&Domain=www.example.com
&InstanceId=waf_elasticity-cn-0xldbqtm005
&ModuleStatus=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
```

`JSON` format

```
{
    "RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## Error codes.

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

