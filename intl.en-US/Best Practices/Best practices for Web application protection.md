# Best practices for Web application protection {#concept_trh_4l4_m2b .concept}

This topic describes the best practices for Web application protection based on WAF. The following aspects are covered: scenarios, protection policies, protection effects, and rule updates.

## Scenarios {#section_ryv_pl4_m2b .section}

WAF provides protection against Web attacks, such as SQL injection, XSS, remote command execution, and webshell upload. For more information about Web attacks, see [OWASP 2017 Top 10](https://www.owasp.org/index.php/Top_10-2017_Top_10).

**Note:** Server intrusions caused by security issues in host layers, such as unauthorized access to Redis and MySQL, are not covered by WAF.

## Protection policies {#section_syv_pl4_m2b .section}

After you add your domain to WAF, log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf). In the left-side navigation pane, choose **Management** \> **Website Configuration**. Select your domain and click **Policies** to view the protection status of your website, as shown in the following figure:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768238640_en-US.jpg)

By default, Web Application Protection is enabled and the normal mode protection is used. The parameters are as follows:

-   **Status**
    -   **Enabled** indicates that Web Application Protection is enabled.
    -   **Disabled** indicates that Web Application Protection is disabled.
-   **Mode**: Two modes are provided: Protection and Warning.
    -   The **Protection** mode indicates that WAF automatically blocks malicious requests and logs attacks when the application is under attack.
    -   The **Warning** mode indicates that WAF does not block malicious requests but logs attacks when the application is under attack.
-   **Protection Policy**: Three protection policies are available when the Protection mode is selected: Loose, Normal, and Strict.
    -   **Loose**: This policy only blocks requests that display typical attack patterns.
    -   **Normal**: This policy blocks requests that display common attack patterns.
    -   **Strict**: This policy blocks crafted requests that display specific types of attack patterns.

**Protection tips**:

-   If you are not clear about your website's traffic patterns, we recommend that you use the Warning mode first. You can observe the traffic flow for one or two weeks and then analyze the attack log.
    -   If you do not find any record indicating that normal requests are blocked, you can switch to the Protection mode to enable further protection.
    -   If normal requests are found in the attack log, contact customer service to resolve the issue.
-   If you add domains of PHPMyAdmin or tech forums to WAF, normal requests may be mistakenly blocked. We recommend that you contact customer service to resolve the issue.
-   Note the following points in your operations:
    -   Do not pass raw SQL statements or JavaScript code in HTTP requests.
    -   Do not use special keywords, such as UPDATE and SET, to define the path in URLs, such as `www.example.com/abc/update/mod.php? set=1`.
    -   If file uploads are required, restrict the maximum file size to 50 MB. We recommend that you use OSS or other methods to upload files exceeding the size limit.
-   After Web Application Protection is enabled, do not disable the All Requests option in the default rule of HTTP ACL Policy, as shown in the following figure:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768248641_en-US.jpg)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768248642_en-US.jpg)


## Protection effects {#section_dzv_pl4_m2b .section}

After Web Application Protection is enabled, you can choose **Reports** \> **Reports** to view details about blocked attacks, as shown in the following figure:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768248643_en-US.jpg)

On the Reports page, you can view attack details by time, such as yesterday, today, last seven days, or last month. You can click **View Attack Details** to view detailed attack information, as shown in the following figure:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768248644_en-US.jpg)

The figure displays the details about a SQL injection attack that has been blocked by WAF.

**Note:** If you find that normal requests are mistakenly blocked by WAF, we recommend that you [whitelist](../../../../../reseller.en-US/User Guide/Configuration/Configure a whitelist or blacklist.md#) the affected URLs in HTTP ACL policies and then contact customer service to resolve the issue.

## Rule updates {#section_gzv_pl4_m2b .section}

When new vulnerabilities are discovered, WAF updates protection rules and releases security bulletins in a timely manner.

Log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf). In the left-side navigation pane, choose **Overview** \> **Security** to view the latest security bulletins.

**Note:** Web attacks usually have more than one proof of concept \(POC\). A thorough analysis is conducted to determine the cause of the vulnerability so that the protection rule can prevent all exploits of this vulnerability.

