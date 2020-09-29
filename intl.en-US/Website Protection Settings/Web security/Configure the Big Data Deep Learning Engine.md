---
keyword: [web protection, web intrusion prevention, , Big Data Deep Learning Engine, artificial intelligence, malicious attack samples, repeated learning]
---

# Configure the Big Data Deep Learning Engine

After you add a website to Web Application Firewall \(WAF\), you can enable the Big Data Deep Learning Engine for your website. The Big Data Deep Learning Engine is based on the deep neural network system of Alibaba Cloud. It performs classification training on all web attack data and normal business data in the cloud. This way, potential attacks can be blocked in real time. You can adjust the protection policies of the Big Data Deep Learning Engine based on your requirements.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   The instance is deployed in **mainland China**.

        **Note:** Instances that are deployed **outside mainland China** do not support the Big Data Deep Learning Engine.

    -   The instance must be of the **Business** edition or higher. For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).
    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

Web attack methods keep evolving as the Internet develops. Traditional single-method protection no longer meets the security requirements of complex Internet services. Collaborative protection that uses multiple detection engines is more powerful.

Based on massive operations data of Alibaba Cloud, the Big Data Deep Learning Engine trains models for normal web applications and identifies abnormalities from these models. It also refines attack models from various web application attacks. The Big Data Deep Learning Engine uses these models to detect zero-day vulnerabilities. It also blocks potential attacks online in real time to make up for the deficiencies of other protection engines. When WAF is used to prevent web attacks, protected traffic is forwarded to the RegEx Protection Engine. Then, the traffic is forwarded to the Big Data Deep Learning Engine. The two engines complement each other.

## Scenarios

The Big Data Deep Learning Engine is used to block web requests with weak attack characteristics rather than HTTP flood attacks. If you have more precise requirements on web attack protection, we recommend that you enable the Big Data Deep Learning Engine.

The RegEx Protection Engine uses strong regular expression rules. It provides optimal protection against requests with strong attack characteristics. The RegEx Protection Engine may fail to detect potential risks from requests with weak attack characteristics, such as cross-site scripting \(XSS\) attacks. It may also fail to detect these attacks even in strict mode. In this case, you can enable the Big Data Deep Learning Engine to identify and block requests with weak attack characteristics that cannot be detected based on strict rules of the RegEx Protection Engine.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch domain name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  On the **Web Security** tab, specify the following parameters in the **Big Data Deep Learning Engine** card of the **Web Intrusion Prevention** section.

    ![Big Data Deep Learning Engine](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p73903.png)

    |Parameter|Description|
    |---------|-----------|
    |**Status**|Enable or disable the Big Data Deep Learning Engine.|
    |**Mode**|Specify the action that is taken on attack requests when they are detected. Valid values:    -   **Block**: blocks requests.
    -   **Warn**: triggers alerts but does not block requests. |
    |**Attack Probability**|Set the threshold of the probability that a request is identified as an attack under deep learning. The value is an integer ranging from 50 to 100.If the parameter value is large, the standard for determining that a request is an attack is strict, and the Big Data Deep Learning Engine blocks real attacks more accurately. However, the engine may also leave more potential risks unblocked.

If the parameter value is small, the standard for determining that a request is an attack is not strict, and the Big Data Deep Learning Engine blocks more suspicious requests. However, the engine may also block some normal requests. |


