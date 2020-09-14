---
keyword: [website protection, data security, data leakage prevention, block HTTP status code, sensitive information, blur, data masking]
---

# Configure data leakage prevention

After you set up Web Application Firewall \(WAF\) for a website, you can enable data leakage prevention for the website. Data leakage prevention helps websites filter content \(abnormal pages and keywords\) returned from the servers, and mask sensitive information, such as identity card numbers, bank card numbers, phone numbers, and sensitive words. WAF then returns masked information or default response pages denying access to visitors. You can customize data leakage prevention rules as needed.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.

        -   If the instance is deployed in **mainland China**, the instance must be the **Pro** edition or higher.
        -   If the instance is deployed **outside mainland China**, the instance must be the **Business** edition or higher.
        For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).

    For more information, see [Activate Alibaba Cloud WAF](/intl.en-US/Pricing/Subscription/Activate Alibaba Cloud WAF.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

WAF provides the data leakage prevention feature to comply with the following regulations required by Cybersecurity Law of the People's Republic of China: Network operators shall adopt technological and other necessary measures to ensure the security of personal information they collect, and prevent information leaks, damage or loss. Where a situation of information leakage, damage or loss occurs, or might occur, they shall promptly take remedial measures, timely notify users and report the matter to the authority according to regulations. Data leakage prevention masks sensitive information \(phone numbers, identity card numbers, and bank card numbers\) in website content and triggers alerts upon sensitive information. You can also use data leakage prevention to block a specific HTTP status code.

Features

Information maintained by a website may be leaked in the following scenarios: allowing unauthorized access to a URL, such as access to the backend management system, horizontal and vertical privilege escalation, and malicious crawlers retrieving sensitive information from web pages. To prevent common sensitive information leaks, data leakage prevention provides the following functions:

-   Detects and identifies personal information on web pages, masks the information, and triggers alerts to protect website data. Personal information includes but is not limited to identity card numbers, phone numbers, and bank card numbers.

    **Note:** Only phone numbers and landline numbers in mainland China can be identified.

-   Masks sensitive server information, including web applications used by the website, the operating system, and the version of the server.
-   Maintains a library that contains illicit and sensitive keywords to detect and mask illicit or sensitive website content, and trigger alerts.

How data leakage prevention works

Based on the specified protection rules, data leakage prevention detects whether a web page contains sensitive information, such as identity card numbers, phone numbers, and band card numbers. If a rule is matched, WAF triggers alerts or masks the information based on the action specified in the rule. Data leakage prevention masks sensitive information with asterisks \(\*\).

Data leakage prevention allows you to set Content-Type to `text/*`, `image/*`, and `application/*` to protect web applications, native apps, and API operations.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch domain name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Web Security** tab and find **Anti Sensitive Information Leakage** in the **Data Security** section. Turn on the **Status** switch and click **Settings**.

    **Note:** You must enable data risk prevention before you can set protection rules.

    ![Data leakage prevention](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1328549951/p74237.png)

6.  Create a data leakage prevention rule.

    1.  On the **Anti Sensitive Information Leakage** page, click **Add Rule**.

    2.  In the **Add Rule** dialog box that appears, configure the following parameters.

        ![Create an alert rule](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1328549951/p74239.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule name**|Specify a name for the rule.|
        | |Specify the types of information that you need to detect. Supported types include:         -   **Status Code**: 400, 401, 402, 403, 404, 500, 501, 502, 503, 504, 405 to 499, and 505 to 599.
        -   **Sensitive Info**: **ID Card**, **Credit Card**, **Telephone No.**, and **Default Sensitive Word**
**Note:** **Phone Number** supports only phone numbers and landline numbers in mainland China.

You can specify one or more HTTP status codes or sensitive information types.

If you select the **and** check box, you can specify the **URL** that you want to check. In this case, WAF scans for sensitive information on only the specified page. |
        |**Matching Action**|Specify the action to be performed on detected sensitive information.         -   If you set the match condition to HTTP status codes, supported actions include:
            -   **Warn**: triggers alerts upon sensitive information leaks.
            -   **Block**: blocks requests and returns the default page denying access.
        -   If you set the match condition to sensitive information, supported actions include:
            -   **Warn**: triggers alerts upon sensitive information leaks.
            -   **Sensitive information filtering**: masks sensitive information in responses. |

        Sample configurations

        -   Mask sensitive information: Web pages may contain sensitive information, such as phone numbers and identity card numbers. You can create rules to mask or trigger alerts upon sensitive information. The following example shows you how to create a rule that masks phone numbers and identity card numbers.

            -   Matching conditions: ID Card and Telephone No.
            -   Matching Action: Sensitive information filtering
            After this rule is applied, all phone numbers and identity card numbers on the website are masked, as shown in the following figure.

            **Note:** Phone numbers that must be provided to the public to manage business affairs, such as business cooperation and complaints, may also be masked by data leakage prevention rules.

        -   Block HTTP status codes: You can create a rule to block or generate alerts upon specific HTTP status codes to prevent sensitive server information leaks. The following example shows you how to create a rule that blocks the 404 HTTP code.

            -   Matching conditions: 404
            -   Matching Action: Block
            After this rule is applied, if a requested page does not exist, the specified page denying access is returned, as shown in the following figure.

        -   Masks specific sensitive information on specific pages: You can create rules to mask or generate alerts upon specific sensitive information, such as phone numbers and identity card numbers, on specific pages. The following example shows you how to create a rule that masks identity card numbers on pages whose URLs contain `admin.php`.

            -   Matching conditions: ID Card numbers on pages whose URLs contain `admin.php`
            -   Matching Action: Sensitive information filtering
            After this rule is applied, identity card numbers on pages whose URLs contain admin.php are masked.

    3.  Click **Confirm**.

        After a data leakage prevention rule is created, it takes effect automatically. You can view newly created rules, and modify or delete rules in the rule list as needed.


After you enable data leakage prevention, you can view log data of filtered or blocked requests that triggered data leakage prevention rules. To view the log data, navigate to the **Security report** page and choose **Web Security** \> **Data Leakage Prevention** to view the relevant security report. For more information, see [View security reports](/intl.en-US/.md).

