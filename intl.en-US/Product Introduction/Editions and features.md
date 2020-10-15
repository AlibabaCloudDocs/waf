# Editions and features

This topic describes the Pro, Business, Enterprise, and Exclusive editions of Web Application Firewall \(WAF\) and related features. If you want to purchase the Exclusive edition, you must submit a ticket. Each edition applies to a different business scale and provides specific protection features. You can purchase WAF instances by using the subscription billing method.

## Editions and supported business scales

The following table lists the business scales supported by each edition. We recommend that you choose the Business or Enterprise edition for medium-sized enterprise websites.

**Note:** If you want to purchase the Exclusive edition, you must submit a[ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80).

|Business specification|Pro edition|Business edition|Enterprise edition|Exclusive edition \(can be purchased only by submitting a ticket\)|
|----------------------|-----------|----------------|------------------|------------------------------------------------------------------|
|Website scale|Small- and medium-sized websites that do not have special security requirements|Medium-sized enterprise websites that provide services to all Internet users and have high data security requirements|Medium- and large-sized enterprise websites that have custom security requirements|Large-sized enterprise websites that require business-specific configurations|
|Peak queries per second \(QPS\)|2,000|5,000|Higher than 10,000|5,000|
|Maximum bandwidth, in Mbit/s \(The origin server is deployed on Alibaba Cloud.\)|50|100|200|100|
|Maximum bandwidth, in Mbit/s \(The origin server is not deployed on Alibaba Cloud.\)|10|30|50|30|
|Default number of second-level domains that can be protected|1|1|1|1,000|
|Default number of subdomains of the second-level domains that can be protected in total \(Wildcard domains are supported.\)|10|10|10|1,000|

For more information about how to activate WAF, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

## Editions and supported features \(in mainland China\)

The following table describes the features that are supported by each edition of WAF **in mainland China**. A WAF instance is billed on a subscription basis.

Symbol descriptions:

-   √: indicates that the feature is supported.
-   ×: indicates that the feature is not supported.
-   Value-added: indicates a value-added service. If you want to use a value-added service, you must enable it when you purchase or upgrade a WAF instance.
-   Supported after configuration: indicates a feature that must be separately enabled on the **Feature Settings** page for a pay-as-you-go WAF instance.

|Feature|Description|Pro edition|Business edition|Enterprise edition|Exclusive edition\(can be purchased only by submitting a ticket\) |
|-------|-----------|-----------|----------------|------------------|-------------------------------------------------------------------|
|**Website access**|
|[HTTPS protection](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md)|Allows you to implement HTTPS protection for websites with a few clicks.|√|√|√|√|
|[Non-standard port protection](/intl.en-US/Website Access/Supported custom ports.md)|Protects traffic over the ports other than standard ports 80, 8080, 443, and 8443.|×|√|√|√|
|[Intelligent load balancing](/intl.en-US/Pricing/Subscription/Intelligent load balancing.md)|Connects to multiple SLB service nodes to implement automatic disaster recovery and optimal routing with low latency.|Value-added|Value-added|Value-added|Value-added|
|[Exclusive IP addresses](/intl.en-US/Pricing/Subscription/Exclusive IP addresses.md)|Provides exclusive IP addresses to protect specific domains.|Value-added|Value-added|Value-added|Value-added|
|[Exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md)|Allows you to customize service access and protection capabilities based on business requirements.|×|×|×|√|
|**Website protection**|
|[RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md)|Protects against common web attacks, such as SQL injection and cross-site scripting \(XSS\).|√|√|√|√|
|Enables automatic update of protection rules against web zero-day vulnerabilities.|√|√|√|√|
|[Protection rule group](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)|Allows you to customize protection rule groups.|×|√|√|√|
|[Big Data Deep Learning Engine](/intl.en-US/Website Protection Settings/Web security/Configure the Big Data Deep Learning Engine.md)|Detects web zero-day vulnerabilities.|×|√|√|√|
|[Positive security model](/intl.en-US/Website Protection Settings/Web security/Configure the positive security model.md)|Provides positive defense capabilities based on deep learning of website traffic.|×|×|√|√|
|[Website tamper-proofing](/intl.en-US/Website Protection Settings/Web security/Configure Website Tamper-proofing.md)|Locks web pages to prevent tampering with content.|√|√|√|√|
|[Data leak prevention](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)|Prevents against the leak of sensitive data, such as ID card numbers, mobile numbers, and bank card numbers.|√|√|√|√|
|[HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)|Protects against common HTTP flood attacks in Prevention or Prevention-emergency mode.|√|√|√|√|
|[IP address blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure an IP address blacklist.md)|Blocks access requests from specific IP addresses or CIDR blocks.|√|√|√|√|
|Supports the above blocking capability and also blocks access requests from IP addresses in specific regions.|×|√|√|√|
|[Scan protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|Blocks the IP addresses where web attacks and path traversal are frequently initiated and the IP addresses of scanning tools, and provides collaborative defense. Default rules are used to block the first type of IP addresses.|√|√|√|√|
|Supports the above protection capability and allows you to customize blocking rules for high-frequency web attacks and path traversal.|×|√|√|√|
|[Custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|Implements ACL-based access control by using basic fields, such as IP, URL, Referer, User-Agent, and Params.|√|√|√|√|
|Supports the above protection capability and advanced fields, such as Cookie, Content-Type, Header, and Http-Method.|×|√|√|√|
|Allows you to customize rules for HTTP flood protection. You can define a throttling policy, where the request frequency can be measured based on IP addresses or sessions.|×|√|√|√|
|Allows you to measure the request frequency based on IP addresses, sessions, or custom fields.|×|×|√|√|
|[Data risk control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|Protects crucial website services, such as registrations, logons, activities, and forums, against fraud.|Value-added|Value-added|Value-added|Value-added|
|[Bot management](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md)|Provides intelligent protection for bot traffic and against automated attacks. This feature is suitable for human-machine identification, scalping, and spam registration scenarios.|Value-added|Value-added|Value-added|Value-added|
|[Application protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md)|Provides trusted communications and anti-bot protection for native applications to identify proxies, emulators, and requests with invalid signatures.|Value-added|Value-added|Value-added|Value-added|
|[Account security](/intl.en-US/Protection Lab/Configure account security.md)|Detects credential stuffing, brute-force attacks, spam registration, weak passwords, and SMS interface abuse on service endpoints, such as registration and logon endpoints.|√|√|√|√|
|[API request security](/intl.en-US/Protection Lab/Enable API request security.md)|Allows upload of custom API definition files to ensure that only API requests that comply with the definitions are processed.|×|√|√|√|
|**Security analysis and support**|
|[Log Service for WAF](/intl.en-US/Log Management/Log service/Overview.md)|Collects and stores all logs, enables near-real-time query and analysis, and provides online reports.|Value-added|Value-added|Value-added|Value-added|

## Editions and supported features \(outside mainland China\)

The following table describes the features that are supported by each edition of WAF **outside mainland China**. A WAF instance is billed on a subscription basis.

|Feature|Description|Pro edition|Business edition|Enterprise edition|Exclusive edition\(can be purchased only by submitting a ticket\) |
|-------|-----------|-----------|----------------|------------------|-------------------------------------------------------------------|
|**Website access**|
|[HTTPS protection](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md)|Allows you to implement HTTPS protection for websites with a few clicks.|√|√|√|√|
|[Non-standard port protection](/intl.en-US/Website Access/Supported custom ports.md)|Protects traffic over the ports other than standard ports 80, 8080, 443, and 8443.|×|√|√|√|
|[Intelligent load balancing](/intl.en-US/Pricing/Subscription/Intelligent load balancing.md)|Connects to multiple SLB service nodes to implement automatic disaster recovery and optimal routing with low latency.|×|Value-added|Value-added|Value-added|
|[Exclusive IP addresses](/intl.en-US/Pricing/Subscription/Exclusive IP addresses.md)|Provides exclusive IP addresses to protect specific domains.|Value-added|Value-added|Value-added|Value-added|
|[Exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md)|Allows you to customize service access and protection capabilities based on business requirements.|×|×|×|√|
|**Website protection**|
|[RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md)|Protects against common web attacks, such as SQL injection and XSS.|√|√|√|√|
|Enables automatic update of protection rules against web zero-day vulnerabilities.|√|√|√|√|
|[Protection rule group](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)|Allows you to customize protection rule groups.|×|×|√|√|
|[Big Data Deep Learning Engine](/intl.en-US/Website Protection Settings/Web security/Configure the Big Data Deep Learning Engine.md)|Detects web zero-day vulnerabilities.|×|×|×|×|
|[Positive security model](/intl.en-US/Website Protection Settings/Web security/Configure the positive security model.md)|Provides positive defense capabilities based on deep learning of website traffic.|×|×|×|×|
|[Website tamper-proofing](/intl.en-US/Website Protection Settings/Web security/Configure Website Tamper-proofing.md)|Locks web pages to prevent tampering with content.|×|×|√|√|
|[Data leak prevention](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)|Prevents against the leak of sensitive data, such as ID card numbers, mobile numbers, and bank card numbers.|×|√|√|√|
|[HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)|Protects against common HTTP flood attacks in Prevention or Prevention-emergency mode.|√|√|√|√|
|[IP address blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure an IP address blacklist.md)|Blocks access requests from specific IP addresses or CIDR blocks.|√|√|√|√|
|Supports the above blocking capability and also blocks access requests from IP addresses in specific regions.|×|×|√|√|
|[Scan protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|Blocks the IP addresses where web attacks and path traversal are frequently initiated and the IP addresses of scanning tools, and provides collaborative defense. Default rules are used to block the first type of IP addresses.|√|√|√|√|
|Supports the above protection capability and allows you to customize blocking rules for high-frequency web attacks and path traversal.|×|√|√|√|
|[Custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|Implements ACL-based access control by using basic fields, such as IP, URL, Referer, User-Agent, and Params.|√|√|√|√|
|Supports the above protection capability and advanced fields, such as Cookie, Content-Type, Header, and Http-Method.|×|√|√|√|
|Allows you to customize rules for HTTP flood protection. You can define a throttling policy, where the request frequency can be measured based on IP addresses or sessions.|×|√|√|√|
|Allows you to measure the request frequency based on IP addresses, sessions, or custom fields.|×|×|√|√|
|[Data risk control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|Protects crucial website services, such as registrations, logons, activities, and forums, against fraud.|×|×|×|×|
|[Bot management](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md)|Provides intelligent protection for bot traffic and against automated attacks. This feature is suitable for human-machine identification, scalping, and spam registration scenarios.|Value-added|Value-added|Value-added|Value-added|
|[Application protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md)|Provides trusted communications and anti-bot protection for native applications to identify proxies, emulators, and requests with invalid signatures.|Value-added|Value-added|Value-added|Value-added|
|[Account security](/intl.en-US/Protection Lab/Configure account security.md)|Detects credential stuffing, brute-force attacks, spam registration, weak passwords, and SMS interface abuse on service endpoints, such as registration and logon endpoints.|√|√|√|√|
|[API request security](/intl.en-US/Protection Lab/Enable API request security.md)|Allows upload of custom API definition files to ensure that only API requests that comply with the definitions are processed.|×|×|√|√|
|**Security analysis and support**|
|[Log Service for WAF](/intl.en-US/Log Management/Log service/Overview.md)|Collects and stores all logs, enables near-real-time query and analysis, and provides online reports.|×|Value-added|Value-added|Value-added|

