---
keyword: [access control/throttling, custom protection policy, custom, rate limiting, access control, HTTP flood protection]
---

# Create a custom protection policy

After you add a website to Web Application Firewall \(WAF\), you can enable the custom protection policy feature to protect the website. This feature allows you to customize ACL rules based on precise match conditions and configure rate limiting. Custom protection policies can be tailored for different scenarios, such as hotlink protection and website backend protection. You can create custom protection rules as needed.

## Prerequisites

-   A WAF instance is purchased. For more information, see [Purchase a WAF instance](/intl.en-US/Billing and Service Activation/Subscription/Purchase a WAF instance.md).
-   Your website is added to WAF. For more information, see [Add websites](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).

## Background information

The custom protection policy feature is implemented by using custom protection rules. Custom protection rules include ACL rules and HTTP flood protection rules.

-   An ACL rule filters requests based on precise match conditions such as client IP addresses, request URLs, and common request headers.
-   An HTTP flood protection rule filters requests based on the precise match conditions and rate limiting you have configured.

## Limits

Subscription WAF instances have the following limits on custom protection policies.

|Specification|Description|Enterprise edition|Business edition|Pro edition|
|-------------|-----------|------------------|----------------|-----------|
|Number of custom protection rules|The maximum number of custom protection rules that you can create.|200|100|100|
|Advanced match fields|The advanced match fields other than IP addresses and URLs that you can specify in custom protection rules.|Supported|Supported|Not supported|
|Rate limiting|The rate limiting settings in a custom protection policy. The settings define an HTTP flood protection rule.|Supported|Supported|Not supported|
|Custom statistical objects|The custom statistical objects other than IP addresses and sessions that can be used to configure rate limiting.|Supported|Supported|Not supported|

按量付费开通的Web应用防火墙实例，其自定义防护策略功能有以下限制：

-   支持添加的自定义规则数量：100（条）。
-   高级匹配字段：必须在**Feature Settings**中开启**精确访问控制**的**高级防护**模式才能使用。
-   频率设置：必须在**Feature Settings**中开启**缓解CC攻击**的**高级防护**模式才能使用。
-   自定义统计对象：必须在**Feature Settings**中开启**自定义限速**后才能使用。

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf)[Web Application Firewall console](https://partners-yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Access Control/Throttling** tab and find the **Custom Protection Policy** section. Then, turn on **Status** and click **Settings**.

    ![Custom Protection Policy](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2628549951/p74272.png)

    **Note:** When the custom protection policy feature is enabled, all requests destined for your website are checked by the feature. You can configure a whitelist rule for Access Control/Throttling to allow requests that match the whitelist rule to bypass the check. For more information, see [Configure a whitelist for Access Control/Throttling](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Access Control/Throttling.md).

6.  Create a custom protection rule.

    1.  On the **Custom Protection Policy** page, click **Create Custom Rule**.

    2.  In the **Create Rule** dialog box, configure the following parameters.

        ![ACL](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2628549951/p74273.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule name**|The name of the rule that you want to create.|
        |**Matching Condition**|The match conditions of the rule. The rule is triggered only when match conditions are met. Click **Add rule** to add more match conditions. You can specify a maximum of five match conditions. If you specify multiple match conditions, the rule is triggered only after all the match conditions are met. For more information about match conditions, see [Fields in match conditions](/intl.en-US/Website Protection Settings/Fields in match conditions.md). |
        |**Rate Limiting**|Enables or disables rate limiting. WAF starts calculating the request rate only when match conditions are met. When you enable rate limiting, you must configure the parameters to collect statistics. ![HTTP flood protection](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2628549951/p74274.png)

For more information about rate limiting parameters, see [Rate limiting parameters](#table_p8w_f11_5h6). |
        |**Action**|The action to be performed after the rule is triggered. Valid values:         -   **Monitor**: triggers alerts but does not block requests.
        -   **Block**: blocks requests.
        -   **CAPTCHA**: redirects requests to another page to implement CAPTCHA verification.
        -   **Strict Captcha**: redirects requests to another page to implement strict CAPTCHA verification.
        -   **JavaScript Validation**: triggers JavaScript verification.
If you enable **Rate Limiting**, you must specify **TTL \(Seconds\)** during which the action takes effect.

**Note:** A certain latency may exist in the statistical process because WAF collects data from multiple servers in a cluster to calculate the request rate. |
        |**Protection Type**|The type of the rule. This parameter is automatically set based on the status of **Rate Limiting**.         -   If rate limiting is enabled, the value is set to **HTTP Flood Protection**.
        -   If rate limiting is disabled, the value is set to **ACL**. |

        The following table describes the rate limiting parameters.

        |Parameter|Description|
        |---------|-----------|
        |**Statistical Object**|The object based on which the request rate is calculated. Valid values:         -   **IP**: calculates the number of requests from a specific IP address.
        -   **Session**: calculates the number of requests transmitted over a specific session.
        -   **Custom-Header**: calculates the number of requests with the same specified header content.
        -   **Custom-Param**: calculates the number of requests with the same specified parameter content.
        -   **Custom-Cookie**: calculates the number of requests with the same specified cookie content. |
        |**Interval \(Seconds\)**|The time period during which the number of requests is calculated.|
        |**Threshold \(Occurrences\)**|The maximum number of requests that are allowed from the object during the specified time period. If this limit is exceeded, rate limiting is triggered.|
        |**Status Code**|The HTTP status code. After the detection logic takes effect, the number or percentage of the specified **Status Code** within the specified time period is calculated. Select either the amount or the percentage.         -   **Amount**: the maximum number of the specified HTTP status code.
        -   **Percentage \(%\)**: the maximum percentage of the requests for which the specified HTTP status code is returned in the total request. |
        |**Take Effect For**|The objects to which rate limiting is applied.         -   **Feature Matching Objects**
        -   **Applied Domains** |

    3.  Click **Save**.

    After a custom protection rule is created, it is automatically enabled. You can view, disable, modify, or delete the newly created rule in the rule list based on your business requirements.


## References

[Fields in match conditions](/intl.en-US/Website Protection Settings/Fields in match conditions.md)

