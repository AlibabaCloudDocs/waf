# Product specification for Alibaba Cloud DNS version of WAF {#concept_lhm_sbl_q2b .concept}

The following table lists product specifications for the Alibaba Cloud DNS version of WAF:

|Product parameter|Description|DNS version|
|HTTP|Supports HTTP \(80\) port|Supported|
|HTTPS|Supports HTTPS \(443\) port|Not supported|
|Data centers outside cloud|Supports websites outside Alibaba Cloud|Supported|
|Basic Web application protection|Protects against common Web attacks such as SQL injection and command execution|Supported|
|0day vulnerability defense|Quickly protects against the latest Web vulnerabilities|Supported|
|Service availability|Protects the data center where the server is deployed|Supports single data center|
|Custom Web protection policies|Customizes Web protection policies for websites|Not supported|
|Custom HTTP flood protection policies|Provides security professionals to customize protection rules for specific service interfaces|Not supported|
|HTTP flood protection threshold|Maximum attack requests per second that can be defended|1,000|
|HTTP ACL policies|Number of rules for access control that can be added|5 \(IP/URL\)|
|Number of protected domain names|Number of domain names that can be protected|2|
|Daily QPS threshold|Normal requests per second|100|
|Bandwidth threshold|Maximum bandwidth per second \(Mbps\)|10 \(origins outside Alibaba Cloud\) 200 \(origins inside Alibaba Cloud\)|
|Number of back-to-source IP addresses|Maximum number of IP addresses that are passed back to the origin at the same time for the same domain name|2|
|Custom requirement|Supports various custom requirements|Not supported|

If the product specifications of the DNS version cannot fit your requirements, you can upgrade the service in the console.

