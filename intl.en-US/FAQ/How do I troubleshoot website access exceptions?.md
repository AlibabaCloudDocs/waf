# How do I troubleshoot website access exceptions?

This topic describes how to troubleshoot access exceptions on websites that are protected by Web Application Firewall \(WAF\).

## Instructions

If you cannot access a website that is protected by WAF, you can use the following methods to troubleshoot the exception:

1.  [Determine whether the origin server is faulty](#section_d0f_ksp_1jy): Bypass WAF and check whether the origin server responds to access requests in an expected manner.
2.  [Determine whether WAF blocks valid requests](#section_zfn_1zl_q2b): Disable protection modules to check whether WAF blocks access requests.
3.  [Determine whether the exception is a common exception](#section_ozr_xyl_q2b): Analyze and troubleshoot the exception by following the instructions in the common access exceptions table.

**Note:** If the exception persists after troubleshooting, submit a [ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80) to contact Alibaba Cloud technical support.

For more information about the tools that are used during troubleshooting, see [Appendix: Common tools](#section_t3v_1br_qop).

## Determine whether the origin server is faulty

To bypass WAF and determine whether the origin server responds to access requests in an expected manner, perform the following steps:

1.  Disable the security groups, blacklists, whitelists, firewalls, SafeDog, and Yunsuo on the origin server to prevent back-to-origin IP addresses of WAF from being blocked.
2.  Modify the hosts file in your computer to resolve the domain name to the public IP address of the required Elastic Compute Service \(ECS\) instance, Server Load Balancer \(SLB\) instance, or on-premises server. The public IP address is the IP address of the origin server that you add to WAF.
3.  Use a browser of your computer to access the domain name of the origin server and check whether the same exception occurs.
    -   If you cannot access the origin server, the origin server is faulty. We recommend that you check the working status of the origin server, including processes, CPU utilization, memory, and web logs, and fix the exception.
    -   If you can access the origin server, the exception is not due to the origin server. Check whether the exception occurs because WAF blocks the access requests. For more information, see [Determine whether WAF blocks valid requests](#section_zfn_1zl_q2b).

## Determine whether WAF blocks valid requests

To disable the blocking functions of WAF and determine whether WAF blocks valid access requests, perform the following steps:

1.  Disable **RegEx Protection Engine** for the domain name of the origin server to check whether the exception persists. For more information, see [Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md).

    If you can access the website after you disable this function, we recommend that you set **Protection Rule Group** to **Loose rule group** in the **RegEx Protection Engine** section. By default, **Medium rule group** is selected. Alternatively, you can analyze the URL of the origin server by using Log Service for WAF. Then, add a custom protection policy to WAF to allow all access requests to this URL. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).

2.  If the problem persists after you disable **RegEx Protection Engine**, disable **HTTP Flood Protection** for the domain name of the origin server. For more information, see [Configure HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md).

    If you can access the website after you disable this function, we recommend that you set Mode to **Prevention** in the **HTTP Flood Protection** section. If Mode is already set to **Prevention**, skip this step. Alternatively, you can analyze the URL of the origin server by using Log Service for WAF. Then, add a custom protection policy to WAF to allow all access requests to this URL. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).

    If the exception persists after you disable **HTTP Flood Protection**, this exception is not due to the blocking functions of WAF. For more information, see [Determine whether the exception is a common exception](#section_ozr_xyl_q2b).


## Determine whether the exception is a common exception

If the exception disappears after you disable WAF and continues to occur after you enable WAF, troubleshoot the exception by following the instructions in the following table.

|Exception|Description|Cause|Solution|
|---------|-----------|-----|--------|
|Access blocked \(405 error\)|The error message "405 Method Not Allowed" appears, or the HTTP status code 405 is returned.|The access request is blocked by a custom protection policy or the RegEx Protection Engine.|1.  Disable the custom protection policy for the domain name of the origin server and check whether the error message appears. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).

If the error message no longer appears, the custom protection policy blocks the access request. Find the custom protection policy and delete it.

2.  If the error message still appears after you disable the custom protection policy, disable **RegEx Protection Engine** for the domain name of the origin server to check whether the exception persists. For more information, see [Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md).

If you can access the website after you disable this function, we recommend that you set **Protection Rule Group** to **Loose rule group** in the **RegEx Protection Engine** section. By default, **Medium rule group** is selected. Alternatively, you can analyze the URL of the origin server by using Log Service for WAF. Then, add a custom protection policy to WAF to allow all access requests to this URL. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md). |
|Connection reset \(302 error\)|The system prompts that the connection is reset. The HTTP status code is 302, and the Set-Cookie header is contained in the response.|Access from an IP address triggers HTTP Flood Protection.|Disable **HTTP Flood Protection** for the domain name of the origin server. For more information, see [Configure HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md).If you can access the website after HTTP Flood Protection is disabled, the access requests are blocked by the HTTP flood protection rule. We recommend that you set Mode to **Prevention** in the **HTTP Flood Protection** section. If Mode is already set to **Prevention**, skip this step. Alternatively, you can analyze the URL of the origin server by using Log Service for WAF. Then, add a custom protection policy to WAF to allow all access requests to this URL. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md). |
|HTTPS access exceptions|After a client sends an HTTPS request, the certificate `www.notexist.com` is returned.|WAF requires the browser to support Server Name Indication \(SNI\), whereas the browser of the client may not support SNI.|By default, macOS and iOS operating systems support SNI. For Windows and Android operating systems, make sure that they are compatible with SNI. For more information, see [HTTPS access exceptions arising from SNI compatibility \("Certificate not trusted"\)](/intl.en-US/FAQ/HTTPS access exceptions arising from SNI compatibility ("Certificate not trusted").md).|
|Blank screen \(502 error\)|When you access a website, a blank screen error occurs and the HTTP status code 502 is returned.|When the origin server such as an ECS or SLB instance or a server experiences a packet loss or becomes unreachable, WAF returns the HTTP status code 502.|1.  Check whether the origin server has security software or policies configured, such as a blacklist, the iptables program, a firewall, SafeDog, or Yunsuo. If the origin server has security software or policies configured, stop or uninstall them, clear the blacklist, and check whether the exception is resolved.
2.  Bypass WAF to check whether the website can be accessed. For more information, see [Determine whether the origin server is faulty](#section_d0f_ksp_1jy). If the exception persists, check the processes, CPU utilization, memory, or web logs of the origin server for errors. |
|Ping failure of a domain name|The domain name cannot be pinged. A text message is received. The message indicates that WAF experiences DDoS attacks, and blackhole filtering is triggered.|WAF cannot mitigate DDoS attacks.|Activate Anti-DDoS to mitigate DDoS attacks. For more information, see [Overview](/intl.en-US/Product Introduction on Alibaba DDoS Protection/Overview.md).|
|Unbalanced server load|The load is unbalanced among multiple ECS instances in the backend.|WAF uses Layer 4 hash algorithms for IP addresses. If Anti-DDoS Pro or Anti-DDoS Premium is deployed together with WAF, or SLB uses Layer 4 forwarding, ECS instances may have unbalanced load.|Configure WAF and ECS instances to directly use SLB to balance the load. Use Layer 7 forwarding and enable cookie session persistence or load balancing.|
|WeChat or Alipay callback failure|WeChat or Alipay callback fails.|The possible reason is that HTTP flood protection rules block high-frequency requests, or HTTPS callback is used but WeChat or Alipay does not support SNI.|-   HTTP Flood Protection:
    1.  Disable **HTTP Flood Protection** for the domain name of the origin server. For more information, see [Configure HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md).
    2.  If WeChat or Alipay can be accessed after HTTP Flood Protection is disabled, the access request is blocked by HTTP flood protection rules. We recommend that you set Mode to **Prevention** in the **HTTP Flood Protection** section. If Mode is already set to **Prevention**, skip this step. Alternatively, you can analyze the URL of the origin server by using Log Service for WAF. Then, add a custom protection policy to WAF to allow all access requests to this URL. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).
-   SNI: Configure WeChat or Alipay to bypass WAF and directly use the IP address of the ECS or SLB instance. For more information, see [HTTPS access exceptions arising from SNI compatibility \("Certificate not trusted"\)](/intl.en-US/FAQ/HTTPS access exceptions arising from SNI compatibility ("Certificate not trusted").md). |

## Appendix: Common tools

-   Chrome DevTools: It is provided by Google Chrome. It can be used to view loading status of elements on pages. Press **F12** to open the tool and navigate to the **Network** tab.
-   ping: The ping test tool can be used to analyze and determine network faults. This tool is available in Windows and Linux. In Windows, press Win+R and enter cmd to open Command Prompt. Command: `ping domain name or IP address`.
-   traceroute for Linux and tracert for Windows: The link tracing tools can be used to detect the hop where the packet loss occurs. In Windows, press Win+R and enter cmd to open Command Prompt. Command: `tracert -d domain name or IP address`.
-   nslookup: This tool can be used to detect whether domain name resolution is functional. In Windows, press Win+R and enter cmd to open Command Prompt. Command: `nslookup domain name`.

