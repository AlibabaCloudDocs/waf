# Step 2: Update the DNS settings {#concept_afg_dy1_p2b .concept}

After you use the DNS proxy mode to configure Web Application Firewall \(WAF\) for your website and add the website configuration, WAF automatically generates a CNAME address for your website. You can use this CNAME address to update the CNAME value to redirect requests that are sent to your website to WAF for monitoring.

-   If the DNS settings have been automatically updated in [Step 1: Automatically add a website configuration](reseller.en-US/Quick Start/Step 1: Automatically add a website configuration.md#) and the DNS resolution status is Normal, skip this step and perform [Step 3: Configure WAF protection policies](reseller.en-US/Quick Start/Step 3: Configure WAF protection polices.md#).
-   If you are required to update DNS settings manually or the DNS resolution status is Exception in [Step 1: Automatically add a website configuration](reseller.en-US/Quick Start/Step 1: Automatically add a website configuration.md#), perform the following steps to update the DNS settings.

    The following example uses **Alibaba Cloud DNS** to describe how to change a **CNAME** record. If your domain name is managed by Alibaba Cloud DNS, perform the following steps to update the DNS settings. If your domain name is managed by other DNS service providers, perform the following steps to update the DNS settings in the system of your DNS service provider.

    **Note:** To enable WAF, you need to add a CNAME or A record to redirect requests. For more information about using A records, see [Configure DNS settings](../../../../../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#).


## Prerequisites {#section_iz2_pdl_5fb .section}

-   You have obtained the WAF CNAME address.
    1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
    2.  On the top of the page, select **Mainland China** or **International**.
    3.  Choose **Management** \> **Website Configuration** and select **DNS Proxy Mode**. Select the website configuration and hover over the domain name. A **Copy CName** button appears.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15532337907565_en-US.png)

    4.  Click **Copy CName** to copy the WAF CNAME address.

        **Note:** If you want to use an A record to redirect requests to WAF, ping this CNAME address to obtain the corresponding WAF IP address. For more information, see [Set DNS settings](../../../../../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#). The IP address of the WAF instance that protects your website changes infrequently.

-   You have the permissions to change the domain DNS settings in the system of your DNS service provider. This example uses a DNS record that is managed by Alibaba Cloud DNS, and WAF is activated under the same account.

## Procedure {#section_nxs_bfl_5fb .section}

1.  Log on to the **Alibaba Cloud DNS console**.
2.  Select the domain name and click **Configure**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15532337907588_en-US.jpg)

3.  Select the specified **host** \(hostname\) and click **Edit**.

    The following example uses `abc.com`:

    -   **www**: Used to select domain names that begin with www, such as `www.abc.com`.
    -   **@**: Matches the root domain `abc.com`.
    -   **\***: Matches all wildcard domains including root domains and subdomains, such as `blog.abc.com`, `www.abc.com`, and `abc.com`.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15532337917589_en-US.jpg)

4.  In the Edit Record dialog box, perform the following operations:

    -   **Type**: Select **CNAME**.
    -   **Value**: Paste the WAF CNAME address that you have copied in the preceding step.
    -   Keep the remaining settings unchanged. We recommend that you set the TTL to 10 minutes. A longer TTL indicates that the system takes a longer time to synchronize and update the DNS record.
    Notes:

    -   You can only specify one CNAME record for each hostname. Change the value to the WAF CNAME address.
    -   Different record types conflict with each other. For example, a CNAME record, an A record, an MX record, and a TXT record cannot coexist with each other under the same hostname. If you cannot change the record type, delete all conflicting records, and then add a new CNAME record.

        **Note:** You must delete conflicting records and add the new CNAME record in a short period of time. Otherwise, your domain becomes inaccessible.

    -   If you must keep the MX record, you can use an A record to redirect requests to WAF. For more information, see [Set DNS settings](../../../../../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#).
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15532337917590_en-US.jpg)

5.  Click **OK** and wait for the DNS record to take effect.
6.  \(Optional\) Verify the DNS settings. Ping the domain or use [DNS Check](https://mxtoolbox.com/dnscheck.aspx) to check whether the DNS record takes effect.

    **Note:** It takes some time for the DNS record to take effect. If the verification fails, verify the DNS record again in 10 minutes.

7.  Check the DNS resolution status.
    1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf).
    2.  Choose **Management** \> **Website Configuration** and select **DNS Proxy Mode** to view the **DNS translation status**.
        -   **Normal** indicates that WAF has been successfully configured for your website. All requests that are sent to your website are redirected to WAF for monitoring.
        -   **Exception** indicates that you have not correctly configured WAF for you website if the following error messages appear: **No CNAME resolution detected**, **No traffic**, and **DNS check failed**.

            If you confirm that the DNS settings are correct, check the DNS translation status again in an hour, or troubleshoot the errors. For more information about troubleshooting, see [DNS resolution status exception](../../../../../reseller.en-US/FAQ/DNS resolution status exception.md#).

            **Note:** The error message, as shown in the following figure, only indicates whether you have correctly configured WAF for your website. It does not indicate whether your website is accessible.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15532337917591_en-US.jpg)


