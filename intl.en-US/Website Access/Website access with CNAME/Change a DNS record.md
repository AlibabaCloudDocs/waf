# Change a DNS record

After you add your website to WAF, you must use the CNAME or IP address of WAF to change the DNS record to redirect requests destined for your website to WAF. This topic describes how to change the DNS record.

-   The website configurations are manually added to WAF in CNAME mode. For more information, see [Manually add website configurations](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).
-   You have the permissions to change the DNS record at your DNS service provider.
-   Requests from WAF back-to-origin CIDR blocks are allowed on the origin server. For more information, see [Allow access from WAF back-to-origin CIDR blocks](/intl.en-US/Website Access/Website access with CNAME/Allow access from WAF back-to-origin CIDR blocks.md).

    **Note:** If you use security software such as FortiGate for your origin server, you must add the WAF back-to-origin CIDR blocks to the whitelist of the software. This prevents normal traffic from being blocked by access control policies.

-   The forwarding configurations for your website are correct and in effect. Before you change the DNS record, you must verify that the website forwarding configurations are correct. This prevents service interruptions caused by invalid configurations. For more information, see [Verify domain name settings](/intl.en-US/Website Access/Website access with CNAME/Verify domain name settings.md).

    **Warning:** If you change the DNS record before the forwarding configurations for your website take effect, service interruptions may occur.


WAF redirects requests in one of the following methods:

-   CNAME record: resolves the domain name to the CNAME assigned by WAF.

    We recommend that you use the CNAME record method. If failures occur, such as node failures or failures in a data center, the CNAME record allows WAF to use another WAF IP address or directs requests to the origin server directly. This ensures service continuity and provides high availability and disaster recovery capabilities.

-   A record: resolves the domain name to the WAF IP address.

    We recommend that you use the A record method only when the CNAME record conflicts with the existing DNS settings. For example, the CNAME record conflicts with the MX record, and the MX record must be retained.


The following sections describe how to configure WAF for a website that does not use proxy services, such as CDN and Anti-DDoS Pro or Anti-DDoS Premium. If you want to deploy both WAF and other proxy services, see the following topics:

-   [t15558.md\#](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and CDN together.md)
-   [Deploy WAF and Anti-DDoS Pro together](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and Anti-DDoS Pro together.md)

## Obtain the WAF CNAME and WAF IP address

You must obtain the WAF CNAME or WAF IP address of your domain name before you change the DNS record. If you have already obtained the WAF CNAME or IP address, skip the following steps.

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Asset Center** \> **Website Access**.

4.  On the **Domain Names** tab of the Website Access page, move the pointer over the domain name and copy the WAF CNAME.

    ![CNAME record](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7801549951/p97144.png)

5.  Obtain the WAF IP address of the domain name.

    **Note:** Perform this step only when you use the A record. If you use the CNAME record, skip this step.

    1.  Open Command Prompt in Windows.

    2.  Run the following command to obtain the WAF IP address:

        ```
        ping <WAF CNAME that you have copied>
        ```

    3.  Record the WAF IP address in the command output.


## Use Alibaba Cloud DNS to change the DNS record

The following example demonstrates how to change the DNS record in Alibaba Cloud DNS. If your domain name is hosted on Alibaba Cloud DNS, perform the following steps to change the DNS record. If your domain name is not hosted on Alibaba Cloud DNS, refer to the following steps to change the DNS record at your DNS service provider.

1.  Log on to the[Alibaba Cloud DNS console](https://partners-dns.console.aliyun.com/#/dns/domainList).

2.  On the **Manage DNS** page, find the domain name and click **Configure** in the Actions column.

3.  On the **DNS Settings** page, find the record in the **Host** column and click **Edit** in the Actions column.

    In the following example, `aliyun.com` is used:

    -   **www**: matches domain names that begin with www, such as `www.aliyun.com`.
    -   **@**: matches the root domain name, for example, `aliyun.com`.
    -   **\***: matches all wildcard domain names, such as `blog.aliyun.com`, `www.aliyun.com`, and `aliyun.com`. The wildcard domain names include root domain names and subdomain names.
4.  In the **Add Record** dialog box, select the CNAME record or the A record to change the DNS record.

    -   CNAME record: Set **Type** to **CNAME** and **Value** to the WAF CNAME and keep other settings unchanged.

        **Note:** We recommend that you set the TTL to 10 minutes. The greater the TTL is, the longer it takes to synchronize and change the DNS record.

        ![Change a DNS record ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7801549951/p7590.png)

        Note the following descriptions about conflicts:

        -   You can specify only one CNAME value for each record name. Set Value to the CNAME assigned by WAF.
        -   Different types of DNS records conflict with each other. For example, you cannot add a CNAME record and an A, MX, or TXT record with the same record name. If you cannot change the record type, delete all conflicting records and add a new CNAME record.

            **Warning:** You must delete all conflicting records and add the new CNAME record in a short period of time. Otherwise, your domain name becomes inaccessible.

        -   If you must retain the MX record, we recommend that you use the A record method to resolve the domain name to the WAF IP address.
    -   A record: Set **Type** to **A** and **Value** to the WAF IP address and keep other settings unchanged.

        **Note:** We recommend that you set the TTL to 10 minutes. The greater the TTL is, the longer it takes to synchronize and change the DNS record.

        ![A record](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7801549951/p97160.png)

5.  Click **OK** and wait for the new DNS record to take effect

6.  Verify the DNS record. You can ping the domain name of your website or use a DNS detection tool to verify whether the DNS record takes effect.

    **Note:** The DNS record does not take effect immediately. If the verification fails, verify the DNS record again after 10 minutes.


## References

-   Protect the origin server.

    If the IP address of your origin server is exposed, attackers may bypass WAF and directly attack your origin server. To avoid such attacks, we recommend that you configure an ECS security group or SLB whitelist. For more information, see [Configure protection for an origin server](/intl.en-US/Website Access/Website access with CNAME/Configure protection for an origin server.md).

-   Retrieve actual IP addresses of clients.

    After you add your website to WAF, WAF processes all requests destined for your website and forwards normal requests to the origin server. In this case, you must use the `X-Forwarded-For` header to retrieve the actual IP addresses of clients. For more information, see [Retrieve actual IP addresses of clients](/intl.en-US/Website Access/Retrieve actual IP addresses of clients.md).


