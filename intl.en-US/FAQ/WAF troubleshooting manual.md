# WAF troubleshooting manual {#concept_zz3_xyl_q2b .concept}

This topic describes the symptoms, issues and provides the solution for the critical problems that arise when a domain name that accesses WAF encounters any abnormal access.

## Tools {#section_ezr_xyl_q2b .section}

-   **Chrome browser - Developer tool**: The developer tool provided by the Chrome browser can be conveniently used to view loading of page elements. Press **F12** to open the tool and switch to the **Network** tab.
-   **ping**: The ping test tool provided by Windows and Linux operating systems can be used to analyze and determine network faults. In the Windows OS, you can press Win+R and enter CMD to open the tool. Usage: `ping domain name/IP address`.
-   **traceroute \(Linux\)/tracert \(Windows\)**: The link tracing tool can be used to detect the hop where the data loss occurs. In the Windows OS, press **CTRL+R** and enter **cmd** to open the tool. Usage: `tracert -d domain name/IP address`.
-   **nslookup**: This tool can be used to detect whether domain name resolution is functional. In the Windows OS, press **CTRL+R** and enter **cmd** to open the tool. Usage: `nslookup domain name`.

## Troubleshooting methods {#section_zfn_1zl_q2b .section}

**Check if the origin is normal**

Follow these steps to bypass WAF and verify if the problem lies in the origin.

1.  Disable the security group, blacklist, whitelist, firewall, dongle, and cloud lock on the origin to prevent the WAF IP address from being added in the blacklist.
2.  Modify the local hosts file and direct the domain name to the public network IP address \(the origin IP address specified on WAF\) of the corresponding ECS, SLB, or server.
3.  Check if the problem still occurs without WAF.

**Check if the access request is intercepted falsely**

Follow these steps to adjust the protection policy to check if the access request is intercepted falsely.

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  Go to the **Management** \> **Website Configuration** page.
3.  Find the domain name with abnormal access and click **policies** under the Operation list.
4.  Disable **Web Application Protection** and check if the problem persists. If the problem disappears,
    -   We recommend that you [Configure the Web Application Protection policy](../../../../../reseller.en-US/User Guide/Protection configuration/Web application protection.md#) to Loose.
    -   You can also analyze the URL, and use [HTTP ACL Policy](../../../../../reseller.en-US/User Guide/Protection configuration/HTTP ACL policy.md#) to add a new rule to allow access from normal URLs.
5.  If the problem still exists, disable **HTTP Flood Protection** and check if the problem persists. If the problem disappears,
    -   We recommend that you [Configure the HTTP Flood Protection mode](../../../../../reseller.en-US/User Guide/Protection configuration/HTTP flood protection.md#) to Normal.
    -   You can also analyze the URL or IP address, and use [HTTP ACL Policy](../../../../../reseller.en-US/User Guide/Protection configuration/HTTP ACL policy.md#) to add a new rule to allow access from normal URLs or IP addresses.

## Common problems about WAF {#section_ozr_xyl_q2b .section}

If the problem continues to appear when WAF is connected and discontinues when WAF is disconnected, the following procedure can troubleshoot such issues.

**Access blocked \(405 error\)**

Symptoms

The page indicating the access is blocked is displayed and 405 is returned in the response.

Causes

Possible causes include:

-   The access is blocked because of HTTP ACL policy.
-   The access is blocked because of Web Application Protection.

Resolution

1.  Log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf).
2.  Go to the **Management** \> **Website Configuration** page.
3.  Find the domain name with abnormal access and click **policies** under the Operation list.
4.  Disable **HTTP ACL Policy** and check if the page \(405\) is still displayed. If the page is no longer displayed, the access is intercepted because of the ACL rule. You can resolve the problem by deleting the rule.
5.  If the problem appears even after you disable HTTP ACL Policy, you must try disabling **Web Application Protection** and check if the problem continues to occur. If the problem disappears,
    -   We recommend that you [Configure the Web Application Protection policy](../../../../../reseller.en-US/User Guide/Protection configuration/Web application protection.md#) to Loose.
    -   You can also analyze the URL, and use [HTTP ACL Policy](../../../../../reseller.en-US/User Guide/Protection configuration/HTTP ACL policy.md#) to add a new rule to allow access from normal URLs.

**Connection reset \(302 error\)**

Symptoms

When some IP addresses are used to access the website, a message “the connection is reset” is displayed and 302 is returned in the response. Set-cookie is also sent.

Causes

Access based on an IP address triggers HTTP Flood protection rules.

Resolution

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  Go to the **Management** \> **Website Configuration** page.
3.  Find the domain name with abnormal access and click **policies** under the Operation list.
4.  Disable **HTTP Flood Protection** and check if access recovers. If access recovers after HTTP Flood protection is disabled, the access is intercepted because of HTTP Flood Protection rules.
    -   You can set [HTTP ACL Policy](../../../../../reseller.en-US/User Guide/Protection configuration/HTTP ACL policy.md#) to add a new rule to allow access from normal URLs or IP addresses.
    -   If the HTTP Flood Protection mode is **Emergency**, we recommend that you [Configure the HTTP Flood Protection mode](../../../../../reseller.en-US/User Guide/Protection configuration/HTTP flood protection.md#) to Normal.

**HTTPS access abnormal**

Symptoms

After an HTTPS request is sent, the certificate www.notexist.com is returned.

Causes

WAF requires the browser to support SNI. Generally, iOS primitively supports SNI. For Windows and Android operation systems, you must confirm that they are compatible with SNI.

Resolution

See [HTTPS access exceptions arising from SNI compatibility \(Certificate not trusted\)](reseller.en-US/FAQ/HTTPS access exceptions arising from SNI compatibility ("Certificate not trusted").md#).

**White screen \(502 error\)**

Symptoms

During access to the website, white screen occurs and 502 is returned in the response.

Causes

When packet loss occurs on the origin \(ECS, SLB, or server\) or the origin becomes unreachable, WAF returns white screen.

Resolution

-   Check if security software or policies such as blacklist, iptables, firewall, dongle, and cloud lock are set for the origin. If yes, stop or uninstall the related service, clear the blacklist, and check if the problem disappears.
-   See [Troubleshooting methods](reseller.en-US/FAQ/WAF troubleshooting manual.md#section_zfn_1zl_q2b). Access by bypassing WAF and check if the access is normal. If access is still abnormal, check if the processes, CPU, memory, and Web logs of the origin are abnormal.

**Ping failure and black hole triggered**

Symptoms

Pinging a domain name fails. In addition, a short message is received, indicating that WAF encounters a DDoS attack and enters the black hole.

Causes

The DDoS attack is not in the protection scope of WAF.

Resolution

Enable **Anti-DDoS Pro** to defend against DDoS attacks.

**The load of multiple servers in the backend is unbalanced**

Causes

WAF uses Layer 4 IP address hash algorithm. Therefore,

-   When Anti-DDoS Pro is connected to WAF, the load on the ECS may not be balanced.
-   When the SLB uses Layer 4 forwarding, the load on the ECS may not be balanced.

Resolution

Set WAF and ECS to directly use SLB to balance load, that is, enable Layer 7 forwarding, cookie session persistence, and load balancing.

**WeChat or Alipay callback failure**

Symptoms

WeChat or Alipay callback fails.

Causes

-   High-frequency access is intercepted by HTTP Flood Protection.
-   HTTPS is used for callback and WeChat and Alipay do not support SNI. For more information about SNI, see [HTTPS access exceptions arising from SNI compatibility \(Certificate not trusted\)](reseller.en-US/FAQ/HTTPS access exceptions arising from SNI compatibility ("Certificate not trusted").md#).

Resolution

-   HTTP Flood Protection
    1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
    2.  Go to the **Management** \> **Website Configuration** page.
    3.  Find the domain name with abnormal access and click **policies** under the Operation list.
    4.  Disable **HTTP Flood Protection** and check if access recovers. If access recovers once HTTP Flood protection is disabled, the access is intercepted because of the HTTP Flood Protection rules.
        -   You can set [HTTP ACL Policy](../../../../../reseller.en-US/User Guide/Protection configuration/HTTP ACL policy.md#) to add a new rule to allow access from normal URLs or IP addresses.
        -   If the HTTP Flood Protection mode is **Emergency**, we recommend that you [Configure the HTTP Flood Protection mode](../../../../../reseller.en-US/User Guide/Protection configuration/HTTP flood protection.md#) to Normal.
-   SNI compatibility

    Set WeChat or Alipay to make it directly call the IP address of the ECS or SLB, without going through WAF.


