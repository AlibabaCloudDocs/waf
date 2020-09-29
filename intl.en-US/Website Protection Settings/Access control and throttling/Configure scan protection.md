---
keyword: [website protection, access control and throttling, scan protection, high-frequency web attack blocking, directory traversal, scanning tool, collaborative defense]
---

# Configure scan protection

After you add a website to Web Application Firewall \(WAF\), you can enable the scan protection feature for your website. If you enable the scan protection feature, access requests from the specific IP addresses are automatically blocked. These IP addresses include the source IP addresses of requests that initiate high-frequency web attacks and malicious directory traversal attacks, and IP addresses defined in the common scanning tools or the Alibaba Cloud malicious IP library. You can customize the policy of scan protection based on your requirements.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   If you purchase a subscription instance, the instance must be of the **Pro** edition or higher.

        If you need to customize policies of **high-frequency web attack blocking** and **directory traversal prevention**, the instance must be of the **Business** edition or higher. The WAF instance of the **Pro** edition or lower can use only the default policy to enable scan protection. For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).

    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

The scan protection feature provides high-frequency web attack blocking, directory traversal prevention, scanning tool blocking, and collaborative defense.

-   High-frequency web attack blocking automatically blocks IP addresses from which multiple web attacks are initiated within a short period of time. If the number of web attacks initiated from a client IP address exceeds a specific number, the access requests from this IP address are blocked for a specific period of time. You can customize the protection policy of high-frequency web attack blocking. You can manually unblock a blocked IP address.
-   Directory traversal prevention automatically blocks client IP addresses from which multiple web attacks are initiated within a short period of time. If the total number of requests initiated from a client IP address exceeds a specific number and the proportion of the requests for which the HTTP status code 404 is returned to the total requests exceeds a specific proportion, the access requests from this IP address are blocked for a specific period. You can customize the protection policy of directory traversal prevention. You can manually unblock a blocked IP address.
-   Scanning tool blocking automatically blocks access requests from IP addresses defined in the common scanning tools. Blocked scanning tools include sqlmap, AWVS, Nessus, AppScan, WebInspect, Netsparker, Nikto, and RSAS.
-   Collaborative defense automatically blocks access requests from IP addresses in the Alibaba Cloud malicious IP library.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch domain name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  On the **Access Control/Throttling** tab, find the **Scan Protection** card in the **Access Control/Throttling** section, and configure the following settings:

    ![Scan protection](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9628549951/p74001.png)

    -   **Blocking IPs Initiating High-frequency Web Attacks**: You can enable or disable high-frequency web attack blocking.

        Configure the protection policy of high-frequency web attack blocking.

        1.  Enable high-frequency web attack blocking.
        2.  Click **Settings**.
        3.  In the **Rule Setting** dialog box, specify the following parameters: **Inspection Time Range**, **The number of attacks exceeds**, and **Blocked IP Addresses**.

            ![Rule Setting](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0628549951/p73999.png)

            If the number of web attacks initiated from a client IP address in the specified inspection time range exceeds a specific number, the access requests from this IP address are blocked for the specified time range.

            **Note:** We recommend that you use **Mode** and select a built-in configuration mode from **Flexible Mode**, **Strict Mode**, and **Normal Mode**. You can modify the parameters based on your requirements.

        4.  Click **Confirm**.
        You can click **Unblock IP Address** to unblock the IP address.

    -   **Directory Traversal Prevention**: You can enable or disable directory traversal prevention.

        Configure the protection policy of directory traversal prevention.

        1.  Enable directory traversal protection.
        2.  Click **Settings**.
        3.  In the **Rule Setting**dialog box, specify the following parameters: **Inspection Time Range**, **The total requests exceed**, **And the percentage of responses with 404 exceeds**, **Blocked IP Addresses**, and **Directory number**.

            ![Rule Setting](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0628549951/p74004.png)

            If the total number of requests initiated from a client IP address in the specified inspection time range exceeds a specific number and the proportion of the requests for which the HTTP status code 404 is returned to the total requests exceeds a specific proportion, or the number of directories to which requests are sent within the specified inspection time range exceeds a specific number, the access requests from this IP address are blocked for the specified time range.

            **Note:** We recommend that you use **Mode** and select a built-in configuration mode from **Flexible Mode**, **Strict Mode**, and **Normal Mode**. You can modify the parameters based on your requirements.

        4.  Click **Confirm**.
        You can click **Unblock IP Address** to unblock the IP address.

    -   **Scanning Tool Blocking**: Enable or disable scanning tool blocking.

        After you enable scanning tool blocking, the common scanning tool behaviors are automatically detected. If an access request meets the characteristics of scanning, this request is always blocked. If you disable scanning tool blocking, scanning activities are no longer blocked.

    -   **Collaborative Defense**: Enable or disable collaborative defense.

        After you enable collaborative defense, all access requests from the IP addresses in the Alibaba Cloud malicious IP library are blocked.


