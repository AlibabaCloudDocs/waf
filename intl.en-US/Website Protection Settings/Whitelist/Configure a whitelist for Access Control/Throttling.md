---
keyword: [website protection, Access Control/Throttling, whitelist, HTTP Flood Protection, IP Blacklist, Scan Protection, Custom Protection Policy]
---

# Configure a whitelist for Access Control/Throttling

After you add a website to Web Application Firewall \(WAF\), you can configure a whitelist for Access Control/Throttling to allow trusted access requests of the website to bypass the detection of HTTP Flood Protection, IP Blacklist, Scan Protection, and Custom Protection Policy. This whitelist is used to allow access requests that are blocked by mistake.

## Prerequisites

-   A WAF instance is purchased. For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).
-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

Access Control/Throttling provides custom access control policies and traffic management policies at the application layer to ensure website accessibility. It provides the following detection modules:

-   [HTTP Flood Protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md)
-   [IP Blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure a blacklist.md)
-   [Scan Protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md)
-   [Custom Protection Policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)

After the preceding detection modules are enabled, normal access requests may be blocked by mistake. In this case, you can configure a whitelist to allow trusted access requests to bypass the detection of a specific module in Access Control/Throttling.

We recommend that you specify rules for the whitelist as precisely as possible to ensure that only trusted access requests are allowed.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Access Control/Throttling** tab, find the **Access Control/Throttling** section, and then click **Settings**.

6.  Create a whitelist for Access Control/Throttling.

    1.  On the **Access Control/Throttling - Whitelisting** page, click **Create Rule**.

    2.  In the **Create Rule** dialog box, configure the following parameters.

        ![Access Control/Throttling - Whitelisting](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2122523061/p74268.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule name**|Specify a name for the rule.|
        |**Matching Condition**|Specify match conditions for the rule. Click **Add rule** to add more match conditions. A maximum of five match conditions are allowed. If you specify multiple match conditions, the rule is triggered only after all the match conditions are met. For more information about match conditions, see [Fields in match conditions](/intl.en-US/Website Protection Settings/Fields in match conditions.md). |
        |**Modules Bypassing Check**|Select the detection modules to bypass after the match conditions are met. Valid Values:         -   **HTTP Flood Protection**
        -   **Custom Rules**
        -   **IP Blacklist**
        -   **Anti-Scan** |

    3.  Click **Save**.

    After you create rules for the whitelist, the rules are automatically enabled. You can view created rules in the rule list. You can also disable, edit, or delete rules as required.


## References

[Fields in match conditions](/intl.en-US/Website Protection Settings/Fields in match conditions.md)

