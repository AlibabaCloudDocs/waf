# Exclusive WAF IP {#concept_qp5_k5n_42b .concept}

An exclusive WAF IP lets you deliver WAF protection to an important domain name through a WAF IP other than the default one, which may be used for multiple domain names.

## What is an exclusive WAF IP? {#section_zcb_n5n_42b .section}

By default, each Alibaba Cloud WAF subscription is assigned a WAF IP address. This WAF IP can be used to access multiple domain names. An exclusive WAF IP gives you an additional WAF IP to access one specific domain name to deliver exclusive protection.

**Note:** Each exclusive WAF IP can only be used for one domain name.

An exclusive WAF IP helps you prevent an important domain name from being affected when other domain names associated with the same WAF IP suffer from massive DDoS attacks. By default, domain names that are configured with the same WAF instance are associated with the same WAF IP. When one of the domain names suffers from high-volume DDoS attacks, the WAF IP address can be blocked by a black hole. As a result, all domain names configured with the WAF IP are affected and become inaccessible. By assigning an exclusive WAF IP for important domain names, you can eliminate the possible impact from other domain names.

## How to buy exclusive WAF IPs? {#section_kpn_55n_42b .section}

When activating Alibaba Cloud WAF, you can include exclusive WAF IPs in your subscription.

**Note:** If you have already activated Alibaba Cloud WAF, you can buy exclusive WAF IPs by upgrading the service. For more information, see [Renewal and upgrade](intl.en-US/Pricing/Renewal and upgrade.md#ol_ut4_hdn_42b).

## How to use exclusive WAF IPs? {#section_fdb_n5n_42b .section}

Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf), and go to the **Management** \> **Website Configuration** page. Locate the target domain name, and enable **Exclusive IP address** for it.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15542/15420727587433_en-US.png)

After the exclusive IP address is enabled, the CNAME address of this domain name is automatically resolved to the new exclusive IP address. You can ping the CNAME of this domain name, and see if the domain name is successfully resolved to the new WAF IP address.

**Note:** If you use A record rather than CNAME resolution, the automatic switching is unavailable. In this case, you must ping the CNAME address to get the new WAF IP, and manually update the DNS records by using the new WAF IP.

