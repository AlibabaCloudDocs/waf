# Enable Log Service for WAF

WAF integrates Log Service to provide the Log Service for WAF feature. This feature collects real-time logs of websites protected by WAF, allows you to query and analyze the collected log data, and displays results on dashboards. This feature meets the classified protection requirements and your website protection and operations requirements. This topic describes how to enable the Log Service for WAF feature.

-   A WAF instance is purchased. If the instance is a subscription WAF instance, the edition of the instance must be **Pro** or higher. For more information, see [Activate Alibaba Cloud WAF](/intl.en-US/Pricing/Subscription/Activate Alibaba Cloud WAF.md).
-   Log Service is activated.

    The first time you log on to the [Log Service console](https://sls.console.aliyun.com), activate Log Service as prompted.


## Enable Log Service for WAF for a subscription WAF instance

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Log Management** \> **Log Service**.

4.  On the **Log Service** page, click **Upgrade**.

    **Note:** If the Log Service for WAF feature is enabled, the **Upgrade** button is not displayed.

5.  On the Upgrade/Downgrade page, set **Access Log Service** to YES. Then, specify **Log Storage Period** and **Log Storage Size** based on your business requirements.

6.  Click **Buy Now** and complete the payment.

7.  Authorize WAF to access Log Service.

    If this is the first time you enable Log Service for WAF, you must authorize WAF to access Log Service. If you have already completed the authorization, skip this step.

    To authorize WAF to access Log Service, perform the following operations:

    1.  On the **Log Service** page, click **Authorize Now**.

        **Note:**

    2.  On the **Cloud Resource Access Authorization** page, click **Confirm Authorization Policy**.

        ![Cloud Resource Access Authorization](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4308101061/p21284.png)


Then, you can use the Log Service for WAF feature on the **Log Service** page. To use this feature, perform the following steps:

1.  On the Log Service page, turn on the Status switch of the domain name. This way, Log Service for WAF can collect and store the logs of the website that uses the domain name. For more information, see [Enable log collection](/intl.en-US/Log Management/Log service/Enable log collection.md).
2.  Query and analyze the collected logs. For more information, see [Enable log query](/intl.en-US/Log Management/Log service/Enable log query.md) and [Enable log analysis](/intl.en-US/Log Management/Log service/Enable log analysis.md).

## What to do next

[Enable log collection](/intl.en-US/Log Management/Log service/Enable log collection.md)

