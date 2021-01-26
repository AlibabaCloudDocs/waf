# ModifyProtectionModuleRule

调用ModifyProtectionModuleRule修改指定WAF防护功能模块（包括Web入侵防护、数据安全、高级防护、Bot管理、访问控制或限流、白名单等模块）中的规则配置。

您可以通过设置**DefenseType**参数值指定要配置的防护功能模块。具体参数值的含义，请参见请求参数**DefenseType**的描述。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=ModifyProtectionModuleRule&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyProtectionModuleRule|要执行的操作。取值：**ModifyProtectionModuleRule**。 |
|DefenseType|String|是|ac\_custom|要配置的防护功能模块。取值：

 -   **tamperproof**：表示配置网站防篡改规则。
-   **dlp**：表示配置防敏感信息泄漏规则。
-   **ng\_account**：表示配置账户安全规则。
-   **bot\_intelligence**：表示配置爬虫威胁情报。
-   **antifraud**：表示配置数据风控防护请求。
-   **antifraud\_js**：表示配置数据风控JS插入页面。
-   **bot\_algorithm**：表示配置Bot管理的智能算法规则。
-   **bot\_wxbb\_pkg**：表示配置App防护的版本防护规则。
-   **bot\_wxbb**：表示配置App防护的路径防护规则。
-   **ac\_blacklist**：表示配置IP黑名单规则。
-   **ac\_highfreq**：表示配置高频Web攻击IP自动封禁规则。
-   **ac\_dirscan**：表示配置目录扫描防护规则。
-   **ac\_custom**：表示配置自定义防护策略规则。
-   **whitelist**：表示配置白名单规则。 |
|Domain|String|是|www.example.com|要配置的域名名称。

 **说明：** 您可以调用[DescribeDomainNames](~~86373~~)查询所有已添加到WAF进行防护的域名。 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqt\*\*\*\*|WAF实例ID。

 **说明：** 您可以通过调用[DescribeInstanceInfo](~~140857~~)接口查看当前WAF实例ID。 |
|LockVersion|Long|是|2|规则配置记录版本号。 |
|Rule|String|是|\{"action":"monitor","name":"test","scene":"custom\_acl","conditions":\[\{"opCode":1,"key":"URL","values":"/example"\}\]\}|规则配置内容，以一系列参数构造的JSON格式转化成字符串。

 **说明：** 根据所指定的防护功能模块配置（**DefenseType**）不同，具体涉及的参数有所不同。详细信息，请参见Rule参数具体说明。 |
|RuleId|Long|是|369998|要配置的规则ID。

 **说明：** 您可以调用[DescribeProtectionModuleRules](~~100398~~)查询所有已创建的规则的ID。 |

调用API时，除了本文中该API的请求参数，还需加入阿里云API公共请求参数。公共请求参数的详细介绍，请参见[公共参数](~~162719~~)。

调用API的请求格式，请参见本文**示例**中的请求示例。

**Rule参数具体说明**

-   网站防篡改规则配置（**tamperproof**）对应的JSON字符串中包含以下参数：
    -   **uri**：String类型 \| 必选 \| 所需防护的具体URL。
    -   **name**：String类型 \| 必选 \| 规则名称。
    -   **status**：Integer类型 \| 可选 \| 规则的防护状态。取值：
        -   **0**（默认）：表示不生效。
        -   **1**：表示生效。
    -   **示例**

        ```
        
            {
                "name":"example",
                "uri":"http://www.example.com/example",
                "status":1 
            }
            
        ```


-   防敏感信息泄露规则配置（**dlp**）对应的JSON字符串中包含以下参数：
    -   **name**：String类型 \| 必选 \| 规则名称。
    -   **conditions**：Array类型 \| 必选 \| 以JSON字符串格式描述匹配条件，支持设置最多两条匹配条件且条件间的关系为并且。其中包含以下具体参数：
        -   **key**：匹配项。
            -   **0**：表示防护的URL。
            -   **10**：表示敏感信息。
            -   **11**：表示响应码。

**说明：** 您无法在**conditions**参数中同时为响应码（**11**）和敏感信息（**10**）设置匹配条件。

        -   **operation**：匹配逻辑，取值固定为**1**，表示包含。
        -   **value**：以JSON字符串描述匹配条件值，支持填写多个条件值。其中包含以下具体参数：
            -   **v**：仅适用于匹配项（**key**）为URL（**0**）或响应码（**11**）的场景。
                -   URL：当`"key":0`时，参数值为URL地址。
                -   响应码：当`"key":11`，参数取值包括**400**、**401**、**402**、**403**、**404**、**405-499**、**500**、**501**、**502**、**503**、**504**、**505-599**。
            -   **k**：仅适用于匹配项（**key**）为敏感信息（**10**）的场景，取值：
                -   **100**：表示身份证。
                -   **101**：表示信用卡。
                -   **102**：表示电话号码。
                -   **103**：表示默认敏感词。
    -   **action**：匹配动作。
        -   **3**：表示告警。
        -   **10**：表示敏感信息过滤，该动作仅适用于包含敏感信息（`"key":10`）的匹配条件场景。
        -   **11**：表示返回系统内置拦截页面，该动作仅适用于包含响应码（`"key":11`）的匹配条件场景。
    -   **示例**

        ```
        
          {
        	"name":"example",
        	"conditions":[{"key":11,"operation":1,"value":[{"v":401}]},{"key":"0","operation":1,"value":[{"v":"www.example.com"}]}],
        	"action":3
          }
          
        ```

-   账户安全规则配置（**ng\_account**）对应的JSON字符串中包含以下参数：
    -   **url\_path**：String类型 \| 必选 \| 检测接口，以URL路径表示，必须以“/”开头。
    -   **method**：String类型 \| 必选 \| 检测的请求方式，包括POST、GET、PUT、DELETE。支持设定多个请求方式，以英文逗号（,）分隔。
    -   **account\_left**：String类型 \| 必选 \| 账号参数名。
    -   **password\_left**：String类型 \| 可选 \| 密码参数名。
    -   **action**：String类型 \| 必选 \| 防护动作。取值：
        -   **monitor**：表示预警。
        -   **block**：表示拦截。
    -   **示例**

        ```
        
            {
                "url_path":"/example",
                "method":"POST,GET,PUT,DELETE",
                "account_left":"aaa",
                "password_left:"123",
                "action":"monitor"
            }
            
        ```

-   Bot管理的爬虫威胁情报配置（**bot\_intelligence**）对应的JSON字符串中包含以下参数：
    -   **name**：String类型 \| 必选 \| 规则名称，必须与规则ID（**RuleId**）参数对应。
    -   **urlList**：Array类型 \| 必选 \| 防护路径，最多指定10个防护路径。以JSON字符串方式表示，具体包含以下参数：
        -   **mode**：String类型 \| 必选 \| 匹配方式，与路径关键字（**url**）参数结合指定防护路径。取值：**eq**（精准匹配）、**prefix-match**（前缀匹配）、**regex**（正则匹配）。
        -   **url**：String类型 \| 必选 \| 路径关键字，必须以“/”开头。
    -   **action**：String类型 \| 必选 \| 处置动作。取值：
        -   **monitor**：表示观察。
        -   **captcha**：表示滑块。
        -   **captcha\_strict**：表示严格滑块 。
        -   **js**：表示JavaScript校验。
        -   **block**：表示阻断。
    -   **status**：Integer类型 \| 必选 \| 启用状态。取值：
        -   **0**：表示禁用。
        -   **1**：表示启用。
    -   **示例**

        ```
        
            {
                "urlList":[
                    {"mode":"prefix-match","url":"/indexa"},
                    {"mode":"regex","url":"/"},
                    {"mode":"eq","url":"/"}],
                "name":"IDC IP库-腾讯云",
                "action":"captcha_strict",
                "status":1
            }
            
        ```

-   Bot管理的智能算法规则配置（**bot\_algorithm**）对应的JSON字符串中包含以下参数：
    -   **name**：String类型 \| 必选 \| 规则名称。
    -   **algorithmName**：String类型 \| 必选 \| 算法名称。取值：
        -   **RR**：表示专项资源爬虫识别算法。
        -   **PR**：表示定向路径爬虫识别算法。
        -   **DPR**： 表示参数轮询爬虫识别算法。
        -   **SR**：表示动态IP爬虫识别算法。
        -   **IND**：表示代理设备爬虫识别算法。
        -   **Periodicity**：表示周期性爬虫识别算法。
    -   **timeInterval**：Integer类型 \| 必选 \| 检测周期。单位：秒，取值：30、60、120、300、600。
    -   **action**：String类型 \| 必选 \| 处置动作。取值：
        -   **monitor**：表示观察。
        -   **captcha**：表示滑块。
        -   **js**：表示JavaScript校验。
        -   **block**：表示阻断。选择阻断作为处置动作时，必须传入阻断时长（**blocktime**）参数。
    -   **blocktime**：Integer类型 \| 可选 \| 阻断时长。单位：分钟，取值：1~600。
    -   **config**：String类型 \| 必选 \| 算法配置信息，以JSON字符串格式表示。算法配置信息中的具体子参数与所选择的算法名称（**algorithmName**）相关。
        -   专项资源爬虫识别算法（**RR**）对应的配置信息应包含以下子参数：
            -   **resourceType**：Integer类型 \| 可选 \| 请求的资源类型。取值：
                -   **1**：表示动态资源类型。
                -   **2**：表示静态资源类型。
                -   **-1**：表示自定义资源类型。选择自定义资源组时，需要再传入**extensions**参数，以字符串格式指定具体的资源后缀名，多个后缀名间以英文逗号（,）分隔，例如`css,jpg,xls`。
            -   **minRequestCountPerIp**：Integer类型 \| 必选 \| 检测周期中检测IP的范围，大于等于一定访问请求数量的IP才会被检测。通过该参数指定访问请求数量的最小值。取值范围：5~10000。
            -   **minRatio**：Float类型 \| 必选 \| 风险判定条件，即IP访问请求中访问指定资源类型的占比阈值，超过阈值后判定为风险。取值范围：0.01~1。
        -   定向路径爬虫识别算法（**PR**）对应的配置信息应包含以下子参数：
            -   **keyPathConfiguration**：Array类型 \| 可选 \| 请求的路径信息，支持指定最多10条路径，只在使用定向路径爬虫识别算法时需传入该子参数。以JSON字符串格式表示。具体包含以下参数：
                -   **method**：String类型 \| 必选 \| 请求方法。取值：**POST**、**GET**、**PUT**、**DELETE**、**HEAD**、**OPTIONS**。
                -   **url**：String类型 \| 必选 \| 请求路径关键字，必须以“/”开头。
                -   **matchType**：String类型 \| 必选 \| 匹配方式，与请求路径关键字（**url**）参数结合指定请求路径。取值：**all**（精准匹配）、**prefix**（前缀匹配）、**regex**（正则匹配）。
            -   **minRequestCountPerIp**：Integer类型 \| 必选 \| 检测周期中检测IP的范围，大于等于一定访问请求数量的IP才会被检测。通过该参数指定访问请求数量的最小值。取值范围：5~10000。
            -   **minRatio**：Float类型 \| 必选 \| 风险判定条件，即IP访问请求中访问指定路径的占比阈值，超过阈值后判定为风险。取值范围：0.01~1。
        -   参数轮询爬虫识别算法（**DPR**）对应的配置信息应包含以下子参数：
            -   **method**：String类型 \| 必选 \| 请求方法。取值：**POST**、**GET**、**PUT**、**DELETE**、**HEAD**、**OPTIONS**。
            -   **urlPattern**：String类型 \| 必选 \| 关键参数路径，必须以“/”开头。用\{\}表示关键参数，配置多个\{\}时将拼接这些参数作为关键参数。例如，`/company/{}/{}/{}/user.php?uid={}`。
            -   **minRequestCountPerIp**：Integer类型 \| 必选 \| 检测周期中检测IP的范围，大于等于一定访问请求数量的IP才会被检测。通过该参数指定访问请求数量的最小值。取值范围：5~10000。
            -   **minRatio**：Float类型 \| 必选 \| 风险判定条件，即IP访问请求中不同关键参数值的计数占比阈值，超过阈值后判定为风险。取值范围：0.01~1。
        -   动态IP爬虫识别算法（**SR**）对应的配置信息应包含以下子参数：
            -   **maxRequestCountPerSrSession**：Integer类型 \| 必选 \| 通过设定每个会话中存在的最小请求次数定义异常会话，即单个会话中的请求次数小于该值即判定为异常会话。取值范围：1~8。
            -   **minSrSessionCountPerIp**：Integer类型 \| 必选 \| 风险判定条件，即IP访问请求中存在的异常会话数量阈值，单个IP访问请求中的异常会话次数超过该值后判定为风险。取值范围：5~300。
        -   代理设备爬虫识别算法（**IND**）对应的配置信息应包含以下子参数：
            -   **minIpCount**：Integer类型 \| 必选 \| 恶意设备判定条件，即设备使用WIFI关联的IP变换个数阈值，超过该阈值后判定为风险。取值范围：5~500。
            -   **keyPathConfiguration**：Array类型 \| 可选 \| 检测路径信息，支持指定最多10条路径。以JSON字符串格式表示，具体包含以下参数：
                -   **method**：String类型 \| 必选 \| 请求方法。取值：**POST**、**GET**、**PUT**、**DELETE**、**HEAD**、**OPTIONS**。
                -   **url**：String类型 \| 必选 \| 检测路径关键字，必须以“/”开头。
                -   **matchType**：String类型 \| 必选 \| 匹配方式，与检测路径关键字（**url**）参数结合指定请求路径。取值：**all**（精准匹配）、**prefix**（前缀匹配）、**regex**（正则匹配）。
        -   周期性爬虫识别算法（**Periodicity**）对应的配置信息应包含以下子参数：
            -   **minRequestCountPerIp**：Integer类型 \| 必选 \| 检测周期中检测IP的范围，大于等于一定访问请求数量的IP才会被检测。通过该参数指定访问请求数量的最小值。取值范围：5~10000。
            -   **level**：Integer类型 \| 必选 \| 风险判定等级，即访问IP的周期性特征的明显程度。取值：
                -   **0**：表示明显。
                -   **1**：表示中等。
                -   **2**：表示较弱。
    -   **示例**

        ```
        
            {
                "name":"代理设备爬虫识别",
                "algorithmName":"IND",
                "timeInterval":"60",
                "action":"warn",
                "config":{
                    "minIpCount":5,
                    "keyPathConfiguration":[{"url":"/index","method":"GET","matchType":"prefix"}]
                }
            }
            
        ```

-   App防护的版本防护规则配置（**bot\_wxbb\_pkg**）对应的JSON字符串中包含以下参数：
    -   **name**：String类型 \| 必选 \| 规则名称。
    -   **action**：String类型 \| 必选 \| 处置动作。取值：
        -   **test**：表示观察。
        -   **close**：表示阻断。
    -   **nameList**：Array类型 \| 必选 \| 合法版本信息，最多指定五条规则。以JSON字符串方式表示，具体包含以下参数：
        -   **name**：String类型 \| 必选 \| 合法包名称。
        -   **signList**：Array类型 \| 必选 \| 对应的包签名，最多填写15个，以英文逗号（,）分隔。
    -   **示例**

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

-   App防护的路径防护规则配置（**bot\_wxbb**）对应的JSON字符串中包含以下参数：
    -   **name**：String类型 \| 必选 \| 规则名称。
    -   **uri**：String类型 \| 必选 \| 防护路径，必须以“/”开头。
    -   **matchType**：String类型 \| 必选 \| 匹配方式。取值：**all**（精准匹配）、**prefix**（前缀匹配）、**regex**（正则匹配）。
    -   **arg**：String类型 \| 必选 \| 参数包含，与匹配方式（**matchType**）参数结合指定防护路径配置。
    -   **action**：String类型 \| 必选 \| 处置动作。取值：
        -   **test**：表示观察。
        -   **close**：表示阻断。
    -   **hasTag**：Boolean类型 \| 必选 \| 是否需要自定义加签字段。
        -   **true**：表示是。选择需要自定义加签字段时，需传入**wxbbVmpFieldType**和**wxbbVmpFieldValue**参数指定加签字段的类型和对应值。
        -   **false**：表示否。
    -   **wxbbVmpFieldType**：Integer类型 \| 可选 \| 自定义加签字段类型。当**hasTag**参数值为**true**时，必须传入参数。取值：
        -   **0**：表示header。
        -   **1**：表示参数。
        -   **2**：表示cookie。
    -   **wxbbVmpFieldValue**：String类型 \| 可选 \| 自定义加签字段值。当**hasTag**参数值为**true**时，必须传入参数。
    -   **blockInvalidSign**：Integer类型 \| 必选 \| 是否对非法签名执行处置动作，固定值**1**。路径防护规则的默认防护策略。
    -   **blockProxy**：Integer类型 \| 可选 \| 是否对代理执行处置动作，固定值**1**。如果无需对代理行为执行处置动作时无需传入该参数。
    -   **blockSimulator**：Integer类型 \| 可选 \| 是否对模拟器执行处置动作，固定值**1**。如果无需对模拟器行为执行处置动作时无需传入该参数。
    -   **示例**

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

-   数据风控防护请求配置（**antifraud**）对应的JSON字符串中包含以下参数：
    -   **uri**：String类型 \| 必选 \| 具体的防护请求URL。
    -   **示例**

        ```
        
            {
                "uri": "http://1.example.com/example"
            }
            
        ```

-   数据风控JS插入页面配置（**antifraud\_js**）对应的JSON字符串中包含以下参数：
    -   **uri**：String类型 \| 必选 \| 需要插入数据风控JS页面的URL，系统将为所指定的URL路径下的所有页面插入数据风控JS，必须以“/”开头。
    -   **示例**

        ```
        
            {
                "uri": "/example/example"
            }
            
        ```

-   IP黑名单规则配置（**ac\_blacklist**）对应的JSON字符串中包含以下参数：
    -   **remoteAddr**：Array类型 \| 可选 \| 黑名单中的IP。支持填写IP和IP地址段。多个IP以英文逗号（,）分隔，最多可以添加200个。填写空值表示清空IP黑名单。
    -   **area**：Array类型 \| 可选 \| 地域级IP黑名单中的地域。使用JSON数组转化的字符串格式表示，JSON数组中的每个元素是一个结构体，包含以下字段：
        -   **countryCodes**：Array类型 \| 必选 \| 国家代码。只填写`["CN"]`，表示封禁中国境内地域，必须同时填写**regionCodes**；填写`["CN"]`以外内容，表示封禁中国境外地域，无需填写**regionCodes**。您可以调用[DescribeProtectionModuleCodeConfig](~~201108~~)查询中国境内地域代码和中国境外地域代码。
        -   **regionCodes**：Array类型 \| 可选 \| 中国境内地域代码。
    -   **示例**

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

-   高频Web攻击IP自动封禁规则配置（**ac\_highfreq**）对应的JSON字符串中包含以下参数：
    -   **interval**：Integer类型 \| 必选 \| 检测时间范围。单位：秒，取值范围：5~1800。
    -   **ttl**：Integer类型 \| 必选 \| 封禁IP时长。单位秒，取值范围：60~86400。
    -   **count**：Integer类型 \| 必选 \| Web攻击次数阈值，检测时间范围内攻击次数超过该值，触发封禁。取值范围：2~50000。
    -   **示例**

        ```
        
            {
            	"interval":60,
            	"ttl":300,
            	"count":60
             }
            
        ```

-   目录扫描防护规则配置（**ac\_dirscan**）对应的JSON字符串中包含以下参数：
    -   **interval**：Integer类型 \| 必选 \| 检测时间范围。单位秒，取值范围：5~1800。
    -   **ttl**：Integer类型 \| 必选 \| 封禁IP时长。单位秒，取值范围：60~86400。
    -   **count**：Integer类型 \| 必选 \| 访问次数阈值。取值范围：2~50000。
    -   **weight**：Float类型 \| 必选 \| 404响应码占比阈值（百分比）。取值范围：0~1。
    -   **uriNum**：Integer类型 \| 必选 \| 扫描目录数量阈值。取值范围：2~50000。
    -   **示例**

        ```
        
            {
            	"interval":10,
            	"ttl":1800,
            	"count":50,
            	"weight":0.7,
                "uriNum":20 
            }
            
        ```

-   自定义防护策略规则配置（**ac\_custom**），通过其对应的JSON字符串中的**scene**参数来设置ACL访问控制规则和CC攻击防护规则。
    -   设置ACL访问控制规则（**scene**参数值为**custom\_acl**），其对应的JSON字符串中包含以下参数：
        -   **name**：String类型 \| 必选 \| 规则名称。
        -   **scene**：String类型 \| 必选 \| 防护类型。设置ACL访问控制规则时，取值固定为**custom\_acl**。
        -   **action**：String类型 \| 必选 \| 处置动作。取值：
            -   **monitor**：表示观察。
            -   **captcha**：表示滑块。
            -   **captcha\_strict**：表示严格滑块。
            -   **js**：表示JS验证。
            -   **block**：表示阻断。
        -   **conditions**：Array类型 \| 必选 \| 匹配条件，最多支持填写5个匹配条件。以JSON字符串格式进行描述，具体包含以下参数：
            -   **key**：匹配字段。取值：**URL**、**IP**、**Referer**、**User-Agent**、**Params**、**Cookie**、**Content-Type**、**Content-Length**、**X-Forwarded-For**、**Post-Body**、**Http-Method**、**Header**、**URLPath**。
            -   **opCode**：逻辑符。取值：
                -   **0**：表示不包含、不属于。
                -   **1**：表示包含、属于。
                -   **2**：表示不存在。
                -   **10**：表示不等于。
                -   **11**：表示等于。
                -   **20**：表示长度小于。
                -   **21**：表示长度等于。
                -   **22**：表示长度大于。
                -   **30**：表示值小于。
                -   **31**：表示值等于。
                -   **32**：表示值大于。
            -   **values**：匹配内容。根据需要填写相应的内容，以String类型表示。

**说明：** 匹配条件参数中的逻辑符（**opCode**）、匹配内容（**values**）参数取值范围与所指定的匹配字段（**key**）相关。关于支持的匹配条件配置详细信息，请参见[匹配条件字段说明](~~147945~~)。

        -   **示例**

            ```
            
                    {
                        "action":"monitor",
                        "name":"test",
                        "scene":"custom_acl",
                    	"conditions":[{"opCode":1,"key":"URL","values":"/example"}]
                    }
                    
            ```

    -   设置CC攻击防护规则（**scene**参数值为**custom\_cc**），对应的JSON字符串中包含以下参数：
        -   **name**：String类型 \| 必选 \| 规则名称。
        -   **scene**：String类型 \| 必选 \| 防护类型。设置CC攻击防护规则时，取值固定为**custom\_cc**。
        -   **conditions**：Array类型 \| 必选 \| 匹配条件，最多支持填写5个匹配条件。以JSON字符串格式进行描述，具体包含以下参数：
            -   **key**：匹配字段。取值：**URL**、**IP**、**Referer**、**User-Agent**、**Params**、**Cookie**、**Content-Type**、**Content-Length**、**X-Forwarded-For**、**Post-Body**、**Http-Method**、**Header**、**URLPath**。
            -   **opCode**：逻辑符。取值：
                -   **0**：表示不包含、不属于。
                -   **1**：表示包含、属于。
                -   **2**：表示不存在。
                -   **10**：表示不等于。
                -   **11**：表示等于。
                -   **20**：表示长度小于。
                -   **21**：表示长度等于。
                -   **22**：表示长度大于。
                -   **30**：表示值小于。
                -   **31**：表示值等于。
                -   **32**：表示值大于。
            -   **values**：匹配内容。根据需要填写相应的内容，以String类型表示。

**说明：** 匹配条件参数中的逻辑符（**opCode**）、匹配内容（**values**）参数取值范围与所指定的匹配字段（**key**）相关。

        -   **action**：String类型 \| 必选 \| 处置动作，取值：
            -   **monitor**：表示观察。
            -   **captcha**：表示滑块。
            -   **captcha\_strict**：表示严格滑块。
            -   **js**：表示JS验证。
            -   **block**：表示阻断。
        -   **ratelimit**：JSON格式 \| 必选 \| 频率设置。以JSON字符串格式进行描述，具体包含以下参数：
            -   **target**：String类型 \| 必选 \| 统计对象类型，取值：
                -   **remote\_addr**：表示IP。
                -   **cookie.acw\_tc**：表示Session。
                -   **queryarg**：表示自定义参数。选择自定义参数时，必须在**subkey**参数中填写需要统计的自定义参数名称。
                -   **cookie**：表示自定义cookie。选择自定义cookie时，必选在**subkey**参数中填写需要统计的cookie内容。
                -   **header**：表示自定义header。选择自定义header时，必选在**subkey**参数中填写需要统计的header内容。
            -   **subkey**：String类型 \| 可选 \| 当**target**参数值为**cookie**、**header**或**queryarg**时，必选在**subkey**参数中填写对应的信息。
            -   **interval**： Integer类型 \| 必选 \| 统计时长（单位：秒），即访问次数的统计周期，与阈值（**threshold**）参数配合。
            -   **threshold**：Integer类型 \| 必选 \| 在检测时长内，允许单个统计对象访问被防护地址的次数阈值。
            -   **status**：JSON格式 \| 可选 \| 响应码频率设置。以JSON字符串格式进行描述，具体包含以下参数：
                -   **code**：Integer类型 \| 必选 \| 指定响应码。
                -   **count**：Integer类型 \| 可选 \| 出现次数阈值，即表示当指定的响应码出现次数超过该阈值时命中防护规则。取值范围：1~999999999。**count**参数与**ratio**参数两者选其一，不可同时配置。
                -   **ratio**：Integer类型 \| 可选 \| 出现比例阈值（百分比），即表示当指定的响应码出现比例超过该阈值时命中防护规则。取值范围：1~100。**count**参数与**ratio**参数两者选其一，不可同时配置。
            -   **scope**：String类型 \| 必选 \| 生效范围，取值：
                -   **rule**：表示当前特征匹配范围内。
                -   **domain**：表示当前规则作用的域名范围内。
            -   **ttl**：Integer类型 \| 必选 \| 处置动作的生效时长。单位：秒，取值范围：60~86400。
            -   **示例**

                ```
                
                        {
                            "name":"CC防护",
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

-   网站白名单规则配置（**whitelist**）对应的JSON字符串中包含以下参数：
    -   **name**：String类型 \| 必选 \| 规则名称。
    -   **tags**：Array类型 \| 必选 \| 不检测模块，可填写多个模块。取值：
        -   **waf**：表示网站白名单。
        -   **cc**：表示系统CC防护。
        -   **customrule**：表示自定义规则。
        -   **blacklist**：表示IP黑名单。
        -   **antiscan**：表示防扫描。
        -   **regular**：表示Web应用攻击防护。
        -   **deeplearning**：表示深度学习。
        -   **antifraud**：表示数据风控。
        -   **dlp**：表示防敏感信息泄露。
        -   **tamperproof**：表示网站防篡改。
        -   **bot\_intelligence**：表示爬虫威胁情报。
        -   **bot\_algorithm**：表示智能算法。
        -   **bot\_wxbb**：表示App防护。
    -   **conditions**：Array类型 \| 必选 \| 匹配条件，最多支持填写5个匹配条件。以JSON字符串格式进行描述，具体包含以下参数：
        -   **key**：匹配字段。取值：**URL**、**IP**、**Referer**、**User-Agent**、**Params**、**Cookie**、**Content-Type**、**Content-Length**、**X-Forwarded-For**、**Post-Body**、**Http-Method**、**Header**、**URLPath**。
        -   **opCode**：逻辑符，取值：
            -   **0**：表示不包含、不属于。
            -   **1**：表示包含、属于。
            -   **2**：表示不存在。
            -   **10**：表示不等于。
            -   **11**：表示等于。
            -   **20**：表示长度小于。
            -   **21**：表示长度等于。
            -   **22**：表示长度大于。
            -   **30**：表示值小于。
            -   **31**：表示值等于。
            -   **32**：表示值大于。
        -   **values**：匹配内容。根据需要填写相应的内容，以String类型表示。

**说明：** 匹配条件参数中的逻辑符（**opCode**）、匹配内容（**values**）参数取值范围与所指定的匹配字段（**key**）相关。

    -   **示例**

        ```
        
            {
                "name": "test",
                "tags": ["cc","customrule"],
                "conditions":[{"opCode":1,"key":"URL","values":"/example"}],
           }
           
        ```


## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|本次请求的ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ModifyProtectionModuleRule
&DefenseType=ac_custom
&Domain=www.example.com
&InstanceId=waf_elasticity-cn-0xldbqt****
&LockVersion=2
&Rule={"action":"monitor","name":"test","scene":"custom_acl","conditions":[{"opCode":1,"key":"URL","values":"/example"}]}
&RuleId=369998
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyProtectionModuleRuleResponse>
	  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
</ModifyProtectionModuleRuleResponse>
```

`JSON`格式

```
{
    "RequestId": "D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/waf-openapi)查看更多错误码。

