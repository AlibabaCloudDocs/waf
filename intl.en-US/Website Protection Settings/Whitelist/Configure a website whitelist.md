---
keyword: [website protection, website whitelist]
---

# Configure a website whitelist

After you add a website to Web Application Firewall \(WAF\), you can configure a website whitelist to allow trusted access requests of the website to be directly routed to the origin server. Trusted access requests include requests from trusted vulnerability scan tools and trusted authenticated third-party system endpoints.

## Prerequisites

-   A WAF instance is purchased. For more information, see [t15539.md\#](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).
-   Your website is added to the WAF console. For more information, see [t63401.md\#](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

WAF provides multiple detection modules. If a website is added to WAF, all requests to this website are automatically detected by the modules that are enabled. To directly route trustworthy requests to your origin server, you can configure a website whitelist that allows the requests to bypass all detection modules of WAF.

You can also configure a whitelist for a specific detection module. This allows trusted access requests to bypass the detection of the specific detection module. You can configure the following types of whitelists:

-   [Whitelist for Web Intrusion Prevention](/intl.en-US/Website Protection Settings/Whitelist/Configure the web intrusion prevention whitelist.md): Trusted access requests are not detected by RegEx Protection Engine or Big Data Deep Learning Engine.
-   [Whitelist for Data Security](/intl.en-US/Website Protection Settings/Whitelist/Configure the data security whitelist.md): Trusted access requests are not detected by Data Leakage Prevention, Website Tamper-proofing, or Account Security.
-   [Whitelist for Bot Management](/intl.en-US/Website Protection Settings/Whitelist/Configure the bot management whitelist.md): Trusted access requests are not detected by Bot Threat Intelligence, Data Risk Control, Intelligent Algorithm, or App Protection.
-   [Whitelist for Access Control/Throttling](/intl.en-US/Website Protection Settings/Whitelist/Configure the access control and throttling whitelist.md): Trusted access requests are not detected by HTTP Flood Protection, IP Blacklist, Scan Protection, or Custom Protection Policy.

**Note:** We recommend that you create a whitelist for a specific detection module as required. A whitelist with more precise rules improves website security. A whitelist for a detection module provides better security protection than a website whitelist.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  In the upper-right corner, click **Website Whitelisting**.

6.  Create a website whitelist.

    1.  On the **Website Whitelisting** page, click **Create Rule**.

    2.  In the **Create Rule** dialog box, configure the following parameters.

        ![Website Whitelisting](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5412523061/p74249.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule name**|Specify a name for the rule.|
        |**Matching Condition**|Specify match conditions for the rule. Click **Add rule** to add more match conditions. A maximum of five match conditions are allowed. If you specify multiple match conditions, the rule is triggered only after all the match conditions are met. For more information about match conditions, see [t1851222.md\#](/intl.en-US/Website Protection Settings/Fields in match conditions.md). |

    3.  Click **Save**.

    After you create rules for the whitelist, the rules are automatically enabled. You can view created rules in the rule list. You can also disable, edit, or delete rules as required.


## References

[t1851222.md\#](/intl.en-US/Website Protection Settings/Fields in match conditions.md)

