# Best practices for the protection rules engine

This topic describes best practices for the protection rules engine provided by Web Application Firewall \(WAF\).

## Scenarios

WAF protects your website against web attacks, such as SQL injections, XSS attacks, remote code executions, and webshell attacks. For more information about web attacks, see [Definitions of common web vulnerabilities]().

**Note:** WAF cannot defend against server intrusions caused by host security issues, such as unauthorized access to ApsaraDB for Redis or ApsaraDB RDS for MySQL.

## Configure protection policies

By default, **Protection Rules Engine** is enabled and Protection Rule Group is set to Medium rule group after you add your website to WAF. This blocks common attacks. You can go to the **Website Protection** page to view the status of **Protection Rules Engine** and configure protection policies. For more information, see [Configure the protection rules engine](/intl.en-US/Website Protection Settings/Web security/Configure the protection rules engine.md).

![Web application protection ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3969021161/p8640.jpg)

**Protection status description**

-   **Status**: Turn on or off the switch to enable or disable the protection rules engine. This engine is enabled by default.
-   **Mode**: Select the action that you want WAF to take on requests when WAF detects attacks. Valid values:
    -   **Block**: WAF automatically blocks requests and logs attacks in the backend.
    -   **Warn**: WAF does not block requests but logs attacks in the backend.
-   **Protection Rule Group**: Select a group of protection rules that you want to apply. Valid values:

    -   **Medium rule group**: blocks common web application attacks in a standard way. These attacks can bypass protection policies.
    -   **Strict rule group**: blocks web application attacks in a strict way. These attacks can bypass complex protection policies.
    -   **Loose rule group**: blocks common web application attacks.
    **Note:** These settings take effect only when you enable the protection rules engine.

    If you use WAF Business or Enterprise in mainland China or WAF Enterprise outside mainland China, you can customize protection rule groups. The custom rule groups combine all protection rules provided by WAF and provide specific protection policies for your website. For more information, see [Customize protection rule groups](/intl.en-US/Website Protection Settings/Customize protection rule groups.md).


**Recommended configurations**

-   If you are not clear about the characteristics of your business traffic, we recommend that you set Mode to **Warn**. After one or two weeks, analyze the attack logs in this mode.
    -   If the attack logs show that normal traffic is not blocked, you can set Mode to **Block**.
    -   If the attack logs show that normal traffic is blocked, you can contact Alibaba Cloud security experts to resolve the issue.
-   If you add phpMyAdmin and development technology forums to WAF for protection, WAF may block normal traffic. If this occurs, we recommend that you contact Alibaba Cloud security experts to resolve the issue.
-   We recommend that you take note of the following points:
    -   Do not pass raw SQL statements or JavaScript code in the HTTP requests for your normal business.
    -   Do not use special keywords, such as UPDATE or SET, in the paths for normal business URLs. For example, do not use `www.example.com/abc/update/mod.php?set=1`.
    -   Do not use a browser to upload files that exceed 50 MB. We recommend that you upload the files by using OSS or other methods. For more information, see [Get started with OSS](/intl.en-US/Quick Start/Get started with OSS.md).

## View protection effects

After you enable the protection rules engine, you can view its protection records. To view the records, click **Security report**. On the page that appears, click **Web Security** and view the report on the **Web Intrusion Prevention** tab. For more information, see [View security reports](/intl.en-US/.md).

The **Web Intrusion Prevention** tab provides charts that display attack records over the last 30 days. The section below the charts lists specific attack records. You can select **Regular Protection**, find an attack record, and click **View Details** to view the attack details. The following figure shows an SQL injection request that is blocked by WAF.

![View attack details ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7628549951/p8644.png)

**Note:** If you find that WAF blocks normal traffic, we recommend that you configure a whitelist for the blocked URLs in the **Web Intrusion Prevention** section and then contact Alibaba Cloud security experts to find a solution. For more information, see [Configure a whitelist for Web Intrusion Prevention](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Web Intrusion Prevention.md).

## View rule updates

WAF updates protection rules and releases protection bulletins in a timely manner to fix known and zero-day vulnerabilities. To view **Rule updates notice**, go to the **Product Information** page. For more information, see [View product information](/intl.en-US/System Management/View product information.md).

![Rule updates ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7628549951/p8645.png)

**Note:** Web attacks have more than one proof of concept \(POC\). Alibaba Cloud security experts conduct a thorough analysis of vulnerability principles to ensure that published web protection rules cover all disclosed and undisclosed vulnerabilities.

