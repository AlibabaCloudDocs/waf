---
keyword: [website protection, web intrusion prevention, , RegEx Protection Engine, built-in rule groups, common web attacks, custom rule groups]
---

# Configure the RegEx Protection Engine

After you add a website to Web Application Firewall \(WAF\), the RegEx Protection Engine is enabled by default. The RegEx Protection Engine is based on built-in expert rule groups. It automatically protects the website against common application vulnerability attacks such as SQL injection, XSS cross-site, webshell upload, command injection, backdoor isolation, invalid file requests, path traversing, common web attacks. You can adjust the protection policies of the RegEx Protection Engine as needed.

## Prerequisite

-   A WAF instance is purchased. For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).
-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Web Security** tab, find the **RegEx Protection Engine** section, and then configure the following parameters.

    ![Web Application Protection](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3051583951/p73893.png)

    |Parameter|Description|
    |---------|-----------|
    |**Status**|Enable or disable the RegEx Protection Engine. By default, the RegEx Protection Engine is enabled after you add a website to WAF.**Note:** After the RegEx Protection Engine is enabled, all requests destined for the website are checked by the function. You can configure a Web Intrusion Prevention rule so that requests that meet the rule bypass the check. For more information, see [Configure a whitelist for Web Intrusion Prevention](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Web Intrusion Prevention.md). |
    |**Mode**|The action that is taken on attack requests when they are detected. Valid values:     -   **Block**: blocks requests.
    -   **Warn**: triggers alerts but does not block the attack requests. |
    |**Protection Rule Group**|The protection rule group you want to use. Built-in rule groups and custom rule groups are supported. Built-in rule groups include:    -   **Medium rule group**: This rule group detects common web application attacks and default applications in a standard way. This rule group is applied by default.
    -   **Strict rule group**: This rule group detects web application attacks such as path traversal, SQL injections, and command executions in a strict way.
    -   **Loose rule group**: This rule group detects common web application attacks in a loose way. If you find a high false positive rate with the medium rule group or your business has a high amount of uncontrollable user input such as rich text editors and technical forums, we recommend that you select this rule group.
Click **Settings** to go to the **Protection Rule Group** page. On this page you can create custom rule groups or select built-in rule groups as needed. For more information, see [Customize protection rule groups](/intl.en-US/Website Protection Settings/Customize protection rule groups.md). |
    |**Decoding Settings**|The data formats that need to be decoded and analyzed by the RegEx Protection Engine. To ensure higher performance, the RegEx Protection Engine decodes and analyzes the request content of all formats by default. If the RegEx Protection Engine blocks normal requests that contain content of specified formats, you can clear the format to reduce the false positive rate.

Procedure

    1.  Unfold the configuration menu.

![Decoding Settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4051583951/p73894.png)

    2.  Select or clear the format that you want to decode.
        -   You cannot clear the following formats: **URL Decoding**, **JavaScript Unicode Decoding**, **Hex Decoding**, **Comment Processing**, and **Space Compression**.
        -   You can clear the following format: **Multipart Data Parsing**, **JSON Data Parsing**, **XML Data Parsing**, **Serialized PHP Data Decoding**, **HTML Entity Decoding**, **UTF-7 decoding**, **Base64 Decoding**, and **Form Data Parsing**.
    3.  Click **Confirm**. |


