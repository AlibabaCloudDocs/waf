---
keyword: [Web Application Firewall, WAF, website protection, IP address blacklist, access control and throttling, region-based IP address blacklist]
---

# Configure an IP address blacklist

After you add a website to Web Application Firewall \(WAF\), you can enable the IP address blacklist feature. The IP address blacklist blocks the access requests from specified IP addresses and CIDR blocks. It also blocks the access requests from specified regions. You can specify the IP address blacklist and region-based IP address blacklist based on your requirements.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.

        To use the **region-based IP address blacklist** feature, make sure that your WAF instance is of the **Business** edition or higher. If your WAF instance is of the **Pro** edition or lower, you can use only the **IP address blacklist** feature.

        For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).

    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

WAF supports the IP address blacklist and the region-based IP address blacklist.

-   The IP address blacklist blocks the access requests from specified IP addresses and CIDR blocks.
-   The region-based IP address blacklist blocks the access requests from specified regions inside or outside China. You can specify a total of 247 regions inside and outside China as blocked regions.

    You can use the IP address library of Taobao to query the source region of the IP address. For more information, visit the [IP address library of Taobao](http://ip.taobao.com/).


## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch domain name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  On the **Access Control/Throttling** tab, find the **IP Blacklist** card. Turn on **Status** and click **Settings**.

    ![IP address blacklist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5528549951/p73946.png)

6.  On the **IP Blacklist** page, specify the parameters in the **IP Blacklist** and **Area-based IP Blacklist** sections.

    -   **IP Blacklist**: Enter the IP addresses that you want to block and click **Save** in the lower part of the page. Separate multiple IP addresses with commas \(,\). You can add a maximum of 200 IP addresses.

        ![IP address blacklist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5528549951/p73978.png)

    -   **Area-based IP Blacklist**: Select the regions that you want to block from the **Inside China** and **Outside China** tabs. Then, click **Save** in the lower part of the page.

        ![Region-based IP address blacklist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5528549951/p73979.png)

    After you turn on Status, all the access requests from blocked regions are blocked.


## Related operations

-   If you need more precise access control based on the IP address blacklist, we recommend that you use the custom protection policy. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).
-   If you want to allow access requests from a specified IP address, we recommend that you configure the access control policy or throttling whitelist. For more information, see [Configure the access control and throttling whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the access control and throttling whitelist.md).

