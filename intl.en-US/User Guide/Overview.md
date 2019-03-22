# Overview {#concept_lpz_q5l_l2b .concept}

This topic describes common operations and best practices for activating and using Web Application Firewall \(WAF\), and helps you learn about WAF and its configuration procedure.

## How to use WAF {#section_exg_kvj_wgb .section}

Web Application Firewall \(WAF\) helps you monitor HTTP and HTTPS requests to your website and implement access control. WAF supports custom ACL rules and provides multiple built-in scenario-based protection features.

Configuration procedure:

1.  [Activate WAF](#) and [configure WAF for your website](#) to redirect requests that are sent to your website to WAF for monitoring.
2.  After you have configured WAF for your website, [specify WAF protection policies](#). WAF detects and filters malicious requests to your website based on the specified protection policy. Only valid requests are allowed to access the origin server.
3.  After WAF is enabled, you can [view WAF security reports](#) to learn about security details and risks. You can also configure [WAF settings](#) to view WAF resource usage status and adjust alarm settings.
4.  You can use [WAF best practices](#) to improve security management, or [contact technical support](#).

## Activate WAF {#activate .section}

WAF supports the Subscription billing method. When you use the Subscription billing method, you are billed on a monthly or annual basis. After you choose a Subscription plan, the payment must be settled immediately. WAF services are available during the valid subscription period.

After you activate WAF, you will obtain a WAF instance and a WAF IP address. This WAF instance provides protection for up to 10 domains. These domains must use the same top-level domain.

**Related topics**

-   [WAF billing methods](../../../../../reseller.en-US/Pricing/Billing method.md#)
-   [Activate Web Application Firewall](../../../../../reseller.en-US/Pricing/Subscription/Activate Alibaba Cloud WAF.md#)
-   [WAF renewal and upgrade](../../../../../reseller.en-US/Pricing/Renewal and upgrade.md#)
-   [Disable Web Application Firewall](reseller.en-US/User Guide/Setting/Release WAF instance.md#)

**WAF instance specifications**

-   [Subscription plans](../../../../../reseller.en-US/Pricing/Subscription/Subscription plans.md#)

    Web Application Firewall offers three Subscription plans: Advanced, Enterprise, and Flagship. You can select an appropriate Subscription plan based on your Web business scale and actual protection requirements.

-   [Extra bandwidth](../../../../../reseller.en-US/Pricing/Subscription/Extra bandwidth.md#)

    Before you choose a WAF Subscription plan, you need to evaluate your normal business traffic to separate normal traffic from unusual traffic, such as DDoS attacks. Different Subscription plans support different bandwidth conditions. If your actual business traffic exceeds the upper limit offered by the plan, you must purchase extra bandwidth.

-   [Extra domain quotas](../../../../../reseller.en-US/Pricing/Subscription/Extra domain quota.md#)

    If you need to protect domain names that use different top-level domains, you must purchase extra domain quotas.

-   [Exclusive WAF IP addresses](../../../../../reseller.en-US/Pricing/Subscription/Exclusive WAF IP.md#)

    If you need exclusive protection for an important domain, instead of using one WAF IP address to protect all domains, you can purchase an exclusive WAF IP address.


## Configure WAF {#implement .section}

After you activate WAF, you can use the transparent proxy mode or DNS proxy mode to configure WAF for your website.

**Note:** You can choose either mode to configure WAF. If you choose the transparent proxy mode, clear the website configuration that you have set for the DNS proxy mode. If you choose the DNS proxy mode, clear the website configuration for the transparent proxy mode.

-   Transparent proxy mode: This mode directs HTTP requests that are received on port 80 of the specified origin server to WAF. WAF processes the requests and then redirects the requests to the origin server.

    To use this mode, you must authorize WAF to access the ECS instances where your services are deployed. To configure this mode, add a domain and specify the IP address of the server that hosts your website in the WAF console.

-   DNS proxy mode: This mode directs requests that are sent to the protected domain to WAF based on the specified DNS record. WAF then processes and redirects the requests to the specified origin server.

    In DNS proxy mode, you must add website configuration and specify the domain that needs protection in the WAF console. Requests sent to the website are directed to WAF for monitoring based on [DNS settings](https://en.wikipedia.org/wiki/Domain_Name_System).

    -   Add website configuration: Website configuration specifies the domain that needs protection and the origin server IP address. WAF can automatically add website configuration. You can also manually add website configuration. You must specify required information including the domain name of the website that needs protection and the IP address of the server that hosts the website in the website configuration. After you add website configuration, WAF assigns an exclusive [CNAME record](https://en.wikipedia.org/wiki/CNAME_record) for the domain name.

        **Note:** If you use Alibaba Cloud DNS to translate your domain name, website configuration is automatically added. Otherwise, you need to manually add website configuration and change the DNS record.

    -   Change the DNS record: Only after you have added and enabled the WAF CNAME record for the specified domain name, requests sent to the website can be redirected to WAF for monitoring.

After you configure WAF for your website, WAF can filter out malicious requests. Only valid requests are allowed to access the origin server.

**Related topics**

-   [Use the transparent proxy mode to configure WAF](reseller.en-US/User Guide/Use the transparent proxy mode to implement WAF.md#)
-   [Website configuration \(DNS proxy mode\)](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#)
-   [Configure DNS settings \(DNS proxy mode\)](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#)

## Configure protection policies {#configure .section}

Alibaba Cloud WAF offers multiple protection policies. You can adjust your protection policies based on your actual needs.

You can create custom ACL rules or use the built-in protection features. The Web Application Firewall team wrote the filtering algorithms based on attacks patterns and analysis of request headers and request bodies, and encapsulated the algorithms into the protection features for efficient use.

**Note:** WAF uses a multi-layer filtering mechanism. After you enable WAF and configure a protection policy, a request sent from a client to WAF has been filtered on multiple layers. Default detection sequence: **Access Control** \> **HTTP Flood Protection** \> **Web Application Protection**.

**Related topics**

-   [HTTP ACL policy](reseller.en-US/User Guide/Configuration/HTTP ACL policy.md#) and [Configure a whitelist or blacklist](reseller.en-US/User Guide/Configuration/Configure a whitelist or blacklist.md#)

    Custom access control rules allow WAF to filter requests based on client IP addresses, request URLs, and common request header fields.

-   [Web application protection](reseller.en-US/User Guide/Configuration/Web application protection.md#)

    This feature protects your Web applications against common Web attacks, such as SQL injection and XSS attacks.

-   [HTTP flood protection](reseller.en-US/User Guide/Configuration/HTTP flood protection.md#) and [Custom HTTP flood protection](reseller.en-US/User Guide/Configuration/Custom HTTP flood protection.md#)

    These features protect your Web applications against HTTP floods.

-   [New intelligent protection engine](reseller.en-US/User Guide/Configuration/New intelligent protection engine.md#)

    This feature performs semantic analysis on requests, detects malicious requests, and protects your Web applications against attacks such as confusion attacks and attack variants.

-   [Malicious IP blocking](reseller.en-US/User Guide/Configuration/Malicious IP Penalty.md#)

    This feature automatically blocks a client IP address that has launched multiple attacks on your website in a short period of time.

-   [Blocked regions](reseller.en-US/User Guide/Configuration/Blocked regions.md#)

    This feature blocks access requests based on the geographic location of the client's IP address and supports blocking all requests from one or more specified Chinese provinces or other countries or regions.

-   [Antifraud Service](reseller.en-US/User Guide/Configuration/Data risk control.md#)

    This feature protects your Web applications against bot attacks such as zombie accounts, account theft, vote cheating, and spam messages.

-   [Webpage defacement protection](reseller.en-US/User Guide/Configuration/Website tamper-proofing.md#)

    This feature can lock specified webpages to avoid content tampering. When a locked webpage receives a request, only the cached page that you have set is returned.

-   [Data leakage prevention](reseller.en-US/User Guide/Configuration/Data leakage prevention.md#)

    This feature masks sensitive information in the response returned by the server, such as the ID number, bank card number, telephone number, and sensitive words.


## Security reports {#reporting .section}

Web Application Firewall provides visualized data and statistics for you to learn about your business status and security statistics.

**Related topics**

-   [Overview](reseller.en-US/User Guide/Reporting/Business and security overview.md#)

    View business QPS data and security protection statistics.

-   [Security reports](reseller.en-US/User Guide/Reporting/WAF security reports.md#)

    Search for attack details and risk warnings on your domain name within 30 days.

-   [Full logs](reseller.en-US/User Guide/Reporting/Log search.md#)

    Search for your website logs and use online analysis to quickly locate requests.

    **Note:** You must enable the **Log Query** feature on the Website Configuration page for the domain name for WAF to collect access logs for a specified domain name.


## WAF settings {#setting .section}

You can learn about WAF resources and manage alarm settings and custom rule groups on the Settings page.

**Related topics**

-   [View product information](reseller.en-US/User Guide/Setting/View product information.md#)

    You can view resource details of your WAF instance, updates on WAF protection policies and features, and WAF back-to-origin CIDR block.

-   [Alarm settings](reseller.en-US/User Guide/Setting/Configure alarm settings.md#)

    WAF informs you about security events and system alarms through emails or SMS. You can configure the alarm triggering condition, alarm interval, and the method to receive alarms.

-   [Custom rule groups](reseller.en-US/User Guide/Setting/Custom rule groups.md#)

    A rule group is a combination of the built-in protection rules of WAF that make up a protection policy for a specific protection feature. You can create and use a custom rule group for a specific protection feature of WAF to suit your needs.


## Best practices {#practice .section}

Best practices help you improve the management and use of WAF.

**Related topics**

-   [Obtain authentic client IP address](../../../../../reseller.en-US/Best Practices/Get real client IP address.md#)

    After you configure WAF for a website, all requests that are received by the origin server are redirected by WAF. The IP addresses of the clients that initiate the requests are not displayed. This topic describes how to obtain the real IP address that initiates the request to your origin server.

-   [Protect your origin server](../../../../../reseller.en-US/Best Practices/Protect your origin server.md#)

    After WAF is activated, the origin server IP address is not visible to the client. If your origin server IP address is exposed or unintentionally disclosed, attackers can bypass WAF and launch attacks on your origin server. This topic describes how to configure protection features to protect your origin server.

-   [Deploy WAF and Anti-DDoS Pro together](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Deploy WAF and Anti-DDoS Pro together.md#)

    If you have activated Alibaba Cloud Anti-DDoS Pro and Web Application Firewall, you can follow the procedures in this topic to complete the configuration.

-   [Deploy WAF and CDN together](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Deploy WAF and CDN together.md#)

    If you have activated Alibaba CloudCDN and Web Application Firewall, you can follow the procedures in this topic to complete the configuration.


## Technical support {#expert .section}

If you experience any problems while using Web Application Firewall, hover over the **Technical Support** icon in the left-side navigation pane in the [WAF console](https://partners-intl.console.aliyun.com/#/waf). A DingTalk QR code is displayed.

Scan the QR code with DingTalk to join the technical support group to consult the experts on any technical problems or urgent issues.

**Note:** You can download DingTalk on the [DingTalk website](https://www.dingtalk.com/).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15550/15532340347113_en-US.png)

