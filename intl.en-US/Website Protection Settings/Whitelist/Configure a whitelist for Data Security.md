---
keyword: [website protection, Data Security, Website Tamper-proofing, Data Leakage Prevention, Account Security]
---

# Configure a whitelist for Data Security

After you add a website to Web Application Firewall \(WAF\), you can configure a whitelist for Data Security to allow trusted access requests of the website to bypass the detection of Website Tamper-proofing, Data Leakage Prevention, and Account Security. This whitelist is used to allow access requests that are blocked by mistake.

## Prerequisites

-   A WAF instance is purchased. For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).
-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

Data Security protects your website against page content leaks and tampering to ensure the integrity and confidentiality of website data. It provides the following detection modules:

-   [Website Tamper-proofing](/intl.en-US/Website Protection Settings/Web security/Configure Website Tamper-proofing.md)
-   [Data Leakage Prevention](/intl.en-US/Website Protection Settings/Web security/Configure data leakage prevention.md)
-   [Account Security](/intl.en-US/Protection Lab/Configure account security.md)

After the preceding detection modules are enabled, normal access requests may be blocked by mistake. In this case, you can configure a whitelist to allow trusted access requests to bypass the detection of a specific module in Data Security.

We recommend that you specify rules for the whitelist as precisely as possible to ensure that only trusted access requests are allowed.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Web Security** tab, find the **Data Security** section, and then click **Settings**.

6.  Create the whitelist for Data Security.

    1.  On the **Data Risk Control - Whitelisting** page, click **Create Rule**.

    2.  In the **Create Rule** dialog box, configure the following parameters.

        ![Data Security Control - Whitelisting](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4022523061/p74270.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule name**|Specify a name for the rule.|
        |**Matching Condition**|Specify match conditions for the rule. Click **Add rule** to add more match conditions. A maximum of five match conditions are allowed. If you specify multiple match conditions, the rule is triggered only after all the match conditions are met. For more information about match conditions, see [Fields in match conditions](/intl.en-US/Website Protection Settings/Fields in match conditions.md). |
        |**Modules Bypassing Check**|Select the detection modules to bypass after the match conditions are met. Valid Values:         -   **Data Leakage Prevention**
        -   **Website Tamper-proofing**
        -   **Account Security** |

    3.  Click **Save**.

    After you create rules for the whitelist, the rules are automatically enabled. You can view created rules in the rule list. You can also disable, edit, or delete rules as required.


## References

[Fields in match conditions](/intl.en-US/Website Protection Settings/Fields in match conditions.md)

