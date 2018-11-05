# Features {#concept_fyq_f1n_42b .concept}

Alibaba Cloud WAF \(Web Application Firewall\) helps to protect your website against various web attacks and to guarantee website security and availability. It leverages both core defense capabilities and big data capabilities to achieve reliable web security. Alibaba Cloud WAF offers the following features:

## Request monitoring {#section_h5z_f1n_42b .section}

Monitors the HTTP and HTTPS \(only for WAF Business and Enterprise editions\) requests that are forwarded to your website.

## Web application protection {#section_i5z_f1n_42b .section}

**Protects your website against common web application attacks**

-   **Defense against common OWASP threats**, such as SQL injection, XSS attacks, Webshell uploading, command injection, illegal HTTP protocol requests, common Web server vulnerability attacks, unauthorized access to core files, and path traversing. Also provides backdoor isolation and scanning protection services.
-   **Websites stealth**: Keeps the website address invisible to attackers to avoid direct attacks that bypass WAF.
-   **Regular and timely patches against 0day vulnerabilities**: The protection rules used by Alibaba WAF are tried and tested and cover the latest vulnerability patches, which are updated in a timely manner and synchronized globally immediately after release.
-   **User-friendly observation mode**: Provides observation mode for newly launched businesses on the website. In this mode, a suspected attack only triggers a warning, instead of a blocking action, in a bid to facilitate the statistics of business false alarms.

**Protection against HTTP flood attacks**

-   Manages the access frequency from a single source IP address by using re-direction verification and human/machine identification.
-   Prevents massive and slow request attacks based on precise access control policies and recognition of exceptional response code, URL request distribution, Referer, and User-Agent requests.
-   Establishes threat intelligence and trustful access analysis models to quickly identify malicious requests by making full use of Alibaba Group's big data security advantages.

**HTTP ACL Policy**

-   Provides a user-friendly configuration console that supports condition combinations of common HTTP fields such as IP, URL, Referer, and User-Agent to form precise access control policies. Also supports anti-leech protection, website back end protection, and so on.
-   Combined with common web attack protection and HTTP flood protection, access control helps to create multiple layers of protection to suit a variety of needs to identify legitimate and malicious requests.

**Virtual patches**

Adjusts web protection policies to enable swift protection before patches are released for rectification of web application vulnerabilities.

## Attack event management {#section_m5z_f1n_42b .section}

Supports centralized management and analysis of attack events, attack traffic, and attack scales.

## Reliability {#section_n5z_f1n_42b .section}

-   **Load balancing**: Provides services in cluster mode, with load balancing among multiple devices. Supports multiple load balancing policies.
-   **Smooth capacity expansion**: Reduces or increases the number of cluster devices based on actual traffic and performs flexible capacity expansion of service.
-   **No single-point issues**: Even if a single device breaks down or is offline for repair, services are not affected at all.

For more information, see the [Web Application Firewall product detail](https://www.alibabacloud.com/zh/product/waf) page.

