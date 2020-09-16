---
keyword: [Website protection, Data security, Website tamper-proofing, Data leakage prevention, Response, Integrity, Confidentiality]
---

# Configure the data security whitelist

The data security feature prevents the content of web pages protected by Web Application Firewall \(WAF\) from being leaked or modified. This feature helps you maintain data integrity and confidentiality. Data security supports website tamper-proofing and data leakage prevention. You can configure the data security whitelist to have specific requests skip specified detection modules.

**Note:** This topic uses the new version of the WAF console released in January 2020. If your WAF instance was created before January 2020, you cannot use the data security whitelist.

## Prerequisites

-   A WAF instance is purchased. For more information, see [Activate Alibaba Cloud WAF](/intl.en-US/Pricing/Subscription/Activate Alibaba Cloud WAF.md).
-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

For more information about detection modules supported by data security, see the following topics:

-   [Configure tamper-proofing](/intl.en-US/Website Protection Settings/Web intrusion prevention/Configure tamper-proofing.md)
-   [Configure data leakage prevention](/intl.en-US/Website Protection Settings/Web intrusion prevention/Configure data leakage prevention.md)

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch domain name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Web Security** tab, find the **Data Security** section, and then click **Settings**.

6.  Create a data security whitelist.

    1.  On the **Data Risk Control - Whitelisting** page, click **Create Rule**.

    2.  In the **Add Rule** dialog box that appears, set the following parameters.

        ![Data security, whitelist, create a rule](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2228549951/p74270.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule name**|Specify a name for the rule.|
        |**Matching Condition**|Specify the match conditions of the whitelist rule. Click **Add rule** to add more conditions. You can specify a maximum of five conditions. If you have specified multiple conditions, the rule is matched only after all the specified conditions are met. For more information about match conditions, see [Fields of match conditions](/intl.en-US/Website Protection Settings/Fields of match conditions.md). |
        |**Modules Bypassing Check**|Valid values:         -   **Data Leakage Prevention**
        -   **Website Tamper-proofing**
        -   **Account Security** |

    3.  Click **Save**.

    After a whitelist rule is created, it is automatically enabled. You can view newly created rules, and disable, modify, or delete rules as needed.

    ![Data security-whitelist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2228549951/p96145.png)


