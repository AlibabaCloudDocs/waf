# Purchase a WAF instance

This topic describes how to purchase a Web Application Firewall \(WAF\) instance.

## Background information

WAF supports the subscription billing method. To purchase a subscription WAF instance, you must select an edition based on your requirements. Different editions have different protection features and specifications. For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).

## Procedure

1.  Go to the [Web Application Firewall buy page](https://common-buy-intl.alibabacloud.com/?commodityCode=waf_intl#/buy) by using your Alibaba Cloud account.

2.  On the **Web Application Firewall** buy page, configure the following parameters.

    ![WAF buy page](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0869177951/p130125.png)

    |Parameter|Description|
    |---------|-----------|
    |**Region**|Specify the region where the WAF cluster resides. Valid values:     -   **China Mainland**: regions in mainland China.
    -   **International**: regions outside mainland China, including China \(Hong Kong\), Singapore \(Singapore\), Malaysia \(Kuala Lumpur\), US \(Silicon Valley\), Australia \(Sydney\), Germany \(Frankfurt\), India \(Mumbai\), Indonesia \(Jakarta\), UAE \(Dubai\), and Japan \(Tokyo\). |
    |**Plan**|Specify the edition of WAF that you want to purchase. Valid values:     -   **Pro**

**Note:** This edition does not support **Access Log Service**.

    -   **Business**
    -   **Enterprise**
After you select an edition, the **Specification** section displays the details about the selected edition. For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md). |
    |**Extra Domain**|Enter the number of extra domain name packages that you want to purchase. If you want to add multiple domain names or more than 10 subdomains to WAF, we recommend that you purchase extra domain name packages. For more information, see [Extra domain name packages](/intl.en-US/Pricing/Subscription/Extra domain quota.md). |
    |**Exclusive IP**|Enter the number of exclusive IP addresses that you want to purchase for WAF. You can purchase an exclusive IP address and assign it to a specific domain name. For more information, see [Exclusive IP addresses](/intl.en-US/Pricing/Subscription/Exclusive IP addresses.md). |
    |**Extra Traffic**|Specify the extra bandwidth in Mbit/s. If the total bandwidth of your websites exceeds the service bandwidth of WAF, we recommend that you purchase extra bandwidth. For more information, see [Extra bandwidth](/intl.en-US/Pricing/Subscription/Extra bandwidth.md). |
    |**GSLB**|Determine whether to enable intelligent load balancing. You can enable intelligent load balancing for your services to meet the high availability and low latency requirements of automatic disaster recovery. For more information, see [Intelligent load balancing](/intl.en-US/Pricing/Subscription/Intelligent load balancing.md). |
    |**Access Log Service**|Determine whether to activate Log Service for WAF. You can enable Log Service for WAF to store, view, and analyze WAF logs in real time. For more information, see [Log Service for WAF](/intl.en-US/Log Management/Log service/Overview.md).

**Note:** The **Pro** edition does not support this option. |
    |**Log Storage Period**|Specify the period for which you want to store WAF logs. Valid values: **180 Days** and **360 Days**. **Note:** The **Pro** edition does not support this option. |
    |**Log Storage Size**|Specify the maximum size of stored logs after you set Access Log Service to YES.**** Valid values: **3T**, **5T**, **10T**, **15T**, **20T**, **25T**, and **50T**. **Note:** The **Pro** edition does not support this option. |
    |**Bot Manager**|Determine whether to enable the bot management feature. To mitigate security threats caused by bot traffic, you can enable this feature. For more information, see [Set a bot threat intelligence rule](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md) and [Set a threat intelligence rule to allow requests from specific crawlers](/intl.en-US/Website Protection Settings/Bot management/Set a threat intelligence rule to allow requests from specific crawlers.md).

**Note:** The bot management feature is available for only the new protection engine of WAF. If you enable this feature by upgrading the existing WAF instance, make sure that you have upgraded to the new protection engine. For more information, see [Protection engine upgrade](/intl.en-US/Announcements & Updates/Protection engine upgrade.md).

Submit a [ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80) and apply to upgrade the protection engine if you enabled the bot management feature but did not upgrade your WAF instance to the new protection engine. |
    |**Mobile App Protection**|Determine whether to enable the app protection feature. If your website service is built on the native apps and you have security needs, such as the need for trusted communications and the prevention of bot script abuse, you can enable this feature. For more information, see [Configure application protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md).

**Note:** This feature is available only for the new protection engine of WAF. If you enable this feature by upgrading the existing WAF instance, make sure that you have upgraded to the new protection engine. For more information, see [Protection engine upgrade](/intl.en-US/Announcements & Updates/Protection engine upgrade.md).

Submit a [ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80) and apply to upgrade the protection engine if you enabled the Mobile App Protection feature but did not upgrade your WAF instance to the new protection engine. |
    |**Validity Period**|Specify a validity period for the WAF instance.|

3.  Click **Buy Now** and complete the payment.

    **Note:** WAF does not provide the 5-day money-back guarantee or partial refunds.


