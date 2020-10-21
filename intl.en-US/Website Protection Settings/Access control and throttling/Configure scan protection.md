---
keyword: [website protection, access control and throttling, scan protection, high-frequency web attack blocking, directory traversal, scanning tool, collaborative defense]
---

# Configure scan protection

After you add a website to Web Application Firewall \(WAF\), you can enable the scan protection function for your website. If you do that, access requests from specific IP addresses are automatically blocked. These IP addresses include source IP addresses that initiate high-frequency web attacks and malicious directory traversal attacks, and IP addresses defined in common scanning tools or the Alibaba Cloud malicious IP library. You can customize scan protection policies based on your requirements.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   If the instance is billed on a subscription basis, the instance must be of the **Pro** edition or higher.

        If you need to customize policies of **Blocking IPs Initiating High-frequency Web Attacks** and **Directory Traversal Prevention**, the instance must be of the **Business** edition or higher. The WAF instance of the **Pro** edition or lower can use only the default scan protection policies. For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).

    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

The scan protection function provides the following policies:

-   Blocking IPs Initiating High-frequency Web Attacks: automatically blocks client IP addresses that initiate multiple web attacks within a short period of time. You can customize the protection policy and manually unblock a blocked IP address.
-   Directory Traversal Prevention: automatically blocks client IP addresses that initiate multiple directory traversal attacks in a short period of time. You can customize the protection policy and manually unblock a blocked IP address.
-   Scanning Tool Blocking: automatically blocks access requests from IP addresses defined in common scanning tools. The scanning tools include sqlmap, AWVS, Nessus, AppScan, WebInspect, Netsparker, Nikto, and RSAS.
-   Collaborative Defense: automatically blocks access requests from IP addresses in the Alibaba Cloud malicious IP library.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  On the **Access Control/Throttling** tab, find the **Scan Protection** section and configure the following settings:

    ![Scan protection](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9628549951/p74001.png)

    **Note:** By default, all requests destined for your website are checked by scan protection when any policy in this section is enabled. You can configure a **Access Control/Throttling** rule so that requests that match the rule bypass the check. For more information, see [Configure a whitelist for Access Control/Throttling](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Access Control/Throttling.md).

    -   **Blocking IPs Initiating High-frequency Web Attacks**: You can enable or disable it.

        Configure the protection policy.

        1.  Turn on Blocking IPs Initiating High-frequency Web Attacks.
        2.  Click **Settings**.
        3.  In the **Rule Setting** dialog box, specify the following parameters: **Inspection Time Range**, **The number of attacks exceeds**, and **Blocked IP Addresses**.

            ![Rule settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0628549951/p73999.png)

            If the number of web attacks initiated from a client IP address in the specified inspection time range exceeds a specific number, the access requests from this IP address are blocked for the specified time range.**Inspection Time Range****The number of attacks exceeds****Blocked IP Addresses**

            **Note:** We recommend that you select a built-in configuration mode from **Flexible Mode**, **Strict Mode**, and **Normal Mode** in the **Mode** section. You can modify the parameters based on your requirements.

        4.  Click **Confirm**.
        You can click **Unblock IP Address** to unblock IP addresses that are blocked by the policy.

    -   **Directory Traversal Prevention**: You can enable or disable it.

        Configure the protection policy.

        1.  Turn on Directory Traversal Prevention.
        2.  Click **Settings**.
        3.  In the **Rule Setting**dialog box, specify the following parameters: **Inspection Time Range**, **The total requests exceed**, **And the percentage of responses with 404 exceeds**, **Blocked IP Addresses**, and **Directory number**.

            ![Rule settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0628549951/p74004.png)

            If the total number of requests initiated from a client IP address in the specified inspection time range exceeds a specific number and the proportion of the requests for which the HTTP status code 404 is returned to the total requests exceeds a specific proportion, or the number of directories to which requests are sent within the specified inspection time range exceeds a specific number, the access requests from this IP address are blocked for the specified time range.**Inspection Time Range****The total requests exceed****Inspection Time Range****Blocked IP Addresses**

            **Note:** We recommend that you select a built-in configuration mode from **Flexible Mode**, **Strict Mode**, and **Normal Mode** in the **Mode** section. You can modify the parameters based on your requirements.

        4.  Click **Confirm**.
        You can click **Unblock IP Address** to unblock IP addresses that are blocked by the policy.

    -   **Scanning Tool Blocking**: You can enable or disable it.

        After you enable Scanning Tool Blocking, the behaviors of common scanning tools are automatically detected. If an access request meets the characteristics of scanning, this request is always blocked. If you disable Scanning Tool Blocking, scanning behaviors are no longer blocked.

    -   **Collaborative Defense**: You can enable or disable it.

        After you enable Collaborative Defense, all access requests from the IP addresses in the Alibaba Cloud malicious IP library are blocked.


