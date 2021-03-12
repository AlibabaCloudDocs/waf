# ModifyProtectionModuleRule

You can call this operation to modify the rules of a Web Application Firewall \(WAF\) protection module, such as web intrusion prevention, data security, advanced protection, anti-Bot, access control and throttling, and whitelist.

You can set the **DefenseType** parameter to specify the protection module. For more information about the values of this parameter, see the description of **DefenseType** in the following section.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=ModifyProtectionModuleRule&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|Boolean|No|ModifyProtectionModuleRule|The operation that you want to perform. Set the value to **ModifyProtectionModuleRule**. |
|DefenseType|String|No|ac\_custom|Specify the protection module. Valid values:

-   **tamperproof**: tamper protection.
-   **dlp**: data leakage prevention.
-   **ng\_account**: account security rule configuration
-   **bot\_intelligence**: Bot Threat Intelligence configuration
-   **antifraud**: data risk control
-   **antifraud\_js**: data risk control JavaScript
-   **bot\_algorithm**: intelligent algorithm rules for Bot management
-   **bot\_wxbb\_pkg**: version protection rules for App protection
-   **bot\_wxbb**: path protection rules for App protection
-   **ac\_blacklist**: IP blacklist
-   **ac\_highfreq**: IP blocking based on the request rate
-   **block\_dirscan**: directory traversal
-   **ac\_custom**: custom protection policies
-   **whitelist**: whitelist |
|Domain|String|No|www.example.com|The domain name that has been added to WAF. |
|InstanceId|String|No|waf\_elasticity-cn-0xldbqtm005|The ID of the WAF instance.

**Note:** You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|LockVersion|Long|Yes|env|The version of the configuration to be modified. |
|Rule|String|No|\{"action":"monitor","name":"test","scene":"custom\_acl","conditions":\[\{"opCode":1,"key":"URL","values":"/example"\}\]\}|The content of the rule. It is a JSON string that contains multiple parameters.

**Note:** According to the specified protection function module configuration \(**DefenseType**\), the specific parameters involved vary. For more information, see Rule parameters. |
|RuleId|Long|Yes|369998|The ID of the rule. |

**Rule parameters**

-   To modify a tamper protection rule, set DefenseType to **tamperproof** and construct a JSON string that includes the following parameters:
    -   **uri**: Required. The URL that needs protection. Data type: string.
    -   **name**: Required. The name of the rule. Data type: string.
    -   **status**: Optional. The protection status of the rule. Data type: integer.
        -   **0**: disabled \(default\).
        -   **1**: enabled.
    -   **Sample request**

        ```
        
            {
                "name":"example",
                "uri":"http://www.example.com/example",
                "Status":1 
            }
                                    
        ```


-   To modify a data leakage prevention rule, set DefenseType to **dlp** and construct a JSON string that includes the following parameters:
    -   **name**: Required. The name of the rule. Data type: string.
    -   **conditions**: Required. The matching condition, which is described in a JSON string. You can specify up to two conditions that have the AND logical relation to apply the conditions at the same time. Data type: array. The array must include the following parameters:
        -   **key**: The matching items.
            -   **0**: Sets the matching item to URLs.
            -   **10**: indicates sensitive information.
            -   **11**: indicates the response code.

**Note:** You cannot set HTTP status codes \(**11**\) and sensitive information \(**10**\) as the matching conditions in the **conditions** parameter at the same time.

        -   **operation**: The matching logic. This value is set to **1** by default, which specifies the INCLUDES logical operator.
        -   **value**: The matching condition values, which are formulated in a JSON string. You can specify multiple values. The JSON string must include the following parameters:
            -   **v**: only applies to scenarios where the matching condition \(**key**\) is set to URLs \(**0**\) or HTTP status codes \(**11**\).
                -   URL: when`"key":0` the parameter value is the URL address.
                -   Response Code: when`"key":11` valid values for the parameter include**400**,**401**,**402**,**403**,**404**,**405-499**,**500**,**501**,**502**,**503**,**504**,**505-599**.
            -   **k**: only applies to scenarios where the matching item \(**key**\) is set to sensitive information \(**10**\). Valid values:
                -   **100**: masks resident ID card numbers.
                -   **101**: masks credit card numbers.
                -   **102**: masks phone numbers.
                -   **103**: masks the default sensitive words.
    -   **action**: The matching action.
        -   **3**: sets the matching action to warn.
        -   **10**: filters sensitive information. This action only applies to scenarios where sensitive information is contained \(`"key":10`\) to find matching conditions.
        -   **11**: indicates that the system returns to the built-in intercept page, this action only applies to response codes \(`"key":11`\) to find matching conditions.
    -   **Sample request**

        ```
        
          {
            "name":"example",
            "conditions":[{"key":11,"operation":1,"value":[{"v":401}]},{"key":"0","operation":1,"value":[{"v":"www.example.com"}]}],
            "action":3
          }
                                    
        ```

-   Configure account security rules \(**ng\_account**\) corresponding to the JSON string contains the following parameters:
    -   **url\_path**: Required. The URL to the operation that runs detection tasks. The URL must start with a slash \(/\). Data type: string.
    -   **Method**: The request method to be moderated. Valid values: POST, GET, PUT, and DELETE. Data Type: String. You can set multiple request methods. Separate multiple request methods with commas \(,\).
    -   **account\_left**: Required. The parameter that specifies the account. Data type: string.
    -   **password\_left**: Optional. The password of the account. Data type: string.
    -   **Action**: \(required\) The protection action. Valid values:
        -   **Monitor**: indicates an alert.
        -   **Block**: indicates interception.
    -   **Sample request**

        ```
        
            {
                "url_path":"/example",
                "method":"POST,GET,PUT,DELETE",
                "account_left":"aaa",
                "password_left:" 123 ",
                "action":"monitor"
            }
                                    
        ```

-   Bot Threat Intelligence configurations \(**bot\_intelligence**\) corresponding to the JSON string contains the following parameters:
    -   **Name**: Required. The rule name. It must be consistent with the rule ID \(**RuleId**\) parameter. Data type: string.
    -   **urlList**: Required. The protected paths. You can specify a maximum of ten protected paths. Data type: array. The code is represented as a JSON string, which includes the following parameters:
        -   **Mode**: Required. The matching method. This parameter must be the same as the path keyword \(**URL**\) parameter in combination with the specified protected path. Optional values: **EQ**\(Precise matching\),**prefix-match**\(Prefix matching\),**regex**\(Regular expression matching\).
        -   **URL**: Required. The path keyword, which must start with a forward slash \(/\). Data Type: string.
    -   **action**: Required. The action performed after the rule is matched. Data type: string. Valid values:
        -   **monitor**: monitors requests
        -   **captcha**: requires CAPTCHA verification
        -   **captcha\_strict**: indicates the strict slider.
        -   **JS**: indicates JavaScript validation.
        -   **block**: blocks requests
    -   **Status**: Required. The status of the instance. Valid values: integer.
        -   **0**: disables the rule.
        -   **1**: enables the rule.
    -   **Sample request**

        ```
        
            {
                "urlList":[
                    {"mode":"prefix-match","url":"/indexa"},
                    {"mode":"regex","url":"/"},
                    {"mode":"eq","url":"/"}],
                "name":"IDC IP Address Library-Tencent Cloud",
                "action":"captcha_strict",
                "Status":1
            }
                                    
        ```

-   Bot management intelligent algorithm rule configuration \(**bot\_algorithm**\) corresponding to the JSON string contains the following parameters:
    -   **name**: Required. The name of the rule. Data type: string.
    -   **algorithmName**: Required. The name of the algorithm. Valid values:
        -   **RR**: indicates the crawler identification algorithm for special resources.
        -   **PR**: indicates the targeted path Crawler identification algorithm.
        -   **DPR**: indicates the round-robin Crawler identification algorithm.
        -   **SR**: indicates the dynamic IP Crawler identification algorithm.
        -   **IND**: indicates the proxy Crawler identification algorithm.
        -   **Periodicity**: indicates the periodic crawler recognition algorithm.
    -   **timeInterval**: Required. The detection period. Valid values: 30, 60, 120, 300, and 600. Unit: Seconds. Data type: integer.
    -   **action**: Required. The action performed after the rule is matched. Data type: string. Valid values:
        -   **Monitor**: indicates observation.
        -   **CAPTCHA**: indicates the slider.
        -   **JS**: indicates JavaScript validation.
        -   **Block**: indicates the block. When blocking is selected as the disposal action, the blocking duration \( **blocktime**\) parameter.
    -   **blocktime**: Optional. The blocking duration. Unit: Minutes. Value range: 1 to 600.
    -   **config**: Required. The algorithm configuration, in JSON format. Data type: string. The specific sub-parameters in the algorithm configuration and the selected algorithm name \( **algorithmName**\) related.
        -   Crawler identification algorithm for special resources \(**RR**\) the corresponding configuration information shall contain the following sub-parameters:
            -   **resourceType**: The type of the requested resource. Data type: integer. Valid values:
                -   **1**: represents a dynamic resource type.
                -   **2**: represents a static resource type.
                -   **-1**: indicates custom resource types. If you select a custom Resource Group, **extensions** the parameter that specifies the resource suffix in string format. Separate multiple file extensions with commas \(,\), for example,`css,jpg,xls`.
            -   **minRequestCountPerIp**: Required. The IP address range in the detection period. Only IP addresses that have a specified number of access requests are detected. Data type: integer. This parameter specifies the minimum number of requests. Valid values: 5 to 10000.
            -   **minRatio**: Required. The risk determination condition. A risk is determined when the proportion of requests sent by an IP address exceeds the threshold. Valid values: 0.01 to 1.
        -   Directed path Crawler identification algorithm \(**PR**\) the corresponding configuration information shall contain the following sub-parameters:
            -   **keyPathConfiguration**: The request path. You can specify a maximum of 10 Paths. This parameter is required only when a Crawler identification algorithm is used. Data type: array. The parameters must be in a JSON string. The following parameters must be included:
                -   **Method**: Required. The request method. Valid values:**POST**,**GET**,**PUT**,**DELETE**,**HEAD**,**OPTIONS**.
                -   **URL**: Required. The request path keyword, which must start with a forward slash \(/\). Data type: string.
                -   **matchType**: Required. The matching method. This parameter must be the same as the request path keyword \(**URL** parameter in combination with the specified request path. Valid values: **all**\(Precise matching\),**prefix**\(Prefix matching\),**regex**\(Regular expression matching\).
            -   **minRequestCountPerIp**: Required. The IP address range in the detection period. Only IP addresses that have a specified number of access requests are detected. Data type: integer. This parameter specifies the minimum number of requests. Valid values: 5 to 10000.
            -   **minRatio**: Required. The risk determination condition. A risk is determined when the proportion of requests sent from an IP address to the specified path exceeds the threshold. Valid values: 0.01 to 1.
        -   Parameter polling Crawler identification algorithm \(**DPR**\) the corresponding configuration information shall contain the following sub-parameters:
            -   **Method**: Required. The request method. Valid values:**POST**,**GET**,**PUT**,**DELETE**,**HEAD**,**OPTIONS**.
            -   **urlPattern**: Required. The path of the key parameter, which must start with a forward slash \(/\). Data type: string. Key parameters are indicated by braces \(\{\}\). When multiple braces \(\{\}\) are set, these parameters are joined as key parameters. For example, `/company/{}/{}/{}/user.php? uid={}`.
            -   **minRequestCountPerIp**: Required. The IP address range in the detection period. Only IP addresses that have a specified number of access requests are detected. Data type: integer. This parameter specifies the minimum number of requests. Valid values: 5 to 10000.
            -   **minRatio**: Required. The risk determination condition. If the value of a key parameter exceeds the threshold, the request is considered as a risk. A value of 0.01 to 1 indicates a risk. \(required\)
        -   Dynamic IP Crawler identification algorithm \(**SR**\) the corresponding configuration information shall contain the following sub-parameters:
            -   **maxRequestCountPerSrSession**: Required. It specifies the minimum number of requests in each session. If the number of requests in each session is smaller than the value of this parameter, a session is abnormal. Valid values: 1 to 8.
            -   **minSrSessionCountPerIp**: Required. The risky condition. The value is the threshold for the number of abnormal sessions in an IP access request. If the number of abnormal sessions exceeds this threshold, a risk is detected. Valid values: 5 to 300.
        -   Proxy Crawler identification algorithm \(**IND**\) the corresponding configuration information shall contain the following sub-parameters:
            -   **minIpCount**: Required. The condition for determining the number of IP addresses associated with the Wi-Fi connection of a malicious device. If the threshold is exceeded, a risk is detected. Valid values: 5 to 500.
            -   **keyPathConfiguration**: The detection path information. You can specify up to 10 paths. Data type: array. The parameters must be in a JSON string. The following parameters must be included:
                -   **Method**: Required. The request method. Valid values:**POST**,**GET**,**PUT**,**DELETE**,**HEAD**,**OPTIONS**.
                -   **URL**: Required. The keyword of the detection path, which must start with a forward slash \(/\). Data type: string.
                -   **matchType**: Required. The matching method. This parameter must be the same as the keyword of the detection path \(**URL** parameter in combination with the specified request path. Valid values: **all**\(Precise matching\),**prefix**\(Prefix matching\),**regex**\(Regular expression matching\).
        -   Periodic Crawler identification algorithm \(**Periodicity**\) the corresponding configuration information shall contain the following sub-parameters:
            -   **minRequestCountPerIp**: Required. The IP address range in the detection period. Only IP addresses that have a specified number of access requests are detected. Data type: integer. This parameter specifies the minimum number of requests. Valid values: 5 to 10000.
            -   **level**: Required. The risk level of the Accessed IP address. It indicates the visibility of the periodic features of the IP address. Data type: Integer. Valid values:
                -   **0**: indicates obvious
                -   **1**: Medium
                -   **2**: indicates weak.
    -   **Sample request**

        ```
        
            {
                "name":"proxy Crawler identification",
                "algorithmName":"IND",
                "timeInterval":"60",
                "action":"warn",
                "config":{
                    "minIpCount":5,
                    "keyPathConfiguration":[{"url":"/index","method":"GET","matchType":"prefix"}]
                }
            }
                                    
        ```

-   Version protection rule configuration for App protection \(**bot\_wxbb\_pkg**\) corresponding to the JSON string contains the following parameters:
    -   **name**: Required. The name of the rule. Data type: string.
    -   **action**: Required. The action performed after the rule is matched. Data type: string. Valid values:
        -   **Test**: indicates observation.
        -   **Close**: indicates the block.
    -   **nameList**: Required. The version information. You can specify up to five rules. Data type: array. The parameter is represented as a JSON string, which includes the following parameters:
        -   **Name**: Required. The name of the valid package. Data type: string.
        -   **signList**: Required. The maximum number of package signatures. You can specify up to 15. Separate multiple signatures with commas \(,\). Data type: array.
    -   **Sample request**

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

-   Configure the path protection rule for App protection**bot\_wxbb**\) corresponding to the JSON string contains the following parameters:
    -   **name**: Required. The name of the rule. Data type: string.
    -   **uri**: Required. The path, which must start with a forward slash \(/\). Data type: string.
    -   **matchType**: Required. The matching method. Data type: string. Valid values: **all**\(Precise matching\),**prefix**\(Prefix matching\),**regex**\(Regular expression matching\).
    -   **Arg**: Required. The parameter value defines the specified protected path configuration with the **matchType** parameter. Data type: string.
    -   **action**: Required. The action performed after the rule is matched. Data type: string. Valid values:
        -   **Test**: Indicates the observation.
        -   **Close**: Indicates the block.
    -   **hasTag**: Required. Data type: boolean. You must specify whether to sign the fields.
        -   **true**: indicates yes. When you select fields that require custom signing, you must pass in **wxbbVmpFieldType** and**wxbbVmpFieldValue** the parameters specify the type and value of the field that you want to sign.
        -   **false**: indicates no.
    -   **wxbbVmpFieldType**: Optional. The type of the user-defined field. Data type: Integer. When the **hasTag** parameter value is**true** you must specify the parameter. Valid values:
        -   **0**: indicates the header.
        -   **1**: represents the parameter.
        -   **2**: indicates a cookie.
    -   **wxbbVmpFieldValue**: Optional. The value of the user-defined field. Data type: string. When the **hasTag** parameter value is**true**, you must specify the parameter.
    -   **blockInvalidSign**: Required. The action to be taken against the invalid signature. Data type: integer. Static value: **1**. The default protection policies of the path protection rule.
    -   **blockProxy**: Required. The processing method of the proxy. Data type: integer. Static value: **1**. This parameter is not required if you do not need to perform the action on the proxy behavior.
    -   **blockSimulator**: Required. Indicates whether to perform the action on the simulator. Data type: integer. Static value: **1**. This parameter is not required if you do not need to perform the action on the simulator behavior.
    -   **Sample request**

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

-   To modify a data risk control request, set DefenseType to **antifraud** and construct a JSON string that includes the following parameters:
    -   **uri**: Required. The request URL. Data type: string.
    -   **Sample request**

        ```
        
            {
                "uri": "http://1.example.com/example"
            }
                                    
        ```

-   To modify the data risk control JavaScript that is inserted into a web page, set DefenseType to **antifraud\_js** and construct a JSON string that includes the following parameters:
    -   **uri**: Required. The URL of the web page into which you want to insert the data risk control JavaScript. The system inserts data risk control JavaScript into all the pages under the specified URL directory. Data type: string.
    -   **Sample request**

        ```
        
            {
                "uri": "/example/example"
            }
                                    
        ```

-   To modify an IP blacklist rule, set DefenseType to **ac\_blacklist**, and construct a JSON string that contains the following parameters:

**Note:** You cannot call API operations to block regions. Use this feature in the console.

    -   **remoteAddr**: Required. The IP addresses in the blacklist. You can specify IP addresses and CIDR blocks. Separate IP addresses with commas \(,\). You can add up to 200 IP addresses to the blacklist. Data type: array. If no value is specified, it indicates that the blacklist is empty.
    -   **Sample request**

        ```
        
            {
                "remoteAddr":["1.1.1.1","12.11.1.2"]
            }
                                    
        ```

-   To modify the rule that automatically blocks IP addresses initiating attacks, set DefenseType to **ac\_highfreq**, and construct a JSON string that contains the following parameters:
    -   **Interval**: Required. The time range to be detected, in seconds. Data type: integer. Valid values:`[5,1800]`.
    -   **TTL**: Required. The duration of blocked IP addresses. Unit: Seconds. Data type: integer. Valid values:`[60,86400]`.
    -   **count**: Required. The maximum number of requests allowed from an IP address. If the number of requests initiated from an IP address during the specified time period exceeds this limit, the IP address is blocked. Data type: integer. Valid values: `[2,50000]`.
    -   **Sample request**

        ```
        
            {
                "interval":60,
                "ttl":300,
                "count":60
             }
                                    
        ```

-   To modify a directory traversal protection rule, set DefenseType to **block\_dirscan** and construct a JSON string that includes the following parameters:
    -   **Interval**: Required. The time range to be detected, in seconds. Valid values:`[5,1800]`.
    -   **TTL**: Required. The duration of blocked IP addresses. Unit: Seconds. Valid values:`[60,86400]`.
    -   **Count**: Required. The number of visits. Valid values:`[2,50000]`.
    -   **Weight**: Required. The threshold of HTTP status codes 404 \(as a percentage\). Valid values:`(0,1]`.
    -   **uriNum**: Required. The threshold of the number of directories to be scanned. Valid values:`[2,50000]`.
    -   **Sample request**

        ```
        
            {
                "interval":10,
                "ttl":1800,
                "count":50,
                "weight":0.7,
                "uriNum":20 
            }
                                    
        ```

-   To modify a custom protection policy, set DefenseType to **ac\_custom**, and set the **scene** parameter in the JSON string to modify an ACL or HTTP flood protection rule.
    -   To modify an ACL rule, set **scene** to **custom\_acl**, and construct a JSON string that includes the following parameters.
        -   **name**: Required. The name of the rule. Data type: string.
        -   **scene**: Required. The type of the protection policy. Data type: string. If you need to modify an ACL rule, set the value to **custom\_acl**.
        -   **action**: Required. The action performed after the rule is matched. Data type: string. Valid values:
            -   **monitor**: monitors requests
            -   **captcha**: requires CAPTCHA verification
            -   **captcha\_strict**: requires more strict CAPTCHA verification
            -   **js**: requires JavaScript verification
            -   **block**: blocks requests
        -   **Conditions**: Required. The matching conditions. You can specify up to five matching conditions. Data type: array. Describe the rate in a JSON string that includes the following parameters:
            -   **Key**: the matching field. Valid values:**URL**,**IP**,**Referer**,**user-Agent**,**Params**,**Cookie**,**content-Type**,**content-Length**,**x-Forwarded-For**,**post-Body**,**http-Method**,**Header**,**URLPath**.
            -   **opCode**: The logical operator. Valid values:
                -   **0**: does not include
                -   **1**: includes
                -   **2**: does not exist
                -   **10**: does not equal
                -   **11**: equals
                -   **20**: length smaller than
                -   **21**: length equals
                -   **22**: length greater than
                -   **30**: value smaller than
                -   **31**: value equals
                -   **32**: value greater than
                -   **40**: does not belong to
                -   **41**: belongs to
            -   **values**: The matching content. Set the content as required, in String format.

**Note:** The logical operator in the matching condition \(**opCode**\) and the values of the matching content \(**values**\) must be set based on the specified matching field \(**key**\). For more information about matching condition configurations, see [matching Condition fields](~~147945~~).

        -   **Sample request**

            ```
            
                    {
                        "action":"monitor",
                        "name":"test",
                        "scene":"custom_acl",
                        "conditions":[{"opCode":1,"key":"URL","values":"/example"}]
                    }
                                                
            ```

    -   Set HTTP flood protection rules \(**scene** the parameter value is**custom\_cc**\), the corresponding JSON string contains the following parameters:
        -   **name**: Required. The name of the rule. Data type: string.
        -   **scene**: Required. The type of the protection policy. Data type: string. If you need to modify a protection rule against HTTP flood attacks, set the value to **custom\_cc**.
        -   **Conditions**: Required. The matching conditions. You can specify up to five matching conditions. Data type: array. Describe the rate in a JSON string that includes the following parameters:
            -   **Key**: the matching field. Valid values:**URL**,**IP**,**Referer**,**user-Agent**,**Params**,**Cookie**,**content-Type**,**content-Length**,**x-Forwarded-For**,**post-Body**,**http-Method**,**Header**,**URLPath**.
            -   **opCode**: The logical operator. Valid values:
                -   **0**: does not include
                -   **1**: includes
                -   **2**: does not exist
                -   **10**: does not equal
                -   **11**: equals
                -   **20**: length smaller than
                -   **21**: length equals
                -   **22**: length greater than
                -   **30**: value smaller than
                -   **31**: value equals
                -   **32**: value greater than
                -   **40**: does not belong to
                -   **41**: belongs to
            -   **values**: The matching content. Set the content as required, in String format.

**Note:** The logical operator in the matching condition \(**opCode**\) and the values of the matching content \(**values**\) must be set based on the specified matching field \(**key**\).

        -   **action**: Required. The action performed after the rule is matched. Data type: string. Valid values:
            -   **monitor**: monitors requests
            -   **captcha**: requires CAPTCHA verification
            -   **captcha\_strict**: requires more strict CAPTCHA verification
            -   **js**: requires JavaScript verification
            -   **block**: block requests
        -   **ratelimit**: Required. The maximum request rate from an object. Data type: JSON. Describe the rate in a JSON string that includes the following parameters:
            -   **target**: Required. The type of the object whose request rate is calculated. Data type: string. Valid values:
                -   **remote\_addr**: IP addresses.
                -   **cookie.acw\_tc**: sessions.
                -   **queryarg**: custom parameters. If you choose to use custom parameters, specify the name of the object in the **subkey** parameter.
                -   **cookie**: custom cookies. If you choose to use custom cookies, specify the cookie content in the **subkey** parameter.
                -   **header**: custom headers. If you choose to use custom headers, specify the header content in the **subkey** parameter.
            -   **subkey**: Optional. When **target** is set to **cookie**, **header**, or **queryarg**, you must specify the required information in the **subkey** parameter. Data type: string.
            -   **interval**: Required. The time period \(in seconds\) during which the number of requests from the specified object is calculated. This parameter must be used together with the **threshold** parameter. Data type: integer.
            -   **threshold**: Required. During the specified time period, the maximum number of requests that are allowed from an individual object. Data type: integer.
            -   **status**: Optional. The maximum number of an HTTP status code. Data type: string. It is described in a JSON string that contains the following parameters:
                -   **code**: Required. The specified HTTP status code. Data type: integer.
                -   **Count**: Optional. It indicates the occurrence threshold. If the number of occurrences exceeds the threshold, a protection rule is hit. Valid values:`[1,999999999]`.**Count** parameters and**ratio** you can select either parameter.
                -   **Ratio**: Optional. The threshold \(in percentage\) of the response code. If the occurrence ratio of a specified response code exceeds this threshold, the rule is hit. Valid values:`[1,100]`. You can select either **Count** and**ratio** parameters.
            -   **scope**: Required. This parameter specifies where the settings take effect. Data type: string. Valid values:
                -   **rule**: objects that match the specified conditions.
                -   **domain**: domains where the rule is applied.
            -   **ttl**: Required. The effective time period \(in seconds\) of the action. Data type: integer. Valid values: 60, 86400.
            -   **Sample request**

                ```
                
                        {
                            "name":"HTTP flood protection",
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

-   Website whitelist rule configuration \(**whitelist**\) corresponding to the JSON string contains the following parameters:
    -   **name**: Required. The name of the rule. Data type: string.
    -   **tags**: Required. The protection modules that can be skipped. You can specify multiple modules. Valid values:
        -   **waf**: the website whitelist
        -   **cc**: system HTTP flood protection
        -   **customrule**: custom rules
        -   **blacklist**: the IP blacklist
        -   **antiscan**: anti-scan protection
        -   **regular**: web application protection
        -   **deeplearning**: deep learning
        -   **antifraud**: data risk control
        -   **dlp**: data leakage prevention
        -   **tamperproof**: tamper protection
        -   **bot\_intelligence**: indicates bot threat intelligence.
        -   **bot\_algorithm**: indicates an intelligent algorithm.
        -   **bot\_wxbb**: indicates App protection.
    -   **Conditions**: Required. The matching conditions. You can specify up to five matching conditions. Data type: array. Describe the rate in a JSON string that includes the following parameters:
        -   **Key**: the matching field. Valid values:**URL**,**IP**,**Referer**,**user-Agent**,**Params**,**Cookie**,**content-Type**,**content-Length**,**x-Forwarded-For**,**post-Body**,**http-Method**,**Header**,**URLPath**.
        -   **opCode**: The logical operator. Valid values:
            -   **0**: does not include
            -   **1**: includes
            -   **2**: does not exist
            -   **10**: does not equal
            -   **11**: equals
            -   **20**: length smaller than
            -   **21**: length equals
            -   **22**: length greater than
            -   **30**: value smaller than
            -   **31**: value equals
            -   **32**: value greater than
            -   **40**: does not belong to
            -   **41**: belongs to
        -   **values**: The matching content. Set the content as required, in String format.

**Note:** The logical operator in the matching condition \(**opCode**\) and the values of the matching content \(**values**\) must be set based on the specified matching field \(**key**\).

    -   **Sample request**

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

## Samples

Sample request

```
http(s)://[Endpoint]/? Action=ModifyProtectionModuleRule
&DefenseType=ac_custom
&Domain=www.example.com
&InstanceId=waf_elasticity-cn-0xldbqtm005
&LockVersion=2
&Rule={"action":"monitor","name":"test","scene":"custom_acl","conditions":[{"opCode":1,"key":"URL","values":"/example"}]}
&RuleId=369998
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

