# Step 2: Update the DNS settings {#concept_afg_dy1_p2b .concept}

When a website configuration is created, Alibaba Cloud WAF generates a dedicated CNAME address for the website. In this step, you enable a CNAME record for the website by using the WAF CNAME address as the value, to redirect web requests to WAF for inspection.

-   If the DNS settings have been updated in **Step 1: Add a website configuration** and the DNS resolution status is Normal, go to [Step 3: Configure WAF protection policies](intl.en-US/Quick Start/Step 3: Configure WAF protection polices.md#).
-   If you are prompted to manually update the DNS settings in **Step 1: Add a website configuration**, or the DNS resolution status is Exception, perform this task.

    The following procedure takes **Alibaba Cloud DNS** as an example to explain how to update the DNS settings, especially the **CNAME record**. If your domain’s DNS is hosted on Alibaba Cloud DNS, follow the procedure. Otherwise, refer to the following procedure and log on to your DNS host's system to update the DNS settings.

    **Note:** We recommend that you use the WAF CNAME address to update the DNS settings. However, using an A record is also supported. In case you must use an A record to update the DNS settings \(for example, CNAME record conflicts with MX record\), see **WAF deployment guide**.


## Prerequisites {#section_iz2_pdl_5fb .section}

-   Obtain the WAF CNAME address.
    1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
    2.  On the top of the page, select the region: **Mainland China**, **International**.
    3.  On the **Management** \> **Website Configuration** page, move the pointer onto the domain name you want to operate. You will see the **Copy CName** button.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15438310577565_en-US.png)

    4.  Click **Copy CName** to copy the WAF CNAME address to the clipboard.

        **Note:** If you want to update A record to redirect web traffic to WAF, you can ping this CNAME address to obtain the corresponding WAF IP address. For more information, see **WAF deployment guide**. In general, the WAF IP address seldom changes.

-   You have permissions to edit the domain’s DNS settings in the DNS host's system. In this example, the domain name is hosted on Alibaba Cloud DNS with the same Alibaba Cloud account as the WAF subscription.

## Procedure {#section_nxs_bfl_5fb .section}

1.  Log on to the [Alibaba Cloud DNS console](https://dns.console.aliyun.com/#/dns/domainList).
2.  Select the domain to be operated and click **Configure**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15438310577588_en-US.jpg)

3.  Select the **Host** \(hostname\) to be operated and click **Edit**.

    Take `abc.com` as an example. You can select hostname as follows:

    -   **www**: matches the subdomain starting with www, in this case `www.abc.com`.
    -   **@**: matches the root domain, in this case `abc.com`.
    -   **\***： matches a wildcard domain name that includes both the root domain and all subdomains, in this case `blog.abc.com`, `www.abc.com`, `abc.com`, and so on.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15438310577589_en-US.jpg)

4.  In the Edit Record dialog box, do the following:

    -   **Type**: Select **CNAME**.
    -   **Value**: Enter the WAF CNAME address.
    -   Leave other settings as they are. We recommend that you set TTL value to 10 minutes. The larger the TTL value, the slower the DNS propagation.
    Notes about editing DNS records:

    -   For a hostname, the CNAME record is unique. You must edit it to the WAF CNAME address.
    -   Different record type conflicts with each other. For example, for a hostname, the CNAME record cannot coexist with an A record, MX record, or TXT record. If you cannot change the record type directly, you can first delete the conflicting records and add a new CNAME record.

        **Note:** The whole process of deleting and adding must be performed in a short time. Otherwise, your domain becomes inaccessible.

    -   If the MX record is being used, you can use an A record to redirect web traffic to WAF. For more information, see **WAF deployment guide**.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15438310577590_en-US.jpg)

5.  Click **OK** to complete the DNS settings and wait for the DNS change to take effect.
6.  \(Optional\) Verify the DNS settings. You can ping the domain or use [DNS Check](https://mxtoolbox.com/dnscheck.aspx) to validate whether the DNS change is effective.

    **Note:** It takes a certain time for the setting to be in effect. If the validation fails, wait for about 10 minutes and re-validate it again.

7.  Check the DNS resolution status.
    1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
    2.  On the **Management** \> **Website Configuration** page, check the **DNS resolution status** of the domain name.
        -   **Normal**: Alibaba Cloud WAF has been successfully deployed and the web traffic is being monitored by WAF.
        -   **Exception**: With the exception messages of **NO CNAME resolution detected**, **No traffic**, or **DNS check failed**, the DNS settings might be incorrect.

            In this case, check the DNS settings. If you confirm that the DNS settings are correct, wait for an hour and refresh the DNS resolution status. For more information, see **DNS resolution status exception**.

            **Note:** The exception here indicates that WAF is not properly deployed. Your website access is not affected.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15553/15411313787685_zh-CN.jpg)


