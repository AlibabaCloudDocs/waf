# WAF FAQ {#concept_rws_35k_q2b .concept}

-   [Can servers outside Alibaba Cloud use WAF?](#)
-   [Does WAF support cloud virtual hosts?](#)
-   [How to prevent HTTP flood attacks?](#)
-   [Does WAF support HTTPS?](#)
-   [Does WAF support user-defined ports?](#)
-   [Does the QPS limitation of WAF aim at the QPS summarized by the whole WAF instances or the QPS upper limit for one configured domain name?](#)
-   [Which edition of WAF provides security against malicious SMS?](#)
-   [Can the origin IP address in WAF be set to an internal network IP address of ECS?](#)
-   [Can WAF be connected together with CDN or Anti-DDoS IP?](#)
-   [Can WAF protect IP addresses of multiple origins under one domain name?](#)
-   [How does WAF share load when multiple origins are configured?](#)
-   [Does WAF support health check?](#)
-   [Does WAF support session persistence?](#)
-   [Can there be a delay, when an origin IP address of WAF is being modified?](#)
-   [When does the modified configuration take effect in WAF console?](#)
-   [What is the back-to-source IP address of WAF?](#)
-   [Does WAF automatically add its back-to-source IP addresses to the security group?](#)
-   [Do I need to allow accesses from all client IP addresses to enable WAF back-to-source?](#)
-   [Can the source IP addresses of HTTP flood attacks be viewed in WAF console?](#)
-   [How to query the bandwidth traffic used by WAF?](#)
-   [Does the IP field in HTTP ACL policies of WAF support entry of a network segment?](#)
-   [What are the features of the Anti-DDoS capability provided by WAF?](#)
-   [Does WAF support HTTPS two-way authentication?](#)
-   [Does WAF support Websocket and HTTP 2.0 or SPDY protocol?](#)
-   [Which SSL protocols are supported by WAF?](#)
-   [Can I use different Alibaba Cloud accounts to deploy Alibaba Cloud WAF, CDN, and Anti-DDoS Pro for the same domain name?](#)
-   [Can I use double slashes \(//\) in the URL matching condition of an HTTP ACL rule?](#)
-   [Can I deploy Alibaba Cloud WAF for websites that enable NTML \(NT LAN Manager\) authentication?](#section_wgn_qt3_mgb)

## Can servers outside Alibaba Cloud use WAF? {#section_tfb_j5k_q2b .section}

Yes, WAF can protect any web server/applications that can be accessed through the Internet, whether it is inside or outside Alibaba Cloud. You can protect your web service in AWS, Azure, or any other cloud and data centers.

**Note:** Domain names accessed within Mainland China must apply for an ICP license at the Ministry of Industry and Information Technology.

## Does WAF support cloud virtual hosts? {#section_ufb_j5k_q2b .section}

The Business and Enterprise editions of WAF support exclusive virtual hosts, which can be configured after WAF is enabled.

Shared hosts use shared IP addresses, which means that the origin is used by multiple users. We recommend that you not to configure WAF separately.

## How to prevent HTTP flood attacks? {#section_vfb_j5k_q2b .section}

WAF provides HTTP flood protection in the Normal and Emergency modes. You can switch the protection mode based on the actual situation. For more information, see [Configure the HTTP flood protection mode](../../../../intl.en-US/User Guide/Configuration/HTTP flood protection.md#).

For better protection effects and lower false positives rate, you can use the WAF Business Edition or WAF Enterprise Edition, to customize or request the security professional to customize targeted protection policies for you. For more information, see [Customize HTTP flood protection](../../../../intl.en-US/User Guide/Configuration/Custom HTTP flood protection.md#).

## Does WAF support HTTPS? {#section_wfb_j5k_q2b .section}

Yes, all editions of WAF fully support HTTPS businesses and wildcard domain names.

WAF can handle HTTPS traffic if the SSL certificate and key are uploaded as needed. WAF decrypts the requests, examines the data, and then encrypts them again, before forwarding them back to the origin.

## Does WAF support user-defined ports? {#section_xfb_j5k_q2b .section}

The Business and Enterprise editions of WAF support user-defined non-standard ports. The Business version supports up to 10 non-standard ports and the Enterprise version supports up to 50 non-standard ports.

**Note:** For more information, see [Supported non-standard ports](../../../../intl.en-US/User Guide/Use the DNS proxy mode to configure WAF/Supported non-standard ports.md#).

## Does the QPS limitation of WAF aim at the QPS summarized by the whole WAF instances or the QPS upper limit for one configured domain name? {#section_yfb_j5k_q2b .section}

The QPS limitation of WAF is for all WAF instances. For example, if the configuration of your WAF protects three domain names, then the accumulated QPS of the three domain names cannot exceed the upper limit. If the accumulated QPS exceeds the QPS limitation of WAF instances, rate limiting is triggered and packet loss may occur.

## Which edition of WAF provides security against malicious SMS? {#section_zfb_j5k_q2b .section}

All editions of WAF provides security against malicious SMS. For more information, see [How to select the WAF edition](../../../../intl.en-US/Pricing/Subscription/Subscription plans.md#).

## Can the origin IP address in WAF be set to an internal network IP address of ECS? {#section_agb_j5k_q2b .section}

In WAF, traffic is returned to origin through a public network. Direct entry of an internal network IP address is not supported.

## Can WAF be connected together with CDN or Anti-DDoS IP? {#section_bgb_j5k_q2b .section}

The WAF is fully compatible with CDN and Anti-DDoS services. Fundamental architecture: **Client \> Anti-DDoS \> CDN \> WAF \> SLB \> Origin**

For service combination with Anti-DDoS or CDN, WAF’s CNAME must be entered as the origin for Anti-DDoS or CDN. This action turns the traffic towards WAF after it goes through Anti-DDoS or CDN. WAF then returns the traffic to the origin.

For more information, see [Use Anti-DDoS Pro with WAF](../../../../intl.en-US/User Guide/Use the DNS proxy mode to configure WAF/Deploy WAF and Anti-DDoS Pro together.md#) and [Use CDN with WAF](../../../../intl.en-US/User Guide/Use the DNS proxy mode to configure WAF/Deploy WAF and CDN together.md#).

## Can WAF protect IP addresses of multiple origins under one domain name? {#section_cgb_j5k_q2b .section}

Yes. Individual domain protection can hold up to 20 origin IPs. These IPs are separated with commas. If multiple origins are added to one domain, WAF loads balance requests based on the round-robin method, and performs health checks for all the origins. When WAF fails to get a response from any origin, WAF stops forwarding requests to that origin until it returns to normal.

## How does WAF share load when multiple origins are configured? {#section_dgb_j5k_q2b .section}

If you configure multiple origin IP addresses, WAF automatically uses polling to perform a load balance to access requests.

## Does WAF support health check? {#section_egb_j5k_q2b .section}

By default, WAF enables health check. WAF checks the access status of all origin IP addresses. If an origin IP address does not respond, WAF does not forward any requests to the origin IP address until the access status of the IP address is completely recovered.

## Does WAF support session persistence? {#section_fgb_j5k_q2b .section}

Yes, WAF supports session persistence. However, you must enable the function by submitting a ticket to the technical support team.

## Can there be a delay, when an origin IP address of WAF is being modified? {#section_ggb_j5k_q2b .section}

Not really. Once the origin IP address that is protected by WAF gets modified, the modification is effective within a minute.

## When does the modified configuration take effect in WAF console? {#section_hgb_j5k_q2b .section}

Generally, the modified configuration is effective within a minute.

## What is the back-to-source IP address of WAF? {#section_igb_j5k_q2b .section}

You can view the back-to-source IP address on the **Management** \> **Website Configuration** page of the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf). For more information, see [How to View the WAF back-to-source IP address](intl.en-US/FAQ/How to view the WAF back-to-source IP addresses?.md#).

## Does WAF automatically add its back-to-source IP addresses to the security group? {#section_jgb_j5k_q2b .section}

No, WAF does not automatically add its back-to-source IP addresses to the security group. If your origin is deployed with other firewall or host security protection software, we recommend that you manually add the WAF back-to-source IP addresses to the whitelist.

For more information, see [Protect your origin server](../../../../intl.en-US/Best Practices/Protect your origin server.md#).

## Do I need to allow accesses from all client IP addresses to enable WAF back-to-source? {#section_kgb_j5k_q2b .section}

No, because according to your service type you can only allow the WAF back-to-source IP addresses or IP addresses of all clients.

For the Web service, we recommend that you only allow the WAF back-to-source IP addresses to [protect the origin](../../../../intl.en-US/Best Practices/Protect your origin server.md#).

## Can the source IP addresses of HTTP flood attacks be viewed in WAF console? {#section_lgb_j5k_q2b .section}

For the WAF Enterprise edition, you can view the full logs of source IP addresses of HTTP flood attacks on the service analysis page.

## How to query the bandwidth traffic used by WAF? {#section_mgb_j5k_q2b .section}

You can view query the used bandwidth traffic on the overview page in the WAF console.

## Does the IP field in HTTP ACL policies of WAF support entry of a network segment? {#section_ngb_j5k_q2b .section}

Yes, WAF supports the entry of an IP network segment in the IP field of HTTP ACL policies.

## What are the features of the Anti-DDoS capability provided by WAF? {#section_pgb_j5k_q2b .section}

-   WAF provides independent IP addresses to each user. These IP addresses are also subject to Anti-DDoS blackhole policies, and are consistent with ECS and Server Load Balancer.
-   The blackhole threshold for WAF is the same as the ECS default threshold in the current region.

You can purchase [Anti-DDoS Pro](https://www.alibabacloud.com/product/ddos-pro) to protect your website against DDoS attacks.

## Does WAF support HTTPS two-way authentication? {#section_rgb_j5k_q2b .section}

No. WAF does not support HTTPS two-way authentication.

## Does WAF support Websocket and HTTP 2.0 or SPDY protocol? {#section_sgb_j5k_q2b .section}

WAF is already supporting the WebSocket protocol. However, it currently does not support HTTP 2.0 or SPDY protocol.

## Which SSL protocols are supported by WAF? {#section_tgb_j5k_q2b .section}

**Supported SSL protocols**:

-   WAF instance of the Mainland China region supports the following SSL protocols:
    -   TLSv1
    -   TLSv1.1
    -   TLSv1.2
-   WAF instance of the International region supports the following SSL protocols:
    -   TLSv1.1
    -   TLSv1.2

**Example of SSL\_ciphers suite**:

``` {#codeblock_87e_512_6v8}
"ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES128-SHA256:DHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:DES-CBC3-SHA:HIGH:! aNULL:! eNULL:! EXPORT:! DES:! MD5:! PSK:! RC4"
```

## Can I use different Alibaba Cloud accounts to deploy Alibaba Cloud WAF, CDN, and Anti-DDoS Pro for the same domain name? {#section_vgb_j5k_q2b .section}

Yes. You can deploy Alibaba Cloud WAF, CDN, and Anti-DDoS Pro for the same domain name by using different Alibaba Cloud accounts. For example, you can use Alibaba Cloud account A to deploy Alibaba Cloud WAF for your domain name and use another Alibaba Cloud account B to deploy Anti-DDoS Pro for the same domain name to protect against Web attacks and DDoS attacks.

## Can I use double slashes \(//\) in the URL matching condition of an HTTP ACL rule? {#section_wgb_j5k_q2b .section}

No. The Alibaba Cloud WAF HTTP ACL rule processing engine compresses double or multiple forward slashes into a single slash for standard purposes. Therefore, URL matching conditions with double slashes cannot be correctly matched.

We recommend that you replace the double slash in the URL matching condition with a single slash \(/\). For example, use `/api/sms/request` instead of `//api/sms/request` to let WAF inspect web requests that contain this URI.

## Can I deploy Alibaba Cloud WAF for websites that enable NTML \(NT LAN Manager\) authentication? {#section_wgn_qt3_mgb .section}

No. We recommend that you do not deploy Alibaba Cloud WAF for websites that support NTML authentication. Since the valid web request forwarded by WAF cannot pass the NTML authentication of the origin server, the client encounters repeated authentication requests.

We recommend that you use other authentication methods for your website.

