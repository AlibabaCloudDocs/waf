# Implement Alibaba Cloud WAF {#concept_ngy_ws3_p2b .concept}

Deploying Alibaba Cloud WAF for a website indicates updating the DNS records \(CNAME or A type\) after the website configuration is created, to redirect web requests to WAF for inspection.

You can use a [CNAME record](#) or [A record](#) to redirect web traffic. We recommend that you use CNAME. Using CNAME supports node switch or even redirecting traffic back to source in case of node failure or machine failure, which improves your business’s availability and failure recovery capacity.

The following content applies to deploying Alibaba Cloud WAF exclusively for the website, that is, the website does not use CDN, DDoS protection, and other proxy services. For other scenarios, see the following documents:

-   [Deploy Alibaba Cloud WAF and CDN together](reseller.en-US/User Guide/Implementation/Deploy WAF and CDN together.md#): explains how to deploy CDN and WAF together for your website.
-   [Deploy Alibaba Cloud WAF and DDoS protection together](reseller.en-US/User Guide/Implementation/Deploy WAF and Anti-DDoS Pro together.md#): explains how to deploy DDoS protection and WAF together for your website.

## \(Recommended\) Edit CNAME record to deploy WAF {#cname .section}

**Prerequisites**

-   Website configuration is successfully created. For more information, see [Website configuration](reseller.en-US/User Guide/Implementation/Website configuration.md#).
-   Obtain the WAF CNAME address.
    1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
    2.  On the top of the page, select the region: **Mainland China**, **International**.
    3.  On the **Management** \> **Website Configuration** page, move the pointer onto the domain name you want to operate. You will see the **Copy CName** button.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15507166407565_en-US.png)

    4.  Click **Copy CName** to copy the WAF CNAME address to the Clipboard.

        **Note:** If you want to update A record to redirect web traffic to WAF, you can ping this CNAME address to obtain the corresponding WAF IP address. For more information, see [WAF deployment guide](../reseller.en-US/User Guide/Implementation/Implement Alibaba Cloud WAF.md#). In general, the WAF IP address seldom changes.

-   You have permissions to update the domain’s DNS settings in its DNS host’s system.
-   \(Optional\) Whitelist Alibaba Cloud WAF IP addresses. If your origin web server has enabled non-Alibaba Cloud security software \(such as Fortinet FortiGate\), you must whitelist WAF IP addresses in the software to prevent legitimate traffic returned by WAF from being blocked. For more information, see [Whitelist Alibaba Cloud WAF IP addresses](reseller.en-US/User Guide/Implementation/Whitelist Alibaba Cloud WAF IP addresses.md#).
-   \(Optional\) Perform redirect check with a local computer. Perform a redirect check to guarantee that all configuration is correct, before you change the DNS settings. This helps avoid business interruption due to incorrect configuration. For more information, see [Perform redirect check with a local computer](reseller.en-US/User Guide/Implementation/Perform redirect check with a local computer.md#).

**Procedure**

The following steps explain how to update the **CNAME** record in **Alibaba Cloud DNS**. If your domain is hosted in Alibaba Cloud DNS, follow these steps. Otherwise, you must log on to your DNS host’s system to do the modification.

1.  Log on to the **Alibaba Cloud DNS console**.
2.  Select the domain to be operated and click **Configure**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15507166407588_en-US.jpg)

3.  Select the **Host** \(hostname\) to be operated and click **Edit**.

    Take `abc.com` as an example. You can select hostname as follows:

    -   **www**: matches the subdomain starting with www, in this case `www.abc.com`.
    -   **@**: matches the root domain, in this case `abc.com`.
    -   **\***: matches a wildcard domain name that includes both the root domain and all subdomains, in this case `blog.abc.com`, `www.abc.com`, `abc.com`, and so on.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15507166407589_en-US.jpg)

4.  In the Edit Record dialog box, do the following:

    -   **Type**: Select **CNAME**.
    -   **Value**: Enter the WAF CNAME address.
    -   Leave other settings as they are. We recommend that you set TTL value to 10 minutes. The larger the TTL value, the slower the DNS propagation.
    Notes about editing DNS records:

    -   For a hostname, the CNAME record is unique. You must edit it to the WAF CNAME address.
    -   Different record type conflicts with each other. For example, for a hostname, the CNAME record cannot coexist with an A record, MX record, or TXT record. If you cannot change the record type directly, you can first delete the conflicting records and add a new CNAME record.

        **Note:** The whole process of deleting and adding must be performed in a short time. Otherwise, your domain becomes inaccessible.

    -   If the MX record is being used, you can use an A record to redirect web traffic to WAF. For more information, see [WAF deployment guide](../reseller.en-US/User Guide/Implementation/Implement Alibaba Cloud WAF.md#).
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15507166407590_en-US.jpg)

5.  Click **OK** to complete the DNS settings and wait for the DNS change to take effect.
6.  \(Optional\) Verify the DNS settings. You can ping the domain or use [DNS Check](https://mxtoolbox.com/dnscheck.aspx) to validate whether the DNS change is effective.

    **Note:** It takes a certain time for the setting to be in effect. If the validation fails, wait for about 10 minutes and re-validate it again.

7.  Check the DNS resolution status.
    1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
    2.  On the **Management** \> **Website Configuration** page, check the **DNS resolution status** of the domain name.
        -   **Normal**: Alibaba Cloud WAF has been successfully deployed and the web traffic is being monitored by WAF.
        -   **Exception**: With the exception messages of **NO CNAME resolution detected**, **No traffic**, or **DNS check failed**, the DNS settings may be incorrect.

            In this case, check the DNS settings. If you confirm that the DNS settings are correct, wait for an hour and refresh the DNS resolution status. For more information, see [DNS resolution status exception](../reseller.en-US/FAQ/DNS resolution status exception.md#).

            **Note:** The exception here indicates that WAF is not properly deployed. Your website access is not affected.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15507166407591_en-US.jpg)


**Protect the origin**

When the origin server IP address is exposed, attackers may exploit it to bypass Alibaba Cloud WAF and start direct-to-origin attacks. To prevent such attacks, we recommend that you configure the ECS security group or SLB whitelist to block all web requests that do not come from Alibaba Cloud WAF’s IP addresses. For more information, see [Protect your origin server](../reseller.en-US/Best Practices/Protect your origin server.md#).

## Edit A record to deploy WAF {#a-record .section}

The A record method is same as the CNAME one, except the following differences.

-   **Prerequisites**: After obtaining the WAF CNAME address, do the following to obtain the associated WAF IP address.
    1.  In a Windows operating system, open the cmd command line tool.
    2.  Run the following command: `ping “copied WAF Cname address”`.
    3.  In the result, view the WAF IP address.
-   **Procedure**: In step 4 editing record, do the following:
    -   **Type**: Select **A**.
    -   **Value**: Enter the WAF IP address.
    -   Leave other settings as they are.

