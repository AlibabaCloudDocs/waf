# Overview

This topic describes the website protection features supported by Web Application Firewall \(WAF\).

|Module|Feature|Description|Enabling method|Reference|
|------|-------|-----------|---------------|---------|
|**Web Security**|**RegEx Protection Engine**|The feature protects your websites against common web attacks based on built-in rule groups. The common web attacks include SQL injection, XSS, webshell upload, command injection, backdoor isolation, invalid file requests, path traversing, and common application attacks.|The feature is enabled by default after you add a domain name.|[Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md)[Best practices for using RegEx Protection Engine](t15589.md#) |
|**Protection Rule Group**|The feature allows you to combine protection rules to create a custom rule group and apply the group to specific websites as needed. **Note:** You can create a custom rule group for only **RegEx Protection Engine**.

|You need to enable it after you add a domain name.|[Customize protection rule groups](/intl.en-US/Website Protection Settings/Customize protection rule groups.md)[Best practices for using custom rule groups to provide enhanced protection](t78570.md#) |
|**Big Data Deep Learning Engine**|The feature is based on the deep neural network system of Alibaba Cloud. It classifies all web attack data and normal business data in the cloud and then creates a data model. This way, potential attacks can be blocked in real time.|You need to enable it after you add a domain name.|[Configure the Big Data Deep Learning Engine](/intl.en-US/Website Protection Settings/Web security/Configure the Big Data Deep Learning Engine.md)|
|**Website Tamper-proofing**|The feature helps you lock specific web pages, such as those that contain sensitive information. When a locked web page is requested, the page cached in WAF is returned. This prevents the tampering of the web pages.|You need to enable it after you add a domain name.|[Configure website tamper-proofing](/intl.en-US/Website Protection Settings/Web security/Configure website tamper-proofing.md)|
|**Data Leakage Prevention**|The feature filters content, such as abnormal pages and keywords, returned from the servers to websites and masks sensitive information, such as identity card numbers, bank card numbers, phone numbers, and sensitive words. WAF then returns masked information or default error pages to visitors.|You need to enable it after you add a domain name.|[Configure data leakage prevention](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)|
|**Positive Security Model**|The feature uses Alibaba Cloud machine learning algorithms to automatically analyze the normal network traffic of a website. It then generates security protection policies tailored for the website based on the collected data.|You need to enable it after you add a domain name.|[Configure the positive security model](/intl.en-US/Website Protection Settings/Web security/Configure the positive security model.md)|
|**Bot Management**|**Allowed Crawlers**|The feature maintains a whitelist for authorized search engines, such as Google, Bing, Baidu, Sogou, 360, and Yandex. The crawlers of these search engines are allowed to access specified domain names.|You need to enable it after you add a domain name.|[Set a threat intelligence rule to allow requests from specific crawlers](/intl.en-US/Website Protection Settings/Bot management/Set a threat intelligence rule to allow requests from specific crawlers.md)|
|**Bot Threat Intelligence**|The feature provides information about suspicious IP addresses of dialers, on-premises data centers, and malicious scanners based on the powerful computing capabilities of Alibaba Cloud. This feature also maintains a dynamic IP library of malicious crawlers and prevents crawlers from accessing your websites or specific directories.|You need to enable it after you add a domain name.|[Set a bot threat intelligence rule](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md)|
|**Data Risk Control**|The feature protects crucial website services, such as registrations, logons, campaigns, and forums, against fraud.|You need to enable it after you add a domain name.|[Configure data risk control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)|
|**App Protection**|The feature provides secure connections and anti-bot protection for native applications. This feature also identifies proxies, emulators, and requests with invalid signatures.|You need to enable it after you add a domain name.|[Configure application protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md)|
|**Access Control/Throttling**|**HTTP Flood Protection**|This feature helps you defend against HTTP flood attacks and provides protection policies in different modes.|The feature is enabled by default after you add a domain name.|[Configure HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)[Best practices for preventing HTTP flood attacks](t81368.md#) |
|**IP Blacklist**|The feature blocks access requests from specified IP addresses, CIDR blocks, and IP addresses in specified regions.|You need to enable it after you add a domain name.|[Configure a blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure a blacklist.md)|
|**Scan Protection**|The feature automatically blocks access requests that have specific characteristics. For example, if the source IP address of requests initiates multiple web attacks or targeted directory traversal attacks in a short period of time, WAF automatically blocks the requests. Source IP addresses are also blocked if they are from common scan tools or the Alibaba Cloud malicious IP library.|You need to enable it after you add a domain name.|[Configure scan protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)|
|**Custom Protection Policy**|The feature allows you to customize ACL rules and configure rate limiting based on precise match conditions.|You need to enable it after you add a domain name.|[Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)|
|**Protection Lab**|**Account Security**|The feature allows you to monitor user authentication-related interfaces, such as the endpoints used for registration and logon, and to detect events that may pose a threat to user credentials. These threats include credential stuffing, brute-force attacks, spam registration, weak password sniffing, and SMS flood attacks.|You need to enable it after you add a domain name.|[Configure account security](/intl.en-US/Protection Lab/Configure account security.md)[Account security best practices](t1840545.md#) |
|**API Request Security**|The feature allows you to upload a custom API rule file to execute only requests that comply with the rules. This protects your website assets against threats such as tampering and replay attacks.|You need to enable it after you add a domain name.|[Enable API request security](/intl.en-US/Protection Lab/Enable API request security.md)|
|**Whitelists**|**Website Whitelisting**|After you configure a rule, requests that match the rule bypass all protection features and are directly forwarded to origin servers.|You need to enable it after you add a domain name.|[Configure a website whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure a website whitelist.md)|
|**Whitelisting Rules in Web Intrusion Prevention**|After you configure a rule, requests that match the rule bypass specified protection features, such as RegEx Protection Engine and Big Data Deep Learning Engine.|You need to enable it after you add a domain name.|[Configure a whitelist for Web Intrusion Prevention](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Web Intrusion Prevention.md)|
|**Whitelisting Rules in Data Security**|After you configure a rule, requests that match the rule bypass specified protection features, such as website tamper-proofing, data leak prevention, and account security.|You need to enable it after you add a domain name.|[Configure a whitelist for Data Security](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Data Security.md)|
|**Whitelisting Rules in Bot Management**|After you configure a rule, requests that match the rule bypass specified protection features, such as bot threat intelligence, data risk control, intelligent algorithm, and application protection.|You need to enable it after you add a domain name.|[Configure a whitelist for Bot Management](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Bot Management.md)|
|**Whitelisting Rules in Access Control/Throttling**|After you configure a rule, requests that match the rule bypass specified protection features, such as HTTP flood protection, blacklist, scan protection, and custom protection policy.|You need to enable it after you add a domain name.|[Configure a whitelist for Access Control/Throttling](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Access Control/Throttling.md)|
