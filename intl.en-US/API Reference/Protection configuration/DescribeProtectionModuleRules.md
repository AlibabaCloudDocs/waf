# DescribeProtectionModuleRules

Queries the information about the rules that are configured in a specific WAF protection module, such as the web intrusion prevention, data security, bot management, access control or throttling, and website whitelist module.

You can set the **DefenseType** parameter to specify the protection module. For more information about the values of this parameter, see the description of **DefenseType**.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DescribeProtectionModuleRules&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeProtectionModuleRules|The operation that you want to perform. Set the value to **DescribeProtectionModuleRules**. |
|DefenseType|String|Yes|ac\_highfreq|The protection module whose rules you want to query. Valid values:

-   **waf-codec**: queries the decoding settings of the RegEx protection engine module.
-   **tamperproof**: queries the rules of the website tamper-proofing module.
-   **dlp**: queries the rules of the data leak prevention module.
-   **account**: queries the rules of the account security module.
-   **bot\_crawler**: queries the rules of the legitimate crawlers module.
-   **bot\_intelligence**: queries the rules of the bot threat intelligence module.
-   **antifraud**: queries the rules of the data risk control module.
-   **antifraud\_js**: queries the web page into which the JavaScript plug-in is inserted.
-   **bot\_algorithm**: queries the rules of the intelligent algorithm module.
-   **bot\_wxbb\_pkg**: queries the version protection rules of the app protection module.
-   **bot\_wxbb**: queries the path protection rules of the app protection module.
-   **ac\_blacklist**: queries the rules of the IP address blacklist module.
-   **ac\_highfreq**: queries the rules that block IP addresses initiating high-frequency web attacks.
-   **block\_dirscan**: queries the rules of the scan protection module.
-   **ac\_custom**: queries the rules of the custom protection policy module.
-   **whitelist**: queries the rules of the website whitelist module. |
|InstanceId|String|Yes|waf\_elasticity-cn-0xldbqt\*\*\*\*|The ID of the WAF instance.

**Note:** You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|PageSize|Integer|No|10|The number of entries to return on each page. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.Default value: 1 |
|Domain|String|No|www.example.com|The domain name that is protected by WAF.

**Note:** If the **DefenseType** parameter is set to **account**, you can leave this parameter unspecified. In other cases, you must specify this parameter. |
|Query|String|No|e2ZpbHRlcjp7InJ1bGVJZCI6NDI3NTV9LG9yZGVyQnk6ImdtdF9tb2RpZmllZCIsZGVzYzp0cnVlfQ==|The methods to filter and sort the rules. This parameter is a JSON string that contains the following parameters:

**Note:** The value of the **Query** parameter must be Base64-encoded.

-   **filter**: the filter conditions. This parameter is optional. Data type: JSON string. This parameter is a JSON string that contains the following parameters:
    -   **nameId**: queries the rules whose IDs are the same as the value of this parameter or the rules whose names contain the parameter value. This parameter is optional. Data type: string.
    -   **scene**: the protection module whose rules you want to query. The valid values of this parameter are the same as those of the **DefenseType** parameter. This parameter is optional. Data type: string.
    -   **enabled**: specifies whether the rules are enabled. This parameter is optional. Data type: Boolean. Valid values:
        -   **false**: disabled
        -   **true**: enabled
    -   **status**: the status of the rules. The meaning of this parameter is the same as that of the **enabled** parameter. This parameter is optional. Data type: integer. Valid values:
        -   **0**: disabled
        -   **1**: enabled
    -   **ruleId**: the ID of the rule. This parameter is optional. Data type: integer.
    -   **ruleIdList**: the list of rule IDs. Separate multiple rule IDs with commas \(,\). This parameter is optional. Data type: array.
    -   **sceneList**: the list of protection modules. The valid values of this parameter are the same as those of the **DefenseType** parameter. This parameter is optional. Data type: array.
    -   **originList**: the list of rule sources. Separate multiple rule sources with commas \(,\). This parameter is optional. Data type: array. Valid values: **system** \(system-generated\) and **custom** \(user-customized\).
    -   **tag**: If the DefenseType parameter is set to **whitelist**, you can set this parameter to query the whitelist rules of specific modules that skip detection. This parameter is optional. Data type: string. For more information about **tag**, see the descriptions of whitelist rules in the "Content parameters" section.
    -   **category**: If the DefenseType parameter is set to **whitelist**, you can set this parameter to query a specific type of whitelist. This parameter is optional. Data type: string. Valid values:
        -   **waf**: website whitelist
        -   **ws**: Web Intrusion Prevention whitelist
        -   **ac**: Access Control/Throttling whitelist
        -   **ds**: Data Security whitelist
-   **orderBy**: the sorting method. This parameter is optional. Data type: string. Valid values:
    -   **action**: the action performed after the rules are matched. This parameter is valid only when you query the rules of the custom protection policy module.
    -   **gmt\_modified**: the time when the rules were last modified. This is the default value.
    -   **name**: the names of the rules.
    -   **status**: the status of the rules.
-   **desc**: specifies whether the rules are sorted in descending order. This parameter is optional. Data type: Boolean. Valid values:
    -   **false**: ascending order.
    -   **true**: descending order. This is the default value. |
|Lang|String|No|zh|The natural language in which the rule names are displayed. Valid values:

-   **zh**: Chinese
-   **en**: English
-   **ja**: Japanese |
|ResourceGroupId|String|No|rg-acfm2pz25js\*\*\*\*|The ID of the resource group to which the WAF instance belongs in Resource Management. This parameter is empty by default, which indicates that the WAF instance belongs to the default resource group.

For more information about resource groups, see [Create a resource group](~~94485~~). |

All Alibaba Cloud API operations must include common request parameters. For more information about common request parameters, see [Common parameters](~~162719~~).

For more information about sample requests, see the **"Examples"** section of this topic.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|The ID of the request. |
|Rules|Array of Rule| |The configurations of the rules, including the rule IDs, creation time, and status. |
|Content|Map|\{"count":60,"interval":60,"ttl":300\}|The content of the rule. This value is a JSON string that contains multiple parameters.

**Note:** The parameters vary based on the value of the **DefenseType** parameter. For more information, see the **"Content parameters"** section. |
|RuleId|Long|42755|The ID of the rule. |
|Status|Long|1|The status of the rule. Valid values:

-   **0**: disabled
-   **1**: enabled |
|Time|Long|1570700044|The time when the rule was created. This value is a UNIX timestamp representing the number of seconds that have elapsed since the epoch time January 1, 1970, 00:00:00 UTC. |
|Version|Long|2|The system data identifier that is used to control optimistic locking. |
|TotalCount|Integer|1|The total number of entries returned. |

**Content parameters**

-   If the DefenseType parameter is set to **waf-codec**, the value of the Content parameter contains the following parameters:
    -   **codecList**: the enabled decoding settings. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "codecList":["url","base64"]
            }
            
        ```


-   If the DefenseType parameter is set to **tamperproof**, the value of the Content parameter contains the following parameters:
    -   **uri**: the URL that requires protection. This parameter is required. Data type: string.
    -   **name**: the name of the rule. This parameter is required. Data type: string.
    -   **status**: the status of the rule. This parameter is optional. Data type: integer. Valid values:
        -   **0**: disabled. This is the default value.
        -   **1**: enabled.
    -   **Example**

        ```
        
            {
                "name":"example",
                "uri":"http://www.example.com/example",
                "status":1
            }
            
        ```

-   If the DefenseType parameter is set to **dlp**, the value of the Content parameter contains the following parameters:
    -   **name**: the name of the rule. This parameter is required. Data type: string.
    -   **conditions**: the matching conditions, which are formulated in a JSON string. You can specify a maximum of two conditions. The two conditions must have the AND logical relation. This parameter is required. Data type: array. The JSON string contains the following parameters:
        -   **key**: the matching item. Valid values:
            -   **0**: URL
            -   **10**: sensitive information
            -   **11**: HTTP status code
        -   **operation**: the matching logic. This value is fixed as **1**, which indicates the INCLUDES logical relation.
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

-   If the DefenseType parameter is set to **ng\_account**, the value of the Content parameter contains the following parameters:
    -   **domain**: the domain name that is protected by WAF. This parameter is required. Data type: string.
    -   **method**: the method of the requests that are detected. This parameter is required. Data type: string. Valid values: POST, GET, PUT, and DELETE. You can specify multiple request methods. Separate the request methods with commas \(,\).
    -   **url\_path**: the URL path in the requests that are detected. The path must start with a forward slash \(/\). This parameter is required. Data type: string.
    -   **account\_left**: the account. This parameter is required. Data type: string.
    -   **password\_left**: the password. This parameter is optional. Data type: string.
    -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
        -   **monitor**: generates alerts.
        -   **block**: blocks requests.
    -   **Example**

        ```
        
            {
                "domain":"www.example.com",
                "method":"GET,POST",
                "url_path":"/example",
                "account_left":"aaa",
                "action":"monitor"
            }
            
        ```

-   If the DefenseType parameter is set to **bot\_crawler**, the value of the Content parameter contains the following parameters:
    -   **Status**: the status of the rule. This parameter is required. Data type: integer. Valid values:
        -   0: disabled
        -   1: enabled
    -   **Version**: the version of the rule. This parameter is required. Data type: integer.
    -   **Content**: the details of the rule. This parameter is required. Data type: string. This parameter is a JSON string that contains the following parameters:
        -   **name**: the name of the rule. This parameter is required. Data type: string.
        -   **conditions**: the conditions for URL paths that are protected. This parameter is optional. Data type: array. If the DefenseType parameter is set to bot\_crawler, the value of the conditions parameter is fixed as empty, which indicates that all URL paths are protected.
        -   **expressions**: the conditional expression of the rule. The expression represents all the conditions of the rule. This parameter is required. Data type: array.
        -   **bypassTags**: the protection module that skips detection. This parameter is required. Data type: string. If the DefenseType parameter is set to bot\_crawler, the value of the bypassTags parameter is fixed as **antibot**, which indicates the bot management module.
        -   **tags**: the protection module to which the rule belongs. This parameter is required. Data type: array. If the DefenseType parameter is set to bot\_crawler, the value of the tags parameter is fixed as `["antibot"]`, which indicates the bot management module.
    -   **RuleId**: the ID of the rule. This parameter is required. Data type: integer.
    -   **Time**: the time when the rule was last modified. This value is a UNIX timestamp representing the number of seconds that have elapsed since the epoch time January 1, 1970, 00:00:00 UTC. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "Status":0,
                "Version":1,
                "Content":{
                    "name":"Baidu Spider whitelist",
                    "conditions":[],
                    "expressions":["remote_addr inl 'ioc.210d077a-cf34-49ad-a9b3-0aa48095c595' && uri =^ '/'"],
                    "bypassTags":"antibot",
                    "tags":["antibot"]
                },
            "RuleId":20384,
            "Time":1585818161
            }
            
        ```

-   If the DefenseType parameter is set to **bot\_intelligence**, the value of the Content parameter contains the following parameters:
    -   **Status**: the status of the rule. This parameter is required. Data type: integer. Valid values:
        -   0: disabled
        -   1: enabled
    -   **Version**: the version of the rule. This parameter is required. Data type: integer.
    -   **Content**: the details of the rule. This parameter is required. Data type: string. This parameter is a JSON string that contains the following parameters:
        -   **name**: the name of the rule. This parameter is required. Data type: string.
        -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
            -   **monitor**: monitors requests.
            -   **captcha**: performs CAPTCHA verification.
            -   **captcha\_strict**: performs strict CAPTCHA verification.
            -   **js**: performs JavaScript verification.
            -   **block**: blocks requests.
        -   **urlList**: the URL paths that require protection. You can specify a maximum of 10 URL paths. This parameter is required. Data type: array. This parameter is a JSON string that contains the following parameters:
            -   **mode**: the matching method. This parameter is required. Data type: string. This parameter specifies a URL path in combination with the **url** parameter. Valid values: **eq** \(exact match\), **prefix-match** \(prefix match\), and **regex** \(regular expression match\).
            -   **url**: the keyword of the URL path. The path must start with a forward slash \(/\). This parameter is required. Data type: string.
        -   **keyType**: the type of the intelligence library. Valid values: **IP** \(IP address library\) and **ua** \(fingerprint library\).
    -   **RuleId**: the ID of the rule. This parameter is required. Data type: integer.
    -   **Time**: the time when the rule was last modified. This value is a UNIX timestamp representing the number of seconds that have elapsed since the epoch time January 1, 1970, 00:00:00 UTC. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "Status":1,
                "Version":1,
                "Content":{
                    "name":"IDC IP Address Library-Tencent Cloud",
                    "action":"captcha_strict",
                    "urlList":[{"mode":"prefix-match","url":"/indexa"},    {"mode":"regex","url":"/"},{"mode":"eq","url":"/"}],
                    "keyType":"ip"
                },
                "RuleId":922777,
                "Time":1585907112
            }
            
        ```

-   If the DefenseType parameter is set to **antifraud**, the value of the Content parameter contains the following parameters:
    -   **uri**: the requested URL. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "uri": "http://1.example.com/example"
            }
            
        ```

-   If the DefenseType parameter is set to **antifraud\_js**, the value of the Content parameter contains the following parameters:
    -   **uri**: the URL path of the web page into which the JavaScript plug-in for data risk control is inserted. The path must start with a forward slash \(/\). The system inserts the JavaScript plug-in into all the pages in the specified URL path. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "uri": "/example/example"
            }
            
        ```

-   If the DefenseType parameter is set to **bot\_algorithm**, the value of the Content parameter contains the following parameters:
    -   **Status**: the status of the rule. This parameter is required. Data type: integer. Valid values:
        -   0: disabled
        -   1: enabled
    -   **Version**: the version of the rule. This parameter is required. Data type: integer.
    -   **Content**: the details of the rule. This parameter is required. Data type: string. This parameter is a JSON string that contains the following parameters:
        -   **name**: the name of the rule. This parameter is required. Data type: string.
        -   **timeInterval**: the interval of detection. This parameter is required. Data type: integer. Valid values: 30, 60, 120, 300, and 600. Unit: seconds.
        -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
            -   **monitor**: monitors requests.
            -   **captcha**: performs CAPTCHA verification.
            -   **js**: performs JavaScript verification.
            -   **block**: blocks requests. If you set the parameter to block, you must also specify the **blocktime** parameter.
        -   **blocktime**: the period during which requests are blocked. This parameter is optional. Data type: integer. Valid values: 1 to 600. Unit: minutes.
        -   **algorithmName**: the name of the algorithm. This parameter is required. Data type: string. Valid values:
            -   **RR**: identification algorithm for specific resource crawlers
            -   **PR**: identification algorithm for specific path crawlers
            -   **DPR**: identification algorithm for parameter round-robin crawlers
            -   **SR**: identification algorithm for dynamic IP address crawlers
            -   **IND**: identification algorithm for proxy device crawlers
            -   **Periodicity**: identification algorithm for periodical crawlers
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
                    -   **0:** obvious
                    -   **1:** moderate
                    -   **2**: weak
    -   **RuleId**: the ID of the rule. This parameter is required. Data type: integer.
    -   **Time**: the time when the rule was last modified. This value is a UNIX timestamp representing the number of seconds that have elapsed since the epoch time January 1, 1970, 00:00:00 UTC. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "Status":1,
                "Version":1,
                "Content":{
                    "name":"Dynamic IP address",
                    "timeInterval":60,
                    "action":"warn",
                    "algorithmName":"IND",
                    "config":{"minIpCount":5,"keyPathConfiguration":[{"method":"GET","matchType":"prefix","url":"/index"}]}
                },
                "RuleId":940180,
                "Time":1585832957
            }
            
        ```

-   If the DefenseType parameter is set to **bot\_wxbb\_pkg**, the value of the Content parameter contains the following parameters:
    -   **Version**: the version of the rule. This parameter is required. Data type: integer.
    -   **Content**: the details of the rule. This parameter is required. Data type: string. This parameter is a JSON string that contains the following parameters:
        -   **name**: the name of the rule. This parameter is required. Data type: string.
        -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
            -   **test**: monitors requests.
            -   **close**: blocks requests.
        -   **nameList**: the version information of valid packages. You can specify the version information for a maximum of five valid packages. This parameter is required. Data type: array. This parameter is a JSON string that contains the following parameters:
            -   **name**: the name of the valid package. This parameter is required. Data type: string.
            -   **signList**: the signature for the package. You can specify a maximum of 15 signatures. Separate them with commas \(,\). This parameter is required. Data type: array.
    -   **RuleId**: the ID of the rule. This parameter is required. Data type: integer.
    -   **Time**: the time when the rule was last modified. This value is a UNIX timestamp representing the number of seconds that have elapsed since the epoch time January 1, 1970, 00:00:00 UTC. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "Version":0,
                "Content":{
                    "nameList":[{"signList":["xxxxxx","xxxxx","xxxx","xx"],"name":"apk-xxxx"}],
                    "name":"test",
                    "action":"close"
                },
                "RuleId":271,
                "Time":1585836143
            }
            
        ```

-   If the DefenseType parameter is set to **bot\_wxbb**, the value of the Content parameter contains the following parameters:
    -   **Version**: the version of the rule. This parameter is required. Data type: integer.
    -   **Content**: the details of the rule. This parameter is required. Data type: string. This parameter is a JSON string that contains the following parameters:
        -   **name**: the name of the rule. This parameter is required. Data type: string.
        -   **uri**: the keyword of the URL path that requires protection. The path must start with a forward slash \(/\). This parameter is required. Data type: string.
        -   **matchType**: the matching method. This parameter is required. Data type: string. Valid values: **all** \(exact match\), **prefix** \(prefix match\), and **regex** \(regular expression match\).
        -   **arg**: the included parameters. This parameter specifies a URL path in combination with the **matchType** parameter. This parameter is required. Data type: string.
        -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
            -   **test**: monitors requests.
            -   **close**: blocks requests.
        -   **wxbbVmpFieldType**: the type of the signature field. This parameter is optional. Data type: integer. If no custom signature fields are added to the rule, this parameter is not returned. Valid values:
            -   **0**: header
            -   **1**: parameter
            -   **2**: cookie
        -   **wxbbVmpFieldValue**: the value of the signature field. This parameter is optional. Data type: string. If no custom signature fields are added to the rule, this parameter is not returned.
        -   **blockInvalidSign**: specifies whether to take actions on an invalid signature. This parameter is required. Data type: Boolean.
        -   **blockProxy**: specifies whether to take actions on a proxy. This parameter is required. Data type: Boolean.
        -   **blockSimulator**: specifies whether to take actions on a simulator. This parameter is required. Data type: Boolean.
    -   **RuleId**: the ID of the rule. This parameter is required. Data type: integer.
    -   **Time**: the time when the rule was last modified. This value is a UNIX timestamp representing the number of seconds that have elapsed since the epoch time January 1, 1970, 00:00:00 UTC. This parameter is required. Data type: string.
    -   **Example**

        ```
        
            {
                "Version":6,
                "Content":{
                    "blockInvalidSign":true,
                    "wxbbVmpFieldValue":"test",
                    "blockSimulator":true,
                    "matchType":"all",
                    "arg":"test",
                    "name":"test",
                    "action":"close",
                    "blockProxy":true,
                    "uri":"/index",
                    "wxbbVmpFieldType":1
                },
                "RuleId":2585,
                "Time":1586241849
            }
            
        ```

-   If the DefenseType parameter is set to **ac\_blacklist**, the value of the Content parameter contains the following parameters:
    -   **empty**: specifies whether the blacklist is empty. This parameter is required. Data type: Boolean.
    -   **remoteAddr**: the IP addresses in the blacklist. This parameter is required. Data type: array.
    -   **area**: the region blocking rule, which is formulated in a JSON string that contains the countryCodes, regionCodes, and not parameters. \(The not parameter specifies whether to allow access.\) This parameter is required. Data type: string. The blocked countries and regions are returned as codes. We recommend that you go to the console to view the blocked countries and regions.
    -   **Example**

        ```
        
            {
                "empty":false,
                "remoteAddr":["1.1.1.1","12.11.1.2"]
            }
            
        ```

-   If the DefenseType parameter is set to **ac\_highfreq**, the value of the Content parameter contains the following parameters:
    -   **interval**: the interval of detection. This parameter is required. Data type: integer. Valid values: `[5,1800]`. Unit: seconds.
    -   **ttl**: the period during which an IP address is blocked. Data type: integer. Valid values: 60 to 86400. Unit: seconds.
    -   **count**: the threshold for the number of web attacks initiated from an IP address. If the number of attacks initiated from an IP address during the specified period is greater than the threshold, the IP address is blocked. This parameter is required. Data type: integer. Valid values: 2 to 50000.
    -   **Example**

        ```
        
            {
                "interval":60,
                "ttl":300,
                "count":60
             }
            
        ```

-   If the DefenseType parameter is set to **ac\_dirscan**, the value of the Content parameter contains the following parameters:
    -   **interval**: the interval of detection. This parameter is required. Data type: integer. Valid values: `[5,1800]`. Unit: seconds.
    -   **ttl**: the period during which an IP address is blocked. This parameter is required. Data type: integer. Unit: seconds.
    -   **count**: the maximum number of requests allowed from an IP address. This parameter is required. Data type: integer. Valid values: `[2,50000]`.
    -   **weight**: the proportion of requests with 404 HTTP status codes to all requests. This parameter is required. Data type: float. Valid values: `(0,1]`.
    -   **uriNum**: the maximum number of paths that can be scanned. This parameter is required. Data type: integer. Valid values: `[2,50000]`.
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

-   If the DefenseType parameter is set to **ac\_custom**, the value of the Content parameter vary based on the **scene** parameter.
    -   If **scene** is set to **custom\_acl** to configure an ACL rule, the value of the Content parameter contains the following parameters:
        -   **name**: the name of the rule. This parameter is required. Data type: string.
        -   **scene**: the type of the protection policy. This parameter is required. Data type: string. If an ACL rule is configured, the value of this parameter is fixed as **custom\_acl**.
        -   **action**: the action performed after the rule is matched. This parameter is required. Data type: string. Valid values:
            -   **monitor**: monitors requests.
            -   **captcha**: performs CAPTCHA verification.
            -   **captcha\_strict**: performs strict CAPTCHA verification.
            -   **js**: performs JavaScript verification.
            -   **block**: blocks requests.
        -   **conditions**: the matching conditions. This parameter is required. Data type: array. This parameter is a JSON string that contains the following parameters:
            -   **key**: the matching item. Valid values: **URL**, **IP**, **Referer**, **User-Agent**, **Params**, **Cookie**, **Content-Type**, **Content-Length**, **X-Forwarded-For**, **Post-Body**, **Http-Method**, **Header**, and **URLPath**.
            -   **opCode**: the logical operator. Valid values:
                -   **0**: DOES NOT INCLUDE
                -   **1**: INCLUDES
                -   **2**: DOES NOT EXIST
                -   **10**: DOES NOT EQUAL
                -   **11**: EQUALS
                -   **20**: LENGTH LESS THAN
                -   **21**: LENGTH EQUAL TO
                -   **22**: LENGTH GREATER THAN
                -   **30**: VALUE SMALLER THAN
                -   **31**: VALUE EQUAL TO
                -   **32**: VALUE GREATER THAN
                -   **40**: DOES NOT BELONG TO
                -   **41**: BELONGS TO
            -   **values**: the matching value. You can specify this parameter based on your business requirements. Data type: string.
            -   **contain**: the logical operator. The valid values of this parameter are the same as those of the **opCode** parameter.
            -   **opValue**: the description of the abbreviated logical operator. For more information, see the description of **opCode**.
            -   **pattern**: the description of the abbreviated logical operator. The valid values of this parameter are the same as those of the **opValue** parameter.
        -   **expressions**: the conditional expression of the rule. The expression represents all the conditions of the rule. This parameter is required. Data type: array.
        -   **Example**

            ```
            
                    {
                        "name":"test2",
                        "action":"monitor",
                        "conditions":[{"contain":1,"values":"login","pattern":"contain","opCode":1,"opValue":"contain","key":"URL"}],
                        "expressions":["request_uri contains 'login' "],
                        "scene":"custom_acl"
                    }
                    
            ```

    -   If **scene** is set to **custom\_cc** to configure an HTTP flood protection rule, the value of the Content parameter contains the following parameters:
        -   **name**: the name of the rule. This parameter is required. Data type: string.
        -   **scene**: the type of the protection policy. This parameter is required. Data type: string. If an HTTP flood protection rule is configured, the value of this parameter is fixed as **custom\_cc**.
        -   **conditions**: the matching conditions. This parameter is required. Data type: array. This parameter is a JSON string that contains the following parameters:
            -   **key**: the matching item. Valid values: **URL**, **IP**, **Referer**, **User-Agent**, **Params**, **Cookie**, **Content-Type**, **Content-Length**, **X-Forwarded-For**, **Post-Body**, **Http-Method**, **Header**, and **URLPath**.
            -   **opCode**: the logical operator. Valid values:
                -   **0**: DOES NOT INCLUDE
                -   **1**: INCLUDES
                -   **2**: DOES NOT EXIST
                -   **10**: DOES NOT EQUAL
                -   **11**: EQUALS
                -   **20**: LENGTH LESS THAN
                -   **21**: LENGTH EQUAL TO
                -   **22**: LENGTH GREATER THAN
                -   **30**: VALUE SMALLER THAN
                -   **31**: VALUE EQUAL TO
                -   **32**: VALUE GREATER THAN
                -   **40**: DOES NOT BELONG TO
                -   **41**: BELONGS TO
            -   **values**: the matching value. You can specify this parameter based on your business requirements. Data type: string.
            -   **contain**: the logical operator. The valid values of this parameter are the same as those of the **opCode** parameter.
            -   **opValue**: the description of the abbreviated logical operator. For more information, see the description of **opCode**.
            -   **pattern**: the description of the abbreviated logical operator. The valid values of this parameter are the same as those of the **opValue** parameter.
        -   **expressions**: the conditional expression of the rule. The expression represents all the conditions of the rule. This parameter is required. Data type: array.
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
                -   **queryarg**: custom parameters. If you choose to use custom parameters, you must specify the name of the custom parameter in the **subkey** parameter.
                -   **cookie**: custom cookies. If you choose to use custom cookies, you must specify the cookie content in the **subkey** parameter.
                -   **header**: custom headers. If you choose to use custom headers, you must specify the header content in the **subkey** parameter.
            -   **subkey**: This parameter is required only when the **target** parameter is set to **cookie**, **header**, or **queryarg**. The **subkey** parameter is optional. Data type: string.
            -   **interval**: the period for measuring the number of requests from the specified object. This parameter must be used together with the **threshold** parameter. This parameter is required. Data type: integer. Unit: seconds.
            -   **threshold**: the maximum number of requests that are allowed from an individual object during the specified period. This parameter is required. Data type: integer.
            -   **status**: the frequency of an HTTP status code. This parameter is optional. Data type: JSON string. This parameter is a JSON string that contains the following parameters:
                -   **code**: the HTTP status code. This parameter is required. Data type: integer.
                -   **count**: the threshold for the number of times that the specified HTTP status code is returned. The threshold is used to determine whether a rule is matched. If an actual number is greater than the threshold, the rule specified by the name parameter is matched. This parameter is optional. Data type: integer. Valid values: `[1,999999999]`. You can set the **count** or **ratio** parameter. You cannot set both parameters at the same time.
                -   **ratio**: the threshold for the percentage of times that the specified HTTP status code is returned. The threshold is used to determine whether a rule is matched. If an actual percentage is greater than the threshold, the rule specified by the name parameter is matched. This parameter is optional. Data type: integer. Valid values: `[1,100]`. You can set the **count** or **ratio** parameter. You cannot set both parameters at the same time.
            -   **scope**: the scope in which the settings take effect. This parameter is required. Data type: string. Valid values:
                -   **rule**: the objects that match the specified conditions
                -   **domain**: the domain names to which the rule is applied
            -   **ttl**: the period during which the specified action is performed. This parameter is required. Data type: integer. Valid values: `[60,86400]`. Unit: seconds.
            -   **Example**

                ```
                
                        {
                            "name":"HTTP flood protection rule",
                            "conditions":[{"contain":1,"values":"login","pattern":"contain","opCode":1,"opValue":"contain","key":"URL"}],
                            "expressions":["request_uri contains 'login' "],
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

-   If the DefenseType parameter is set to **whitelist**, the value of the Content parameter contains the following parameters:
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
    -   **bypassTags**: the protection modules that skip detection. This parameter is required. Data type: string.
    -   **conditions**: the matching conditions. This parameter is required. Data type: array. This parameter is a JSON string that contains the following parameters:
        -   **key**: the matching item. Valid values: **URL**, **IP**, **Referer**, **User-Agent**, **Params**, **Cookie**, **Content-Type**, **Content-Length**, **X-Forwarded-For**, **Post-Body**, **Http-Method**, **Header**, and **URLPath**.
        -   **opCode**: the logical operator. Valid values:
            -   **0**: DOES NOT INCLUDE
            -   **1**: INCLUDES
            -   **2**: DOES NOT EXIST
            -   **10**: DOES NOT EQUAL
            -   **11**: EQUALS
            -   **20**: LENGTH LESS THAN
            -   **21**: LENGTH EQUAL TO
            -   **22**: LENGTH GREATER THAN
            -   **30**: VALUE SMALLER THAN
            -   **31**: VALUE EQUAL TO
            -   **32**: VALUE GREATER THAN
            -   **40**: DOES NOT BELONG TO
            -   **41**: BELONGS TO
        -   **values**: the matching value. You can specify this parameter based on your business requirements. Data type: string.
        -   **contain**: the logical operator. The valid values of this parameter are the same as those of the **opCode** parameter.
        -   **opValue**: the description of the abbreviated logical operator. For more information, see the description of **opCode**.
        -   **pattern**: the description of the abbreviated logical operator. The valid values of this parameter are the same as those of the **opValue** parameter.
    -   **expressions**: the conditional expression of the rule. The expression represents all the conditions of the rule. This parameter is required. Data type: array.
    -   **Example**

        ```
        
            {
                "name": "test",
                "tags": ["cc","customrule"],
                "bypassTags":"antifraud,dlp,tamperproof", 
                "conditions":[{"contain":1,"values":"login","pattern":"contain","opCode":1,"opValue":"contain","key":"URL"}],
                "expressions":["request_uri contains 'login' "]
           }
           
        ```


## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=DescribeProtectionModuleRules
&InstanceId=waf_elasticity-cn-0xldbqt****
&Domain=www.example.com
&DefenseType=ac_highfreq
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeProtectionModuleRulesResponse>
      <TotalCount>1</TotalCount>
      <Rules>
            <Version>2</Version>
            <Status>1</Status>
            <Content>
                  <count>60</count>
                  <interval>60</interval>
                  <ttl>300</ttl>
            </Content>
            <RuleId>42755</RuleId>
            <Time>1570700044</Time>
      </Rules>
      <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
</DescribeProtectionModuleRulesResponse>
```

`JSON` format

```
{
    "TotalCount": 1,
    "Rules": [
        {
            "Version": 2,
            "Status": 1,
            "Content": {
                "count": 60,
                "interval": 60,
                "ttl": 300
            },
            "RuleId": 42755,
            "Time": 1570700044
        }
    ],
    "RequestId": "D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

