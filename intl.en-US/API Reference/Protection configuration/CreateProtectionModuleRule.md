# CreateProtectionModuleRule

Creates a rule for a specific Web Application Firewall \(WAF\) protection module, such as the web intrusion protection, data security, advanced mitigation, bot management, or access control and throttling module

You can set the **DefenseType** parameter to specify the protection module. For more information about the valid values of this parameter, see the description of **DefenseType**.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=CreateProtectionModuleRule&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateProtectionModuleRule|The operation that you want to perform. Set the value to **CreateProtectionModuleRule**. |
|DefenseType|String|Yes|ac\_custom|The protection module for which you want to create a rule. Valid values:

-   **waf-codec**: protection rules engine
-   **tamperproof**: website tamper-proofing
-   **dlp**: data leak prevention
-   **ng\_account**: account security
-   **antifraud**: data risk control
-   **antifraud\_js**: configuration of a webpage into which you want to insert a JavaScript plug-in for data risk control
-   **bot\_algorithm**: intelligent algorithm rule for bot management
-   **bot\_wxbb\_pkg**: version protection rule for application protection
-   **bot\_wxbb**: path protection rule for application protection
-   **ac\_custom**: custom protection policy
-   **whitelist**: whitelist rule |
|Domain|String|Yes|www.example.com|The domain name that is added to WAF.

**Note:** You can call the [DescribeDomainNames](~~86373~~) operation to query the domain names that are added to WAF. |
|InstanceId|String|Yes|waf\_elasticity-cn-0xldbqt\*\*\*\*|The ID of the WAF instance.

**Note:** You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|Rule|String|Yes|\{"action":"monitor","name":"test","scene":"custom\_acl","conditions":\[\{"opCode":1,"key":"URL","values":"/example"\}\]\}|The configurations of the rule. This parameter is a string consisting of JSON structs.

**Note:** The parameters that are contained in the string vary based on the protection module, which is specified by the **DefenseType** parameter. For more information, see the "Rule parameters" section. |

**Rule parameters**

-   If the DefenseType parameter is set to **waf-codec**, the value of the Rule parameter contains the following parameters:
    -   **codecList**: required. The enabled decoding settings. Data type: array. You can view the valid values of this parameter in the WAF console.
    -   **Example**

        ```
        
            {
                "codecList":["url","base64"]
            }
            
        ```


-   If the DefenseType parameter is set to **tamperproof**, the value of the Rule parameter contains the following parameters:
    -   **uri**: required. The URL that requires protection. Data type: string.
    -   **name**: required. The name of the rule. Data type: string.
    -   **Example**

        ```
        
            {
                "name":"example",
                "uri":"http://www.example.com/example"
            }
            
        ```

-   If the DefenseType parameter is set to **dlp**, the value of the Rule parameter contains the following parameters:
    -   **name**: required. The name of the rule. Data type: string.
    -   **conditions**: required. The matching condition, which is formulated in a JSON string. You can specify a maximum of two conditions. The two conditions must have the AND logical relation. Data type: array. The JSON string contains the following parameters:
        -   **key**: the matching item. Valid values:
            -   **0**: URL
            -   **10**: sensitive information
            -   **11**: HTTP status code

**Note:** You cannot set HTTP status codes \(**11**\) and sensitive information \(**10**\) as the matching items in the **conditions** parameter at the same time.

        -   **operation**: the matching logic. Set the value to **1**, which indicates the INCLUDES logical relation.
        -   **value**: the matching value, which is formulated in a JSON string. You can specify multiple values. The JSON string contains the following parameters:
            -   **v**: This parameter is valid only when **key** is set to **0** or **11**.
                -   URL: If `key` is set to 0, the value of the v parameter is a URL.
                -   HTTP status code: If `key` is set to 11, the valid values of the v parameter are **400**, **401**, **402**, **403**, **404**, **405 to 499**, **500**, **501**, **502**, **503**, **504**, and **505 to 599**.
            -   **k**: This parameter is valid only when **key** is set to **10**. Valid values:
                -   **100**: ID card numbers
                -   **101**: credit card numbers
                -   **102**: phone numbers
                -   **103**: default sensitive words
    -   **action**: the action performed after the rule is matched. Valid values:
        -   **3**: generates alerts.
        -   **10**: filters sensitive information. This action is valid only when `key` is set to 10.
        -   **11**: returns the built-in interception page of the system. This action is valid only when `key` is set to 11.
    -   **Example**

        ```
        
          {
            "name":"example",
            "conditions":[{"key":11,"operation":1,"value":[{"v":401}]},{"key":"0","operation":1,"value":[{"v":"www.example.com"}]}],
            "action":3
          }
          
        ```

-   If the DefenseType parameter is set to **ng\_account**, the value of the Rule parameter contains the following parameters:
    -   **url\_path**: required. The URL path in the requests that are detected. The path must start with a forward slash \(/\). Data type: string.
    -   **method**: required. The method of the requests that are detected. Valid values: POST, GET, PUT, and DELETE. Data type: string. You can specify multiple request methods. Separate the request methods with commas \(,\).
    -   **account\_left**: required. The account. Data type: string.
    -   **password\_left**: optional. The password. Data type: string.
    -   **action**: required. The action performed after the rule is matched. Data type: string. Valid values:
        -   **monitor**: generates alerts.
        -   **block**: blocks requests.
    -   **Example**

        ```
        
            {
                "url_path":"/example",
                "method":"POST,GET,PUT,DELETE",
                "account_left":"aaa",
                "password_left:"123",
                "action":"monitor"
            }
            
        ```

-   If the DefenseType parameter is set to **antifraud**, the value of the Rule parameter contains the following parameters:
    -   **uri**: required. The requested URL. Data type: string.
    -   **Example**

        ```
        
            {
                "uri": "http://1.example.com/example"
            }
            
        ```

-   If the DefenseType parameter is set to **antifraud\_js**, the value of the Rule parameter contains the following parameters:
    -   **uri**: required. The URL path of the web page into which you want to insert a JavaScript plug-in for data risk control. The path must start with a forward slash \(/\). The system inserts the JavaScript plug-in into all the pages under the specified URL path. Data type: string.
    -   **Example**

        ```
        
            {
                "uri": "/example/example"
            }
            
        ```

-   If the DefenseType parameter is set to **bot\_algorithm**, the value of the Rule parameter contains the following parameters:
    -   **name**: required. The name of the rule. Data type: string.
    -   **algorithmName**: required. The name of the algorithm. Data type: string. Valid values:
        -   **RR**: the identification algorithm for special resource crawlers
        -   **PR**: the identification algorithm for specific path crawlers
        -   **DPR**: the identification algorithm for parameter round-robin crawlers
        -   **SR**: the identification algorithm for dynamic IP address crawlers
        -   **IND**: the identification algorithm for proxy device crawlers
        -   **Periodicity**: the identification algorithm for periodic crawlers
    -   **timeInterval**: required. The interval of detection. Data type: integer. Valid values: 30, 60, 120, 300, and 600. Unit: seconds.
    -   **action**: required. The action performed after the rule is matched. Data type: string. Valid values:
        -   **monitor**: monitors requests.
        -   **captcha**: performs CAPTCHA verification.
        -   **js**: performs JavaScript verification.
        -   **block**: blocks requests. If you set the parameter to block, you must also specify the **blocktime** parameter.
    -   **blocktime**: optional. The period during which requests are blocked. Data type: integer. Unit: minutes. Valid values: 1 to 600.
    -   **config**: required. The configurations of the algorithm, which are formulated in a JSON string. Data type: string. The parameters that are contained in the JSON string vary based on the value of the **algorithmName** parameter.
        -   If you set algorithmName to **RR**, the value of the config parameter contains the following parameters:
            -   **resourceType**: optional. The type of the requested resources. Data type: integer. Valid values:
                -   **1**: dynamic resources.
                -   **2**: static resources.
                -   **-1**: custom resources. In this case, you must also use the **extensions** parameter to specify resource suffixes in a string. Separate suffixes with commas \(,\). Example: `css,jpg,xls`.
            -   **minRequestCountPerIp**: required. The minimum number of requests from an IP address. The system detects an IP address only when the number of requests from this IP address is greater than or equal to the value of this parameter. Data type: integer. Valid values: 5 to 10000.
            -   **minRatio**: required. The threshold for the proportion of requests that access specified types of resources or specified paths to requests that are initiated from an IP address. This threshold is used to determine whether risks exist. If the actual proportion is greater than the threshold, risks exist. The requests that access specified types of resources are identified by using the identification algorithm for special resource crawlers. The requests that access specified paths are identified by using the identification algorithm for specific path crawlers. Data type: float. Valid values: 0.01 to 1.
        -   If you set algorithmName to **PR**, the value of the config parameter contains the following parameters:
            -   **keyPathConfiguration**: optional. The requested URL path. You can specify a maximum of 10 URL paths. This parameter is required only when the algorithmName parameter is set to PR. Data type: array. This parameter is a JSON string that contains the following parameters:
                -   **method**: required. The request method. Data type: string. Valid values: **POST**,**GET**,**PUT**,**DELETE**,**HEAD**, and**OPTIONS**.
                -   **url**: required. The keyword of the URL path. The path must start with a forward slash \(/\). Data type: string.
                -   **matchType**: required. The matching method. This parameter specifies a requested URL path in combination with the **url** parameter. Data type: string. Valid values: **all** \(exact match\), **prefix** \(prefix match\), and **regex** \(regular expression match\).
            -   **minRequestCountPerIp**: required. The minimum number of requests from an IP address. The system detects an IP address only when the number of requests from this IP address is greater than or equal to the value of this parameter. Data type: integer. Valid values: 5 to 10000.
            -   **minRatio**: required. The threshold for the proportion of requests that access specified types of resources or specified paths to requests that are initiated from an IP address. This threshold is used to determine whether risks exist. If the actual proportion is greater than the threshold, risks exist. The requests that access specified types of resources are identified by using the identification algorithm for special resource crawlers. The requests that access specified paths are identified by using the identification algorithm for specific path crawlers. Data type: float. Valid values: 0.01 to 1.
        -   If you set algorithmName to **DPR**, the value of the config parameter contains the following parameters:
            -   **method**: required. The request method. Data type: string. Valid values: **POST**,**GET**,**PUT**,**DELETE**,**HEAD**, and**OPTIONS**.
            -   **urlPattern**: required. The path of key parameters. The path must start with a forward slash \(/\). Data type: string. You can specify multiple key parameters and include each parameter with braces \{\}. Example: `/company/{}/{}/{}/user.php?uid={}`.
            -   **minRequestCountPerIp**: required. The minimum number of requests from an IP address. The system detects an IP address only when the number of requests from this IP address is greater than or equal to the value of this parameter. Data type: integer. Valid values: 5 to 10000.
            -   **minRatio**: required. The threshold for the proportion of requests that use specified key parameters to requests that are initiated from an IP address. This threshold is used to determine whether risks exist. If an actual proportion is greater than the threshold, risks exist. Data type: float. Valid values: 0.01 to 1.
        -   If you set algorithmName to **SR**, the value of the config parameter contains the following parameters:
            -   **maxRequestCountPerSrSession**: required. The minimum number of requests in each session. This threshold is used to determine whether risks exist. If the number of requests in a single session is smaller than the value of this parameter, the session is considered abnormal. Data type: integer. Valid values: 1 to 8.
            -   **minSrSessionCountPerIp**: required. The threshold for the number of abnormal sessions in the requests that are initiated from an IP address. This threshold is used to determine whether risks exist. If the actual number is greater than the threshold, risks exist. Data type: integer. Valid values: 5 to 300.
        -   If you set algorithmName to **IND**, the value of the config parameter contains the following parameters:
            -   **minIpCount**: required. The threshold for the number of IP addresses that the Wi-Fi connected device accesses. This parameter specifies the condition that is used to determine malicious devices. If an actual number is greater than the threshold, risks exist. Data type: integer. Valid values: 5 to 500.
            -   **keyPathConfiguration**: optional. The requested URL path. You can specify a maximum of 10 URL paths. Data type: array. This parameter is a JSON string that contains the following parameters:
                -   **method**: required. The request method. Data type: string. Valid values: **POST**,**GET**,**PUT**,**DELETE**,**HEAD**, and**OPTIONS**.
                -   **url**: required. The keyword of the URL path. The path must start with a forward slash \(/\). Data type: string.
                -   **matchType**: required. The matching method. This parameter specifies a requested URL path in combination with the **url** parameter. Data type: string. Valid values: **all** \(exact match\), **prefix** \(prefix match\), and **regex** \(regular expression match\).
        -   If you set algorithmName to **Periodicity**, the value of the config parameter contains the following parameters:
            -   **minRequestCountPerIp**: required. The minimum number of requests from an IP address. The system detects an IP address only when the number of requests from this IP address is greater than or equal to the value of this parameter. Data type: integer. Valid values: 5 to 10000.
            -   **level**: required. The risk level, which is the extent of obviousness of periodic access from IP addresses. Data type: integer. Valid values:
                -   **0**: obvious
                -   **1**: moderate
                -   **2**: weak
    -   **Example**

        ```
        
            {
                "name": "Crawler identification for proxy devices",
                "algorithmName":"IND",
                "timeInterval":"60",
                "action":"warn",
                "config":{
                    "minIpCount":5,
                    "keyPathConfiguration":[{"url":"/index","method":"GET","matchType":"prefix"}]
                }
            }
            
        ```

-   If the DefenseType parameter is set to **bot\_wxbb\_pkg**, the value of the Rule parameter contains the following parameters:
    -   **name**: required. The name of the rule. Data type: string.
    -   **action**: required. The action performed after the rule is matched. Data type: string. Valid values:
        -   **test**: monitors requests.
        -   **close**: blocks requests.
    -   **nameList**: required. The version information of valid packages. You can specify the version information for a maximum of five valid packages. Data type: array. This parameter is a JSON string that contains the following parameters:
        -   **name**: required. The name of the valid package. Data type: string.
        -   **signList**: required. The signature for the package. You can specify a maximum of 15 signatures. Separate them with commas \(,\). Data type: array.
    -   **Example**

        ```
        
            {
                "name":"test",
                "action":"close",
                "nameList":[{
                    "name":"apk-xxxx",
                    "signList":["xxxxxx","xxxxx","xxxx","xx"]
                }]
            }
            
        ```

-   If the DefenseType parameter is set to **bot\_wxbb**, the value of the Rule parameter contains the following parameters:
    -   **name**: required. The name of the rule. Data type: string.
    -   **uri**: required. The keyword of the URL path that requires protection. The path must start with a forward slash \(/\). Data type: string.
    -   **matchType**: required. The matching method. Data type: string. Valid values: **all** \(exact match\), **prefix** \(prefix match\), and **regex** \(regular expression match\).
    -   **arg**: required. The included parameters. This parameter specifies a URL path in combination with the **matchType** parameter. Data type: string.
    -   **action**: required. The action performed after the rule is matched. Data type: string. Valid values:
        -   **test**: monitors requests.
        -   **close**: blocks requests.
    -   **hasTag**: required. This parameter specifies whether to add a custom signature field. Data type: Boolean.
        -   **true**: In this case, you must set **wxbbVmpFieldType** and **wxbbVmpFieldValue** to specify the type and value of the field.
        -   **false**
    -   **wxbbVmpFieldType**: optional. The type of the signature field. Data type: integer. If you set **hasTag** to **true**, you must also specify this parameter. Valid values:
        -   **0**: header
        -   **1**: parameter
        -   **2**: cookie
    -   **wxbbVmpFieldValue**: optional. The value of the signature field. Data type: string. If you set **hasTag** to **true**, you must also specify this parameter.
    -   **blockInvalidSign**: required. This parameter specifies whether to take actions on an invalid signature. Data type: integer. Set the value to**1**. The value 1 indicates that the default protection policy for path protection rules is enabled.
    -   **blockProxy**: optional. This parameter specifies whether to take actions on a proxy. Data type: integer. Set the value to **1**. If you do not need to perform actions on the proxy, you can leave this parameter unspecified.
    -   **blockSimulator**: optional. This parameter specifies whether to take actions on a simulator. Data type: integer. Set the value to **1**. If you do not need to perform actions on the simulator, you can leave this parameter unspecified.
    -   **Example**

        ```
        
            {
                "name":"test",
                "uri":"/index",
                "matchType":"all",
                "arg":"test",
                "action":"close",
                "hasTag":true,
                "wxbbVmpFieldType":2,
                "wxbbVmpFieldValue":"test",
                "blockInvalidSign":1,
                "blockProxy":1
            }
            
        ```

-   If the DefenseType parameter is set to **ac\_custom**, the value of the Rule parameter varies based on the **scene** parameter.
    -   To create an ACL rule, set **scene** to **custom\_acl**. The value of the Rule parameter contains the following parameters:
        -   **name**: required. The name of the rule. Data type: string.
        -   **scene**: required. The type of the protection policy. Data type: string. If you want to create an ACL rule, set the value to**custom\_acl**.
        -   **action**: required. The action performed after the rule is matched. Data type: string. Valid values:
            -   **monitor**: monitors requests.
            -   **captcha**: performs CAPTCHA verification.
            -   **captcha\_strict**: performs strict CAPTCHA verification.
            -   **js**: performs JavaScript verification.
            -   **block**: blocks requests.
        -   **conditions**: required. The matching condition. You can specify a maximum of five matching conditions. Data type: array. This parameter is a JSON string that contains the following parameters:
            -   **key**: the matching item. Value values: **URL**,**IP**,**Referer**,**User-Agent**,**Params**,**Cookie**,**Content-Type**,**Content-Length**,**X-Forwarded-For**,**Post-Body**,**Http-Method**,**Header**, and **URLPath**.
            -   **opCode**: the logical operator. Valid values:

**Note:** When you create a custom rule, the available logical operators \(**opCode**\) vary based on the matching item \(**key**\). For more information about the logical operators that are available for each matching item, visit the [WAF console](https://yundun.console.aliyun.com/?p=wafnext). The information displayed in the console shall prevail.

                -   **11**: equals to
                -   **10**: does not equal to
                -   **41**: equals to one of multiple values
                -   **50**: does not equal to any value
                -   **1**: includes
                -   **0**: does not include
                -   **51**: includes one of multiple values
                -   **52**: does not include any value
                -   **82**: exists
                -   **2**: does not exist
                -   **21**: length equal to
                -   **22**: length greater than
                -   **20**: length less than
                -   **60**: does not match a regular expression
                -   **61**: matches a regular expression
                -   **72**: matches a prefix
                -   **81**: matches a suffix
                -   **80**: empty content
            -   **values**: the matching value. You can specify this parameter based on your business requirements. Data type: string.

**Note:** The values of **opCode** and **values** in the matching conditions must be set based on the **key** parameter. For more information about matching conditions, see [Fields in matching conditions](~~147945~~).

        -   **Example**

            ```
            
                    {
                        "action":"monitor",
                        "name":"test",
                        "scene":"custom_acl",
                        "conditions":[{"opCode":1,"key":"URL","values":"/example"}]
                    }
                    
            ```

    -   To create an HTTP flood protection rule, set **scene** to **custom\_acl**. The value of the Rule parameter contains the following parameters:
        -   **name**: required. The name of the rule. Data type: string.
        -   **scene**: required. The type of the protection policy. Data type: string. If you want to create an HTTP flood protection rule, set the value to **custom\_cc**.
        -   **conditions**: required. The matching condition. You can specify a maximum of five matching conditions. Data type: array. This parameter is a JSON string that contains the following parameters:
            -   **key**: the matching item. Value values: **URL**,**IP**,**Referer**,**User-Agent**,**Params**,**Cookie**,**Content-Type**,**Content-Length**,**X-Forwarded-For**,**Post-Body**,**Http-Method**,**Header**, and **URLPath**.
            -   **opCode**: the logical operator. Valid values:

**Note:** When you create a custom rule, the available logical operators \(**opCode**\) vary based on the matching item \(**key**\). For more information about the logical operators that are available for each matching item, visit the [WAF console](https://yundun.console.aliyun.com/?p=wafnext). The information displayed in the console shall prevail.

                -   **11**: equals to
                -   **10**: does not equal to
                -   **41**: equals to one of multiple values
                -   **50**: does not equal to any value
                -   **1**: includes
                -   **0**: does not include
                -   **51**: includes one of multiple values
                -   **52**: does not include any value
                -   **82**: exists
                -   **2**: does not exist
                -   **21**: length equal to
                -   **22**: length greater than
                -   **20**: length less than
                -   **60**: does not match a regular expression
                -   **61**: matches a regular expression
                -   **72**: matches a prefix
                -   **81**: matches a suffix
                -   **80**: empty content
            -   **values**: the matching value. You can specify this parameter based on your business requirements. Data type: string.

**Note:** The values of **opCode** and **values** in the matching conditions must be set based on the **key** parameter.

        -   **action**: required. The action performed after the rule is matched. Data type: string. Valid values:
            -   **monitor**: monitors requests.
            -   **captcha**: performs CAPTCHA verification.
            -   **captcha\_strict**: performs strict CAPTCHA verification.
            -   **js**: performs JavaScript verification.
            -   **block**: blocks requests.
        -   **ratelimit**: required. The maximum rate of requests from an object. Data type: JSON string. This parameter is a JSON string that contains the following parameters:
            -   **target**: required. The type of the object whose request rate is calculated. Data type: string. Valid values:
                -   **remote\_addr**: IP addresses.
                -   **cookie.acw\_tc**: sessions.
                -   **queryarg**: custom parameters. If you choose to use custom parameters, you must specify the name of the custom parameter in the **subkey** parameter.
                -   **cookie**: custom cookies. If you choose to use custom cookies, you must specify the cookie content in the **subkey** parameter.
                -   **header**: custom headers. If you choose to use custom headers, you must specify the header content in the **subkey** parameter.
            -   **subkey**: optional. This parameter is required only when **target** is set to **cookie**, **header** or **queryarg**. Data type: string.
            -   **interval**: required. The period for measuring the number of requests from the specified object. This parameter must be used together with the **threshold** parameter. Data type: integer. Unit: seconds.
            -   **threshold**: required. The maximum number of requests that are allowed from an individual object during the specified period. Data type: integer.
            -   **status**: optional. The frequency of an HTTP status code. Data type: JSON string. This parameter is a JSON string that contains the following parameters:
                -   **code**: required. The specified HTTP status code. Data type: integer.
                -   **count**: optional. The threshold for the number of times that the specified HTTP status code is returned. If the actual number is greater than the threshold, the protection rule is matched. Data type: integer. Valid values: 1 to 999999999. You can set the **count** or **ratio** parameter. You cannot set both parameters at the same time.
                -   **ratio**: optional. The threshold for the percentage of times that the specified HTTP status code is returned. If the actual number is greater than the threshold, the protection rule is matched. Data type: integer. Valid values: 1 to 100. You can set the **count** or **ratio** parameter. You cannot set both parameters at the same time.
            -   **scope**: required. The scope in which the settings take effect. Data type: string. Valid values:
                -   **rule**: the objects that match the specified conditions
                -   **domain**: the domains names to which the rule is applied
            -   **ttl**: required. The period during which the specified action is performed. Data type: integer. Valid values: 60 to 86400.
        -   **Example**

            ```
            
                    {
                        "name":"HTTP flood protection rule",
                        "conditions":[{"opCode":1,"key":"URL","values":"/example"}],
                        "action":"block", 
                        "scene":"custom_cc",  
                        "ratelimit":{
                            "target": "remote_addr", 
                            "interval": 300,
                            "threshold": 2000,
                            "status": {
                                "code": 404,
                                "count": 200
                            },
                            "scope": "rule",
                            "ttl": 1800
                        }
                    }
                    
            ```

-   If the DefenseType parameter is set to **whitelist**, the value of the Rule parameter contains the following parameters:
    -   **name**: required. The name of the rule. Data type: string.
    -   **tags**: required. The protection module that skips detection. You can specify multiple modules. Data type: array. Valid values:
        -   **waf**: website whitelist
        -   **cc**: HTTP flood protection
        -   **customrule**: custom protection policy
        -   **blacklist**: IP address blacklist
        -   **antiscan**: scan protection
        -   **regular**: web application protection
        -   **deeplearning**: deep learning
        -   **antifraud**: data risk control
        -   **dlp**: data leak prevention
        -   **tamperproof**: website tamper-proofing
        -   **bot\_intelligence**: bot threat intelligence
        -   **bot\_algorithm**: intelligent algorithm
        -   **bot\_wxbb**: application protection
    -   **conditions**: required. The matching condition. You can specify a maximum of five matching conditions. Data type: array. This parameter is a JSON string that contains the following parameters:
        -   **key**: the matching item. Value values: **URL**,**IP**,**Referer**,**User-Agent**,**Params**,**Cookie**,**Content-Type**,**Content-Length**,**X-Forwarded-For**,**Post-Body**,**Http-Method**,**Header**, and **URLPath**.
        -   **opCode**: the logical operator. Valid values:

**Note:** When you create a custom rule, the available logical operators \(**opCode**\) vary based on the matching item \(**key**\). For more information about the logical operators that are available for each matching item, visit the [WAF console](https://yundun.console.aliyun.com/?p=wafnext). The information displayed in the console shall prevail.

            -   **11**: equals to
            -   **10**: does not equal to
            -   **41**: equals to one of multiple values
            -   **50**: does not equal to any value
            -   **1**: includes
            -   **0**: does not include
            -   **51**: includes one of multiple values
            -   **52**: does not include any value
            -   **82**: exists
            -   **2**: does not exist
            -   **21**: length equal to
            -   **22**: length greater than
            -   **20**: length less than
            -   **60**: does not match a regular expression
            -   **61**: matches a regular expression
            -   **72**: matches a prefix
            -   **81**: matches a suffix
            -   **80**: empty content
        -   **values**: the matching value. You can specify this parameter based on your business requirements. Data type: string.

**Note:** The values of **opCode** and **values** in the matching conditions must be set based on the **key** parameter.

    -   **Example**

        ```
        
            {
                "name": "test",
                "tags": ["cc","customrule"],
                "conditions":[{"opCode":1,"key":"URL","values":"/example"}],
           }
           
        ```


## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=CreateProtectionModuleRule
&Domain=www.example.com
&InstanceId=waf_elasticity-cn-0xldbqt****
&DefenseType=ac_custom
&Rule= {"action":"monitor","name":"test","scene":"custom_acl","conditions":[{"opCode":1,"key":"URL","values":"/example"}]}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateProtectionModuleRuleResponse>
      <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
</CreateProtectionModuleRuleResponse>
```

`JSON` format

```
{
    "RequestId": "D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

