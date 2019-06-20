# Editions and features {#concept_pf4_xrd_n2b .concept}

If you are using subscription-based WAF instances, you can choose from the following editions based on your needs.

**Note:** We recommend that you choose either the Business or the Enterprise edition to meet different website business and security requirements.

## Editions and applicable website scales {#section_u2t_srm_4gb .section}

|Service scale|Pro|Business|Enterprise|
|-------------|---|--------|----------|
|Website scale|Small and medium websites that do not have special security requirements for their business.|Medium enterprise websites, websites with services available for all Internet users, and websites that have high requirements for data security.|Medium and large enterprise websites with a large business scale or custom security requirements.|
|Peak request rate|2,000 QPS|5,000 QPS|Higher than 10,000 QPS|
|Maximum bandwidth \(origin servers are deployed on Alibaba Cloud\)|50 Mbit/s|100 Mbit/s|200 Mbit/s|
|Maximum bandwidth \(origin servers are not deployed on Alibaba Cloud\)|10 Mbit/s|30 Mbit/s|50 Mbit/s|

## Features supported by each edition {#section_psd_1sm_4gb .section}

|Feature|Reference|Pro|Business|Enterprise|
|-------|---------|---|--------|----------|
|Enable HTTPS protection for a website|[HTTPS advanced settings](../../../../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/HTTPS advanced settings.md#)|√|√|√|
|Protection for ports other than 80, 8080, 443, and 8443.|[Support for non-standard ports](../../../../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Supported non-standard ports.md#)|×|√|√|
|Protection against common Web attacks, such as SQL injection and XSS attacks.|[Web application protection](../../../../reseller.en-US/Best Practices/Best practices for Web application protection.md#)|√|√|√|
|Automatic update of protection rules against Web zero-day vulnerabilities|√|√|√|
|![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15538/156102088738159_en-US.png)Custom rule groups|[Custom rule groups](../../../../reseller.en-US/User Guide/Setting/Custom rule groups.md#)|×|√ **Note:** WAF instances created in International regions must be upgraded to the Enterprise edition.

 |√|
|Protection against HTTP floods targeting Web services|[HTTP flood protection](../../../../reseller.en-US/User Guide/Configuration/HTTP flood protection.md#)|√|√|√|
|Protection against HTTP floods targeting API services|[Custom HTTP flood protection](../../../../reseller.en-US/User Guide/Configuration/Custom HTTP flood protection.md#)|×|√|√|
|Access frequency control for URLs|[Custom HTTP flood protection](../../../../reseller.en-US/User Guide/Configuration/Custom HTTP flood protection.md#)|×|√|√|
|IP whitelist, IP blacklist, URL whitelist, and URL blacklist|[Configure a whitelists or blacklist](../../../../reseller.en-US/User Guide/Configuration/Configure a whitelist or blacklist.md#)|√|√|√|
|Advanced HTTP request control based on header fields including US and Referer|[Access control list](../../../../reseller.en-US/User Guide/Configuration/HTTP ACL policy.md#)|√|√|√|
|Targeted Web attack protection, for example, penetration tests.|[Access control list](../../../../reseller.en-US/User Guide/Configuration/HTTP ACL policy.md#)|√|√|√|
|Location-based IP blocking \(block access requests from international regions\)|[Blocked regions](../../../../reseller.en-US/User Guide/Configuration/Blocked regions.md#)|×|√|√|
|Webpage tamper-proofing|[Website tamper-proofing](../../../../reseller.en-US/User Guide/Configuration/Website tamper-proofing.md#)|√|√|√|
|Malicious registration interception|[Data risk control](../../../../reseller.en-US/User Guide/Configuration/Data risk control.md#)|√|√|√|
|Data masking, such as ID card, phone number, and bank card number.|[Data leakage prevention](../../../../reseller.en-US/User Guide/Configuration/Data leakage prevention.md#)|√|√|√|
|Intelligent retrieval of access logs|[Log search](../../../../reseller.en-US/User Guide/Reporting/Log search.md#)|×|√ **Note:** WAF instances created in International regions must be upgraded to the Enterprise edition.

 |√|
|![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15538/156102088738159_en-US.png)Real-time log query and analysis service **Note:** The real-time log query and analysis service is a value-added service. To use this service, you must purchase the service first. For more information about pricing, see [Billing methods](../../../../reseller.en-US/User Guide/Real-time log query and analysis/Billing method.md#).

 |[Real-time log analysis](../../../../reseller.en-US/User Guide/Real-time log query and analysis/Real-time log analysis.md#)|√|√|√|
|Data visualization|[Data visualization](../../../../reseller.en-US/User Guide/Reporting/Data visualization.md#)|√ **Note:** WAF instances created in international regions must be upgraded to the Business or Enterprise edition.

 |√|√|
|Enterprise-level Web protection rules customized by experts|Managed security service|×|×|√|
|One-to-one consultation service|Consultation service|×|×|√|

