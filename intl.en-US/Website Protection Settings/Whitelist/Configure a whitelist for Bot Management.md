---
keyword: [website protection, Bot Management, Bot Threat Intelligence, Data Risk Control, Intelligent Algorithm, App Protection]
---

# Configure a whitelist for Bot Management

After you add a website to Web Application Firewall \(WAF\), you can configure a whitelist for Bot Management to allow trusted access requests of the website to bypass the detection of Bot Threat Intelligence, Data Risk Control, Intelligent Algorithm, and App Protection. This whitelist is used to allow access requests that are blocked by mistake.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   **Bot Management** is enabled. This feature is a value-added service.
    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

Bot Management protects web applications, native applications, and APIs from malicious crawlers. It provides the following detection modules:

-   [Allowed Crawlers](/intl.en-US/Website Protection Settings/Bot management/Set a threat intelligence rule to allow requests from specific crawlers.md)
-   [Bot Threat Intelligence](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md)
-   [Data Risk Control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md)
-   [App Protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md)
-   Intelligent Algorithm

After the preceding detection modules but Allowed Crawlers are enabled, normal access requests may be blocked by mistake. In this case, you can configure a whitelist to allow trusted access requests to bypass the detection of a specific module in Bot Management.

We recommend that you specify rules for the whitelist as precisely as possible to ensure that only trusted access requests are allowed.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Bot Management** tab, find the **Bot Management** section, and then click **Settings**.

6.  Create a whitelist for Bot Management.

    1.  On the **Bot Management - Whitelist** page, click **Create Rule**.

    2.  In the **Create Rule** dialog box, configure the following parameters.

        ![Bot Management - Whitelist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3212523061/p96029.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule name**|Specify a name for the rule.|
        |**Matching Condition**|Specify match conditions for the rule. Click **Add rule** to add more match conditions. A maximum of five match conditions are allowed. If you specify multiple match conditions, the rule is triggered only after all the match conditions are met. For more information about match conditions, see [Fields in match conditions](/intl.en-US/Website Protection Settings/Fields in match conditions.md). |
        |**Modules Bypassing Check**|Select the detection modules to bypass after the match conditions are met. Valid Values:         -   **Bot Threat Intelligence**
        -   **Data Risk Control**
        -   **Algorithm Model**
        -   **App Protection** |

    3.  Click **Save**.

    After you create rules for the whitelist, the rules are automatically enabled. You can view created rules in the rule list. You can also disable, edit, or delete rules as required.


## References

[Fields in match conditions](/intl.en-US/Website Protection Settings/Fields in match conditions.md)

