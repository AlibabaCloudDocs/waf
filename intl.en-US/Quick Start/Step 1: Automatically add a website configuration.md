# Step 1: Automatically add a website configuration {#concept_ay1_1y1_p2b .concept}

After you activate Web Application Firewall \(WAF\), you need to add the website configuration of the website that needs protection in the WAF console. This topic describes how WAF automatically adds a website configuration when you use the DNS proxy mode to configure WAF.

**Note:** You can use the transparent proxy mode or the DNS proxy mode to configure WAF for your website. The following example demonstrates how to configure WAF by using the DNS proxy mode. For more information about the transparent proxy mode, see [Use the transparent proxy mode to configure WAF](../../../../../reseller.en-US/User Guide/Use the transparent proxy mode to implement WAF.md#).

When you configure WAF by using the DNS proxy mode, WAF can automatically read the A records that you have created on **Alibaba Cloud DNS**, the domain name of the website, and the origin server IP address to automatically add a website configuration. After the website configuration is added, WAF automatically updates the DNS record of the domain name. For more information, see [Step 2: Update the DNS settings](reseller.en-US/Quick Start/Step 2: Update the DNS settings.md#).

## Prerequisites {#section_adb_swb_5fb .section}

-   The DNS records of the website are managed by Alibaba Cloud DNS, and at least one A record is valid.

    If you cannot host your domains on Alibaba Cloud DNS, you must manually add website configurations. For more information, see [Website configuration](../../../../../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#).

-   \(Mainland China regions\) You have obtained an ICP license for the website.
-   \(HTTPS-based websites\) You have obtained the HTTPS certificate and the private key file of the website, or the HTTPS certificate is managed by Alibaba Cloud SSL Certificates Service.

## Procedure {#section_xkv_xlb_p2b .section}

1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  On the top of the page, select **Mainland China** or **International**.
3.  Choose **Management** \> **Website Configuration** and select **DNS Proxy Mode**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/155323392840172_en-US.png)

4.  Click **Add Domain**.

    WAF automatically lists the domain names that have an A record configured on Alibaba Cloud DNS under the current Alibaba Cloud account. If you have not created an A record on Alibaba Cloud DNS, the Please choose your domain page will not appear. You can manually add the website configuration by following the procedure described in [Website configuration](../../../../../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15532339287562_en-US.png)

5.  On the Please choose your domain page, choose the **domain name** and the **protocol type** for the website.
6.  \(Optional\) If you choose **HTTPS**, you must verify the certificate before you add the website configuration.

    **Note:** Alternatively, do not select **HTTPS**. After you have added the website configuration, upload the HTTPS certificate by following the procedure described in [Update HTTPS certificates](../../../../../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Update HTTPS certificates.md#)

    1.  Click **Verify Certificate**.
    2.  In the Verify Certificate dialog box, upload the certificate and private key file.

        -   If you have hosted your certificates on **Alibaba Cloud SSL Certificate Service**, click **Select Existing Certificate** in the Verify Certificate dialog box, and select the certificate that is associated with the domain name.
        -   Manually upload the certificate. Click **Manual Upload**, enter the **certificate name**, and copy the text content of the certificate and private key files to the **Certificate File** and **Private Key File** fields respectively.

            For more information, see [Update HTTPS certificates](../../../../../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Update HTTPS certificates.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15532339287567_en-US.png)

    3.  Click **Verify** to verify the uploaded certificate.
7.  Click **Add domain protection now**.

    After you have added the website configuration, WAF automatically updates the CNAME record of the domain to redirect requests sent to your website to WAF for monitoring. This operation will take 10 to 15 minutes.

    **Note:** If you are required to add DNS records manually, follow the procedure described in [Step 2: Update the DNS settings](reseller.en-US/Quick Start/Step 2: Update the DNS settings.md#) to complete the configuration.

8.  You can choose **Management** \> **Website Configuration** to view the domain name that you have added and the DNS status in the **DNS resolution status** column.
    -   Normal indicates that you have successfully configured WAF for your website. You can follow the procedure described in [Step 3: Configure WAF protection policies](reseller.en-US/Quick Start/Step 3: Configure WAF protection polices.md#) to specify protection policies.
    -   **Exception** may be displayed after you have added the website configuration. Wait a few seconds and check the DNS status again, or check whether the DNS settings are configured correctly at your DNS service provider.

        If the DNS settings are not configured correctly, see [Step 2: Update the DNS settings](reseller.en-US/Quick Start/Step 2: Update the DNS settings.md#). For more information, see [DNS resolution status exception](../../../../../reseller.en-US/FAQ/DNS resolution status exception.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15532339287570_en-US.png)


