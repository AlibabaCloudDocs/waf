# Understand Alibaba Cloud WAF in five minutes {#concept_lpz_q5l_l2b .concept}

Alibaba Cloud WAF \(WAF\) is a web application firewall that helps you monitor HTTP and HTTPS requests to your website and implement website access control. You can use Alibaba Cloud WAF to customize ACL rules or enable the inbuilt scenario-based protection features.

## Activate WAF {#activate .section}

Alibaba Cloud WAF is a paid service and is billed with the Subscription method on a monthly or annually basis. To get started with WAF, you must subscribe to a suitable business plan and make the payment. After that, you can enjoy the protection service specified in the specs within the subscription duration.

**Note:** When purchasing WAF, you must specify the normal business traffic you want WAF to inspect, so that WAF can distinguish abnormal traffic such as DDoS attacks. Different subscription plan has different bandwidth. If your normal business traffic exceeds the bandwidth in the specs, you can purchase [Extra bandwidth](../../../../../intl.en-US/Pricing/Subscription/Extra bandwidth.md#).

For more information, see [Billing method](../../../../../intl.en-US/Pricing/Billing method.md#), [Subscription plans](../../../../../intl.en-US/Pricing/Subscription/Subscription plans.md#), and [Purchase Alibaba Cloud WAF](../../../../../intl.en-US/Pricing/Subscription/Purchase Web Application Firewall.md#).

After activating WAF, you are assigned with a WAF instance \(one WAF IP address\), with which you can associate one domain name and up to 10 related subdomain names for inspecting web traffic.

-   If you want to protect more than one domain name, you must purchase [Extra domain quota](../../../../../intl.en-US/Pricing/Subscription/Extra domain quota.md#).
-   If you have a key interface and want to associate it with an exclusive WAF IP other than the default one, which may be used by multiple subdomains, you can enable [Exclusive WAF IP](../../../../../intl.en-US/Pricing/Subscription/Exclusive WAF IP.md#).

## Implement WAF {#implement .section}

To implement Alibaba Cloud WAF, you first create a website configuration in the WAF console to associate your domain name with the subscribed WAF instance, and then update the domain name’s DNS \([Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System)\) settings to redirect web traffic to WAF for inspection.

-   Create a website configuration

    Website configuration describes the forwarding routes of the websites that are deployed with Alibaba Cloud WAF. You can add a website configuration by using the automatic or manual method. In a website configuration, you specify a domain name to protect and configure the forwarding settings such as the server address. Alibaba Cloud WAF assigns a dedicated WAF CNAME address \([What is CNAME](https://en.wikipedia.org/wiki/CNAME_record)\) to each website configuration.

    For more information, see [Website configuration](intl.en-US/User Guide/Access WAF/Website configuration.md#).

-   Update the DNS settings

    Only when you enable the WAF CNAME address for your domain name at the DNS provider will Alibaba Cloud WAF begin monitoring network traffic requesting the domain name. WAF helps you filter out malicious requests and forward valid requests back to the origin server address.

    For more information, see [WAF deployment guide](intl.en-US/User Guide/Access WAF/WAF deployment guide.md#).

-   Automatically implement Alibaba Cloud WAF

    If you use [Alibaba Cloud DNS](https://www.alibabacloud.com/product/dns) to host your domain name, when you are implementing WAF, WAF can read the existing forwarding settings \(in particular, A records\) to automatically create website configuration, and update the corresponding DNS settings on your behalf. You only have to select the domain name to protect. If not, you have to manually create a website configuration and update the DNS settings yourself.


## Configure WAF protection policies {#policies .section}

When implemented, Alibaba Cloud WAF inspects the HTTP and HTTPS requests to your website and applies access control rules to filter out malicious requests.

**Note:** The following features may not be included in your subscription plan. For more information about whether a feature is available, see the feature description link.

-   You can use **HTTP ACL Policy** to customize access control rules to filer requests based on specified client IP addresses, request URLs, and common request header fields. For more information, see [HTTP ACL Policy](intl.en-US/User Guide/Protection configuration/HTTP ACL policy.md#) and [Create a whitelist or blacklist](intl.en-US/User Guide/Protection configuration/Configure a whitelist or blacklist.md#).
-   You can also use the scenario-based Web protection features to protect against common Web attacks. These inbuilt protection features integrate precise filtering algorithms that are written based on Web attack characteristics and analysis of massive requests. They are ease of use and include the following:

    **Note:** Alibaba Cloud WAF enables multi-layer filtering. After you implement WAF and configure multiple protection policies, client requests have to go through multi-layer filtering. The default protection sequence is: **HTTP ACL Policy** \> **HTTP Flood Protection** \> **Web Application Protection**.

    -   **Web application protection**: This feature helps you protect against common Web attacks such as SQL injection and XSS cross-site attacks. For more information, see [Web application protection](intl.en-US/User Guide/Protection configuration/Web application protection.md#).
    -   **HTTP flood protection**: This feature helps you protect against HTTP flood attacks. For more information, see [HTTP flood protection mode](intl.en-US/User Guide/Protection configuration/HTTP flood protection.md#) and [Customize HTTP flood protection](intl.en-US/User Guide/Protection configuration/Custom HTTP flood protection.md#).
    -   **New intelligent protection engine**: This feature performs semantic analysis on web requests, detects malicious requests, and helps you protect against malicious attacks initiated by confusion attacks and variants. For more information, see [New intelligent protection engine](intl.en-US/User Guide/Protection configuration/New intelligent protection engine.md#).
    -   **Malicious IP penalty**: This feature helps you automatically block the client IP address that has launched multiple Web attacks in a short period of time. For more information, see [Enable malicious IP penalty](intl.en-US/User Guide/Protection configuration/Malicious IP Penalty.md#).
    -   **Blocked region**: This feature helps you block IP access requests based on the geolocation vector and supports blocking all requests from one or more specified China provinces and International countries. For more information, see [Blocked regions](intl.en-US/User Guide/Protection configuration/Blocked regions.md#).
    -   **Data risk control**: This feature helps you defend against machine frauds such as zombie accounts, credential stuffing, brute force cracking, vote cheating, and spam messages. For more information, see [Data risk control](intl.en-US/User Guide/Protection configuration/Data risk control.md#).
    -   **Website tamper-proofing**: This feature helps you lock specified web pages to prevent content tampering. The locked pages only return the cached content. For more information, see [Website tamper-proofing](intl.en-US/User Guide/Protection configuration/Website tamper-proofing.md#).
    -   **Data leakage prevention**: This feature helps you mask sensitive information in the server response, such as the ID number, bank card number, telephone number, and sensitive words. For more information, see [Data leakage prevention](intl.en-US/User Guide/Protection configuration/Data leakage prevention.md#).

## View WAF security reports {#reports .section}

Alibaba Cloud WAF provides convenient data visualization and statistics features:

-   **Security monitoring**: You can view the business QPS data and security protection statistics on the [Overview](intl.en-US/User Guide/Protection reports/Overview of the Alibaba Cloud WAF report.md#) page.
-   **Reports**: You can search for attack details and risk warning information on your domain name within 30 days. For more information, see [Attack protection reports](intl.en-US/User Guide/Protection reports/View the attack protection report.md#) and [Risk warning reports](intl.en-US/User Guide/Protection reports/Risk warning report.md#).
-   **Logs**: You can search for your website logs and use online analysis to quickly locate requests. For more information, see [Alibaba Cloud WAF logging](intl.en-US/User Guide/Protection reports/Log search.md#).

## Additional WAF best practices {#section_o5b_s5l_l2b .section}

For a website that is implemented with WAF, all valid web requests are forwarded to the origin server from the WAF instance, and the origin server address is invisible to clients.

-   If you want to see the real client IP address, see [Get real client IP addresses](../../../../../intl.en-US/Best Practices/Get real client IP address.md#).
-   If your origin IP address is exposed or unintentionally disclosed, an attacker can bypass WAF and attack your origin directly. To protect against this situation, you can [Configure origin protection](../../../../../intl.en-US/Best Practices/Protect your origin server.md#).
-   If you are using Alibaba Cloud WAF with [DDoS Pro](https://www.alibabacloud.com/product/ddos-pro) or [CDN](https://www.alibabacloud.com/product/cdn), see the following topics for detailed implementation method:

    **Note:** You must select **yes** for **Any layer 7 proxy \(e.g. Anti-DDoS/CNS\) enabled ?** in this case.

    -   [Deploy WAF and Anti-DDoS Pro together](intl.en-US/User Guide/Access WAF/Deploy WAF and Anti-DDoS Pro together.md#)
    -   [Deploy WAF and CDN together](intl.en-US/User Guide/Access WAF/Deploy WAF and CDN together.md#)
-   To protect your native apps and resolve issues such as HTTP flood attacks, malicious registrations, and fake orders, see [WAF SDK solution](intl.en-US/User Guide/SDK solution/Access the WAF SDK.md#).

