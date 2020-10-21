# Web Application Firewall FAQ

-   [Can I use Web Application Firewall \(WAF\) to protect servers that are not deployed in Alibaba Cloud?](#section_gh5_30i_8dd)
-   [Does WAF support Cloud Web Hosting instances?](#section_4ot_vhn_lr7)
-   [How can I use WAF to defend against HTTP flood attacks?](#section_w3y_x9e_ik6)
-   [Does WAF protect HTTPS services?](#section_g7h_5wh_954)
-   [Does WAF support custom server ports?](#section_1kb_tmq_etu)
-   [Is the QPS limit configured in the WAF console applied to a WAF instance or a single domain name?](#section_gti_77s_y1g)
-   [Which editions of WAF can prevent SMS flooding?](#section_i9n_4eq_fxi)
-   [Can I enter the internal IP address of an ECS instance as the IP address of an origin server in the WAF console?](#section_f39_s8b_788)
-   [Can WAF be deployed with CDN or with Anti-DDoS Pro or Anti-DDoS Premium?](#section_1jz_tnq_me3)
-   [Can WAF protect IP addresses of multiple origin servers under one domain name?](#section_kiv_2vu_kn4)
-   [How does WAF balance request loads among multiple origin servers?](#section_hnl_jl2_b0f)
-   [Does WAF support the health check feature?](#section_531_5ry_lzh)
-   [Does WAF support session persistence?](#section_g2y_ez7_zxn)
-   [Does latency occur when you change an origin server IP address in the WAF console?](#section_vfn_2gs_sdr)
-   [How long does it take for modifications in the WAF console to take effect?](#section_toy_4ti_4db)
-   [What are back-to-origin CIDR blocks of WAF?](#section_wj9_s6i_6qj)
-   [Does WAF automatically add its back-to-origin CIDR blocks to security groups?](#section_og6_h6h_pf4)
-   [Do I need to allow accesses from all client IP addresses?](#section_7zd_nhc_56u)
-   [Can I view the source IP addresses of HTTP flood attacks in the WAF console?](#section_lcj_2l0_ng8)
-   [How can I query the bandwidth usage of WAF?](#section_tgu_d2s_02g)
-   [Can I enter CIDR blocks in the IP field when I configure custom protection policies \(ACL policies\) in the WAF console?](#section_2c3_w4b_mzi)
-   [Can a WAF instance that uses an exclusive IP address defend against DDoS attacks?](#section_s10_fsh_yxt)
-   [Does WAF support HTTPS two-way authentication?](#section_8vh_d8q_l7q)
-   [Does WAF support the WebSocket, HTTP/2, and SPDY protocols?](#section_o0b_5z7_sfp)
-   [Which SSL protocols does WAF support?](#section_lda_atd_b8h)
-   [Can I deploy WAF with CDN and Anti-DDoS Pro or Anti-DDoS Premium by using different accounts?](#section_g02_y48_bsv)
-   [Why does a custom protection policy in which the URL matching field contains two forward slashes \(//\) not take effect?](#section_cup_65t_0x5)
-   [Can WAF protect websites that use NTLM authentication?](#section_qz6_ku4_9as)
-   [What do I need to know about migrating website configurations across accounts?](#section_isn_6f4_2po)

## Can I use Web Application Firewall \(WAF\) to protect servers that are not deployed in Alibaba Cloud?

Yes, WAF can protect servers that are not deployed in Alibaba Cloud. WAF protects servers that are accessible over the Internet no matter whether they are deployed in Alibaba Cloud, third-party cloud platforms, or on-premises data centers.

**Note:** All domain names that are hosted on servers in mainland China must apply for and receive an ICP filing as stipulated by the Ministry of Industry and Information Technology \(MIIT\). Otherwise, the domain mains cannot be added to the WAF console.

## Does WAF support Cloud Web Hosting instances?

Yes, all editions of WAF support exclusive instances of Cloud Web Hosting. After you activate WAF, you can configure exclusive instances in the WAF console.

Shared instances of Cloud Web Hosting use shared IP addresses, which means that multiple users use the same origin server. We recommend that you do not configure WAF for the shared instances.

## How can I use WAF to defend against HTTP flood attacks?

WAF provides various HTTP flood protection modes. You can select a mode as needed. For more information, see [Configure HTTP flood protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure HTTP flood protection.md).

To achieve better protection and lower false positive rates, you can use the WAF Business edition or WAF Enterprise edition and request security experts to tailor protection algorithms specific to your business. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).

## Does WAF protect HTTPS services?

Yes, all editions of WAF can protect HTTPS services. You can also add wildcard domain names to the WAF console.

To protect HTTPS services, you must upload SSL certificates and private keys as prompted. After the HTTPS services are protected, WAF decrypts access requests, examines request packets, encrypts the requests, and then forwards the requests to origin servers.

## Does WAF support custom server ports?

The Business and Enterprise editions of WAF support custom non-standard ports. The Business edition supports up to 10 non-standard ports and the Enterprise edition supports up to 50 non-standard ports.

**Note:** These non-standard ports must fall in the allowed port range. For more information, see [Supported custom ports](/intl.en-US/Website Access/Supported custom ports.md).

## Is the QPS limit configured in the WAF console applied to a WAF instance or a single domain name?

The QPS limit applies to a WAF instance.

For example, if you configure three domain names in the WAF console, the total QPS of these domain names cannot exceed the limit. If the total QPS exceeds the limit, WAF triggers throttling and may discard packets at random.

## Which editions of WAF can prevent SMS flooding?

All editions of WAF can prevent SMS flooding. For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).

## Can I enter the internal IP address of an ECS instance as the IP address of an origin server in the WAF console?

You cannot enter the internal IP address of an ECS instance. This is because WAF redirects requests to an origin server over the Internet.

## Can WAF be deployed with CDN or with Anti-DDoS Pro or Anti-DDoS Premium?

Yes, WAF is fully compatible with CDN, Anti-DDoS Pro, and Anti-DDoS Premium. If you want to deploy WAF together with CDN and Anti-DDoS Pro or Anti-DDoS Premium, we recommend that you deploy components in the following sequence: client, Anti-DDoS Pro or Anti-DDoS Premium, CDN, WAF, SLB, and origin server.

If you want to deploy WAF with CDN or with Anti-DDoS Pro or Anti-DDoS Premium, configure the address of the origin server to the CNAME address of WAF when you add a domain name to CDN, Anti-DDoS Pro, or Anti-DDoS Premium. In this case, requests are forwarded by CDN, Anti-DDoS Pro, or Anti-DDoS Premium to WAF and then to the origin server. This way, the origin server is protected. For more information, see the following topics:

-   [t15558.md\#](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and CDN together.md)
-   [Deploy WAF and Anti-DDoS Pro together](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and Anti-DDoS Pro together.md)

## Can WAF protect IP addresses of multiple origin servers under one domain name?

Yes, you can add a maximum of 20 origin server IP addresses when you configure a domain name in the WAF console.

## How does WAF balance request loads among multiple origin servers?

If you configure multiple origin servers, WAF balances request loads among them by using a round-robin method.

## Does WAF support the health check feature?

Yes, WAF supports the health check feature. This feature is enabled by default. WAF checks the access status of each origin server IP address. If an origin server IP address does not respond, WAF forwards the requests destined for the IP address to another origin server IP address.

**Note:** If an origin server IP address does not respond, WAF automatically sets a cooldown period during which WAF does not forward requests to this IP address. After the cooldown period elapses, new requests may be forwarded to this origin server IP address. For more information about how the health check feature works, see [Health check overview](/intl.en-US/User Guide/Health check/Health check overview.md).

## Does WAF support session persistence?

Yes, WAF supports session persistence. However, session persistence is disabled by default. If you want to enable session persistence, submit a [ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80) to contact technical support.

## Does latency occur when you change an origin server IP address in the WAF console?

Yes, latency occurs when you change an origin server IP address. The new IP address takes effect about one minute later.

## How long does it take for modifications in the WAF console to take effect?

In most cases, modifications take effect within one minute.

## What are back-to-origin CIDR blocks of WAF?

You can query back-to-origin CIDR blocks in the WAF console. Perform the following operations: Log on to the [WAF console](https://yundun.console.aliyun.com/?p=waf) and choose **System Management** \> **Product Information**. For more information, see [Allow access from WAF back-to-origin CIDR blocks](/intl.en-US/Website Access/Website access with CNAME/Allow access from WAF back-to-origin CIDR blocks.md).

## Does WAF automatically add its back-to-origin CIDR blocks to security groups?

No, WAF does not automatically add its back-to-origin CIDR blocks to security groups. If you deploy other firewall or host protection software for origin servers, we recommend that you add the back-to-origin CIDR blocks of WAF to the required whitelists.

We recommend that you configure protection policies for the origin servers. For more information, see [Configure protection for your origin server](/intl.en-US/Website Access/Website access with CNAME/Configure protection for your origin server.md).

## Do I need to allow accesses from all client IP addresses?

You can allow accesses from only back-to-origin CIDR blocks of WAF or from all client IP addresses.

To protect web services of origin servers, we recommend that you allow accesses from only the back-to-origin CIDR blocks of WAF.

## Can I view the source IP addresses of HTTP flood attacks in the WAF console?

Yes, you can view the source IP addresses of HTTP flood attacks after you enable Log Service of WAF. For more information, see [Enable Log Service for WAF](/intl.en-US/Log Management/Log service/Enable Log Service for WAF.md) and [Enable log query](/intl.en-US/Log Management/Log service/Enable log query.md).

## How can I query the bandwidth usage of WAF?

You can query the bandwidth usage of WAF on the **Overview** page in the [WAF console](https://yundun.console.aliyun.com/?p=waf).

## Can I enter CIDR blocks in the IP field when I configure custom protection policies \(ACL policies\) in the WAF console?

Yes, you can enter CIDR blocks in the IP field when you configure custom protection policies in the WAF console.

## Can a WAF instance that uses an exclusive IP address defend against DDoS attacks?

Yes, a WAF instance that uses an exclusive IP address can defend against DDoS attacks.

-   WAF provides exclusive IP addresses for users. Blackhole filtering that defend against DDoS attacks can apply to these IP addresses, similar to IP addresses of ECS and SLB instances.
-   The default DDoS mitigation capability provided by the WAF instance that uses an exclusive IP address is the same as the DDoS mitigation capability of an ECS instance in the region where WAF is deployed.

## Does WAF support HTTPS two-way authentication?

No, WAF does not support HTTPS two-way authentication.

## Does WAF support the WebSocket, HTTP/2, and SPDY protocols?

All editions of WAF support WebSocket, and WAF Business or a higher edition supports HTTP/2. Currently, WAF does not support SPDY.

## Which SSL protocols does WAF support?

-   In the regions inside mainland China, WAF supports the following SSL protocols:
    -   TLS v1.0
    -   TLS v1.1
    -   TLS v1.2
-   In the regions outside mainland China, WAF supports the following SSL protocols:
    -   TLS v1.1
    -   TLS v1.2

`ssl_ciphers` suite example:

```
"ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES128-SHA256:DHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:DES-CBC3-SHA:HIGH:! aNULL:! eNULL:! EXPORT:! DES:! MD5:! PSK:! RC4"
```

## Can I deploy WAF with CDN and Anti-DDoS Pro or Anti-DDoS Premium by using different accounts?

Yes, you can deploy WAF with CDN and Anti-DDoS Pro or Anti-DDoS Premium by using different accounts to defend against DDoS and web application attacks.

## Why does a custom protection policy in which the URL matching field contains two forward slashes \(//\) not take effect?

When the rules engine of WAF processes the URL matching field, it compresses consecutive forward slashes \(/\). Therefore, the rules engine cannot match the rule of the custom protection policy because the URL matching field contains two forward slashes \(//\).

If you want to define an ACL rule in which the URL matching field has two forward slashes \(//\), enter a single forward slash \(/\) instead. For example, if you want to set the URL matching field to `//api/sms/request`, enter `/api/sms/request` instead. This way, WAF can correctly implement access control based on the rule.

## Can WAF protect websites that use NTLM authentication?

No, WAF cannot protect websites that use NTLM authentication. If your website uses New Technology LAN Manager \(NTLM\) authentication, access requests forwarded by WAF may fail to pass the NTLM authentication of an origin server, and authentication prompts may be repeatedly displayed on the client. We recommend that you use a different authentication method for your website.

## What do I need to know about migrating website configurations across accounts?

To prevent traffic forwarding errors caused by misoperations during website configuration migration, a 30-minute protection period is configured for your website. To migrate the website configurations to another account, you must delete the website configurations from the current account. Thirty minutes later, you can add the website configurations to the WAF instance of another account.

If you want to immediately migrate the website configurations, submit a [ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80) or apply for a protection period cancellation for this domain name in the DingTalk customer support group. After the protection period is canceled, you can add the website configurations to the WAF instance of another account.

