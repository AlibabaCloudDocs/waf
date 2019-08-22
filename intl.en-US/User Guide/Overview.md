# Overview {#concept_lpz_q5l_l2b .concept}

This topic describes common operations and best practices for activating and using Web Application Firewall \(WAF\), and helps you learn about WAF and its configuration procedure.

## How to use WAF {#section_exg_kvj_wgb .section}

Web Application Firewall \(WAF\) helps you monitor HTTP and HTTPS requests to your website and implement access control. WAF supports custom ACL rules and provides Web attack protection.

Configuration procedure:

1.  [Activate WAF](#) and [configure WAF for your website](#) to redirect requests that are sent to your website to WAF for monitoring.
2.  After you have configured WAF for your website, [specify WAF protection policies](#). WAF detects and filters malicious requests to your website based on the specified protection policy. Only valid requests are allowed to access the origin server.
3.  After WAF starts to work, you can [view WAF security reports](#) to learn about security details. You can also configure [WAF settings](#) to view WAF resource usage and adjust alert settings.
4.  You can use [WAF best practices](#) to improve security management and [contact customer services](#) for technical support.

## Activate WAF {#activate .section}

WAF supports the subscription billing method. If you use the subscription billing method, you are billed monthly or annually. After you choose a subscription plan, the payment must be settled immediately. WAF services are available during the specified subscription period.

After you activate WAF, you will obtain a WAF instance with a WAF IP address. This WAF instance can protect up to 10 domains. These domains must use the same top-level domain.

**Related topics**

-   [WAF billing methods](../../../../reseller.en-US/Pricing/Billing method.md#)
-   [Activate WAF](../../../../reseller.en-US/Pricing/Subscription/Activate Alibaba Cloud WAF.md#)
-   [Renew and upgrade WAF](../../../../reseller.en-US/Pricing/Renewal and upgrade.md#)
-   [Disable WAF](reseller.en-US/User Guide/Setting/Release WAF instance.md#)

**WAF instance specifications**

-   [Subscription plans](../../../../reseller.en-US/Pricing/Subscription/Editions and features.md#)

    WAF offers three subscription plans: Pro, Business, and Enterprise. You can select an appropriate Subscription plan based on your Web business scale and actual protection requirements.

-   [Extra bandwidth](../../../../reseller.en-US/Pricing/Subscription/Extra bandwidth.md#)

    Before you choose a WAF subscription plan, evaluate your normal business traffic to separate normal traffic from unusual traffic, such as DDoS attacks. Different subscription plans provide different bandwidth quotas. If your normal service bandwidth exceeds the maximum bandwidth offered by the plan, you must purchase extra bandwidth.

-   [Extra domain packages](../../../../reseller.en-US/Pricing/Subscription/Extra domain quota.md#)

    If you need to protect domain names that use different top-level domains, you must purchase extra domain packages.

-   [Exclusive WAF IP addresses](../../../../reseller.en-US/Pricing/Subscription/Exclusive WAF IP.md#)

    If you need exclusive protection for a domain, instead of using one WAF IP address to protect all domains, you can purchase an exclusive WAF IP address.


## Configure WAF {#implement .section}

After you activate WAF, you can use the transparent proxy mode or DNS proxy mode to configure WAF for your website.

**Note:** You can choose only one mode. If you choose one mode, you must clear the domain configuration for the other mode.

-   Transparent proxy mode: This mode reroutes HTTP requests that are received on port 80 of the specified origin server to WAF. WAF processes these requests and then redirects the requests to the origin server.

    To use this mode, you must authorize WAF to access the ECS instance where your origin server is deployed. To configure this mode, add a domain and specify the IP address of the server that hosts your website in the WAF console.

-   DNS proxy mode: This mode reroutes the requests that are sent to the protected domain to WAF by modifying the DNS record. WAF then processes and redirects the requests to the origin server.

    To use this mode, you must add the domain that needs protection on the Website Configuration page in the WAF console and use [DNS resolution](https://en.wikipedia.org/wiki/Domain_Name_System) to reroute the requests sent to the protected website to WAF.

    -   Add the website configuration. Website configuration specifies the domain that needs protection and how the traffic bound to the domain is forwarded. WAF can automatically add website configuration. You can also manually add website configuration. You must specify required information including the domain name of the website that needs protection and the IP address of the server that hosts the website in the website configuration. After you add website configuration, WAF assigns an exclusive [CNAME record](https://en.wikipedia.org/wiki/CNAME_record) for the domain name.

        **Note:** If you use Alibaba Cloud DNS for domain name resolution, website configuration is automatically added. Otherwise, you need to manually add website configuration and change the DNS record.

    -   Change the DNS record. To reroute the traffic targeting a protected website to WAF, you must add and apply the CNAME record generated by WAF for this domain name.

After you configure WAF for your website, WAF can filter out malicious requests and allow only valid requests to access the origin server.

**Related topics**

-   [Use the transparent proxy mode to configure WAF](reseller.en-US/User Guide/Use the transparent proxy mode to implement WAF.md#)
-   [Website configuration \(DNS proxy mode\)](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#)
-   [Configure WAF \(DNS proxy mode\)](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#)

## Configure protection policies {#configure .section}

Alibaba Cloud WAF offers multiple protection policies. You can adjust your protection policies based on your actual needs.

You can create custom ACL rules or use the built-in protection features. The WAF team wrote the request filtering algorithms based on Web attack patterns and analysis of request headers and request bodies, and encapsulated these algorithms into protection features.

**Note:** WAF uses a multi-layer filtering mechanism. After you activate WAF and configure a protection policy, a request sent from a client to WAF has been filtered on multiple layers. Default detection sequence: **HTTP ACL policies** \> **HTTP flood protection** \> **Web attack protection**.

**Related topics**

-   [HTTP ACL policies](reseller.en-US/User Guide/Configuration/HTTP ACL policy.md#) and [Configure a whitelist or blacklist](reseller.en-US/User Guide/Configuration/Configure a whitelist or blacklist.md#)

    Custom access control rules enable WAF to filter requests based on client IP addresses, request URLs, and common request header fields.

-   [Web attack protection](reseller.en-US/User Guide/Configuration/Web application protection.md#)

    This feature protects your Web applications against common Web attacks, such as SQL injections and XSS attacks.

-   [HTTP flood protection](reseller.en-US/User Guide/Configuration/HTTP flood protection.md#) and [Custom HTTP flood protection](reseller.en-US/User Guide/Configuration/Custom HTTP flood protection.md#)

    These features protect your websites against HTTP floods.

-   [Big data deep learning engine](reseller.en-US/User Guide/Configuration/New intelligent protection engine.md#)

    This feature performs semantic analysis on requests, detects disguised or hidden malicious requests, and protects your Web applications against attacks such as confusion attacks and attack variants.

-   [Block IPs initiating high-frequency Web attacks](reseller.en-US/User Guide/Configuration/IP blocking.md#)

    This feature automatically blocks a client IP address that has launched multiple attacks on your website in a short period of time.

-   [Directory scan protection](reseller.en-US/User Guide/Configuration/Directory traversal protection.md#)

    This feature automatically blocks a client IP address that has launched multiple attacks on your website in a short period of time.

-   [Threat intelligence](reseller.en-US/User Guide/Configuration/Threat intelligence.md#)

    This feature automatically blocks access requests from common vulnerability scanners or from IP addresses in the Alibaba Cloud library of identified port scan attackers.

-   [Blocked regions](reseller.en-US/User Guide/Configuration/Blocked regions.md#)

    This feature blocks access requests from specified Chinese provinces or other countries or regions.

-   [Data risk control](reseller.en-US/User Guide/Configuration/Data risk control.md#)

    This feature protects your Web applications against bot attacks such as zombie accounts, account theft, vote cheating, and spam messages.

-   [Web tamper protection](reseller.en-US/User Guide/Configuration/Website tamper-proofing.md#)

    This feature can lock specified webpages to avoid content tampering. When a locked webpage receives a request, only the cached page that you have set is returned.

-   [Data leakage prevention](reseller.en-US/User Guide/Configuration/Data leakage prevention.md#)

    This feature masks sensitive information in the responses returned by the server, such as the ID number, bank card number, phone number, and sensitive words.


## Security reports {#reporting .section}

WAF provides visualized data and statistics for you to learn about your business status and security statistics.

**Related topics**

-   [Overview](reseller.en-US/User Guide/Reporting/Business overview.md#)

    View the visualized business access data and security protection statistics.

-   [Security reports](reseller.en-US/User Guide/Reporting/WAF security reports.md#)

    Search for attack details and risk alerts on your domain name within 30 days.

-   [Full logs](reseller.en-US/User Guide/Reporting/Log search.md#)

    Search for your website logs and use online analysis to quickly locate requests.

    **Note:** To enable WAF to collect access logs for a domain name, you must enable the **Log search** feature on the Website Configuration page for this domain name.


## WAF settings {#setting .section}

You can learn about and manage WAF instances on the Settings page.

**Related topics**

-   [Product information](reseller.en-US/User Guide/Setting/View product information.md#)

    You can view the resource details of your WAF instances, updates on WAF protection rules and features, and the CIDR blocks of WAF instances.

-   [Alert settings](reseller.en-US/User Guide/Setting/Configure alarm settings.md#)

    WAF informs you of security events and system alerts through emails or SMS. You can configure the alert triggering condition, alert interval, and the method to receive alerts.

-   [Custom rule groups](reseller.en-US/User Guide/Setting/Custom rule groups.md#)

    A rule group is a combination of the built-in protection rules of WAF that make up a protection policy. You can create a custom rule group for a specific protection feature of WAF to suit your needs.


## Best practices {#practice .section}

Best practices help you improve the management and use of WAF.

**Related topics**

-   [Obtain real client IP address](../../../../reseller.en-US/Best Practices/Get real client IP address.md#)

    After you configure WAF for a website, all requests that are received by the origin server are redirected by WAF. The IP addresses of the clients that initiate the requests are not displayed. This topic describes how to obtain the real IP address that initiates the request to your origin server.

-   [Protect your origin server](../../../../reseller.en-US/Best Practices/Protect your origin server.md#)

    After WAF is activated, the origin server IP address is not visible to the client. If your origin server IP address is exposed or leaked, attackers may bypass WAF and launch attacks on your origin server. This topic describes how to configure protection features to protect your origin server.

-   [Deploy WAF and Anti-DDoS Pro together](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Deploy WAF and Anti-DDoS Pro together.md#)

    If you have activated Alibaba Cloud Anti-DDoS Pro and WAF, you can follow the procedures in this topic to complete the configuration.

-   [Deploy WAF and CDN together](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Deploy WAF and CDN together.md#)

    If you have activated Alibaba CloudCDN and WAF, you can follow the procedures in this topic to complete the configuration.


## Technical support {#expert .section}

If you encounter any problems in using WAF, move the pointer over the **Technical Support** icon in the left-side navigation pane in the [WAF console](https://partners-intl.console.aliyun.com/#/waf). A DingTalk QR code is displayed.

Scan the QR code with DingTalk to join the technical support group to consult the experts on any technical problems or urgent issues.

**Note:** You can download DingTalk on the [DingTalk website](https://www.dingtalk.com/).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15550/15664454277113_en-US.png)

