---
keyword: [Website protection, Web intrusion prevention, RegEx Protection Engine, Built-in rule groups, Common web attacks, Custom rule groups]
---

# Configure the RegEx Protection Engine

After you add a website to Web Application Firewall \(WAF\), the RegEx Protection Engine is enabled by default. The RegEx Protection Engine is based on built-in expert rule groups. It automatically protects the website against common application vulnerability attacks such as SQL injection, XSS cross-site, webshell upload, command injection, backdoor isolation, invalid file requests, path traversing, and common web attacks. You can adjust the protection policies of the RegEx Protection Engine as needed.

**Note:** This topic uses the new version of the WAF console released in January 2020. If the WAF instance was created before this date, see [Web application protection](/intl.en-US/User Guide (Unavailable Soon)/Website protection (old engines)/Web application protection.md).

## Prerequisites

-   A WAF instance is purchased. For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).
-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Web Security** tab, and find **RegEx Protection Engine** in the **Web Intrusion Prevention** module to set the following parameters.

    ![Web attack blocking](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3051583951/p73893.png)

    |Parameter|Description|
    |---------|-----------|
    |**Status**|Enable or disable the RegEx Protection Engine.|
    |**Mode**|Specify the action that is taken on attack requests when they are detected. Supported modes include:     -   **Block**: This mode blocks the attack requests.
    -   **Warn** : This mode only triggers alerts without blocking the requests. |
    |**Protection Rule Group**|Specify the detection rule group to be applied. Built-in rule groups and custom rule groups are supported. Built-in rule groups include the medium rule group, strict rule group, and loose rule group.     -   **Medium rule group**: This rule group detects common web application attacks and default applications in a standard way.
    -   **Strict rule group**: This rule group detects web application attacks such as path traversal, SQL injections and command executions in a strict way.
    -   **Loose rule group**: This rule group detects common web application attacks in a loose way. If you find a high false positive rate with the medium rule group or your business has a high amount of uncontrollable user input such as rich text editors and technical forums, we recommend that you select this rule group.
 Click **Settings** to go to the Protection Rule Group page. On this page you can create custom rule groups or select built-in rule groups as needed. For more information, see [t77901.md\#](/intl.en-US/Website Protection Settings/Customize protection rule groups.md). |
    |**Decoding Settings**|Specify the data formats that need to be decoded and analyzed by the RegEx Protection Engine. To ensure higher performance, the RegEx Protection Engine decodes and analyzes the request contents of all formats by default. If the RegEx Protection Engine blocks normal requests that contain contents of specified formats, you can cancel decoding the contents of the corresponding formats to reduce the false positive rate.

 Procedure

    1.  Unfold the configuration menu.

![Decoding settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4051583951/p73894.png)

    2.  Select or clear the target format to be decoded.
        -   The following formats must be decoded: URL decoding, JavaScript unicode decoding, hexadecimal decoding, comment processing, and space compression.
        -   The following formats are optional: multipart data parsing, JSON data parsing, XML data parsing, serialized PHP data decoding, HTML entity decoding, UTF-7 decoding, Base64 decoding, and form data parsing.
    3.  Click **Comfirm**. |


