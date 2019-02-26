# Get started with Alibaba Cloud WAF {#concept_lpz_q5l_l2b .concept}

This topic describes common operations and best practices for enabling and using Alibaba Cloud WAF, so that you can quickly learn about WAF and familiarize yourself with the configuration methods.

## WAF usage flow {#section_exg_kvj_wgb .section}

Alibaba Cloud WAF \(WAF\) is a web application firewall that helps you monitor HTTP and HTTPS requests to your website and implement website access control. You can use Alibaba Cloud WAF to customize ACL rules or enable the inbuilt scenario-based protection features.

Follow these steps to use WAF:

1.  [Activate Alibaba Cloud WAF](#) and [implement WAF for your website](#) to let WAF monitor web traffic.
2.  [Configure WAF protection features](#). WAF inspects access requests according to the configured protection features, and only allows valid requests to your origin server.
3.  [View WAF security reports](#) to know your web business and security information, or [configure WAF settings](#).
4.  Perform [WAF best practices](#) to improve security management, or [contact technical support](#).

## Activate Alibaba Cloud WAF {#activate .section}

Alibaba Cloud WAF is a paid service and is billed with the Subscription method on a monthly or annually basis. To get started with WAF, you must subscribe to a suitable business plan and make the payment. After that, you can enjoy the protection service specified in the specs within the subscription duration.

After activating WAF, you are assigned with a WAF instance \(one WAF IP address\), with which you can associate one domain name and up to 10 related sub-domain names for inspecting web traffic.

**Related topics**

-   [WAF billing method](../../../../../reseller.en-US/Pricing/Billing method.md#)
-   [Activate Alibaba Cloud WAF](../../../../../reseller.en-US/Pricing/Subscription/Activate Alibaba Cloud WAF.md#)
-   [WAF renewal and upgrade](../../../../../reseller.en-US/Pricing/Renewal and upgrade.md#)
-   [Disable Alibaba Cloud WAF](reseller.en-US/User Guide/Setting/Release WAF instance.md#)

**WAF instance specification**

-   [Subscription plans](../../../../../reseller.en-US/Pricing/Subscription/Subscription plans.md#)

    Alibaba Cloud WAF offers three subscription plans: Pro, Business and Enterprise. You can select an appropriate specification based on your web business scale and actual protection requirement.

-   [Extra bandwidth](../../../../../reseller.en-US/Pricing/Subscription/Extra bandwidth.md#)

    When purchasing WAF, you must specify the normal business traffic you want WAF to inspect, so that WAF can distinguish abnormal traffic such as DDoS attacks. Different subscription plan has different bandwidth. If your normal business traffic exceeds the bandwidth in the specs, you can purchase extra bandwidth.

-   [Extra domain](../../../../../reseller.en-US/Pricing/Subscription/Extra domain quota.md#)

    If you want to enable WAF protection for more than one domain name or more than 10 sub-domain names, you can buy an extra domain quota.

-   [Exclusive WAF IP](../../../../../reseller.en-US/Pricing/Subscription/Exclusive WAF IP.md#)

    If you have a key interface and want to associate it with an exclusive WAF IP other than the default one, which may be used by multiple subdomains, you can enable exclusive WAF IP.


## Implement Alibaba Cloud WAF {#implement .section}

To implement Alibaba Cloud WAF, you first create a website configuration in the WAF console to associate your domain name with the subscribed WAF instance, and then update the domain name’s DNS \([Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System)\) settings to redirect web traffic to WAF for inspection.

-   Create a website configuration: Website configuration describes the forwarding routes of the websites that are deployed with Alibaba Cloud WAF. You can add a website configuration by using the automatic or manual method. In a website configuration, you specify a domain name to protect and configure the forwarding settings such as the server address. Alibaba Cloud WAF assigns a dedicated WAF CNAME address \([What is CNAME](https://en.wikipedia.org/wiki/CNAME_record)\) to each website configuration.

    **Note:** If you use Alibaba Cloud DNS to host your domain name, when you are implementing WAF, WAF can read the existing forwarding settings \(in particular, A records\) to automatically create website configuration, and update the corresponding DNS settings on your behalf. You only have to select the domain name to protect. If not, you have to manually create a website configuration and update the DNS settings yourself.

-   Only when you enable the WAF CNAME address for your domain name at the DNS provider will Alibaba Cloud WAF begin monitoring network traffic requesting the domain name.

WAF helps you filter out malicious requests and forward valid requests back to the origin server address.

**Related topics**

-   [Website configuration](reseller.en-US/User Guide/Implementation/Website configuration.md#)
-   [Implement Alibaba Cloud WAF](reseller.en-US/User Guide/Implementation/Deploy Alibaba Cloud WAF.md#)

## Configure WAF protection features {#configure .section}

Alibaba Cloud WAF offers a variety of scenario-based web security features. You can customize your own protection configuration to filter access requests based on actual needs.

You can customize ACL rules or use the inbuilt scenario-based common web protection functions. These inbuilt protection features integrate precise filtering algorithms that are written based on Web attack characteristics and analysis of massive requests.

**Note:** Alibaba Cloud WAF enables multi-layer filtering. After you implement WAF and configure multiple protection policies, client requests have to go through multi-layer filtering. The default protection sequence is: **HTTP ACL Policy** \> **HTTP Flood Protection** \> **Web Application Protection**.

**Related topics**

-   [HTTP ACL policy](reseller.en-US/User Guide/Configuration/HTTP ACL policy.md#), [Configure a blacklist or whitelist](reseller.en-US/User Guide/Configuration/Configure a whitelist or blacklist.md#)

    This feature helps you filter access requests based on the client IP address, request URL, and common request header fields.

-   [Web application protection](reseller.en-US/User Guide/Configuration/Web application protection.md#)

    This feature helps you protect against common Web attacks such as SQL injection and XSS cross-site attacks.

-   [HTTP flood protection](reseller.en-US/User Guide/Configuration/HTTP flood protection.md#), [Custom HTTP flood protection](reseller.en-US/User Guide/Configuration/Custom HTTP flood protection.md#)

    This feature helps you protect against HTTP flood attacks.

-   [New intelligent protection engine](reseller.en-US/User Guide/Configuration/New intelligent protection engine.md#)

    This feature performs semantic analysis on web requests, detects malicious requests, and helps you protect against malicious attacks initiated by confusion attacks and variants.

-   [Malicious IP penalty](reseller.en-US/User Guide/Configuration/Malicious IP Penalty.md#)

    This feature helps you automatically block the client IP address that has launched multiple Web attacks in a short period of time.

-   [Blocked region](reseller.en-US/User Guide/Configuration/Blocked regions.md#)

    This feature helps you block access requests based on the client's IP geolocation and supports blocking all requests from one or more designated Chinese provinces and international countries.

-   [Data risk control](reseller.en-US/User Guide/Configuration/Data risk control.md#)

    This feature helps you defend against machine frauds such as zombie accounts, credential stuffing, brute force cracking, vote cheating, and spam messages.

-   [Website tamper-proofing](reseller.en-US/User Guide/Configuration/Website tamper-proofing.md#)

    This feature helps you lock specified web pages to prevent content tampering. The locked pages only return the cached content.

-   [Data leakage prevention](reseller.en-US/User Guide/Configuration/Data leakage prevention.md#)

    This feature helps you mask sensitive information in the server response, such as the ID number, bank card number, telephone number, and sensitive words.


## View WAF security reports {#reporting .section}

Alibaba Cloud WAF provides convenient data visualization and statistics features.

**Related topics**

-   [Business and security overview](reseller.en-US/User Guide/Reporting/Business and security overview.md#)

    View the business QPS data and security protection statistics.

-   [Security reports](reseller.en-US/User Guide/Reporting/WAF security reports.md#)

    Search for attack details and risk warning information on your domain name within 30 days.

-   [Logs](reseller.en-US/User Guide/Reporting/Log search.md#)

    Search for your website logs and use online analysis to quickly locate requests.

    **Note:** You must first enable the **Log Query** function on the Website Configuration page for the domain name. WAF only collects the access logs for the specified domain name.


## Configure WAF settings {#setting .section}

The Setting page helps you understand your WAF resources and manage alarm settings and custom rule groups.

**Related topics**

-   [Product information](reseller.en-US/User Guide/Setting/View product information.md#)

    The Product Information page provides you with an intuitive view over your subscription details, the built-in protection rule updates, feature changes, and WAF’s IP addresses.

-   [Alarm settings](reseller.en-US/User Guide/Setting/Configure alarm settings.md#)

    Alibaba Cloud WAF informs you about security events and system events through emails. You can configure the alarm triggering condition and alarm time interval.

-   [Custom rule groups](reseller.en-US/User Guide/Setting/Custom rule groups.md#)

    A rule group is a combination of the inbuilt protection rules of Alibaba Cloud WAF that makes up an optional policy for a specific protection function. You can create and apply a custom rule group for a specific protection function of WAF to achieve dedicated protection effect.


## WAF best practices {#practice .section}

Apply WAF best practices for better protection effectiveness.

**Related topics**

-   [Get real client IP address](../../../../../reseller.en-US/Best Practices/Get real client IP address.md#)

    For a website that is implemented with WAF, all valid web requests are forwarded to the origin server from the WAF instance, and the real client IP address is not displayed. Use this practice to get the real client IP address.

-   [Protect your origin server](../../../../../reseller.en-US/Best Practices/Protect your origin server.md#)

    After WAF is enabled, the origin server IP address is invisible to the client. If your origin IP address is exposed or unintentionally disclosed, an attacker can bypass WAF and attack your origin directly. This practice helps you defend against this situation.

-   [Deploy WAF and Anti-DDoS Pro together](reseller.en-US/User Guide/Implementation/Deploy WAF and Anti-DDoS Pro together.md#)

    If you have activated Alibaba Cloud Anti-DDoS Pro and Web Application Firewall, you can refer to this practice for configuration.

-   [Deploy WAF and CDN together](reseller.en-US/User Guide/Implementation/Deploy WAF and CDN together.md#)

    If you have activated Alibaba Cloud CDN and Web Application Firewall, you can refer to this practice for configuration.


## Technical support {#expert .section}

For any technical question about using Alibaba Cloud WAF, use DingTalk to scan the **Technical Support** code in the lower left corner of the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf) to join the WAF Technical Support team.

Our technical experts are ready to serve you.

**Note:** You can go to the [DingTalk official website](https://www.dingtalk.com/) to download and install DingTalk.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15550/15511464917113_en-US.png)

