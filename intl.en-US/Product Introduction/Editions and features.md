# Editions and features

This topic describes the Pro, Business, Enterprise, and Exclusive editions of Web Application Firewall \(WAF\) and related features. If you want to purchase the Exclusive edition, you must submit a ticket. Each edition applies to a different business scale. These editions are billed on a subscription basis and provide specific protection features.

## Editions and supported business scales

The following table lists the business scales supported by each edition. We recommend that you choose the Business or Enterprise edition for medium-sized enterprise websites.

|Business specification|Pro edition|Business edition|Enterprise edition|Exclusive edition|
|----------------------|-----------|----------------|------------------|-----------------|
|Website scale|Small- and medium-sized websites that do not have special security requirements|Medium-sized enterprise websites that provide services to all Internet users and have high data security requirements|Medium- and large-sized enterprise websites that have custom security requirements|Large-sized enterprise websites that require business-specific configurations|
|Peak queries per second \(QPS\)|2,000|5,000|Higher than 10,000|5,000|
|Maximum bandwidth, in Mbit/s \(The origin server is deployed on Alibaba Cloud.\)|50|100|200|100|
|Maximum bandwidth, in Mbit/s \(The origin server is not deployed on Alibaba Cloud.\)|10|30|50|30|
|Default number of second-level domains that can be protected|1|1|1|1,000|
|Default number of subdomains of the second-level domains that can be protected in total \(Wildcard domains are supported.\)|10|10|10|1,000|

For more information about how to activate WAF, see [Activate Alibaba Cloud WAF](/intl.en-US/Pricing/Subscription/Activate Alibaba Cloud WAF.md).

## Editions and supported features

The following table describes the features that are supported by each edition in **mainland China**.

Symbol descriptions:

-   √: indicates that the feature is supported by the edition.
-   ×: indicates that the feature is not supported by the edition.
-   Value-added: indicates a value-added service. If you want to use a value-added service, you must enable it when you purchase or upgrade a WAF instance.

|Feature|Description|Pro edition|Business edition|Enterprise edition|Exclusive edition|Documentation|
|-------|-----------|-----------|----------------|------------------|-----------------|-------------|
|**Website access**|
|HTTPS protection|Allows you to implement HTTPS protection for websites with a few clicks.|√|√|√|√|[Upload HTTPS certificates](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md)|
|Non-standard port protection|Protects traffic over the ports other than standard ports 80, 8080, 443, and 8443.|×|√|√|√|[Supported custom ports](/intl.en-US/Website Access/Supported custom ports.md)|
|Intelligent load balancing|Connects to multiple SLB service nodes to implement automatic disaster recovery and optimal routing with low latency.|Value-added|Value-added|Value-added|Value-added|[Intelligent load balancing](/intl.en-US/Pricing/Subscription/Intelligent load balancing.md)|
|Exclusive WAF IP addresses|Provides exclusive WAF IP addresses to protect specific domains.|Value-added|Value-added|Value-added|Value-added|[Exclusive IP addresses](/intl.en-US/Pricing/Subscription/Exclusive IP addresses.md)|
|Exclusive cluster|Allows you to customize service access and protection capabilities based on business requirements.|×|×|×|√|[Create an exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md)|
|**Website protection**|
|RegEx Protection Engine|Protects against common web attacks, such as SQL injection and cross-site scripting \(XSS\).|√|√|√|√|[Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md)|
|Enables automatic update of protection rules against web zero-day vulnerabilities.|√|√|√|√|[View product information](/intl.en-US/System Management/View product information.md)|
|Allows you to customize protection rule groups.|×|√|√|√|[Customize protection rule groups](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)|
|Big Data Deep Learning Engine|Detects web zero-day vulnerabilities.|×|√|√|√|[Configure the Big Data Deep Learning Engine](/intl.en-US/Website Protection Settings/Web security/Configure the Big Data Deep Learning Engine.md)|
|Positive security model|Provides positive defense capabilities based on deep learning of website traffic.|×|×|√|√|[Configure the positive security model](/intl.en-US/Website Protection Settings/Web security/Configure the positive security model.md)|
|Website tamper-proofing|Locks web pages to prevent tampering with content.|√|√|√|√|[Configure tamper-proofing](/intl.en-US/Website Protection Settings/Web security/Configure tamper-proofing.md)|
|Data leak prevention|Prevents against the leak of sensitive data, such as ID card numbers, mobile numbers, and bank card numbers.|√|√|√|√|[Configure data leakage prevention](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)|
|HTTP flood protection|Protects against common HTTP flood attacks in Prevention or Prevention-emergency mode.|√|√|√|√|[Configure HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)|
|IP address blacklist|Blocks access requests from specific IP addresses or CIDR blocks.|√|√|√|√|[Configure the IP blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure the IP blacklist.md)|
|IP address blacklist \(region-level\)|Blocks access requests from IP addresses in specific regions.|×|√|√|√|
|Scan protection \(basic\)|Blocks the IP addresses where web attacks and path traversal are frequently initiated and the IP addresses of scanning tools, and provides collaborative defense. Default rules are used to block the first type of IP addresses.|√|√|√|√|[Configure scan protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|
|Scan protection \(advanced\)|Supports basic scan protection and allows you to customize blocking rules for high-frequency web attacks and path traversal.|×|√|√|√|
|Custom protection policies \(basic\)|Implements ACL-based access control by using basic fields, such as IP, URL, Referer, User-Agent, and Params.|√|√|√|√|[Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|
|Custom protection policies \(advanced\)|Supports basic custom protection policies and advanced fields, such as Cookie, Content-Type, Header, and Http-Method.|×|√|√|√|
|Custom protection policies \(rate limiting\)|Allows you to customize rules for HTTP flood protection. You can define a throttling policy, where the request frequency can be measured based on IP addresses or sessions.|×|√|√|√|
|Allows you to customize fields that are used to measure requests.|×|×|√|√|
|Data risk control|Protects crucial website services, such as registrations, logons, activities, and forums, against fraud.|Value-added|Value-added|Value-added|Value-added|[Configure data risk control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|
|Bot management|Provides intelligent protection for bot traffic and against automated attacks. This feature is suitable for human-machine identification, scalping, and spam registration scenarios.|Value-added|Value-added|Value-added|Value-added|[Set a threat intelligence rule to allow requests from specific crawlers](/intl.en-US/Website Protection Settings/Bot management/Set a threat intelligence rule to allow requests from specific crawlers.md)[Set a bot threat intelligence rule](t1880502.md#) |
|Application protection|Provides trusted communications and anti-bot protection for native applications to identify proxies, emulators, and requests with invalid signatures.|Value-added|Value-added|Value-added|Value-added|[Configure application protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md)|
|Account security|Detects credential stuffing, brute-force attacks, spam registration, weak passwords, and SMS interface abuse on service endpoints, such as registration and logon endpoints.|√|√|√|√|[Configure account security](/intl.en-US/Protection Lab/Configure account security.md)|
|API security|Allows upload of custom API definition files to ensure that only API requests that comply with the definitions are processed.|×|√|√|√|[API request security](/intl.en-US/Protection Lab/API request security.md)|
|**Security analysis and support**|
|Log Service for WAF|Collects and stores all logs, enables near-real-time query and analysis, and provides online reports.|Value-added|Value-added|Value-added|Value-added|[Overview](/intl.en-US/Log Management/Log service/Overview.md)|

The following table describes the features that are supported by each edition outside **mainland China**.

Symbol descriptions:

-   √: indicates that the feature is supported by the edition.
-   ×: indicates that the feature is not supported by the edition.
-   Value-added: indicates a value-added service. If you want to use a value-added service, you must enable it when you purchase or upgrade a WAF instance.

|Feature|Description|Pro edition|Business edition|Enterprise edition|Exclusive edition|Documentation|
|-------|-----------|-----------|----------------|------------------|-----------------|-------------|
|**Website access**|
|HTTPS protection|Allows you to implement HTTPS protection for websites with a few clicks.|√|√|√|√|[Upload HTTPS certificates](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md)|
|Non-standard port protection|Protects traffic over the ports other than standard ports 80, 8080, 443, and 8443.|×|√|√|√|[Supported custom ports](/intl.en-US/Website Access/Supported custom ports.md)|
|Intelligent load balancing|Connects to multiple SLB service nodes to implement automatic disaster recovery and optimal routing with low latency.|×|Value-added|Value-added|Value-added|[Intelligent load balancing](/intl.en-US/Pricing/Subscription/Intelligent load balancing.md)|
|Exclusive WAF IP addresses|Provides exclusive WAF IP addresses to protect specific domains.|Value-added|Value-added|Value-added|Value-added|[Exclusive IP addresses](/intl.en-US/Pricing/Subscription/Exclusive IP addresses.md)|
|Exclusive cluster|Allows you to customize service access and protection capabilities based on business requirements.|×|×|×|√|[Create an exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md)|
|**Website protection**|
|RegEx Protection Engine|Protects against common web attacks, such as SQL injection and cross-site scripting \(XSS\).|√|√|√|√|[Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md)|
|Enables automatic update of protection rules against web zero-day vulnerabilities.|√|√|√|√|[View product information](/intl.en-US/System Management/View product information.md)|
|Allows you to customize protection rule groups.|×|×|√|√|[Customize protection rule groups](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)|
|Big Data Deep Learning Engine|Detects web zero-day vulnerabilities.|×|×|×|×|[Configure the Big Data Deep Learning Engine](/intl.en-US/Website Protection Settings/Web security/Configure the Big Data Deep Learning Engine.md)|
|Positive security model|Provides positive defense capabilities based on deep learning of website traffic.|×|×|×|×|[Configure the positive security model](/intl.en-US/Website Protection Settings/Web security/Configure the positive security model.md)|
|Website tamper-proofing|Locks web pages to prevent tampering with content.|×|×|√|√|[Configure tamper-proofing](/intl.en-US/Website Protection Settings/Web security/Configure tamper-proofing.md)|
|Data leak prevention|Prevents against the leak of sensitive data, such as ID card numbers, mobile numbers, and bank card numbers.|×|√|√|√|[Configure data leakage prevention](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)|
|HTTP flood protection|Protects against common HTTP flood attacks in Prevention or Prevention-emergency mode.|√|√|√|√|[Configure HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)|
|IP address blacklist|Blocks access requests from specific IP addresses or CIDR blocks.|√|√|√|√|[Configure the IP blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure the IP blacklist.md)|
|IP address blacklist \(region-level\)|Blocks access requests from IP addresses in specific regions.|×|√|√|√|
|Scan protection \(basic\)|Blocks the IP addresses where web attacks and path traversal are frequently initiated and the IP addresses of scanning tools, and provides collaborative defense. Default rules are used to block the first type of IP addresses.|√|√|√|√|[Configure scan protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|
|Scan protection \(advanced\)|Supports basic scan protection and allows you to customize blocking rules for high-frequency web attacks and path traversal.|×|√|√|√|
|Custom protection policies \(basic\)|Implements ACL-based access control by using basic fields, such as IP, URL, Referer, User-Agent, and Params.|√|√|√|√|[Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|
|Custom protection policies \(advanced\)|Supports basic custom protection policies and advanced fields, such as Cookie, Content-Type, Header, and Http-Method.|×|√|√|√|
|Custom protection policies \(rate limiting\)|Allows you to customize rules for HTTP flood protection. You can define a throttling policy, where the request frequency can be measured based on IP addresses or sessions.|×|√|√|√|
|Allows you to customize fields that are used to measure requests.|×|×|√|√|
|Data risk control|Protects crucial website services, such as registrations, logons, activities, and forums, against fraud.|×|×|×|×|[Configure data risk control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|
|Bot management|Provides intelligent protection for bot traffic and against automated attacks. This feature is suitable for human-machine identification, scalping, and spam registration scenarios.|Value-added|Value-added|Value-added|Value-added|[Set a threat intelligence rule to allow requests from specific crawlers](/intl.en-US/Website Protection Settings/Bot management/Set a threat intelligence rule to allow requests from specific crawlers.md)[Set a bot threat intelligence rule](t1880502.md#) |
|Application protection|Provides trusted communications and anti-bot protection for native applications to identify proxies, emulators, and requests with invalid signatures.|Value-added|Value-added|Value-added|Value-added|[Configure application protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md)|
|Account security|Detects credential stuffing, brute-force attacks, spam registration, weak passwords, and SMS interface abuse on service endpoints, such as registration and logon endpoints.|√|√|√|√|[Configure account security](/intl.en-US/Protection Lab/Configure account security.md)|
|API security|Allows upload of custom API definition files to ensure that only API requests that comply with the definitions are processed.|×|×|√|√|[API request security](/intl.en-US/Protection Lab/API request security.md)|
|**Security analysis and support**|
|Log Service for WAF|Collects and stores all logs, enables near-real-time query and analysis, and provides online reports.|Value-added|Value-added|Value-added|Value-added|[Overview](/intl.en-US/Log Management/Log service/Overview.md)|

