# Exclusive IP addresses

You can purchase exclusive IP addresses for Web Application Firewall \(WAF\) to protect important domain names. Each exclusive IP address protects one domain name. A domain name that is protected by an exclusive IP address can be accessed even if other domain names in the same WAF instance are under DDoS attacks. The other domain names use a shared IP address.

## Introduction to exclusive IP addresses

When you purchase a WAF instance, it has a default IP address, which can be used to protect multiple domain names in the instance. This default IP address is a shared IP address. If you want to use one IP address to exclusively protect a domain name, you must purchase an exclusive IP address. One exclusive IP address can be bound to only one domain name.

**Note:** Subscription WAF instances of the Pro edition or higher support exclusive IP addresses.

If a domain name is under DDoS attacks, the exclusive IP address that protects the domain name can also help prevent other domain names in the same WAF instance from access failures. By default, a WAF instance uses a shared IP address to protect all domain names. If traffic of this shared IP address is routed to a blackhole due to DDoS attacks on one of the domain names, the other domain names cannot be accessed. In the preceding situation, we recommend that you purchase exclusive IP addresses to protect important domain names from access failures.

## Purchase an exclusive IP address

You can purchase exclusive IP addresses when you purchase a subscription WAF instance.

**Note:** If you have purchased a WAF instance, you can upgrade the instance to purchase exclusive IP addresses. For more information, see [t15543.md\#section\_h76\_hk9\_g1k](/intl.en-US/Pricing/Renewal and upgrade.md).

## Assign and enable an exclusive IP address

Log on to the [WAF console](https://yundun.console.aliyun.com/?p=waf). In the left-side navigation page, choose **Assets** \> **Website Access**. On the page that appears, set **Protection Resource** to **Shared Cluster and Exclusive IP** in the **Quick Access** column.

After you enable an exclusive IP address for a domain name and the CNAME record is used for access, the domain name is automatically resolved to the exclusive IP address. You can ping the CNAME of the domain name to check whether the resolution directs to the required exclusive IP address.

**Note:** If the A record is used for access, the domain name cannot be automatically resolved to the exclusive IP address. You must ping the CNAME of the domain name to obtain the exclusive IP address and manually change the DNS record.

