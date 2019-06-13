# Subscription plans {#concept_pf4_xrd_n2b .concept}

Alibaba Cloud WAF provides three subscription plans for a variety of business scenarios. These plans are Pro, Business, and Enterprise.

Generally, we recommend that you consider the Business or Enterprise plan to build a relatively strict security environment. The following table gives a brief overview of the differences between all Alibaba Cloud WAF subscription plans.

|Features/Plans|Pro|Business|Enterprise|
|--------------|---|--------|----------|
|Applicable websites|Websites of small and medium businesses that have no special security requirements|Medium enterprise websites that open services to the Internet users and focus on enhanced data security to secure business operations|Medium or large enterprise websites that handle large-scale transactions and have customized security requirements|
|Maximum requests per second \(QPS\)|2,000 QPS|5,000 QPS|Above 10,000 QPS|
|Maximum bandwidth for Alibaba Cloud origin servers \(Mbps\)|50|100|200|
|Maximum bandwidth for non-Alibaba Cloud origin servers \(Mbps\)|10|30|50|
|Protecting against common web attacks such as SQL injection and XSS|√|√|√|
|Automatically updating protection rules against Web 0-day vulnerabilities|√|√|√|
|Mitigating \(Non-API\) HTTP flood attacks|√|√|√|
|Enabling HTTPS for your website|√|√|√|
|Configuring IP/URL blacklist and whitelist for access control|√|√|√|
|Protecting against targeted Web attacks such as penetration testing|√|√|√|
|Webpage tamper-proofing|√|√|√|
|Inspecting and blocking malicious registration|√|√|√|
|Advanced HTTP access control based on most common HTTP request header fields such as UA and Referer|√|√|√|
|Protecting non-standard ports other than 80, 8080, 443, and 8443|×|√|√|
|Retrieving web access logs of the last 30 days|×|√ **Note:** Not supported for international region. Consider the Enterprise plan.

 |√|
|Rated-based access control that can limit the number of requests per specified time interval|×|√|√|
|Geolocation-based access control that can block all requests from the specified region|×|√|√|
|Mitigating \(API\) HTTP flood attacks|×|√|√|
|Protecting sensitive data such as identity card number, mobile phone number, and bank card number|√|√|√|
|Custom protection rule groups|×|×|√|
|Security consulting services|×|×|√|
|Data visualization|√ **Note:** Not support for international region. Consider the Business or Enterprise plan.

 |√|√|
|**Pricing**| -   China Mainland: 499 USD per month
-   International: 299 USD per month

 | -   China Mainland: 1,399 USD per month
-   International: 599 USD per month

 | -   China Mainland: 4,999 USD per month
-   International: 2,999 USD per month

 |

