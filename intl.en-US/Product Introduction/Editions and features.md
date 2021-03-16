# Editions and features

This topic describes the Pro, Business, Enterprise, and Exclusive editions of Web Application Firewall \(WAF\) and related features. If you want to purchase the Exclusive edition, you must submit a ticket. Each edition applies to a different business scale and provides specific protection features. You can purchase WAF instances based on the subscription billing method. This topic describes the business scales and protection features that WAF supports.

## Editions and supported business scales

The following table lists the business scales supported by each edition. We recommend that you choose the Business or Enterprise edition for medium-sized enterprise websites.

**Note:** If you want to purchase the Exclusive edition, you must submit a [工单](https://selfservice.console.aliyun.com/ticket/category/waf/today)[ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80)ticket.

|Business specification|Pro edition|Business edition|Enterprise edition|Public cloud exclusive edition \(submit tickets to purchase\)|Hybrid cloud exclusive edition \(submit tickets to purchase\)|
|----------------------|-----------|----------------|------------------|-------------------------------------------------------------|-------------------------------------------------------------|
|Website scale|Small- and medium-sized websites that do not have special security requirements|Medium-sized enterprise-grade websites that provide services to all Internet users and have high data security requirements|Medium- and large-sized enterprise-grade websites that have custom security requirements|Large-sized enterprise-grade websites that require business-specific configurations|Large-sized enterprise-grade websites that require protection for applications deployed on Alibaba Cloud, on public clouds of other cloud service providers, or in on-site data centers|
|Peak queries per second \(QPS\)|2,000 QPS|5,000 QPS|Higher than 10,000|5,000 QPS|10,000 QPS|
|Maximum bandwidth, in Mbit/s \(The origin server is deployed on Alibaba Cloud.\)|50 Mbit/s|100 Mbit/s|200 Mbit/s|100 Mbit/s|10 Mbit/s|
|Maximum bandwidth, in Mbit/s \(The origin server is not deployed on Alibaba Cloud.\)|10 Mbit/s|30 Mbit/s|50 Mbit/s|30 Mbit/s|10 Mbit/s|
|Default number of second-level domains that WAF can protect|1|1|1|200|100|
|Default number of domains that can be protected in total \(Wildcard domains are supported.\)|10|10|10|200|100|

|Business specification|Pro edition|Business edition|Enterprise edition|Exclusive edition \(submit tickets to purchase\)|Pay-as-you-go|
|----------------------|-----------|----------------|------------------|------------------------------------------------|-------------|
|Website scale|Small- and medium-sized websites that do not have special security requirements|Medium-sized enterprise-grade websites that provide services to all Internet users and have high data security requirements|Medium- and large-sized enterprise-grade websites that have custom security requirements|Large-sized enterprise-grade websites that require business-specific configurations| |
|Peak queries per second \(QPS\)|2,000 QPS|5,000 QPS|Higher than 10,000|5,000 QPS|100 by default \(You can purchase a WAF protection resource plan to extend the QPS specification to 20,000 at most.\)|
|Maximum bandwidth, in Mbit/s \(The origin server is deployed on Alibaba Cloud.\)|50 Mbit/s|100 Mbit/s|200 Mbit/s|100 Mbit/s|30 Mbit/s|
|Maximum bandwidth, in Mbit/s \(The origin server is not deployed on Alibaba Cloud.\)|10 Mbit/s|30 Mbit/s|50 Mbit/s|30 Mbit/s| |
|Default number of second-level domains that WAF can protect|1|1|1|1,000|1 by default|
|Default number of domains that can be protected in total \(Wildcard domains are supported.\)|10|10|10|1,000|10 by default|

For more information about how to activate WAF, see [Purchase a WAF instance](/intl.en-US/Billing and Service Activation/Subscription/Purchase a WAF instance.md).

## 套餐功能列表（中国内地）

下表描述了Web应用防火墙中国内地实例（购买包年包月实例时选择**中国内地**地域）及按量计费实例的主要功能模块在不同套餐中的支持情况。更详细的套餐功能说明，请参见[Web应用防火墙产品定价页面](https://www.aliyun.com/price/product#/waf/detail)。

标识说明：

-   √：表示在当前套餐中支持。
-   ×：表示在当前套餐中不支持。
-   ○：表示需要额外付费开启的增值服务。您可以在购买WAF实例时开启增值服务，或者在购买WAF实例后使用升级功能开启增值服务。
-   △：表示需要在开通按量计费WAF后，通过**功能与规格设置**单独开启的特性。

|功能模块|描述|高级版|企业版|旗舰版|独享版 （仅支持工单开通）

|按量计费|
|----|--|---|---|---|---------------|----|
|**业务接入**|
|[HTTPS安全防护](/intl.en-US/Website Access/Website access with CNAME/Add websites.md)|全站一键实现HTTPS防护。|√|√|√|√|△|
|[非标准端口防护](/intl.en-US/Website Access/View the ports supported by WAF.md)|支持防护80、8080、443、8443以外的特定非标准端口上的业务。|×|√|√|√|△|
|[IPv6防护]()|支持IPv6访问流量的安全检测与防护。|×|√|√|√|△|
|[智能负载均衡](/intl.en-US/Billing and Service Activation/Subscription/Intelligent load balancing.md)|通过多节点智能接入技术，实现源站服务器多节点、多线路自动调度容灾。|○|○|○|○|△|
|[域名独享资源包](/intl.en-US/Billing and Service Activation/Subscription/Exclusive IP addresses.md)|支持为域名开启独享IP防护。|○|○|○|○|△|
|[独享集群](/intl.en-US/System Management/Create an exclusive cluster.md)|基于业务特性的定制化接入和防护能力。|×|×|×|√|×|
|[资产识别](/intl.en-US/.md)|主动发现和管理站点资产，支持一键接入防护。|√|√|√|√|√|
|[透明接入]()|直接牵引源站服务器（SLB实例、ECS实例）的业务流量到Web应用防火墙进行防护。|√|√|√|√|√|
|**网站防护**|
|[规则防护引擎](/intl.en-US/Website Protection Settings/Web security/Configure the protection rules engine.md)|防御常见的Web攻击，例如SQL注入、XSS等。|√|√|√|√|√|
|自动更新Web 0day漏洞攻击防护规则。|√|√|√|√|√|
|[自定义防护规则组](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)|支持自定义防护规则组。|×|√|√|√|△|
|[大数据深度学习引擎](/intl.en-US/Website Protection Settings/Web security/Configure the Big Data Deep Learning Engine.md)|依托于大数据深度学习引擎的0day漏洞风险检测。|×|√|√|√|△|
|[主动防御](/intl.en-US/Website Protection Settings/Web security/Configure the positive security model.md)|基于网站访问流量的深度学习，提供主动防御能力。|×|×|√|√|△|
|[网站防篡改](/intl.en-US/Website Protection Settings/Web security/Configure website tamper-proofing.md)|锁定网站页面，防止内容被恶意篡改。|√|√|√|√|△|
|[防敏感信息泄露](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)|防敏感隐私数据泄露，包括电话号码、身份证、银行卡等重要隐私数据。|√|√|√|√|△|
|[CC安全防护](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)|防御常见的CC攻击，支持内置的防护和防护-紧急模式。|√|√|√|√|√|
|[IP黑名单](/intl.en-US/Website Protection Settings/Access control and throttling/Configure a blacklist.md)|一键封禁特定的IP地址和地址段的访问能力。|√|√|√|√|△|
|包含上述特性，且支持一键封禁指定地理区域IP的访问能力。|×|√|√|√|△|
|[扫描防护](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|支持高频Web攻击封禁（默认规则）、目录遍历封禁（默认规则）、扫描工具封禁、协同防御。|√|√|√|√|△|
|包含上述特性，且支持自定义高频Web攻击封禁、目录遍历封禁规则。|×|√|√|√|△|
|[自定义防护策略](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|基础精准条件访问控制：基于基础字段（包含IP、URL、Referer、User-Agent、Params）的ACL访问控制。|√|√|√|√|√|
|高级精准条件访问控制：包含基础字段，且支持高级字段（例如Cookie、Content-Type、Header、Http-Method等）。|×|√|√|√|△|
|支持访问频率限制（即自定义CC攻击防护规则，在精准匹配条件的基础上，自定义访问频率限制条件，精准过滤异常请求），设置基于IP和Session进行请求次数统计的频率控制策略。|×|√|√|√|△|
|支持访问频率限制，设置基于自定义字段（包含IP和Session）进行请求次数统计的频率控制策略。|×|×|√|√|√|
|[数据风控](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|防御网站关键业务（例如注册、登录、活动、论坛）中可能发生的机器爬虫欺诈行为。|○|○|○|○|△|
|[合法爬虫](/intl.en-US/Website Protection Settings/Bot management/Configure the allowed crawlers function.md)|提供合法搜索引擎白名单（例如Google、Bing、百度、搜狗、360、Yandex等），为域名放行合法爬虫的访问请求。|○|○|○|○|△|
|[爬虫威胁情报](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md)|提供拨号池IP、IDC机房IP、恶意扫描工具IP以及云端实时模型生成的恶意爬虫库等多种维度的爬虫威胁情报规则，方便您在全域名或指定路径下设置阻断恶意爬虫的访问请求。|○|○|○|○|△|
|[App防护](/intl.en-US/Website Protection Settings/Bot management/Application protection/Configure application protection.md)|专门针对原生APP端，提供可信通信，防机器脚本滥刷等安全防护，可以有效识别代理、模拟器、非法签名的请求。|○|○|○|○|△|
|[账户安全](/intl.en-US/Protection Lab/Configure account security.md)|支持识别与账户关联的业务接口（例如注册、登录等）上的撞库、暴力破解、垃圾注册、弱口令嗅探和短信验证码接口滥刷事件。|√|√|√|√|△|
|[API规范校验]()|支持上传自定义的API规则文件，确保只有符合规则的API请求才会被执行。|×|√|√|√|△|
|**安全分析和支持**|
|[日志服务](/intl.en-US/Log Management/Log service/Overview.md)|支持采集WAF所有的日志信息并存储至日志服务中，提供准实时查询分析和在线报表展示等功能。|○|○|○|○|△|
|[可视化大屏服务](/intl.en-US/.md)|提供网站整体业务及安全状况的可视化大屏分析。|○|○|○|○|△|
|[产品专家服务]()|由阿里云安全专家提供钉钉群咨询服务，负责产品配置、策略优化、日常监控等技术支持。|○|○|○|○|×|

## Editions and supported features \(in mainland China\)

The following table describes the features that each edition of WAF supports in **mainland China**. A WAF instance is billed on a subscription basis.

Symbol descriptions:

-   √: indicates that the feature is supported.
-   ×: indicates that the feature is not supported.
-   ○: indicates that the feature is a value-added service. If you want to enable it, you must pay additional fees. You can enable the feature when you purchase or upgrade a WAF instance.
-   △: indicates that the feature must be separately enabled on the **Feature Settings** page for a pay-as-you-go WAF instance.

|Feature|Description|Pro edition|Business edition|Enterprise edition|Exclusive edition \(submit tickets to purchase\) |
|-------|-----------|-----------|----------------|------------------|--------------------------------------------------|
|**Website access**|
|[HTTPS protection](/intl.en-US/Website Access/Website access with CNAME/Add websites.md)|Allows you to implement HTTPS protection for websites with a few clicks.|√|√|√|√|
|[Non-standard port protection](/intl.en-US/Website Access/View the ports supported by WAF.md)|Protects traffic over the ports other than standard ports 80, 8080, 443, and 8443.|×|√|√|√|
|[IPv6防护]()|支持IPv6访问流量的安全检测与防护。|×|√|√|√|
|[Intelligent load balancing](/intl.en-US/Billing and Service Activation/Subscription/Intelligent load balancing.md)|Connects to multiple SLB service nodes to implement automatic disaster recovery and optimal routing with low latency.|○|○|○|○|
|[Exclusive IP address](/intl.en-US/Billing and Service Activation/Subscription/Exclusive IP addresses.md)|Provides exclusive IP addresses to protect specific domain names.|○|○|○|○|
|[Exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md)|Allows you to customize service access and protection capabilities based on business requirements.|×|×|×|√|
|[资产识别](/intl.en-US/.md)|主动发现和管理站点资产，支持一键接入防护。|√|√|√|√|
|[透明接入]()|直接牵引源站服务器（SLB实例、ECS实例）的业务流量到Web应用防火墙进行防护。|√|√|√|√|
|**Website protection**|
|[Protection rules engine](/intl.en-US/Website Protection Settings/Web security/Configure the protection rules engine.md)|Protects against common web attacks, such as SQL injection and XSS attacks.|√|√|√|√|
|Enables automatic update of protection rules against web zero-day vulnerabilities.|√|√|√|√|
|[Custom protection rule group](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)|Allows you to customize protection rule groups.|×|√|√|√|
|[Big Data Deep Learning Engine](/intl.en-US/Website Protection Settings/Web security/Configure the Big Data Deep Learning Engine.md)|Detects web zero-day vulnerabilities.|×|√|√|√|
|[Positive security model](/intl.en-US/Website Protection Settings/Web security/Configure the positive security model.md)|Provides positive defense capabilities based on deep learning of website traffic.|×|×|√|√|
|[Website tamper-proofing](/intl.en-US/Website Protection Settings/Web security/Configure website tamper-proofing.md)|Locks web pages to prevent tampering with content.|√|√|√|√|
|[Data leak prevention](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)|Prevents against the leak of sensitive data, such as ID card numbers, mobile numbers, and bank card numbers.|√|√|√|√|
|[HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)|Protects against common HTTP flood attacks in Prevention or Prevention-emergency mode.|√|√|√|√|
|[IP address blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure a blacklist.md)|Blocks access requests from specific IP addresses or CIDR blocks.|√|√|√|√|
|Blocks access requests from specific IP addresses, specific CIDR blocks, or IP addresses in specific regions.|×|√|√|√|
|[Scan protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|Blocks the IP addresses where web attacks and path traversal are frequently initiated and the IP addresses of scanning tools, and provides collaborative defense. Default rules are used to block the first type of IP addresses.|√|√|√|√|
|Supports the above protection capabilities and allows you to customize blocking rules for high-frequency web attacks and path traversal.|×|√|√|√|
|[Custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|Supports ACL-based access control by using basic fields, such as IP, URL, Referer, User-Agent, and Params.|√|√|√|√|
|Supports ACL-based access control by using basic fields and advanced fields. The advanced fields include Cookie, Content-Type, Header, and Http-Method.|×|√|√|√|
|Allows you to configure rate limiting policies based on IP addresses and sessions. You can customize HTTP flood protection rules in which you can add match conditions and configure rate limiting policies.|×|√|√|√|
|Allows you to configure rate limiting policies based on IP addresses, sessions, and custom fields.|×|×|√|√|
|[Data risk control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|Protects crucial website services, such as registrations, logons, activities, and forums, against fraud.|○|○|○|○|
|[Allowed crawlers](/intl.en-US/Website Protection Settings/Bot management/Configure the allowed crawlers function.md)|Maintains a whitelist that consists of authorized search engines, such as Google, Bing, Baidu, Sogou, 360, and Yandex. The crawlers of these search engines are allowed to access specified domain names.|○|○|○|○|
|[Bot threat intelligence](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md)|Provides information about suspicious IP addresses that are used by dialers, data centers, and malicious scanners. This feature also maintains an IP address library of malicious crawlers and prevents crawlers from accessing all pages under your domain name or specific directories.|○|○|○|○|
|[Application protection](/intl.en-US/Website Protection Settings/Bot management/Application protection/Configure application protection.md)|Provides secure connectivity and anti-bot protection for native apps. This feature can identify requests from proxy servers and emulators and requests with invalid signatures.|○|○|○|○|
|[Account security](/intl.en-US/Protection Lab/Configure account security.md)|Detects credential stuffing, brute-force attacks, spam user registration, weak passwords, and SMS flood attacks on service endpoints, such as registration and logon endpoints.|√|√|√|√|
|[API specification verification]()|Allows upload of custom API definition files to ensure that only API requests that comply with the definitions are processed.|×|√|√|√|
|**Security analysis and support**|
|[Log Service for WAF](/intl.en-US/Log Management/Log service/Overview.md)|Collects and stores all logs, enables near-real-time query and analysis, and provides online reports.|x|○|○|○|

## 套餐功能列表（海外地区）

下表描述了Web应用防火墙海外地区实例（购买包年包月实例时选择**海外地区**地域）的主要功能模块在不同套餐中的支持情况。更详细的套餐功能说明，请参见[Web应用防火墙产品定价页面](https://www.aliyun.com/price/product#/waf/detail)。

标识说明：

-   √：表示在当前套餐中支持。
-   ×：表示在当前套餐中不支持。
-   ○：表示需要额外付费开启的增值服务。您可以在购买WAF实例时开启增值服务，或者在购买WAF实例后使用升级功能开启增值服务。
-   △：表示需要在开通按量计费WAF后，通过**功能与规格设置**单独开启的特性。

**Note:** 海外地区WAF实例不支持按量计费。

|功能模块|描述|高级版|企业版|旗舰版|独享版 （仅支持工单开通） |
|----|--|---|---|---|---------------|
|**业务接入**|
|[HTTPS安全防护](/intl.en-US/Website Access/Website access with CNAME/Add websites.md)|全站一键实现HTTPS防护。|√|√|√|√|
|[非标准端口防护](/intl.en-US/Website Access/View the ports supported by WAF.md)|支持防护80、8080、443、8443以外的特定非标准端口上的业务。|×|√|√|√|
|[IPv6防护]()|支持IPv6访问流量的安全检测与防护。|×|×|×|×|
|[智能负载均衡](/intl.en-US/Billing and Service Activation/Subscription/Intelligent load balancing.md)|通过多节点智能接入技术，实现源站服务器多节点、多线路自动调度容灾。|×|○|○|○|
|[域名独享资源包](/intl.en-US/Billing and Service Activation/Subscription/Exclusive IP addresses.md)|支持为域名开启独享IP防护。|○|○|○|○|
|[独享集群](/intl.en-US/System Management/Create an exclusive cluster.md)|基于业务特性的定制化接入和防护能力。|×|×|×|√|
|[资产识别](/intl.en-US/.md)|主动发现和管理站点资产，支持一键接入防护。|×|×|×|×|
|[透明接入]()|直接牵引源站服务器（SLB实例、ECS实例）的业务流量到Web应用防火墙进行防护。|×|×|×|×|
|**网站防护**|
|[规则防护引擎](/intl.en-US/Website Protection Settings/Web security/Configure the protection rules engine.md)|防御常见的Web攻击，例如SQL注入、XSS等。|√|√|√|√|
|自动更新Web 0day漏洞攻击防护规则。|√|√|√|√|
|[自定义防护规则组](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)|支持自定义防护规则组。|×|×|√|√|
|[大数据深度学习引擎](/intl.en-US/Website Protection Settings/Web security/Configure the Big Data Deep Learning Engine.md)|依托于大数据深度学习引擎的0day漏洞风险检测。|×|×|×|×|
|[主动防御](/intl.en-US/Website Protection Settings/Web security/Configure the positive security model.md)|基于网站访问流量的深度学习，提供主动防御能力。|×|×|×|×|
|[网站防篡改](/intl.en-US/Website Protection Settings/Web security/Configure website tamper-proofing.md)|锁定网站页面，防止内容被恶意篡改。|×|×|√|√|
|[防敏感信息泄露](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)|防敏感隐私数据泄露，包括电话号码、身份证、银行卡等重要隐私数据。|×|√|√|√|
|[CC安全防护](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)|防御常见的CC攻击，支持内置的防护和防护-紧急模式。|√|√|√|√|
|[IP黑名单](/intl.en-US/Website Protection Settings/Access control and throttling/Configure a blacklist.md)|一键封禁特定的IP地址和地址段的访问能力。|√|√|√|√|
|包含上述特性，且支持一键封禁指定地理区域IP的访问能力。|×|√|√|√|
|[扫描防护](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|支持高频Web攻击封禁（默认规则）、目录遍历封禁（默认规则）、扫描工具封禁、协同防御。|√|√|√|√|
|包含上述特性，且支持自定义高频Web攻击封禁、目录遍历封禁规则。|×|√|√|√|
|[自定义防护策略](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|基础精准条件访问控制：基于基础字段（包含IP、URL、Referer、User-Agent、Params）的ACL访问控制。|√|√|√|√|
|高级精准条件访问控制：包含基础字段，且支持高级字段（例如Cookie、Content-Type、Header、Http-Method等）。|×|√|√|√|
|支持访问频率限制（即自定义CC攻击防护规则，在精准匹配条件的基础上，自定义访问频率限制条件，精准过滤异常请求），设置基于IP和Session进行请求次数统计的频率控制策略。|×|√|√|√|
|支持访问频率限制，设置基于自定义字段（包含IP和Session）进行请求次数统计的频率控制策略。|×|×|√|√|
|[数据风控](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|防御网站关键业务（例如注册、登录、活动、论坛）中可能发生的机器爬虫欺诈行为。|×|×|×|×|
|[合法爬虫](/intl.en-US/Website Protection Settings/Bot management/Configure the allowed crawlers function.md)|提供合法搜索引擎白名单（例如Google、Bing、百度、搜狗、360、Yandex等），为域名放行合法爬虫的访问请求。|○|○|○|○|
|[爬虫威胁情报](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md)|提供拨号池IP、IDC机房IP、恶意扫描工具IP以及云端实时模型生成的恶意爬虫库等多种维度的爬虫威胁情报规则，方便您在全域名或指定路径下设置阻断恶意爬虫的访问请求。|○|○|○|○|
|[App防护](/intl.en-US/Website Protection Settings/Bot management/Application protection/Configure application protection.md)|专门针对原生APP端，提供可信通信，防机器脚本滥刷等安全防护，可以有效识别代理、模拟器、非法签名的请求。|○|○|○|○|
|[账户安全](/intl.en-US/Protection Lab/Configure account security.md)|支持识别与账户关联的业务接口（例如注册、登录等）上的撞库、暴力破解、垃圾注册、弱口令嗅探和短信验证码接口滥刷事件。|√|√|√|√|
|[API规范校验]()|支持上传自定义的API规则文件，确保只有符合规则的API请求才会被执行。|×|×|√|√|
|**安全分析和支持**|
|[日志服务](/intl.en-US/Log Management/Log service/Overview.md)|支持采集WAF所有的日志信息并存储至日志服务中，提供准实时查询分析和在线报表展示等功能。|○|○|○|○|
|[可视化大屏服务](/intl.en-US/.md)|提供网站整体业务及安全状况的可视化大屏分析。|×|○|○|○|
|[产品专家服务]()|由阿里云安全专家提供钉钉群咨询服务，负责产品配置、策略优化、日常监控等技术支持。|○|○|○|○|

## Editions and supported features \(outside mainland China\)

The following table describes the features that each edition of WAF supports **outside mainland China**. A WAF instance is billed on a subscription basis.

标识说明：

-   √：表示在当前套餐中支持。
-   ×：表示在当前套餐中不支持。
-   ○：表示需要额外付费开启的增值服务。您可以在购买WAF实例时开启增值服务，或者在购买WAF实例后使用升级功能开启增值服务。
-   △：表示需要在开通按量计费WAF后，通过**功能与规格设置**单独开启的特性。

|Feature|Description|Pro edition|Business edition|Enterprise edition|Exclusive edition \(submit tickets to purchase\) |
|-------|-----------|-----------|----------------|------------------|--------------------------------------------------|
|**Website access**|
|[HTTPS protection](/intl.en-US/Website Access/Website access with CNAME/Add websites.md)|Allows you to implement HTTPS protection for websites with a few clicks.|√|√|√|√|
|[Non-standard port protection](/intl.en-US/Website Access/View the ports supported by WAF.md)|Protects traffic over the ports other than standard ports 80, 8080, 443, and 8443.|×|√|√|√|
|[IPv6防护]()|支持IPv6访问流量的安全检测与防护。|×|×|×|×|
|[Intelligent load balancing](/intl.en-US/Billing and Service Activation/Subscription/Intelligent load balancing.md)|Connects to multiple SLB service nodes to implement automatic disaster recovery and optimal routing with low latency.|×|○|○|○|
|[Exclusive IP address](/intl.en-US/Billing and Service Activation/Subscription/Exclusive IP addresses.md)|Provides exclusive IP addresses to protect specific domain names.|○|○|○|○|
|[Exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md)|Allows you to customize service access and protection capabilities based on business requirements.|×|×|×|√|
|[资产识别](/intl.en-US/.md)|主动发现和管理站点资产，支持一键接入防护。|×|×|×|×|
|[透明接入]()|直接牵引源站服务器（SLB实例、ECS实例）的业务流量到Web应用防火墙进行防护。|×|×|×|×|
|**Website protection**|
|[Protection rules engine](/intl.en-US/Website Protection Settings/Web security/Configure the protection rules engine.md)|Protects against common web attacks, such as SQL injection and XSS attacks.|√|√|√|√|
|Enables automatic update of protection rules against web zero-day vulnerabilities.|√|√|√|√|
|[Custom protection rule group](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)|Allows you to customize protection rule groups.|×|×|√|√|
|[Big Data Deep Learning Engine](/intl.en-US/Website Protection Settings/Web security/Configure the Big Data Deep Learning Engine.md)|Detects web zero-day vulnerabilities.|×|×|×|×|
|[Positive security model](/intl.en-US/Website Protection Settings/Web security/Configure the positive security model.md)|Provides positive defense capabilities based on deep learning of website traffic.|×|×|×|×|
|[Website tamper-proofing](/intl.en-US/Website Protection Settings/Web security/Configure website tamper-proofing.md)|Locks web pages to prevent tampering with content.|×|×|√|√|
|[Data leak prevention](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)|Prevents against the leak of sensitive data, such as ID card numbers, mobile numbers, and bank card numbers.|×|√|√|√|
|[HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)|Protects against common HTTP flood attacks in Prevention or Prevention-emergency mode.|√|√|√|√|
|[IP address blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure a blacklist.md)|Blocks access requests from specific IP addresses or CIDR blocks.|√|√|√|√|
|Blocks access requests from specific IP addresses, specific CIDR blocks, or IP addresses in specific regions.|×|×|√|√|
|[Scan protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|Blocks the IP addresses where web attacks and path traversal are frequently initiated and the IP addresses of scanning tools, and provides collaborative defense. Default rules are used to block the first type of IP addresses.|√|√|√|√|
|Supports the above protection capabilities and allows you to customize blocking rules for high-frequency web attacks and path traversal.|×|√|√|√|
|[Custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|Supports ACL-based access control by using basic fields, such as IP, URL, Referer, User-Agent, and Params.|√|√|√|√|
|Supports ACL-based access control by using basic fields and advanced fields. The advanced fields include Cookie, Content-Type, Header, and Http-Method.|×|√|√|√|
|Allows you to configure rate limiting policies based on IP addresses and sessions. You can customize HTTP flood protection rules in which you can add match conditions and configure rate limiting policies.|×|√|√|√|
|Allows you to configure rate limiting policies based on IP addresses, sessions, and custom fields.|×|×|√|√|
|[Data risk control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|Protects crucial website services, such as registrations, logons, activities, and forums, against fraud.|×|×|×|×|
|[Allowed crawlers](/intl.en-US/Website Protection Settings/Bot management/Configure the allowed crawlers function.md)|Maintains a whitelist that consists of authorized search engines, such as Google, Bing, Baidu, Sogou, 360, and Yandex. The crawlers of these search engines are allowed to access specified domain names.|○|○|○|○|
|[Bot threat intelligence](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md)|Provides information about suspicious IP addresses that are used by dialers, data centers, and malicious scanners. This feature also maintains an IP address library of malicious crawlers and prevents crawlers from accessing all pages under your domain name or specific directories.|○|○|○|○|
|[Application protection](/intl.en-US/Website Protection Settings/Bot management/Application protection/Configure application protection.md)|Provides secure connectivity and anti-bot protection for native apps. This feature can identify requests from proxy servers and emulators and requests with invalid signatures.|○|○|○|○|
|[Account security](/intl.en-US/Protection Lab/Configure account security.md)|Detects credential stuffing, brute-force attacks, spam user registration, weak passwords, and SMS flood attacks on service endpoints, such as registration and logon endpoints.|√|√|√|√|
|[API specification verification]()|Allows upload of custom API definition files to ensure that only API requests that comply with the definitions are processed.|×|×|√|√|
|**Security analysis and support**|
|[Log Service for WAF](/intl.en-US/Log Management/Log service/Overview.md)|Collects and stores all logs, enables near-real-time query and analysis, and provides online reports.|×|○|○|○|

