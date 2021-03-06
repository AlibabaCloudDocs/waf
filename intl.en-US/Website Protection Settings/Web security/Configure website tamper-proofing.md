---
keyword: [web protection, data security, website tamper-proofing, tamper, cache, replace]
---

# Configure website tamper-proofing

After you add a website to Web Application Firewall \(WAF\), you can enable the website tamper-proofing function to protect the website from website defacement. Website tamper-proofing helps you lock specific web pages, such as those that contain sensitive information. When a locked web page is requested, the page cached in WAF is returned. This prevents web pages from being maliciously modified. You can customize website tamper-proofing rules as needed.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.

        -   If the instance is deployed in **mainland China**, the instance must be of the **Pro** edition or higher.
        -   If the instance is deployed **outside mainland China**, the instance must be of the **Enterprise** edition or higher.
        For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).

    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Web Security** tab and find the **Website Tamper-proofing** section. Then, turn on **Status** and click **Settings**.

    **Note:**

    -   You must enable website tamper-proofing before you create protection rules.
    -   After website tamper-proofing is enabled, all requests destined for your website are checked by the function. You can configure a Data Security rule so that the requests that match the rule bypass the check. For more information, see [Configure a whitelist for Data Security](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Data Security.md).
    ![Website Tamper-proofing](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5228549951/p74083.png)

6.  Create a tamper-proofing rule.

    1.  On the **Website Tamper-proofing** page, click **Add Rule**.

    2.  In the **Add Rule** dialog box, specify the **Service Name** and **URL** parameters of the web page that you want to protect.

        -   **Service Name**: Specify the name of the service that the web page provides.
        -   **URL**: Enter an exact path. Wildcard characters such as `/*`, or parameters such as `/abc? xxx=` are not supported. Text data, HTML pages, and images under the specified path are protected.
        ![Create Rule](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5228549951/p74084.png)

    3.  Click **Confirm**.

    After a tamper-proofing rule is created, it is disabled by default. You can find the newly created rule in the rule list and **Protection Status** of the rule is turned off.

    ![Protection status-disabled](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5228549951/p74085.png)

7.  Enable the rule. Find the rule you want to enable in the rule list and turn on **Protection Status**.

    ![Protection status-enabled](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5228549951/p74086.png)

    After the rule is enabled, if the specified web page is requested, the page cached in WAF is returned.

8.  Update cached data. Find the rule that is enabled in the rule list and click **Refresh Cache** in the **Protection Status** column.

    **Note:** If the protected web page is updated, you must click **Refresh Cache** to update the data cached in WAF. If you do not update the cached data after a page is updated, WAF returns the most recent page stored in the cache.


