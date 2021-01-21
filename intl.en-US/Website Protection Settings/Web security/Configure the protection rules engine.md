---
keyword: [website protection, web intrusion prevention, , protection rules engine, built-in rule groups, common web attacks, custom rule groups]
---

# Configure the protection rules engine

After you add a website to Web Application Firewall \(WAF\), the protection rules engine is enabled by default. The protection rules engine uses built-in rules that are developed based on specialized expertise. It automatically protects websites against common web attacks, such as SQL injections, XSS attacks, webshell uploads, command injections, backdoor isolations, invalid file requests, path traversals, and vulnerability exploits. You can adjust the protection policies of the protection rules engine based on your business requirements.

## Prerequisite

-   A WAF instance is purchased. For more information, see [Purchase a WAF instance](/intl.en-US/Billing and Service Activation/Subscription/Purchase a WAF instance.md).
-   Your website is added to WAF. For more information, see [Add websites](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Web Security** tab, find the **Protection Rules Engine** section, and configure the following parameters.

    ![Web application protection](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8958021161/p73893.png)

    |Parameter|Description|
    |---------|-----------|
    |**Status**|The status of the protection rules engine. By default, the protection rules engine is enabled after you add a website to WAF.**Note:** After the protection rules engine is enabled, all requests destined for the website are checked by the engine. You can configure a whitelist in the Web Intrusion Prevention section to allow the requests that meet the rule to bypass the check. For more information, see [Configure a whitelist for Web Intrusion Prevention](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Web Intrusion Prevention.md). |
    |**Mode**|The action on requests when WAF detects attacks. Valid values:     -   **Block**: blocks requests.
    -   **Warn**: triggers alerts but does not block requests. |
    |**Protection Rule Group**|The protection rule group that you want to apply. Built-in rule groups and custom rule groups are both supported. WAF provides the following built-in rule groups:    -   **Medium rule group**: detects common web application attacks in a standard way. This rule group is applied by default.
    -   **Strict rule group**: detects web application attacks, such as path traversals, SQL injections, and command injections, in a strict way.
    -   **Loose rule group**: detects common web application attacks in a loose way. If you encounter a high false positive rate when you apply the medium rule group or your business has a high amount of uncontrollable user input, such as rich text editors and technical forums, we recommend that you select this loose rule group.
You can click **Settings** to go to the **Protection Rule Group** page. On this page, you can create custom rule groups or select built-in rule groups based on your business requirements. For more information, see [Customize protection rule groups](/intl.en-US/Website Protection Settings/Customize protection rule groups.md). |
    |**Decoding Settings**|The data formats that you want the protection rules engine to decode and analyze. To ensure high performance, the protection rules engine decodes and analyzes the request data of all formats by default. If the protection rules engine blocks normal requests that contain data of specific formats, you can clear the formats to reduce the false positive rate.

Procedure

    1.  Unfold the configuration menu.

![Decoding Settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8958021161/p73894.png)

    2.  Select or clear the formats that you want to decode.
        -   The following formats cannot be cleared: **URL Decoding**, **JavaScript Unicode Decoding**, **Hex Decoding**, **Comment Processing**, and **Space Compression**.
        -   The following formats can be cleared: **Multipart Data Parsing**, **JSON Data Parsing**, **XML Data Parsing**, **Serialized PHP Data Decoding**, **HTML Entity Decoding**, **UTF-7 decoding**, **Base64 Decoding**, and **Form Data Parsing**.
    3.  Click **Confirm**. |


## References

[Best practices for using RegEx Protection Engine](/intl.en-US/Website Protection Settings/Best practices for protection settings/Best practices for using RegEx Protection Engine.md)

