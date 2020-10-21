---
keyword: [bot management, bot threat Intelligence, , block]
---

# Set a bot threat intelligence rule

Bot threat intelligence provides information about suspicious IP addresses used by dialers, on-premises data centers, and malicious scanners. This function also maintains an IP address library of malicious crawlers and prevents crawlers from accessing all pages under your domain name or specific directories.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   **Bot Management** is enabled. This feature is a value-added service.
    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

Bot threat intelligence rules can block requests from crawlers that are recorded in the Alibaba Cloud crawler library. The Alibaba Cloud crawler library is updated in real time based on the analysis of network traffic that flows through Alibaba Cloud. It can effectively detect IP addresses of malicious crawlers and provide the characteristics of requests that are initiated from the crawlers.

**Note:** The Alibaba Cloud crawler library covers public clouds and on-premises data centers.

You can set a bot threat intelligence rule that chooses different actions to manage different requests based on the type of the threat intelligence library. For example, you can set a rule that blocks certain requests, or requires JavaScript verification or CAPTCHA verification to verify certain requests. You can also use a bot threat intelligence rule to protect important endpoints against certain threats. This helps you minimize the negative impacts on the services.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Bot Management** tab, find the **Bot Threat Intelligence** section. Then, turn on**Status** and click **Settings**.

    **Note:** After the bot threat Intelligence function is enabled, all requests destined for your website are checked by the function. You can configure a Bot Management rule so that the requests that match the rule bypass the check. For more information, see [Configure a whitelist for Bot Management](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Bot Management.md).

    ![Bot Threat Intelligence](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0428549951/p96048.png)

6.  In the **Bot Threat Intelligence** rule list, find the threat intelligence library you want to use by **Intelligence Name**, and turn on **Status**.

    ![Bot threat intelligence rules](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0428549951/p96052.png)

    The following table lists the bot threat intelligence libraries that WAF supports.

    |Intelligence library|Description|
    |--------------------|-----------|
    |**Malicious Scanner Fingerprint Blacklist**|This library contains characteristics of common scanners.|
    |**Malicious Scanner IP Blacklist**|This library contains malicious IP addresses that are dynamically updated based on the source IP addresses of scan attacks detected on Alibaba Cloud.|
    |**Credential Stuffing IP Blacklist**|This library contains malicious IP addresses that are dynamically updated based on the source IP addresses of credential stuffing and brute-force attacks detected on Alibaba Cloud.|
    |**Fake Crawler Blacklist**|This library identifies crawlers that use the User-Agent of authorized search engines, such as BaiduSpider, to disguise as authorized programs. **Note:** Before you enable this library, make sure that you have configured a whitelist of crawlers. Otherwise, false positives may occur. For more information, see [Configure the allowed crawlers function](/intl.en-US/Website Protection Settings/Bot management/Set a threat intelligence rule to allow requests from specific crawlers.md). |
    |**Malicious Crawler Blacklist**|This library contains malicious IP addresses that are dynamically updated based on the source IP addresses of crawlers detected on Alibaba Cloud. This library is categorized into three severity levels: low, medium, and high. A higher severity indicates more IP addresses in the library and a higher false positive rate. **Note:** We recommend that you set up two-factor authentication, such as CAPTCHA and JavaScript verification, for the high-severity library.

In scenarios where two-factor authentication cannot be implemented, we recommend that you set threat intelligence rules based on the low-severity library. |
    |**IDC IP List**|This library contains IP addresses of public clouds and on-premises data centers, including Alibaba Cloud, Tencent Cloud, Meituan Open Services, and 21Vianet. Attackers typically use CIDR blocks of public clouds or on-premises data centers to deploy crawlers or as proxies to access sites. Regular users rarely access sites in this way.|

    After you enable the default rule, requests initiated from IP addresses in the threat intelligence library to any directory of the protected domain name trigger the **Monitor** action. This action allows the requests to the destination directories and records the events.

    If you need to modify the default rule, such as the protected URL or action, see the following step on how to customize a threat intelligence rule.

7.  Customize a threat intelligence rule.

    1.  Find the target rule and click **Edit** in the Actions column.

    2.  In the **Edit Intelligence** dialog box that appears, set the following parameters.

        ![Edit a bot threat intelligence rule](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0428549951/p96054.png)

        |Parameter|Description|
        |---------|-----------|
        |**Protected Path**|The **URL** that you want to protect, such as /abc, /login/abc, or forward slash \(/\) that indicates all directories. You also need to select a value for **Matching**. Valid values:        -   **Precise Match**: The destination URL must be an exact match of the protected URL.
        -   **Prefix Match**: The prefix of the destination URL matches the protected URL.
        -   **Regex Match**:The destination URL matches the specified regular expression.
You can click **Add Protected URL** to add more URLs. You can add up to 10 URLs. |
        |**Action**|The action to be performed after the match conditions of the rule are met. Valid values:         -   **Monitor**: allows the request to the destination directory and records the event.
        -   **Block**: blocks the request.
        -   **JavaScript Validation**: requires JavaScript verification. Requests are forwarded to the destination directory only after they pass the verification.
        -   **Captcha**: requires CAPTCHA verification on the client side. Requests are forwarded to the destination directory only after they pass the verification.

**Note:** CAPTCHA only supports synchronous requests. To verify asynchronous requests, such as Ajax requests, contact the Alibaba Cloud security team. If you cannot determine whether the protected URL supports CAPTCHA, we recommend that you create a custom protection policy, such as an ACL rule, to run a test. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).

        -   **Strict Captcha**: requires CAPTCHA verification on the client side. Requests are forwarded to the destination directory only after they pass the verification. CAPTCHA verification has a stricter standard to verify visitor identities. |

    3.  Click **Confirm**.


