# DescribeProtectionModuleRules

调用DescribeProtectionModuleRules接口查询指定WAF防护功能模块（包括Web入侵防护、数据安全、Bot管理、访问控制或限流、网站白名单等模块）中的规则配置记录。

您可以通过设置**DefenseType**参数值指定防护功能模块配置。具体参数值的含义，请参见请求参数**DefenseType**的描述。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=DescribeProtectionModuleRules&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeProtectionModuleRules|要执行的操作。取值：**DescribeProtectionModuleRules**。 |
|DefenseType|String|是|ac\_highfreq|防护功能模块配置，取值：

 -   **waf-codec**：正则防护引擎解码设置
-   **tamperproof**：网站防篡改规则配置
-   **dlp**：防敏感信息泄漏规则配置
-   **ng\_account**：账户安全规则配置
-   **bot\_crawler**：合法爬虫规则配置
-   **bot\_intelligence**：爬虫威胁情报规则配置
-   **antifraud**：数据风控防护请求配置
-   **antifraud\_js**：数据风控JS插入页面配置
-   **bot\_algorithm**：智能算法规则配置
-   **bot\_wxbb\_pkg**：App防护的版本防护规则
-   **bot\_wxbb**：App防护的路径防护规则
-   **ac\_blacklist**：IP黑名单规则配置
-   **ac\_highfreq**：高频Web攻击IP自动封禁规则配置
-   **ac\_dirscan**：目录扫描防护规则配置
-   **ac\_custom**：自定义防护策略规则配置
-   **whitelist**：白名单规则配置 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqt\*\*\*\*|WAF实例ID。

 **说明：** 您可以调用[DescribeInstanceInfo](~~140857~~)接口查看当前WAF实例ID。 |
|PageSize|Integer|否|10|每页显示的规则配置记录数。 |
|PageNumber|Integer|否|1|指定返回的页码，默认返回第一页。 |
|Domain|String|否|www.example.com|已添加的域名名称。

 **说明：** 仅在查询项目安全模块规则时（即**DefenseType**参数值为**account**时）可不填写域名名称参数，查询其它功能模块时必须指定域名配置。 |
|Query|String|否|e2ZpbHRlcjp7InJ1bGVJZCI6NDI3NTV9LG9yZGVyQnk6ImdtdF9tb2RpZmllZCIsZGVzYzp0cnVlfQ==|设置规则的过滤和排序，以JSON格式字符串表达，具体包含以下参数：

 **说明：** **query**参数必须以Base64编码格式传入，请按照以下参数说明构造JSON格式字符串后将其转换为Base64编码格式。

 -   **filter**：JSON格式字符串 \| 可选 \| 过滤条件。以JSON字符串格式描述，具体包含以下参数：
    -   **nameId**：String类型 \| 可选 \| 查询规则ID等于该参数值或规则名称中包含该参数值的规则。
    -   **scene**：String类型 \| 可选 \| 指定查询的防护模块，取值与**DefenseType**参数相同。
    -   **enabled**：Boolean类型 \| 可选 \| 指定查询的规则状态，取值：
        -   **false**：表示已禁用。
        -   **true**：表示已启用。
    -   **status**：Integer类型 \| 可选 \| 指定查询的规则状态，与**enabled**参数含义相同，取值：
        -   **0**：表示已禁用。
        -   **1**：表示已启用。
    -   **ruleId**：Integer类型 \| 可选 \| 指定查询的规则ID。
    -   **ruleIdList**：Array类型 \| 可选 \| 指定查询的规则ID列表，多个规则ID间用“,”分隔。
    -   **sceneList**：Array类型 \| 可选 \| 指定查询的防护模块列表，取值与**DefenseType**参数相同，多个防护模块间用“,”分隔。
    -   **originList**：Array类型 \| 可选 \| 指定规则来源，取值为**system**（表示系统自动生成）和**custom**（表示自定义创建），指定多个规则来源时用“,”分隔。
    -   **tag**：String类型 \| 可选 \| 当指定的查询防护模块为白名单（**whitelist**）时，可通过设置该参数查询不检测指定模块的白名单规则。**tag**参数的取值和含义可参考返回参数中白名单规则配置中的描述。
    -   **category**：String类型 \| 可选 \| 当指定的查询防护模块为白名单（**whitelist**）时，可通过设置该参数查询指定白名单分类，取值：
        -   **waf**：表示网站白名单。
        -   **ws**：表示Web入侵防护白名单。
        -   **ac**：表示访问控制/限流白名单。
        -   **ds**：表示数据安全白名单。
-   **orderBy**：String类型 \| 可选\| 排序字段，取值：
    -   **action**：表示规则处置动作，该参数值仅在查询自定义防护策略规则时有效。
    -   **gmt\_modified**：表示最后一次修改时间（默认值）。
    -   **name**：表示规则名称。
    -   **status**：表示规则状态。
-   **desc**：Boolean类型 \| 可选 \| 是否倒序排列，取值：
    -   **false**：表示正序排列。
    -   **true**：表示倒序排列（默认值）。 |
|Lang|String|否|zh|设置规则名称的语言属性，取值：

 -   **zh**：表示规则名称为中文。
-   **en**：表示规则名称为英文。
-   **ja**：表示规则名称为日文。 |
|ResourceGroupId|String|否|rg-acfm2pz25js\*\*\*\*|WAF实例在资源管理服务中所属的资源组ID。默认为空，即属于默认资源组。

 关于资源组的更多信息，请参见[创建资源组](~~94485~~)。 |

调用API时，除了本文中该API的请求参数，还需加入阿里云API公共请求参数。公共请求参数的详细介绍，请参见[公共参数](~~162719~~)。

调用API的请求格式，请参见本文**示例**中的请求示例。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|本次请求的ID。 |
|Rules|Array of Rule| |规则配置信息，包含规则ID、创建时间、状态等。 |
|Content|Map|\{"count":60,"interval":60,"ttl":300\}|规则配置内容，以一系列参数构造的JSON格式转化成字符串。

 **说明：** 根据所指定的防护功能模块配置（**DefenseType**）不同，具体涉及的参数有所不同。详细信息，请参见**Content**参数具体说明。 |
|RuleId|Long|42755|规则ID。 |
|Status|Long|1|规则状态。取值：

 -   **0**：表示已禁用。
-   **1**：表示已启用。 |
|Time|Long|1570700044|规则创建时间，以秒级时间戳格式显示。 |
|Version|Long|2|系统数据标识，用于实现乐观锁控制。 |
|TotalCount|Integer|1|返回的总记录数。 |

**Content参数具体说明**

-   正则防护引擎解码设置（**waf-codec**）对应的JSON字符串中包含以下参数：
    -   **codecList**：String类型 \| 必选 \| 启用的解码配置项。
    -   **示例**

        ```
        
            {
                "codecList":["url","base64"]
            }
            
        ```


-   网站防篡改规则配置（**tamperproof**）对应的JSON字符串中包含以下参数：
    -   **uri**：String类型 \| 必选 \| 所需防护的具体URL。
    -   **name**：String类型 \| 必选 \| 规则名称。
    -   **status**：Integer类型 \| 可选 \| 规则的防护状态：
        -   **0**：表示不生效（默认）
        -   **1**：表示生效
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
        -   **operation**：匹配逻辑，取值固定为**1**，表示包含。
        -   **value**：以JSON字符串描述匹配条件值，支持填写多个条件值。其中包含以下具体参数：
            -   **v**：仅适用于匹配项（**key**）为URL（**0**）或响应码（**11**）的场景。
                -   URL：当`"key":0`时，参数值为URL地址。
                -   响应码：当`"key":11`，参数取值范围包括**400**、**401**、**402**、**403**、**404**、**405-499**、**500**、**501**、**502**、**503**、**504**、**505-599**。
            -   **k**：仅适用于匹配项（**key**）为敏感信息（**10**）的场景，取值范围：
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
    -   **domain**：String类型 \| 必选 \| 防护的域名。
    -   **method**：String类型 \| 必选 \| 检测的请求方式，包括POST、GET、PUT、DELETE。支持设定多个请求方式，以英文逗号“,”分隔。
    -   **url\_path**：String类型 \| 必选 \| 检测接口，以URL路径表示，必须以“/”开头。
    -   **account\_left**：String类型 \| 必选 \| 账号参数名。
    -   **password\_left**：String类型 \| 可选 \| 密码参数名。
    -   **action**：String类型 \| 必选 \| 防护动作，取值：
        -   **monitor**：表示预警
        -   **block**：表示拦截
    -   **示例**

        ```
        
            {
                "domain":"www.example.com",
                "method":"GET,POST",
                "url_path":"/example",
                "account_left":"aaa",
                "action":"monitor"
            }
            
        ```

-   合法爬虫规则配置（**bot\_crawler**）对应的JSON字符串中包含以下参数：
    -   **Status**：Integer类型 \| 必选 \| 是否启用，取值：
        -   0：表示禁用
        -   1：表示启用
    -   **Version**：Integer类型 \| 必选 \| 规则版本号。
    -   **Content**：String类型 \| 必选 \| 规则详细信息，以JSON字符串格式进行描述，具体包含以下参数：
        -   **name**：String类型 \| 必选 \| 规则名称。
        -   **conditions**：Array类型 \| 可选 \| 防护路径条件。在合法爬虫规则配置中固定为空，表示全路径。
        -   **expressions**：Array类型 \| 必选 \| 规则条件表达式，以更易读的方式表示所有规则条件信息。
        -   **bypassTags**：String类型 \| 必选 \| 不检测的模块。在合法爬虫规则配置中固定为**antibot**，表示Bot管理模块。
        -   **tags**：Array类型 \| 必选 \| 规则所属防护功能模块。在合法爬虫规则配置中固定为`["antibot"]`，表示Bot管理模块。
    -   **RuleId**：Integer类型 \| 必选 \| 规则ID。
    -   **Time**：String类型 \| 必选 \| 规则最新修改时间，以秒级时间戳格式表示。
    -   **示例**

        ```
        
            {
                "Status":0,
                "Version":1,
                "Content":{
                    "name":"百度蜘蛛白名单",
                    "conditions":[],
                    "expressions":["remote_addr inl 'ioc.210d077a-cf34-49ad-a9b3-0aa48095c595' && uri =^ '/'"],
                    "bypassTags":"antibot",
                    "tags":["antibot"]
                },
        	"RuleId":20384,
        	"Time":1585818161
            }
            
        ```

-   Bot管理的爬虫威胁情报配置（**bot\_intelligence**）对应的JSON字符串中包含以下参数：
    -   **Status**：Integer类型 \| 必选 \| 是否启用，取值：
        -   0：表示禁用
        -   1：表示启用
    -   **Version**：Integer类型 \| 必选 \| 规则版本号。
    -   **Content**：String类型 \| 必选 \| 规则详细信息，以JSON字符串格式进行描述，具体包含以下参数：
        -   **name**：String类型 \| 必选 \| 规则名称。
        -   **action**：String类型 \| 必选 \| 处置动作，取值：
            -   **monitor**：表示观察
            -   **captcha**：表示滑块
            -   **captcha\_strict**：表示严格滑块
            -   **js**：表示JavaScript校验
            -   **block**：表示阻断
        -   **urlList**：Array类型 \| 必选 \| 防护路径，最多指定十个防护路径。以JSON字符串方式表示，具体包含以下参数：
            -   **mode**：String类型 \| 必选 \| 匹配方式，与路径关键字（**url**）参数结合指定防护路径。可选值：**eq**（精准匹配）、**prefix-match**（前缀匹配）、**regex**（正则匹配）。
            -   **url**：String类型 \| 必选 \| 路径关键字，必须以“/”开头。
        -   **keyType**：String类型 \| 必选 \| 情报库类型，包含IP库（**ip**）、指纹库（**ua**）两种类型。
    -   **RuleId**：Integer类型 \| 必选 \| 规则ID。
    -   **Time**：String类型 \| 必选 \| 规则最新修改时间，以秒级时间戳格式表示。
    -   **示例**

        ```
        
            {
                "Status":1,
                "Version":1,
                "Content":{
                    "name":"IDC IP库-腾讯云",
                    "action":"captcha_strict",
                    "urlList":[{"mode":"prefix-match","url":"/indexa"},	{"mode":"regex","url":"/"},{"mode":"eq","url":"/"}],
                    "keyType":"ip"
                },
                "RuleId":922777,
                "Time":1585907112
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
    -   **uri**：String类型 \| 必选 \| 需要插入数据风控JS页面的URL，系统将为所指定的URL路径下的所有页面插入数据风控JS。
    -   **示例**

        ```
        
            {
                "uri": "/example/example"
            }
            
        ```

-   Bot管理的智能算法规则配置（**bot\_algorithm**）对应的JSON字符串中包含以下参数：
    -   **Status**：Integer类型 \| 必选 \| 是否启用，取值：
        -   0：表示禁用
        -   1：表示启用
    -   **Version**：Integer类型 \| 必选 \| 规则版本号。
    -   **Content**：String类型 \| 必选 \| 规则详细信息，以JSON字符串格式进行描述，具体包含以下参数：
        -   **name**：String类型 \| 必选 \| 规则名称。
        -   **timeInterval**：Integer类型 \| 必选 \| 检测周期，可选值：30、60、120、300、600，单位秒。
        -   **action**：String类型 \| 必选 \| 处置动作，取值：
            -   **monitor**：表示观察。
            -   **captcha**：表示滑块。
            -   **js**：表示JavaScript校验。
            -   **block**：表示阻断。选择阻断作为处置动作时，必须传入阻断时长（**blocktime**）参数。
        -   **blocktime**：Integer类型 \| 可选 \| 阻断时长，单位分钟，取值范围：1~600。
        -   **algorithmName**：String类型 \| 必选 \| 算法名称，取值：
            -   **RR**：表示专项资源爬虫识别算法
            -   **PR**：表示定向路径爬虫识别算法
            -   **DPR**： 表示参数轮询爬虫识别算法
            -   **SR**：表示动态IP爬虫识别算法
            -   **IND**：表示代理设备爬虫识别算法
            -   **Periodicity**：表示周期性爬虫识别算法
        -   **config**：String类型 \| 必选 \| 算法配置信息，以JSON字符串格式表示。算法配置信息中的具体子参数与所选择的算法名称（**algorithmName**）相关。
            -   专项资源爬虫识别算法（**RR**）对应的配置信息应包含以下子参数：
                -   **resourceType**：Integer类型 \| 可选 \| 请求的资源类型，取值：
                    -   **1**：表示动态资源类型。
                    -   **2**：表示静态资源类型。
                    -   **-1**：表示自定义资源类型。选择自定义资源组时，需要再传入**extensions**参数，以字符串格式指定具体的资源后缀名，多个后缀名间以英文逗号“,”分隔，例如`css,jpg,xls`。
                -   **minRequestCountPerIp**：Integer类型 \| 必选 \| 检测周期中检测IP的范围，大于等于一定访问请求数量的IP才会被检测。通过该参数指定访问请求数量的最小值，取值范围：5~10000。
                -   **minRatio**：Float类型 \| 必选 \| 风险判定条件，即IP访问请求中访问指定资源类型的占比阈值，超过阈值后判定为风险，取值范围：0.01~1。
            -   定向路径爬虫识别算法（**PR**）对应的配置信息应包含以下子参数：
                -   **keyPathConfiguration**：Array类型 \| 可选 \| 请求的路径信息，支持指定最多10条路径，只在使用定向路径爬虫识别算法时需传入该子参数。以JSON字符串格式表示，具体包含以下参数：
                    -   **method**：String类型 \| 必选 \| 请求方法，可选值：**POST**、**GET**、**PUT**、**DELETE**、**HEAD**、**OPTIONS**。
                    -   **url**：String类型 \| 必选 \| 请求路径关键字，必须以“/”开头。
                    -   **matchType**：String类型 \| 必选 \| 匹配方式，与请求路径关键字（**url**）参数结合指定请求路径。可选值：**all**（精准匹配）、**prefix**（前缀匹配）、**regex**（正则匹配）。
                -   **minRequestCountPerIp**：Integer类型 \| 必选 \| 检测周期中检测IP的范围，大于等于一定访问请求数量的IP才会被检测。通过该参数指定访问请求数量的最小值，取值范围：5~10000。
                -   **minRatio**：Float类型 \| 必选 \| 风险判定条件，即IP访问请求中访问指定路径的占比阈值（对应定向路径爬虫识别算法），超过阈值后判定为风险，取值范围：0.01~1。
            -   参数轮询爬虫识别算法（**DPR**）对应的配置信息应包含以下子参数：
                -   **method**：String类型 \| 必选 \| 请求方法，可选值：**POST**、**GET**、**PUT**、**DELETE**、**HEAD**、**OPTIONS**。
                -   **urlPattern**：String类型 \| 必选 \| 关键参数路径，必须以“/”开头。用\{\}表示关键参数，配置多个\{\}时将拼接这些参数作为关键参数。例如，`/company/{}/{}/{}/user.php?uid={}`。
                -   **minRequestCountPerIp**：Integer类型 \| 必选 \| 检测周期中检测IP的范围，大于等于一定访问请求数量的IP才会被检测。通过该参数指定访问请求数量的最小值，取值范围：5~10000。
                -   **minRatio**：Float类型 \| 必选 \| 风险判定条件，即IP访问请求中不同关键参数值的计数占比阈值，超过阈值后判定为风险，取值范围：0.01~1。
            -   动态IP爬虫识别算法（**SR**）对应的配置信息应包含以下子参数：
                -   **maxRequestCountPerSrSession**：Integer类型 \| 必选 \| 通过设定每个会话中存在的最小请求次数定义异常会话，即单个会话中的请求次数小于该值即判定为异常会话。取值范围：1~8。
                -   **minSrSessionCountPerIp**：Integer类型 \| 必选 \| 风险判定条件，即IP访问请求中存在的异常会话数量阈值，单个IP访问请求中的异常会话次数超过该值后判定为风险。取值范围：5~300。
            -   代理设备爬虫识别算法（**IND**）对应的配置信息应包含以下子参数：
                -   **minIpCount**：Integer类型 \| 必选 \| 恶意设备判定条件，即设备使用WIFI关联的IP变换个数阈值，超过该阈值后判定为风险，取值范围：5~500。
                -   **keyPathConfiguration**：Array类型 \| 可选 \| 检测路径信息，支持指定最多10条路径。以JSON字符串格式表示，具体包含以下参数：
                    -   **method**：String类型 \| 必选 \| 请求方法，可选值：**POST**、**GET**、**PUT**、**DELETE**、**HEAD**、**OPTIONS**。
                    -   **url**：String类型 \| 必选 \| 检测路径关键字，必须以“/”开头。
                    -   **matchType**：String类型 \| 必选 \| 匹配方式，与检测路径关键字（**url**）参数结合指定请求路径。可选值：**all**（精准匹配）、**prefix**（前缀匹配）、**regex**（正则匹配）。
            -   周期性爬虫识别算法（**Periodicity**）对应的配置信息应包含以下子参数：
                -   **minRequestCountPerIp**：Integer类型 \| 必选 \| 检测周期中检测IP的范围，大于等于一定访问请求数量的IP才会被检测。通过该参数指定访问请求数量的最小值，取值范围：5~10000。
                -   **level**：Integer类型 \| 必选 \| 风险判定等级，即访问IP的周期性特征的明显程度，取值：
                    -   **0**：表示明显
                    -   **1**：表示中等
                    -   **2**：表示较弱
    -   **RuleId**：Integer类型 \| 必选 \| 规则ID。
    -   **Time**：String类型 \| 必选 \| 规则最新修改时间，以秒级时间戳格式表示。
    -   **示例**

        ```
        
            {
                "Status":1,
                "Version":1,
                "Content":{
                    "name":"动态IP",
                    "timeInterval":60,
                    "action":"warn",
                    "algorithmName":"IND",
                    "config":{"minIpCount":5,"keyPathConfiguration":[{"method":"GET","matchType":"prefix","url":"/index"}]}
                },
                "RuleId":940180,
                "Time":1585832957
            }
            
        ```

-   App防护的版本防护规则配置（**bot\_wxbb\_pkg**）对应的JSON字符串中包含以下参数：
    -   **Version**：Integer类型 \| 必选 \| 规则版本号。
    -   **Content**：String类型 \| 必选 \| 规则详细信息，以JSON字符串格式进行描述，具体包含以下参数：
        -   **name**：String类型 \| 必选 \| 规则名称。
        -   **action**：String类型 \| 必选 \| 处置动作，取值：
            -   **test**：表示观察
            -   **close**：表示阻断
        -   **nameList**：Array类型 \| 必选 \| 合法版本信息，最多指定五条规则。以JSON字符串方式表示，具体包含以下参数：
            -   **name**：String类型 \| 必选 \| 合法包名称。
            -   **signList**：Array类型 \| 必选 \| 对应的包签名，最多包含15个，以英文逗号“,”分隔。
    -   **RuleId**：Integer类型 \| 必选 \| 规则ID。
    -   **Time**：String类型 \| 必选 \| 规则最新修改时间，以秒级时间戳格式表示。
    -   **示例**

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

-   App防护的路径防护规则配置（**bot\_wxbb**）对应的JSON字符串中包含以下参数：
    -   **Version**：Integer类型 \| 必选 \| 规则版本号。
    -   **Content**：String类型 \| 必选 \| 规则详细信息，以JSON字符串格式进行描述，具体包含以下参数：
        -   **name**：String类型 \| 必选 \| 规则名称。
        -   **uri**：String类型 \| 必选 \| 防护路径，必须以“/”开头。
        -   **matchType**：String类型 \| 必选 \| 匹配方式。可选值：**all**（精准匹配）、**prefix**（前缀匹配）、**regex**（正则匹配）。
        -   **arg**：String类型 \| 必选 \| 参数包含，与匹配方式（**matchType**）参数结合指定防护路径配置。
        -   **action**：String类型 \| 必选 \| 处置动作，取值：
            -   **test**：表示观察
            -   **close**：表示阻断
        -   **wxbbVmpFieldType**：Integer类型 \| 可选 \| 自定义加签字段类型。如果规则中未设置自定义加签字段，则不返回该参数。取值：
            -   **0**：表示header。
            -   **1**：表示参数。
            -   **2**：表示cookie。
        -   **wxbbVmpFieldValue**：String类型 \| 可选 \| 自定义加签字段值。如果规则中未设置自定义加签字段，则不返回该参数。
        -   **blockInvalidSign**：Boolean类型 \| 必选 \| 是否对非法签名执行处置动作。
        -   **blockProxy**：Boolean类型 \| 必选 \| 是否对代理执行处置动作。
        -   **blockSimulator**：Boolean类型 \| 必选 \| 是否对模拟器执行处置动作。
    -   **RuleId**：Integer类型 \| 必选 \| 规则ID。
    -   **Time**：String类型 \| 必选 \| 规则最新修改时间，以秒级时间戳格式表示。
    -   **示例**

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

-   IP黑名单规则配置（**ac\_blacklist**）对应的JSON字符串中包含以下参数：
    -   **empty**：Boolean类型 \| 必选 \| 黑名单是否为空。
    -   **remoteAddr**：Array类型 \| 必选 \| 黑名单中的IP。
    -   **area**：String类型 \| 必选 \| 以JSON格式字符串表示区域封禁规则，包含国家编码（countryCodes）、区域编码（regionCodes）、是否放行（not）具体参数。由于API接口中以编码形式返回封禁国家和区域，建议您在控制台中查看具体的封禁国家和区域。
    -   **示例**

        ```
        
            {
                "empty":false,
                "remoteAddr":["1.1.1.1","12.11.1.2"]
            }
            
        ```

-   高频Web攻击IP自动封禁规则配置（**ac\_highfreq**）对应的JSON字符串中包含以下参数：
    -   **interval**：Integer类型 \| 必选 \| 检测时间范围，单位秒，取值范围：`[5,1800]`。
    -   **ttl**：Integer类型 \| 必选 \| 封禁IP时长，单位秒，取值范围：60~86400。
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
    -   **interval**：Integer类型 \| 必选 \| 检测时间范围，单位秒，取值范围：`[5,1800]`。
    -   **ttl**：Integer类型 \| 必选 \| 封禁IP时长，单位秒。
    -   **count**：Integer类型 \| 必选 \| 访问次数阈值，取值范围：`[2,50000]`。
    -   **weight**：Float类型 \| 必选 \| 404响应码占比阈值（百分比），取值范围：`(0,1]`。
    -   **uriNum**：Integer类型 \| 必选 \| 扫描目录数量阈值，取值范围：`[2,50000]`。
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

-   自定义防护策略规则配置（**ac\_custom**），通过其对应JSON字符串中的**scene**参数来设置ACL访问控制规则和CC攻击防护规则。
    -   设置ACL访问控制规则（**scene**参数值为**custom\_acl**），其对应的JSON字符串中包含以下参数：
        -   **name**：String类型 \| 必选 \| 规则名称。
        -   **scene**：String类型 \| 必选 \| 防护类型。设置ACL访问控制规则时，固定为**custom\_acl**。
        -   **action**：String类型 \| 必选 \| 处置动作，取值：
            -   **monitor**：表示观察
            -   **captcha**：表示滑块
            -   **captcha\_strict**：表示严格滑块
            -   **js**：表示JS验证
            -   **block**：表示阻断
        -   **conditions**：Array类型 \| 必选 \| 匹配条件，以JSON字符串格式进行描述，具体包含以下参数：
            -   **key**：匹配字段，取值范围：**URL**、**IP**、**Referer**、**User-Agent**、**Params**、**Cookie**、**Content-Type**、**Content-Length**、**X-Forwarded-For**、**Post-Body**、**Http-Method**、**Header**、**URLPath**。
            -   **opCode**：逻辑符，取值：
                -   **0**：表示不包含
                -   **1**：表示包含
                -   **2**：表示不存在
                -   **10**：表示不等于
                -   **11**：表示等于
                -   **20**：表示长度小于
                -   **21**：表示长度等于
                -   **22**：表示长度大于
                -   **30**：表示值小于
                -   **31**：表示值等于
                -   **32**：表示值大于
                -   **40**：表示不属于
                -   **41**：表示属于
            -   **values**：匹配内容。根据需要填写相应的内容，以String类型表示。
            -   **contain**：同样表示规则条件的逻辑符，取值与**opCode**参数相同。
            -   **opValue**：逻辑符的简写含义，您可以参考**opCode**参数取值说明了解详细信息。
            -   **pattern**：同样表示逻辑符的简写含义，取值与**opValue**参数相同。
        -   **expressions**：Array类型 \| 必选 \| 规则条件表达式，以更易读的方式表示所有规则条件信息。
        -   **示例**

            ```
            
                    {
                        "name":"test2",
                        "action":"monitor",
                        "conditions":[{"contain":1,"values":"login","pattern":"contain","opCode":1,"opValue":"contain","key":"URL"}],
                        "expressions":["request_uri contains 'login' "],
                        "scene":"custom_acl"
                    }
                    
            ```

    -   设置CC攻击防护规则（**scene**参数值为**custom\_cc**），对应的JSON字符串中包含以下参数：
        -   **name**：String类型 \| 必选 \| 规则名称。
        -   **scene**：String类型 \| 必选 \| 防护类型。设置CC攻击防护规则时，固定为**custom\_cc**。
        -   **conditions**：Array类型 \| 必选 \| 匹配条件，以JSON字符串格式进行描述，具体包含以下参数：
            -   **key**：匹配字段，取值范围：**URL**、**IP**、**Referer**、**User-Agent**、**Params**、**Cookie**、**Content-Type**、**Content-Length**、**X-Forwarded-For**、**Post-Body**、**Http-Method**、**Header**、**URLPath**。
            -   **opCode**：逻辑符，取值：
                -   **0**：表示不包含
                -   **1**：表示包含
                -   **2**：表示不存在
                -   **10**：表示不等于
                -   **11**：表示等于
                -   **20**：表示长度小于
                -   **21**：表示长度等于
                -   **22**：表示长度大于
                -   **30**：表示值小于
                -   **31**：表示值等于
                -   **32**：表示值大于
                -   **40**：表示不属于
                -   **41**：表示属于
            -   **values**：匹配内容。根据需要填写相应的内容，以String类型表示。
            -   **contain**：同样表示规则条件的逻辑符，取值与**opCode**参数相同。
            -   **opValue**：逻辑符的简写含义，您可以参考**opCode**参数取值说明了解详细信息。
            -   **pattern**：同样表示逻辑符的简写含义，取值与**opValue**参数相同。
        -   **expressions**：Array类型 \| 必选 \| 规则条件表达式，以更易读的方式表示所有规则条件信息。
        -   **action**：String类型 \| 必选 \| 处置动作，取值：
            -   **monitor**：表示观察
            -   **captcha**：表示滑块
            -   **captcha\_strict**：表示严格滑块
            -   **js**：表示JS验证
            -   **block**：表示阻断
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
                -   **count**：Integer类型 \| 可选 \| 出现次数阈值，即表示当指定的响应码出现次数超过该阈值时命中防护规则，取值范围：`[1,999999999]`。**count**参数与**ratio**参数两者选其一，不可同时配置。
                -   **ratio**：Integer类型 \| 可选 \| 出现比例阈值（百分比），即表示当指定的响应码出现比例超过该阈值时命中防护规则，取值范围：`[1,100]`。**count**参数与**ratio**参数两者选其一，不可同时配置。
            -   **scope**：String类型 \| 必选 \| 生效范围，取值：
                -   **rule**：表示当前特征匹配范围内。
                -   **domain**：表示当前规则作用的域名范围内。
            -   **ttl**：Integer类型 \| 必选 \| 处置动作的生效时长（单位：秒），取值范围：`[60,86400]`。
            -   **示例**

                ```
                
                        {
                            "name":"CC防护",
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

-   白名单规则配置（**whitelist**）对应的JSON字符串中包含以下参数：
    -   **name**：String类型 \| 必选 \| 规则名称。
    -   **tags**：Array类型 \| 必选 \| 不检测模块，可填写多个模块，取值：
        -   **waf**：表示网站白名单
        -   **cc**：表示系统CC防护
        -   **customrule**：表示自定义规则
        -   **blacklist**：表示IP黑名单
        -   **antiscan**：表示防扫描
        -   **regular**：表示Web应用攻击防护
        -   **deeplearning**：表示深度学习
        -   **antifraud**：表示数据风控
        -   **dlp**：表示防敏感信息泄露
        -   **tamperproof**：表示网站防篡改
        -   **bot\_intelligence**：表示爬虫威胁情报
        -   **bot\_algorithm**：表示智能算法
        -   **bot\_wxbb**：表示App防护
    -   **bypassTags**：String类型 \| 必选 \| 不检测的模块列表。
    -   **conditions**：Array类型 \| 必选 \| 匹配条件，以JSON字符串格式进行描述，具体包含以下参数：
        -   **key**：匹配字段，取值范围：**URL**、**IP**、**Referer**、**User-Agent**、**Params**、**Cookie**、**Content-Type**、**Content-Length**、**X-Forwarded-For**、**Post-Body**、**Http-Method**、**Header**、**URLPath**。
        -   **opCode**：逻辑符，取值：
            -   **0**：表示不包含
            -   **1**：表示包含
            -   **2**：表示不存在
            -   **10**：表示不等于
            -   **11**：表示等于
            -   **20**：表示长度小于
            -   **21**：表示长度等于
            -   **22**：表示长度大于
            -   **30**：表示值小于
            -   **31**：表示值等于
            -   **32**：表示值大于
            -   **40**：表示不属于
            -   **41**：表示属于
        -   **values**：匹配内容。根据需要填写相应的内容，以String类型表示。
        -   **contain**：同样表示规则条件的逻辑符，取值与**opCode**参数相同。
        -   **opValue**：逻辑符的简写含义，您可以参考**opCode**参数取值说明了解详细信息。
        -   **pattern**：同样表示逻辑符的简写含义，取值与**opValue**参数相同。
    -   **expressions**：Array类型 \| 必选 \| 规则条件表达式，以更易读的方式表示所有规则条件信息。
    -   **示例**

        ```
        
            {
                "name": "test",
                "tags": ["cc","customrule"],
                "bypassTags":"antifraud,dlp,tamperproof", 
                "conditions":[{"contain":1,"values":"login","pattern":"contain","opCode":1,"opValue":"contain","key":"URL"}],
                "expressions":["request_uri contains 'login' "]
           }
           
        ```


## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeProtectionModuleRules
&InstanceId=waf_elasticity-cn-0xldbqt****
&Domain=www.example.com
&DefenseType=ac_highfreq
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/waf-openapi)查看更多错误码。

