---
keyword: [web protection, positive security model, advanced protection, machine learning, custom policy]
---

# Configure the positive security model

After you add a website to Web Application Firewall \(WAF\), you can enable the positive security model for your website. To protect the website against unknown attacks, the positive security model of WAF uses Alibaba Cloud machine learning algorithms to automatically learn normal network traffic of a website. The positive security model then generates security rules customized for the website based on the collected data. You can adjust the protection mode and rules of the positive security model based on your requirements.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   The instance is deployed in **mainland China**.

        **Note:** WAF instances deployed **outside mainland China** do not support positive security models.

    -   The instance must be of the **Enterprise** edition or higher. For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).
    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

Traditional protection methods against web attacks are based on detection rules. The positive security model automatically learns the network traffic of a website and uses machine learning algorithms to generate a standard security score and grade different requests. Based on the request scores, the positive security model defines the baseline traffic of a website and customizes security policies for the website. To offer the website more powerful protection, the positive security model collaborates with other detection modules of WAF to detect attacks at different network layers.

![Positive Security Model](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3328549951/p53450.png)

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch domain name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  On the **Web Security** tab, specify the following parameters in the**Positive Security Model** card of the **Advanced protection** section.

    ![Positive Security Model](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3328549951/p74264.png)

    |Parameter|Description|
    |---------|-----------|
    |**Status**|Enable or disable the positive security model.|
    |**Mode**|Specify the action that is taken on attack requests when they are detected. Valid values:     -   **Warn**: triggers alerts but does not block requests.
    -   **Block**: blocks requests.
**Note:** By default, the positive security model is set to the warn mode. In this mode, WAF only reports requests that match the security rules but does not block the requests. We recommend that you study the data in security reports to make sure that the security rule does not cause false positives before you set the mode to Block. |

    If this is your first time enabling the positive security model for a website, WAF automatically learns the network traffic history of the website based on machine learning algorithms. WAF then customizes security rules to protect the website. The initial machine learning process may take a long time to complete based on the total amount of network traffic data. In most cases, it takes about one hour for WAF to learn the network traffic history of the website and generate security rules. After WAF completes the learning process, it notifies you by using internal messages, text messages, and emails.


