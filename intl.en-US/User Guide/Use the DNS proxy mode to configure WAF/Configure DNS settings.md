# Configure DNS settings {#concept_ngy_ws3_p2b .concept}

This topic describes how to configure DNS settings to activate Web Application Firewall \(WAF\) for your business after you add a website configuration under the DNS proxy mode.

**Note:** You can use the transparent proxy mode to configure WAF for your website if your origin server is deployed on an ECS instance. The ECS instance must be created in the China \(Qingdao\), China \(Beijing\), China \(Zhangjiakou\), or China \(Hohhot\) region, and have a public IP address or be associated with an EIP.

-   Transparent proxy mode: This mode directs HTTP requests that are received on port 80 of the specified origin server to WAF. WAF processes the requests and then redirects the requests to the origin server.

    To use this mode, you must authorize WAF to access the ECS instances where your origin server is deployed. To configure this mode, add a domain and specify the IP address of the server that hosts your website in the WAF console. For more information, see [Use the transparent proxy mode to configure WAF](reseller.en-US/User Guide/Use the transparent proxy mode to implement WAF.md#).

-   DNS proxy mode: This mode directs requests that are sent to the protected domain to WAF based on the specified DNS record. WAF then processes and redirects the requests to the specified origin server.

    This mode requires you to add a website configuration in the WAF console and update DNS settings of the domain.


When you use the DNS proxy mode to configure WAF for your website, you must [add a website configuration](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#) first. After you add the website configuration, you can [edit CNAME records](#) or [A records](#) to update the DNS settings to redirect requests that are sent to your website to WAF for monitoring.

**Note:** We recommend that you use CNAME records. If an error occurs, such as node failures or failures in a server room, CNAME records allow WAF to use another WAF IP address, or direct the requests to the origin server directly. This keeps your business running normally and increases high availability and disaster recovery capabilities.

The following sections describes how to configure WAF for a website that does not use CDN, Anti-DDoS Pro, or other proxy services. For more information about deploying multiple proxy services, see the following topics:

-   [Deploy WAF and CDN together](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Deploy WAF and CDN together.md#): This topic describes how to deploy CDN and WAF for your website.
-   [Deploy WAF and Anti-DDoS Pro together](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Deploy WAF and Anti-DDoS Pro together.md#): This topic describes how to deploy Anti-DDoS Pro and WAF for your website.

## \(Recommended\) Use CNAME records to deploy WAF {#cname .section}

**Prerequisites**

-   You have added the website configuration for your website. For more information, see [Website configuration](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#).
-   You have obtained the WAF CNAME address.
    1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
    2.  On the top of the page, select **Mainland China** or **International**.
    3.  Choose **Management** \> **Website Configuration** and select **DNS Proxy Mode**. Select the website configuration and hover over the domain name. A **Copy CName** button appears.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15532341407565_en-US.png)

    4.  Click **Copy CName** to copy the WAF CNAME address.

        **Note:** If you want to use an A record to redirect requests to WAF, ping this CNAME address to obtain the corresponding WAF IP address. For more information, see [Set DNS settings](../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#). The IP address of the WAF instance that protects your website changes infrequently.

-   You have permissions to update the domain DNS settings at your DNS service provider.
-   \(Optional\) Whitelist WAF back-to-origin CIDR blocks. If your origin server uses non-Alibaba Cloud security software, such as Safedog and Jowto Lock, you must whitelist the WAF back-to-origin CIDR block to prevent normal traffic redirected to the origin server by WAF from being blocked. For more information, see [Whitelist Alibaba Cloud WAF IP addresses](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Whitelist Alibaba Cloud WAF IP addresses.md#).
-   \(Optional\) Verify redirection rules. You can use a local computer to verify that the redirection rules are correctly configured before you change the DNS records of your website. This avoids business interruption caused by configuration errors. For more information, see [Perform redirect check with a local computer](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Perform redirect check with a local computer.md#).

**Procedure**

The following example uses **Alibaba Cloud DNS** to describe how to specify a **CNAME** record. If your domain is hosted on Alibaba Cloud DNS, perform the following steps to change DNS records. If your domain is not hosted on Alibaba Cloud DNS, perform the following steps to change DNS records at your DNS service provider.

1.  Log on to the **Alibaba Cloud DNS console**.
2.  Select the domain name and click **Configure**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15532341407588_en-US.jpg)

3.  Select the specified **host** \(hostname\) and click **Edit**.

    The following example uses `abc.com`:

    -   **www**: Used to select domain names that begin with www, such as `www.abc.com`.
    -   **@**: Matches the root domain `abc.com`.
    -   **\***: Matches all wildcard domains including root domains and subdomains, such as `blog.abc.com`, `www.abc.com`, and `abc.com`.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15532341417589_en-US.jpg)

4.  In the Edit Record dialog box, perform the following operations:

    -   **Type**: Select **CNAME**.
    -   **Value**: Paste the WAF CNAME address that you have copied in the preceding step.
    -   Keep the remaining settings unchanged. We recommend that you set the TTL to 10 minutes. A longer TTL indicates that the system takes a longer time to synchronize and update the DNS record.
    Notes:

    -   You can only specify one CNAME record for each hostname. Change the value to the WAF CNAME address.
    -   Different record types conflict with each other. For example, a CNAME record, an A record, an MX record, and a TXT record cannot coexist with each other under the same hostname. If you cannot change the record type, delete all conflicting records, and then add a new CNAME record.

        **Note:** You must delete conflicting records and add the new CNAME record in a short period of time. Otherwise, your domain becomes inaccessible.

    -   If you must keep the MX record, you can use an A record to redirect requests to WAF. For more information, see [Set DNS settings](../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#).
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15532341417590_en-US.jpg)

5.  Click **OK** and wait for the DNS record to take effect.
6.  \(Optional\) Verify the DNS settings. Ping the domain or use [DNS Check](https://mxtoolbox.com/dnscheck.aspx) to check whether the DNS record takes effect.

    **Note:** It takes some time for the DNS record to take effect. If the verification fails, verify the DNS record again in 10 minutes.

7.  Check the DNS resolution status.
    1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf).
    2.  Choose **Management** \> **Website Configuration** and select **DNS Proxy Mode** to view the **DNS translation status**.
        -   **Normal** indicates that WAF has been successfully configured for your website. All requests that are sent to your website are redirected to WAF for monitoring.
        -   **Exception** indicates that you have not correctly configured WAF for you website if the following error messages appear: **No CNAME resolution detected**, **No traffic**, and **DNS check failed**.

            If you confirm that the DNS settings are correct, check the DNS translation status again in an hour, or troubleshoot the errors. For more information about troubleshooting, see [DNS resolution status exception](../reseller.en-US/FAQ/DNS resolution status exception.md#).

            **Note:** The error message, as shown in the following figure, only indicates whether you have correctly configured WAF for your website. It does not indicate whether your website is accessible.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15532341417591_en-US.jpg)


**Protect the origin server**

If your origin server IP address is exposed, attackers may bypass WAF and launch attacks on your origin server. To avoid attacks, we recommend that you configure an ECS security group or SLB whitelist to block malicious requests. For more information, see [Protect your origin server](../reseller.en-US/Best Practices/Protect your origin server.md#).

## Use A records to deploy WAF {#a-record .section}

The procedures to specify A records and CNAME records are similar. However, they have the following two differences:

-   **Prerequisites**: After you have obtained the WAF CNAME address, follow these steps to obtain the WAF IP address:
    1.  In a Windows operating system, open Command Prompt.
    2.  Run the following command: `ping “copied WAF CNAME address”`.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15553/155323414132229_en-US.png)

    3.  Record the WAF IP address that is displayed in the command output.
-   **Procedure**: Perform the following steps in step 4:
    -   **Type**: Change the type to **A**.
    -   **Value**: Enter the WAF IP address.
    -   Keep the remaining settings unchanged.

