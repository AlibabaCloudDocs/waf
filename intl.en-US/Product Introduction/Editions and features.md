# Editions and features

This topic describes the Pro, Business, Enterprise, and Exclusive editions of Web Application Firewall \(WAF\) and associated features. Each edition is billed on a subscription basis. If you purchase a subscription WAF instance, you can select the Pro, Business, Enterprise, or Exclusive edition. Each WAF edition applies to a different business scale and provides specific protection features. The features that are provided by each edition may vary based on the region where the WAF instance is deployed.

## Supported business scales

The following table lists the business scales supported by each edition. We recommend that you select the Business or Enterprise edition for medium-sized enterprise websites.

|Business specification item|Pro edition|Business edition|Enterprise edition|Exclusive edition|
|---------------------------|-----------|----------------|------------------|-----------------|
|Website scale|Small- and medium-sized websites that do not have special security requirements|Medium-sized enterprise websites that can be accessed over the Internet and have high data security requirements|Medium- and large-sized enterprise websites that have custom security requirements|Large-sized enterprise websites that have custom configuration requirements for business|
|Peak QPS|2,000|5,000|Higher than 10,000|5,000|
|Maximum bandwidth, in Mbit/s \(The origin server is deployed on Alibaba Cloud.\)|50|100|200|100|
|Maximum bandwidth, in Mbit/s \(The origin server is not deployed on Alibaba Cloud.\)|10|30|50|30|
|Default number of first-level domains that can be protected|1|1|1|1,000|
|Default number of domains that can be protected in total \(Wildcard domains are supported.\)|10|10|10|1,000|

## Supported features

The following table lists the features that are supported by each edition. The following symbols are used in the table:

-   √ indicates that the feature is supported by the edition.
-   ○ indicates that the feature is supported only by WAF instances that are deployed in regions in mainland China.
-   × indicates that the feature is not supported by the edition.

|Feature|Documentation|Pro edition|Business edition|Enterprise edition|Exclusive edition|
|-------|-------------|-----------|----------------|------------------|-----------------|
|HTTPS protection with a few clicks for websites|[Enable HTTPS advanced settings]()|√|√|√|√|
|Protection for ports other than standard ports 80, 8080, 443, and 8443|[Supported custom ports](/intl.en-US/Website Access/Supported custom ports.md)|×|√|√|√|
|Protection against common web attacks, such as SQL injection and XSS|[Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web intrusion prevention/Configure the RegEx Protection Engine.md)|√|√|√|√|
|Automatic update of protection rules against web zero-day vulnerabilities|√|√|√|√|
|Intelligent load balancing|[Intelligent load balancing](/intl.en-US/Pricing/Subscription/Intelligent load balancing.md)|○|√|√|√|
|Configuration of custom rule groups|[Customize protection rule groups](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)|×|×|√|√|
|Detection of web zero-day vulnerabilities by using the Big Data Deep Learning Engine|[Configure the Big Data Deep Learning Engine](/intl.en-US/Website Protection Settings/Web intrusion prevention/Configure the Big Data Deep Learning Engine.md)|○|○|○|○|
|Positive security models based on deep learning of website traffic|[Configure the positive security model](/intl.en-US/Website Protection Settings/Web intrusion prevention/Configure the positive security model.md)|×|×|○|○|
|Protection against HTTP flood attacks that target web services|[Configure HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)|√|√|√|√|
|Protection against HTTP flood attacks that target API services|[Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|×|√|√|√|
|Custom access frequency control on URLs|[Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|×|√|√|√|
|IP address whitelist, IP address blacklist, URL whitelist, and URL blacklist for access control|[Configure the IP blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure the IP blacklist.md)|√|√|√|√|
|Advanced settings of access control on HTTP requests based on header fields including User-Agent and Referer|[Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|√|√|√|√|
|Targeted protection against web attacks, such as penetration tests|[Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|√|√|√|√|
|Location-based IP address blocking \(Block access requests from regions outside mainland China with a few clicks.\)|[Configure the IP blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure the IP blacklist.md)|×|×|√|√|
|Web page tamper-proofing|[Configure tamper-proofing](/intl.en-US/Website Protection Settings/Web intrusion prevention/Configure tamper-proofing.md)|×|○|○|○|
|Blocking of spam registration requests **Note:** Data risk control is a value-added service in the bot management module. If you want to use data risk control, you must enable it first.

|[Configure data risk control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|×|○|√|√|
|Scan protection|[Configure scan protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|√|√|√|√|
|Intelligent protection against automated attacks and intelligent protection of bot traffic **Note:** The bot management module is a value-added service. If you want to use this service, you must enable it when you purchase a WAF instance.

|[Set a bot threat intelligence rule](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md)|√|√|√|√|
|Trusted communications to protect native applications and defense against bot script abuse **Note:** The application protection module is a value-added service. If you want to use this service, you must enable it when you purchase a WAF instance.

|[Configure application protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md)|√|√|√|√|
|Prevention against the leak of sensitive data, such as ID card numbers, mobile numbers, and bank card numbers|[Configure data leakage prevention](/intl.en-US/Website Protection Settings/Web intrusion prevention/Configure data leakage prevention.md)|×|√|√|√|
|Account security|[Configure account security](/intl.en-US/Protection Lab/Configure account security.md)|×|√|√|√|
|API security|[API request security](/intl.en-US/Protection Lab/API request security.md)|×|√|√|√|
|Log Service for WAF **Note:** The Log Service for WAF feature is a value-added service. If you want to use this service, you must enable it when you purchase a WAF instance.

|[Overview](/intl.en-US/Log Management/Log service/Overview.md)|×|√|√|√|

