---
keyword: [bot management, allowed crawler, allow]
---

# Configure the allowed crawlers function

The allowed crawlers function maintains a whitelist of authorized search engines, such as Google, Bing, Baidu, Sogou, 360, and Yandex. The crawlers of these search engines are allowed to access all pages on domain names.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   **Bot Management** is enabled. This feature is a value-added service.
    For more information, see [Purchase a WAF instance](/intl.en-US/Billing and Service Activation/Subscription/Purchase a WAF instance.md).

-   Your website is added to WAF. For more information, see [Add websites](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).

## Background information

Rules defined in the function allow requests from specific crawlers to the target domain name based on the Alibaba Cloud crawler library. The Alibaba Cloud crawler library is updated in real time based on the analysis of network traffic that flows through Alibaba Cloud, and captures the characteristics of requests that are initiated from crawlers. The crawler library is updated dynamically and contains crawler IP addresses of mainstream search engines, including Google, Baidu, Sogou, 360, Bing, and Yandex.

After you enable the allowed crawlers function, requests initiated from the crawler IP addresses of the authorized search engines are directly sent to the target domain names. The bot management module no longer detects these requests.

**Note:** To filter some requests from the crawler IP addresses, use the **Access Control/Throttling** module. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Bot Management** tab, find the **Allowed Crawlers** section. Then, turn on **Status** and click **Settings**.

    ![Allowed Crawlers](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8328549951/p96043.png)

6.  In the **Allowed Crawlers** list, find the target rule by **Intelligence Name**, and turn on **Status**.

    ![Set a rule to allow requests from specific crawlers](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8328549951/p96049.png)

    The default rules only allow crawler requests from the following search engines: Google, Bing, Baidu, Sogou, 360, and Yandex. You can enable the **Legit Crawling Bots** rule to allow requests from all search engine crawlers.


