---
keyword: [Website protection, Web intrusion prevention, Whitelist, RegEx Protection engine, Big data deep learning engine, Web applications, Protection, Security]
---

# Configure the web intrusion prevention whitelist

For websites added to Web Application Firewall \(WAF\), web intrusion prevention responds quickly to common web attacks and zero-day vulnerabilities to secure your websites. Web intrusion prevention supports the RegEx Protection engine and the big data deep learning engine. You can configure the web intrusion prevention whitelist. Requests that match specific conditions in the whitelist can skip specified detection modules.

**Note:** This topic uses the new version of the WAF console released in January 2020. If the WAF instance was created before this date, you cannot to use the web intrusion prevention whitelist.

## Prerequisites

-   A WAF instance is purchased. For more information, see [Activate Alibaba Cloud WAF](/intl.en-US/Pricing/Subscription/Activate Alibaba Cloud WAF.md).
-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

The web intrusion prevention whitelist is generally used to allow access requests that are mistakenly blocked. We recommend that you set the match conditions as precisely as possible to ensure that only the specific access requests are allowed.

For more information about supported detection modules of web intrusion prevention, see:

-   [Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web intrusion prevention/Configure the RegEx Protection Engine.md)
-   [Configure the Big Data Deep Learning Engine](/intl.en-US/Website Protection Settings/Web intrusion prevention/Configure the Big Data Deep Learning Engine.md)

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch domain name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Web Security** tab, find the **Web Intrusion Prevention** section, and then click **Settings**.

6.  Create the web intrusion prevention whitelist.

    1.  On the **Web Intrusion Prevention - Whitelisting** page, click **Create Rule**.

    2.  In the **Add Rule** dialogue box, set the following parameters.

        ![Add a rule, web intrusion prevention, whitelist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8128549951/p74254.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule name**|Specify a name for the rule.|
        |**Matching Condition**|Specify the match conditions of the whitelist rule. Click **Add rule** to add more conditions. You can specify a maximum of five conditions. If you have set multiple conditions, the rule is matched only after all of them are met. For more information about match conditions, see [Fields of match conditions](/intl.en-US/Website Protection Settings/Fields of match conditions.md). |
        |**Modules Bypassing Check**|Specify the detection modules to be ignored after the match conditions of the rule are matched. Supported modules include:         -   **Web Attack Protection**
        -   **Deep Learning** |

    3.  Click **Save**.

    After you create rules for the web intrusion prevention whitelist, they are enabled automatically. You can view newly created rules in the rule list and disable, edit, or delete rules as needed.

    ![The web intrusion prevention whitelist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8128549951/p96139.png)


