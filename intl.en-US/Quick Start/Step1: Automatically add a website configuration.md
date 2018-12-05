# Step1: Automatically add a website configuration {#concept_ay1_1y1_p2b .concept}

After activating Alibaba Cloud WAF, you must create a website configuration in the WAF console to associate your website with the WAF instance. In this step, you add a website configuration by using the DNS configurations in Alibaba Cloud DNS.

When you create a website configuration, WAF accesses your A record configurations in [Alibaba Cloud DNS](https://dns.console.aliyun.com) and lists all website domains and their origin server IP addresses. You can simply select the domains for which you want to enable WAF protection and let WAF do the rest of configurations. In this way, WAF also helps update the DNS settings \(**Step 2**\) and complete traffic redirection.

## Prerequisites {#section_adb_swb_5fb .section}

-   The domain to be protected is hosted at Alibaba Cloud DNS. Besides, its DNS settings must include at least one valid A record.

    If you do not use Alibaba Cloud DNS, see **Website configuration** to manually add the website configuration.

-   \(For Mainland China region\) The website is granted an ICP license by the Ministry of Industry and Information Technology \(MIIT\).
-   \(For HTTPS-enabled websites\) You have access to a valid SSL certificate and private key of the website, or you have uploaded the certificate to Alibaba Cloud SSL Certificate Service.

## Procedure {#section_xkv_xlb_p2b .section}

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China**, **International**.
3.  On the **Management** \> **Website Configuration** page, click **Add Domain**.

    WAF automatically lists all domain names that have an A record configured in Alibaba Cloud DNS of the current Alibaba Cloud account. If no A record has been created in Alibaba Cloud DNS, the Please choose your domain page does not appear. In this case, we recommend that you manually create a website configuration. For more information, see **Website configuration**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15439748657562_en-US.png)

4.  On the Please choose your domain page, check the **Domain Name** for which you want to enable WAF protection and the **Protocol Type**.
5.  \(Optional\) If the protocol type includes **HTTPS**, you must verify certificate first to add the configuration.

    **Note:** Alternatively, do not select **HTTPS** here, but edit the website configuration and upload the certificate after you create the configuration. For more information, see [Update HTTPS certificate](../../../../intl.en-US/User Guide/Access WAF/Update HTTPS certificates.md#).

    1.  Click **Verify Certificate**.
    2.  In the Verify Certificate dialog box, upload the certificate and private key.

        -   If the certificate has been hosted in the [Alibaba Cloud SSL Certificate Service console](https://yundunnext.console.aliyun.com/?p=casnext), you can click **Select existing certificate** in the Verity Certificate dialog box and select it to upload.
        -   Manual upload. Click **Manual upload**, enter the **Certificate name**, and paste the text content of the certificate and private key respectively to the **Certificate file** and **Private key file** boxes.

            For more information, see [Update HTTPS certificate](../../../../intl.en-US/User Guide/Access WAF/Update HTTPS certificates.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15439748657567_en-US.png)

    3.  Click **Verify** to upload.
6.  Click **Add domain protection now**.

    After adding the website configuration, WAF automatically updates the DNS settings \(CNAME record\) of the domain name to redirect web requests to WAF for inspection. The whole process takes about 10 to 15 minutes.

    **Note:** If you are prompted to manually change the DNS settings, you must perform **Step 2: Update DNS settings** to redirect web traffic to WAF.

7.  On the **Management** \> **Website Configuration** page, view the newly added domain name and its **DNS Resolution Status**.
    -   Normal indicates that Alibaba Cloud WAF has been successfully deployed for the website. Go on to perform [Step 3: Configure WAF protection policies](intl.en-US/Quick Start/Step 3: Configure WAF protection polices.md#).
    -   **Exception** indicates that you must wait for a while or check the DNS settings at your DNS service provider.

        If the DNS settings are incorrect, perform **Step 2: Update DNS settings**. For more information, see **DNS resolution status exception**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15439748667570_en-US.png)


