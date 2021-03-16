# ModifyProtectionModuleRule

Modifies a rule of a specific WAF protection module, such as the web intrusion prevention, data security, advanced protection, bot management, access control and throttling, or website whitelist module.

You can set the **DefenseType** parameter to specify the protection module. For more information about the values of this parameter, see the description of **DefenseType**.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=ModifyProtectionModuleRule&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyProtectionModuleRule|The operation that you want to perform. Set the value to **ModifyProtectionModuleRule**. |
|DefenseType|String|Yes|ac\_custom|The protection module whose rules you want to modify. Valid values:

 -   **tamperproof**: modifies a rule of the website tamper-proofing module.
-   **dlp**: modifies a rule of the data leakage prevention module.
-   **ng\_account**: modifies a rule of the account security module.
-   **bot\_intelligence**: modifies a rule of the bot threat intelligence module.
-   **antifraud**: modifies a rule of the data risk control module.
-   **antifraud\_js**: modifies the web page into which the JavaScript plug-in is inserted.
-   **bot\_algorithm**: modifies a rule of the intelligent algorithm module.
-   **bot\_wxbb\_pkg**: modifies a version protection rule of the app protection module.
-   **bot\_wxbb**: modifies a path protection rule of the app protection module.
-   **ac\_blacklist**: modifies a rule of the IP address blacklist module.
-   **ac\_highfreq**: modifies a rule that blocks IP addresses initiating high-frequency web attacks.
-   **ac\_dirscan**: modifies a rule of the scan protection module.
-   **ac\_custom**: modifies a rule of the custom protection policy module.
-   **whitelist**: modifies a rule of the website whitelist module. |
|Domain|String|Yes|www.example.com|The domain name for which you want to apply the rule after modification.

 **Note:** You can call the [DescribeDomainNames](~~86373~~) operation to query the domain names that are protected by WAF. |
|InstanceId|String|Yes|waf\_elasticity-cn-0xldbqt\*\*\*\*|The ID of the WAF instance.

 **Note:** You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|LockVersion|Long|Yes|2|The version of the rule that you want to modify. |
|Rule|String|Yes|\{"action":"monitor","name":"test","scene":"custom\_acl","conditions":\[\{"opCode":1,"key":"URL","values":"/example"\}\]\}|The configurations of the rule. This parameter is a string consisting of JSON structs.

 **Note:** The parameters that are contained in the string vary based on the protection module, which is specified by the **DefenseType** parameter. For more information, see the "Rule parameters" section. |
|RuleId|Long|Yes|369998|The ID of the rule that you want to modify.

 **Note:** You can call the [DescribeProtectionModuleRules](~~100398~~) operation to query the IDs of created rules. |

All Alibaba Cloud API operations must include common request parameters. For more information about common request parameters, see [Common parameters](~~162719~~).

For more information about sample requests, see the **"Examples"** section of this topic.

**Rule parameters**

-   If the DefenseType parameter is set to **tamperproof**, the value of the Rule parameter contains the following parameters:
    -   **uri**: the URL that requires protection. This parameter is required. Data type: string.
    -   **name**: the name of the rule. This parameter is required. Data type: string.
    -   **status**: the status of the rule. This parameter is optional. Data type: integer. Valid values:
        -   **0**: disables the rule. This is the default value.
        -   **1**: enables the rule.
    -   **Example**

        ```
        
            {
                "name":"example",
                "uri":"http://www.example.com/example",
                "status":1 
            }
            
        ```


-   If the DefenseType parameter is set to **dlp**, the value of the Rule parameter contains the following parameters:
    -   **name**: the name of the rule. This parameter is required. Data type: string.
    -   **conditions**: the matching conditions, which are formulated in a JSON string. You can specify a maximum of two conditions. The two conditions must have the AND logical relation. This parameter is required. Data type: array. The JSON string contains the following parameters:
        -   **key**: the matching item. Valid values:
            -   **0**: URL
            -   **10**: sensitive information
            -   **11**: HTTP status code

**Note:** You cannot set HTTP status codes \(**11**\) and sensitive information \(**10**\) as the matching items in the **conditions** parameter at the same time.

        -   **operation**: the matching logic. Set the value to **1**, which indicates the INCLUDES logical operator.
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
    -   **url\_path**: the URL path in the requests that are detected. The path must start with a forward slash \(/\). This parameter is required. Data type: string.
    -   **method**: the method of the requests that are detected. This parameter is required. Data type: string. Valid values: POST, GET, PUT, and DELETE. You can specify multiple request methods. Separate the request methods with commas \(,\).
    -   **account\_left**: the account. This parameter is required. Data type: string.
    -   **password\_left**: the password. This parameter is optional. Data type: string.
    -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
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

-   If the DefenseType parameter is set to **bot\_intelligence**, the value of the Rule parameter contains the following parameters:
    -   **name**: the name of the rule, which must match the ID of the rule \(**RuleId**\). This parameter is required. Data type: string.
    -   **urlList**: the URL paths that require protection. You can specify a maximum of 10 protection URL paths. Data type: array. Each URL path is formulated in a JSON string that contains the following parameters:
        -   **mode**: the matching method. This parameter specifies a URL path in combination with the **url** parameter. This parameter is required. Data type: string. Valid values: **eq** \(exact match\), **prefix-match** \(prefix match\), and **regex** \(regular expression match\).
        -   **url**: the keyword of the URL path. The path must start with a forward slash \(/\). This parameter is required. Data type: string.
    -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
        -   **monitor**: monitors requests.
        -   **captcha**: performs CAPTCHA verification.
        -   **captcha\_strict**: performs strict CAPTCHA verification.
        -   **js**: performs JavaScript verification.
        -   **block**: blocks requests.
    -   **status**: the status of the rule. This parameter is required. Data type: integer. Valid values:
        -   **0**: disables the rule.
        -   **1**: enables the rule.
    -   **Example**

        ```
        
            {
                "urlList":[
                    {"mode":"prefix-match","url":"/indexa"},
                    {"mode":"regex","url":"/"},
                    {"mode":"eq","url":"/"}],
                "name":"IDC IP Address Library-Tencent Cloud",
                "action":"captcha_strict",
                "status":1
            }
            
        ```

-   If the DefenseType parameter is set to **bot\_algorithm**, the value of the Rule parameter contains the following parameters:
    -   **name**: the name of the rule. This parameter is required. Data type: string.
    -   **algorithmName**: the name of the algorithm. This parameter is required. Data type: string. Valid values:
        -   **RR**: the identification algorithm for special resource crawlers
        -   **PR**: the identification algorithm for specific path crawlers
        -   **DPR**: the identification algorithm for parameter round-robin crawlers
        -   **SR**: the identification algorithm for dynamic IP address crawlers
        -   **IND**: the identification algorithm for proxy device crawlers
        -   **Periodicity**: the identification algorithm for periodical crawlers
    -   **timeInterval**: the interval of detection. This parameter is required. Data type: integer. Valid values: 30, 60, 120, 300, and 600. Unit: seconds.
    -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
        -   **monitor**: monitors requests.
        -   **captcha**: performs CAPTCHA verification.
        -   **js**: performs JavaScript verification.
        -   **block**: blocks requests. If you set the parameter to block, you must also specify the **blocktime** parameter.
    -   **blocktime**: the period during which requests are blocked. This parameter is optional. Data type: integer. Valid values: 1 to 600. Unit: minutes.
    -   **config**: the configurations of the algorithm, which are formulated in a JSON string. This parameter is required. Data type: string. The parameters that are contained in the JSON string vary based on the value of the **algorithmName** parameter.
        -   If you set algorithmName to **RR**, the value of the config parameter contains the following parameters:
            -   **resourceType**: the type of the requested resources. This parameter is optional. Data type: integer. Valid values:
                -   **1**: dynamic resources.
                -   **2**: static resources.
                -   **-1**: custom resources. In this case, you must also use the **extensions** parameter to specify resource suffixes in a string. Separate suffixes with commas \(,\). Example: `css,jpg,xls`.
            -   **minRequestCountPerIp**: the minimum number of requests from an IP address. The system detects an IP address only when the number of requests from this IP address is greater than or equal to the value of this parameter. This parameter is required. Data type: integer. Valid values: 5 to 10000.
            -   **minRatio**: the threshold for the proportion of requests that access specified types of resources to requests that are initiated from an IP address. This threshold is used to determine whether risks exist. If an actual proportion is greater than the threshold, risks exist. This parameter is required. Data type: float. Valid values: 0.01 to 1.
        -   If you set algorithmName to **PR**, the value of the config parameter contains the following parameters:
            -   **keyPathConfiguration**: the requested URL paths. You can specify a maximum of 10 URL paths. This parameter is required only when the algorithmName parameter is set to PR. This parameter is optional. Data type: array. This parameter is a JSON string that contains the following parameters:
                -   **method**: the request method. This parameter is required. Data type: string. Valid values: **POST**, **GET**, **PUT**, **DELETE**, **HEAD**, and **OPTIONS**.
                -   **url**: the keyword of the URL path. The path must start with a forward slash \(/\). This parameter is required. Data type: string.
                -   **matchType**: the matching method. This parameter specifies a requested URL path in combination with the **url** parameter. This parameter is required. Data type: string. Valid values: **all** \(exact match\), **prefix** \(prefix match\), and **regex** \(regular expression match\).
            -   **minRequestCountPerIp**: the minimum number of requests from an IP address. The system detects an IP address only when the number of requests from this IP address is greater than or equal to the value of this parameter. This parameter is required. Data type: integer. Valid values: 5 to 10000.
            -   **minRatio**: the threshold for the proportion of requests that access specified URL paths to requests that are initiated from an IP address. This threshold is used to determine whether risks exist. If an actual proportion is greater than the threshold, risks exist. This parameter is required. Data type: float. Valid values: 0.01 to 1.
        -   If you set algorithmName to **DPR**, the value of the config parameter contains the following parameters:
            -   **method**: the request method. This parameter is required. Data type: string. Valid values: **POST**, **GET**, **PUT**, **DELETE**, **HEAD**, and **OPTIONS**.
            -   **urlPattern**: the path of key parameters. The path must start with a forward slash \(/\). This parameter is required. Data type: string. You can specify multiple key parameters and include each parameter with braces \{\}. Example: `/company/{}/{}/{}/user.php?uid={}`.
            -   **minRequestCountPerIp**: the minimum number of requests from an IP address. The system detects an IP address only when the number of requests from this IP address is greater than or equal to the value of this parameter. This parameter is required. Data type: integer. Valid values: 5 to 10000.
            -   **minRatio**: the threshold for the proportion of requests that use specified key parameters to requests that are initiated from an IP address. This threshold is used to determine whether risks exist. If an actual proportion is greater than the threshold, risks exist. This parameter is required. Data type: float. Valid values: 0.01 to 1.
        -   If you set algorithmName to **SR**, the value of the config parameter contains the following parameters:
            -   **maxRequestCountPerSrSession**: the minimum number of requests in each session. If the number of requests in a single session is smaller than the value of this parameter, the session is considered abnormal. This parameter is required. Data type: integer. Valid values: 1 to 8.
            -   **minSrSessionCountPerIp**: the threshold for the number of abnormal sessions in the requests that are initiated from an IP address. The threshold is used to determine whether risks exist. If an actual number is greater than the threshold, risks exist. This parameter is required. Data type: integer. Valid values: 5 to 300.
        -   If you set algorithmName to **IND**, the value of the config parameter contains the following parameters:
            -   **minIpCount**: the threshold for the number of IP addresses that the Wi-Fi connected device accesses. This parameter specifies the condition that is used to determine malicious devices. If an actual number is greater than the threshold, risks exist. This parameter is required. Data type: integer. Valid values: 5 to 500.
            -   **keyPathConfiguration**: the requested URL paths. You can specify a maximum of 10 URL paths. This parameter is optional. Data type: array. This parameter is a JSON string that contains the following parameters:
                -   **method**: the request method. This parameter is required. Data type: string. Valid values: **POST**, **GET**, **PUT**, **DELETE**, **HEAD**, and **OPTIONS**.
                -   **url**: the keyword of the URL path. The path must start with a forward slash \(/\). This parameter is required. Data type: string.
                -   **matchType**: the matching method. This parameter specifies a requested URL path in combination with the **url** parameter. This parameter is required. Data type: string. Valid values: **all** \(exact match\), **prefix** \(prefix match\), and **regex** \(regular expression match\).
        -   If you set algorithmName to **Periodicity**, the value of the config parameter contains the following parameters:
            -   **minRequestCountPerIp**: the minimum number of requests from an IP address. The system detects an IP address only when the number of requests from this IP address is greater than or equal to the value of this parameter. This parameter is required. Data type: integer. Valid values: 5 to 10000.
            -   **level**: the risk level, which is the extent of obviousness of periodic access from IP addresses. This parameter is required. Data type: integer. Valid values:
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
    -   **name**: the name of the rule. This parameter is required. Data type: string.
    -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
        -   **test**: monitors requests.
        -   **close**: blocks requests.
    -   **nameList**: the version information of valid packages. You can specify the version information for a maximum of five valid packages. This parameter is required. Data type: array. This parameter is a JSON string that contains the following parameters:
        -   **name**: the name of the valid package. This parameter is required. Data type: string.
        -   **signList**: the signature for the package. You can specify a maximum of 15 signatures. Separate them with commas \(,\). This parameter is required. Data type: array.
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
    -   **name**: the name of the rule. This parameter is required. Data type: string.
    -   **uri**: the keyword of the URL path that requires protection. The path must start with a forward slash \(/\). This parameter is required. Data type: string.
    -   **matchType**: the matching method. This parameter is required. Data type: string. Valid values: **all** \(exact match\), **prefix** \(prefix match\), and **regex** \(regular expression match\).
    -   **arg**: the included parameters. This parameter specifies a URL path in combination with the **matchType** parameter. This parameter is required. Data type: string.
    -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
        -   **test**: monitors requests.
        -   **close**: blocks requests.
    -   **hasTag**: specifies whether to add a custom signature field. This parameter s required. Data type: Boolean.
        -   **true**: In this case, you must set **wxbbVmpFieldType** and **wxbbVmpFieldValue** to specify the type and value of the field.
        -   **false**
    -   **wxbbVmpFieldType**: the type of the signature field. This parameter is optional. Data type: integer. If you set **hasTag** to **true**, you must also specify this parameter. Valid values:
        -   **0**: header
        -   **1**: parameter
        -   **2**: cookie
    -   **wxbbVmpFieldValue**: the value of the signature field. This parameter is optional. Data type: string. If you set **hasTag** to **true**, you must also specify this parameter.
    -   **blockInvalidSign**: specifies whether to take actions on an invalid signature. This parameter is required. Data type: integer. Set the value to **1**. The value 1 indicates that the default protection policy for path protection rules is enabled.
    -   **blockProxy**: specifies whether to take actions on a proxy. This parameter is optional. Data type: integer. Set the value to **1**. If you do not need to perform actions on the proxy, you can leave this parameter unspecified.
    -   **blockSimulator**: specifies whether to take actions on a simulator. This parameter is optional. Data type: integer. Set the value to **1**. If you do not need to perform actions on the simulator, you can leave this parameter unspecified.
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

-   If the DefenseType parameter is set to **antifraud**, the value of the Rule parameter contains the following parameters:
    -   **uri**: the requested URL. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "uri": "http://1.example.com/example"
            }
            
        ```

-   If the DefenseType parameter is set to **antifraud\_js**, the value of the Rule parameter contains the following parameters:
    -   **uri**: the URL path of the web page into which you want to insert the JavaScript plug-in for data risk control. The path must start with a forward slash \(/\). The system inserts the JavaScript plug-in into all the pages in the specified URL path. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "uri": "/example/example"
            }
            
        ```

-   If the DefenseType parameter is set to **ac\_blacklist**, the value of the Rule parameter contains the following parameters:
    -   **remoteAddr**: the IP addresses in the blacklist. This parameter is optional. Data type: array. You can enter both IP addresses and CIDR blocks. Separate multiple IP addresses with commas \(,\). You can enter a maximum of 200 IP addresses. If you leave this parameter unspecified, the system clears the blacklist.
    -   **area**: the regions in the region-level IP address blacklist. This parameter is optional. Data type: array. This parameter is a string consisting JSON arrays. Each element in a JSON array is a JSON struct that includes the following parameters:
        -   **countryCodes**: the code of the country. This parameter is required. Data type: array. If you set this parameter to `["CN"]`, the system blocks requests from regions inside China, and you must also specify the **regionCodes** parameter. If you set this parameter to a non-`["CN"]` value, the system blocks requests from other countries and regions, and you do not need to specify the **regionCodes** parameter. You can call the [DescribeProtectionModuleCodeConfig](~~201108~~) operation to query the codes of regions inside China and the codes of other countries and regions.
        -   **regionCodes**: the code of the region inside China. This parameter is optional. Data type: array.
    -   **Example**

        ```
        
        {
            "remoteAddr": [
                "1.XX.XX.1",
                "2.XX.XX.2"
            ],
            "area": [
                {
                    "countryCodes": [
                        "CN"
                    ],
                    "regionCodes": [
                        "310000",
                        "530000"
                    ]
                },
                {
                    "countryCodes": [
                        "AD",
                        "AL"
                    ]
                }
            ]
        }
            
        ```

-   If the DefenseType parameter is set to **ac\_highfreq**, the value of the Rule parameter contains the following parameters:
    -   **interval**: the interval of detection. This parameter is required. Data type: integer. Valid values: 5 to 1800. Unit: seconds.
    -   **ttl**: the period during which an IP address is blocked. This parameter is required. Data type: integer. Valid values: 60 to 86400. Unit: seconds.
    -   **count**: the threshold for the number of web attacks initiated from an IP address. If the number of attacks initiated from an IP address during the specified period is greater than the threshold, the IP address is blocked. This parameter is required. Data type: integer. Valid values: 2 to 50000.
    -   **Example**

        ```
        
            {
            	"interval":60,
            	"ttl":300,
            	"count":60
             }
            
        ```

-   If the DefenseType parameter is set to **ac\_dirscan**, the value of the Rule parameter contains the following parameters:
    -   **interval**: the interval of detection. This parameter is required. Data type: integer. Valid values: 5 to 1800. Unit: seconds.
    -   **ttl**: the period during which an IP address is blocked. This parameter is required. Data type: integer. Valid values: 60 to 86400. Unit: seconds.
    -   **count**: the maximum number of requests allowed from an IP address. This parameter is required. Data type: integer. Valid values: 2 to 50000.
    -   **weight**: the proportion of requests with 404 HTTP status codes to all requests. This parameter is required. Data type: float. Valid values: 0 to 1.
    -   **uriNum**: the maximum number of paths that can be scanned. This parameter is required. Data type: integer. Valid values: 2 to 50000.
    -   **Example**

        ```
        
            {
            	"interval":10,
            	"ttl":1800,
            	"count":50,
            	"weight":0.7,
                "uriNum":20 
            }
            
        ```

-   If the DefenseType parameter is set to **ac\_custom**, the value of the Rule parameter varies based on the **scene** parameter.
    -   To modify an ACL rule, set **scene** to **custom\_acl**. The value of the Rule parameter contains the following parameters:
        -   **name**: the name of the rule. This parameter is required. Data type: string.
        -   **scene**: the type of the protection policy. This parameter is required. Data type: string. If you want to modify an ACL rule, set the value to **custom\_acl**.
        -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
            -   **monitor**: monitors requests.
            -   **captcha**: performs CAPTCHA verification.
            -   **captcha\_strict**: performs strict CAPTCHA verification.
            -   **js**: performs JavaScript verification.
            -   **block**: blocks requests.
        -   **conditions**: the matching conditions. You can specify a maximum of five matching conditions. This parameter is required. Data type: array. This parameter is a JSON string that contains the following parameters:
            -   **key**: the matching item. Valid values: **URL**, **IP**, **Referer**, **User-Agent**, **Params**, **Cookie**, **Content-Type**, **Content-Length**, **X-Forwarded-For**, **Post-Body**, **Http-Method**, **Header**, and **URLPath**.
            -   **opCode**: the logical operator. Valid values:
                -   **0**: DOES NOT INCLUDE or DOES NOT BELONG TO
                -   **1**: INCLUDES or BELONGS TO
                -   **2**: DOES NOT EXIST
                -   **10**: DOES NOT EQUAL
                -   **11**: EQUALS
                -   **20**: LENGTH LESS THAN
                -   **21**: LENGTH EQUAL TO
                -   **22**: LENGTH GREATER THAN
                -   **30**: VALUE SMALLER THAN
                -   **31**: VALUE EQUAL TO
                -   **32**: VALUE GREATER THAN
            -   **values**: the matching value. You can specify this parameter based on your business requirements. Data type: string.

**Note:** The valid values of **opCode** and **values** in the matching conditions vary based on the **key** parameter. For more information about matching conditions, see [Fields in match conditions](~~147945~~).

        -   **Example**

            ```
            
                    {
                        "action":"monitor",
                        "name":"test",
                        "scene":"custom_acl",
                    	"conditions":[{"opCode":1,"key":"URL","values":"/example"}]
                    }
                    
            ```

    -   To modify an HTTP flood protection rule, set **scene** to **custom\_cc**. The value of the Rule parameter contains the following parameters:
        -   **name**: the name of the rule. This parameter is required. Data type: string.
        -   **scene**: the type of the protection policy. This parameter is required. Data type: string. If you want to modify an HTTP flood protection rule, set the value to **custom\_cc**.
        -   **conditions**: the matching conditions. You can specify a maximum of five matching conditions. This parameter is required. Data type: array. This parameter is a JSON string that contains the following parameters:
            -   **key**: the matching item. Valid values: **URL**, **IP**, **Referer**, **User-Agent**, **Params**, **Cookie**, **Content-Type**, **Content-Length**, **X-Forwarded-For**, **Post-Body**, **Http-Method**, **Header**, and **URLPath**.
            -   **opCode**: the logical operator. Valid values:
                -   **0**: DOES NOT INCLUDE or DOES NOT BELONG TO
                -   **1**: INCLUDES or BELONGS TO
                -   **2**: DOES NOT EXIST
                -   **10**: DOES NOT EQUAL
                -   **11**: EQUALS
                -   **20**: LENGTH LESS THAN
                -   **21**: LENGTH EQUAL TO
                -   **22**: LENGTH GREATER THAN
                -   **30**: VALUE SMALLER THAN
                -   **31**: VALUE EQUAL TO
                -   **32**: VALUE GREATER THAN
            -   **values**: the matching value. You can specify this parameter based on your business requirements. Data type: string.

**Note:** The valid values of **opCode** and **values** in the matching conditions vary based on the **key** parameter.

        -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
            -   **monitor**: monitors requests.
            -   **captcha**: performs CAPTCHA verification.
            -   **captcha\_strict**: performs strict CAPTCHA verification.
            -   **js**: performs JavaScript verification.
            -   **block**: blocks requests.
        -   **ratelimit**: the maximum rate of requests from an object. This parameter is required. Data type: JSON string. This parameter is a JSON string that contains the following parameters:
            -   **target**: the type of the object from which the request rate is measured. This parameter is required. Data type: string. Valid values:
                -   **remote\_addr**: IP addresses.
                -   **cookie.acw\_tc**: sessions.
                -   **queryarg**: custom parameters. If you choose to use custom parameters, you must specify the names of the custom parameters in the **subkey** parameter.
                -   **cookie**: custom cookies. If you choose to use custom cookies, you must specify the cookie content in the **subkey** parameter.
                -   **header**: custom headers. If you choose to use custom headers, you must specify the header content in the **subkey** parameter.
            -   **subkey**: This parameter is required only when the **target** parameter is set to **cookie**, **header**, or **queryarg**. The **subkey** parameter is optional. Data type: string.
            -   **interval**: the period for measuring the number of requests from the specified object. This parameter must be used together with the **threshold** parameter. This parameter is required. Data type: integer. Unit: seconds.
            -   **threshold**: the maximum number of requests that are allowed from an individual object during the specified period. This parameter is required. Data type: integer.
            -   **status**: the frequency of an HTTP status code. This parameter is optional. Data type: JSON string. This parameter is a JSON string that contains the following parameters:
                -   **code**: the HTTP status code. This parameter is required. Data type: integer.
                -   **count**: the threshold for the number of times that the specified HTTP status code is returned. The threshold is used to determine whether a rule is matched. If an actual number is greater than the threshold, the rule specified by the name parameter is matched. This parameter is optional. Data type: integer. Valid values: 1 to 999999999. You can set the **count** or **ratio** parameter. You cannot set both parameters at the same time.
                -   **ratio**: the threshold for the percentage of times that the specified HTTP status code is returned. The threshold is used to determine whether a rule is matched. If an actual percentage is greater than the threshold, the rule specified by the name parameter is matched. This parameter is optional. Data type: integer. Valid values: 1 to 100. You can set the **count** or **ratio** parameter. You cannot set both parameters at the same time.
            -   **scope**: the scope in which the settings take effect. This parameter is required. Data type: string. Valid values:
                -   **rule**: the objects that match the specified conditions
                -   **domain**: the domain names to which the rule is applied
            -   **ttl**: the period during which the specified action is performed. This parameter is required. Data type: integer. Valid values: 60 to 86400. Unit: seconds.
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
    -   **name**: the name of the rule. This parameter is required. Data type: string.
    -   **tags**: the protection modules that skip detection. You can specify multiple modules. This parameter is required. Data type: array. Valid values:
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
        -   **bot\_wxbb**: app protection
    -   **conditions**: the matching conditions. You can specify a maximum of five matching conditions. This parameter is required. Data type: array. This parameter is a JSON string that contains the following parameters:
        -   **key**: the matching item. Valid values: **URL**, **IP**, **Referer**, **User-Agent**, **Params**, **Cookie**, **Content-Type**, **Content-Length**, **X-Forwarded-For**, **Post-Body**, **Http-Method**, **Header**, and **URLPath**.
        -   **opCode**: the logical operator. Valid values:
            -   **0**: DOES NOT INCLUDE or DOES NOT BELONG TO
            -   **1**: INCLUDES or BELONGS TO
            -   **2**: DOES NOT EXIST
            -   **10**: DOES NOT EQUAL
            -   **11**: EQUALS
            -   **20**: LENGTH LESS THAN
            -   **21**: LENGTH EQUAL TO
            -   **22**: LENGTH GREATER THAN
            -   **30**: VALUE SMALLER THAN
            -   **31**: VALUE EQUAL TO
            -   **32**: VALUE GREATER THAN
        -   **values**: the matching value. You can specify this parameter based on your business requirements. Data type: string.

**Note:** The valid values of **opCode** and **values** in the matching conditions vary based on the **key** parameter.

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
http(s)://[Endpoint]/? Action=ModifyProtectionModuleRule
&DefenseType=ac_custom
&Domain=www.example.com
&InstanceId=waf_elasticity-cn-0xldbqt****
&LockVersion=2
&Rule={"action":"monitor","name":"test","scene":"custom_acl","conditions":[{"opCode":1,"key":"URL","values":"/example"}]}
&RuleId=369998
&<common request parameters>
```

Sample success responses

`XML` format

```
<ModifyProtectionModuleRuleResponse>
	  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
</ModifyProtectionModuleRuleResponse>
```

`JSON` format

```
{
    "RequestId": "D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

