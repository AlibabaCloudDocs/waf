# Website configuration {#concept_pym_brk_5fb .concept}

Website configuration describes the forwarding routes of the websites that are deployed with Alibaba Cloud WAF.

You can add a website configuration by using the [automatic](#) or [manual](#) method.

-   Automatically create a website configuration. When you are creating a website configuration, WAF accesses your A record configurations in [Alibaba Cloud DNS](https://dns.console.aliyun.com) and lists all website domains and their origin server IP addresses. You can simply select the domains for which you want to enable WAF protection and let WAF do the rest of configurations. In this way, WAF also helps update the DNS settings to redirect web traffic to WAF for inspection.
-   Manually create a website configuration. If no A record has been created in Alibaba Cloud DNS, you must manually create the website configuration. After that, you must log on to the DNS host’s system to update the DNS settings to redirect web traffic to WAF for inspection.

    For more information about how to update the DNS settings, see [WAF deployment guide](intl.en-US/User Guide/Access WAF/WAF deployment guide.md#).


**Note:** The number of website configurations you can add to the Alibaba Cloud WAF instance depends on your subscription plan and the number of extra domains. For more information, see [Extra domain quota](../intl.en-US/Pricing/Subscription/Extra domain quota.md#).

When your origin server addresses, protocol types, or ports change, or you want to configure the HTTPS advanced settings, you can [edit the website configuration](#).

For websites that do not need WAF protection any more, you can restore their DNS settings and [delete the website configuration](#).

## Automatically add a website configuration {#auto-website-configuration .section}

**Prerequisites**

-   The domain to be protected is hosted at Alibaba Cloud DNS. Besides, its DNS settings must include at least one valid A record.

    If you do not use Alibaba Cloud DNS, see [Website configuration](../intl.en-US/User Guide/Access WAF/Website configuration.md#) to manually add the website configuration.

-   \(For Mainland China region\) The website is granted an ICP license by the Ministry of Industry and Information Technology \(MIIT\).
-   \(For HTTPS-enabled websites\) You have access to a valid SSL certificate and private key of the website, or you have uploaded the certificate to Alibaba Cloud SSL Certificate Service.

**Procedure**

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China**, **International**.
3.  On the **Management** \> **Website Configuration** page, click **Add Domain**.

    WAF automatically lists all domain names that have an A record configured in Alibaba Cloud DNS of the current Alibaba Cloud account. If no A record has been created in Alibaba Cloud DNS, the Please choose your domain page does not appear. In this case, we recommend that you manually create a website configuration. For more information, see [Website configuration](../intl.en-US/User Guide/Access WAF/Website configuration.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15440745157562_en-US.png)

4.  On the Please choose your domain page, check the **Domain Name** for which you want to enable WAF protection and the **Protocol Type**.
5.  \(Optional\) If the protocol type includes **HTTPS**, you must verify certificate first to add the configuration.

    **Note:** Alternatively, do not select **HTTPS** here, but edit the website configuration and upload the certificate after you create the configuration. For more information, see [Update HTTPS certificate](../intl.en-US/User Guide/Access WAF/Update HTTPS certificates.md#).

    1.  Click **Verify Certificate**.
    2.  In the Verify Certificate dialog box, upload the certificate and private key.

        -   If the certificate has been hosted in the [Alibaba Cloud SSL Certificate Service console](https://yundunnext.console.aliyun.com/?p=casnext), you can click **Select existing certificate** in the Verity Certificate dialog box and select it to upload.
        -   Manual upload. Click **Manual upload**, enter the **Certificate name**, and paste the text content of the certificate and private key respectively to the **Certificate file** and **Private key file** boxes.

            For more information, see [Update HTTPS certificate](../intl.en-US/User Guide/Access WAF/Update HTTPS certificates.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15440745157567_en-US.png)

    3.  Click **Verify** to upload.
6.  Click **Add domain protection now**.

    After adding the website configuration, WAF automatically updates the DNS settings \(CNAME record\) of the domain name to redirect web requests to WAF for inspection. The whole process takes about 10 to 15 minutes.

    **Note:** If you are prompted to manually change the DNS settings, you must perform [Step 2: Update DNS settings](../intl.en-US/Quick Start/Step 2: Update the DNS settings.md#) to redirect web traffic to WAF.

7.  On the **Management** \> **Website Configuration** page, view the newly added domain name and its **DNS Resolution Status**.
    -   Normal indicates that Alibaba Cloud WAF has been successfully deployed for the website. Go on to perform [Step 3: Configure WAF protection policies](../intl.en-US/Quick Start/Step 3: Configure WAF protection polices.md#).
    -   **Exception** indicates that you must wait for a while or check the DNS settings at your DNS service provider.

        If the DNS settings are incorrect, perform [Step 2: Update DNS settings](../intl.en-US/Quick Start/Step 2: Update the DNS settings.md#). For more information, see [DNS resolution status exception](../intl.en-US/FAQ/DNS resolution status exception.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15440745157570_en-US.png)


## Manually add a website configuration {#manual-website-configuration .section}

**Prerequisites**

-   Obtain the domain name of the website to be protected.
-   Obtain the origin server IP address or other type of address that is supposed to receive the WAF-returned traffic.
-   Determine whether the website is deployed with CDN, DDoS protection, or other proxy services.
-   \(For Mainland China region\) The website is granted an ICP license by the Ministry of Industry and Information Technology \(MIIT\).
-   \(For HTTPS-enabled websites\) You have access to a valid SSL certificate and private key of the website, or you have uploaded the certificate to Alibaba Cloud SSL Certificate Service.

**Procedure**

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China**, **International**.
3.  On the **Management** \> **Website Configuration** page, click **Add Domain**.

    WAF automatically lists all domain names that have an A record configured in Alibaba Cloud DNS of the current Alibaba Cloud account. If no A record has been created in Alibaba Cloud DNS, the Please choose your domain page does not appear.

4.  \(Optional\) On the Please choose your domain page, click **Add other domain manually**.
5.  In the task of Fill in the website information, complete the following configuration.

    |Configuration|Description|
    |-------------|-----------|
    |**Domain name**|Enter the domain name to be protected.**Note:** 

    -   Supports wildcard domains, such as `*.aliyun.com`. When a wildcard domain is presented, all its associated subdomains are matched.
    -   If you add website configurations for an exact domain \(for example, `www.aliyun.com`\) and a wildcard domain \(for example, `*.aliyun.com`\) that matches the exact domain, the configuration for the exact domain takes priority.
    -   Does not support .edu domain names. If you want to use Alibaba Cloud WAF to protect domain names suffixed with .edu, submit a ticket to us.
|
    |**Protocol type**|Check the protocols used by the website. Optional values: **HTTP**, **HTTPS**.**Note:** 

    -   If your website is enabled with HTTPS, check HTTPS and see [Update HTTPS certificate](intl.en-US/User Guide/Access WAF/Update HTTPS certificates.md#) to upload a valid certificate and private key to let WAF inspect the HTTPS traffic.
    -   When HTTPS is checked, you can configure the **Advanced settings** to enable HTTPS force redirect or HTTP back-to-source to smooth the website access. For more information, see [HTTPS advanced settings](intl.en-US/User Guide/Access WAF/HTTPS advanced settings.md#).
|
    |**Server address**|Enter the origin server address, which can be one or more IP addresses or other addressees, such as an OSS CNAME address. When the website is deployed with Alibaba Cloud WAF, WAF returns the inspected web requests to this address.    -   \(Recommended\) Check **IP** and enter the public IP address of the origin server, such as the ECS instance IP or the SLB instance IP.

**Note:** 

        -   Multiple IP addresses are separated by commas. Up to 20 IP addresses can be added.
        -   If multiple IP addresses are presented, WAF performs health check and load balancing across them when returning the inspected web traffic. For more information, see [Load balancing across multiple origin servers](intl.en-US/User Guide/Access WAF/Load balance across multiple origin IPs.md#).
    -   Check **Other addresses** and enter the server address used to receive the WAF-returned traffic, such as an OSS CNAME address.

**Note:** 

        -   The server address \(Other address\) must not be same as the website domain name.
        -   If you enter an OSS CNAME address, after you create the website configuration, you must log on to the Alibaba Cloud OSS console to associate the custom domain \(in this case, the domain to be protected\) for the specified OSS CNAME address. For more information, see [Associate a custom domain](../../../../../intl.en-US/Console User Guide/Manage buckets/Manage a domain.md#).
|
    |**Server port**|Specify the server port. When the website is deployed with Alibaba Cloud WAF, WAF returns the inspected web requests to this port.    -   When Protocol type includes HTTP, the default HTTP port is **80**.
    -   When Protocol type includes HTTPS, the default HTTPS port is **443**.
    -   If you want to specify other ports, click **custom** to add them.

**Note:** For more information, see [Supported non-standard ports](intl.en-US/User Guide/Access WAF/Supported non-standard ports.md#).

|
    |**Any layer 7 proxy \(e.g. Anti-DDoS/CDN\) enabled?**|Check yes or no according to the actual condition. If any layer 7 proxy is deployed in front of Alibaba Cloud WAF, you must check **yes**. Otherwise, Alibaba Cloud WAF may not be able to obtain the real client IP address.|
    |**Load balancing algorithm**|When multiple origin server addresses are specified, select the load balance method \(**IP HASH** or **Round-robin**\) for WAF to distribute traffic among these addresses.|
    |**Flow Mark**|Enter an unoccupied **Header Filed** name and a custom **Header Field Value** to mark the web requests returned to the origin server by Alibaba Cloud WAF. WAF adds the specified header field into the inspected web requests for your web server to identify the WAF-returned traffic.**Note:** If the web request itself uses the specified header field, Alibaba Cloud WAF overwrites the original value with the specified value.

|

6.  Click **Next** to complete the configuration.

    When the website configuration is created, you can perform the following tasks:

    -   Follow the tutorial to perform the next task **Change DNS Record**. For more information, see [WAF deployment guide](intl.en-US/User Guide/Access WAF/WAF deployment guide.md#).
    -   \(For HTTPS-enabled websites\) Upload the HTTPS certificate and private key. For more information, see [Update HTTPS certificate](intl.en-US/User Guide/Access WAF/Update HTTPS certificates.md#).
    -   Go to the **Management** \> **Website Configuration** page to view the newly added website configuration, and **Edit** or **Delete** it as you need.

## Edit a website configuration {#edit-website-configuration .section}

When your web server’s configuration changes, such as server IP address changes, protocol type or port changes, or when you want to configure the HTTPS advanced settings, you can edit the website configuration.

**Procedure**

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China**, **International**.
3.  On the **Management** \> **Website Configuration** page, select the website configuration to be operated, and click **Edit**.
4.  On the Edit page, complete the configuration by following [Step 5 in Manually add a website configuration](#).

    **Note:** The **Domain name** cannot be modified. If you want to associate another domain name, we recommend that you add a new website configuration and delete the unnecessary one.

5.  Click **OK** to complete the procedure.

## Delete a website configuration {#delete-website-configuration .section}

If you want to disable Alibaba Cloud WAF for your website, you can restore the DNS to redirect traffic to your web servers, and delete the website configuration on the Alibaba Cloud WAF console.

**Procedure**

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China**, **International**.
3.  On the **Management** \> **Website Configuration** page, select the website configuration to be deleted, and click **Delete**.

    **Note:** You must restore the DNS settings before deleting the website configuration. Otherwise, the website may become inaccessible.

4.  In the Prompt message dialog box, click **OK**.

