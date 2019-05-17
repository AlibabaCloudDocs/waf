# Website configuration {#concept_pym_brk_5fb .concept}

A website configuration specifies the request redirect routes for the website for which you have configured Web Application Firewall \(WAF\). You must specify the website configuration in the WAF console. This topic describes how to add and manage website configurations when you use the DNS proxy mode to configure WAF for your website.

**Note:** You can use the transparent proxy mode to configure WAF for your website if your origin server is deployed on an ECS instance. The ECS instance must be created in the China \(Qingdao\), China \(Beijing\), China \(Zhangjiakou\), or China \(Hohhot\) region, and have a public IP address or be associated with an EIP.

-   Transparent proxy mode: This mode directs HTTP requests that are received on port 80 of the specified origin server to WAF. WAF processes the requests and then redirects the requests to the origin server.

    To use this mode, you must authorize WAF to access the ECS instance where your origin server is deployed. To configure this mode, add a domain and specify the IP address of the server that hosts your website in the WAF console. For more information, see [Use the transparent proxy mode to configure WAF](reseller.en-US/User Guide/Use the transparent proxy mode to implement WAF.md#).

-   DNS proxy mode: This mode directs requests that are sent to the protected domain to WAF based on the specified DNS record. WAF then processes and redirects the requests to the specified origin server.

    In DNS proxy mode, you must add the website configuration of your website in the WAF console and change the DNS record of the domain name.


When you use the DNS proxy mode to configure WAF, you can choose to [add website configurations automatically](#) or [add website configurations manually](#).

-   Add website configurations automatically When you add website configurations, WAF can automatically read the A record from the **Alibaba Cloud DNS console** and obtain the domain name of your website and the origin server IP address. After WAF obtains this information, it automatically adds the website configuration. After the website configuration is added, WAF automatically updates the DNS record of the domain name to complete the configuration of WAF for your website.
-   Add website configurations manually If your DNS records are not managed by Alibaba Cloud DNS, you need to add website configurations manually and change DNS records at your DNS service provider to redirect requests to WAF for monitoring.

    For more information about updating DNS settings, see [Configure DNS settings](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#).


**Note:** The number of website configurations that you can add on the Website Configuration page depends on your WAF instance specification and extra domain quota. For more information, see [Extra domain quota](../reseller.en-US/Pricing/Subscription/Extra domain quota.md#).

If the configuration of your website such as the server address, protocol type, or server port is changed, or you need to modify advanced HTTPS settings, [edit the website configuration](#) of your website.

If you no longer need to redirect requests for a domain name, you can restore the DNS settings and then [delete the website configuration](#).

## Add website configurations automatically {#auto-website-configuration .section}

**Prerequisites** 

-   The DNS records of the website are managed by Alibaba Cloud DNS, and at least one A record is valid.

    If you cannot host your domains on Alibaba Cloud DNS, you must manually add website configurations. For more information, see [Website configuration](../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#).

-   \(Mainland China regions\) You have obtained an ICP license for the website.
-   \(HTTPS-based websites\) You have obtained the HTTPS certificate and the private key file of the website, or the HTTPS certificate is managed by Alibaba Cloud SSL Certificates Service.

**Procedure** 

1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  On the top of the page, select **Mainland China** or **International**.
3.  Choose **Management** \> **Website Configuration** and select **DNS Proxy Mode**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/155806173540172_en-US.png)

4.  Click **Add Domain**.

    WAF automatically lists the domain names that have an A record configured on Alibaba Cloud DNS under the current Alibaba Cloud account. If you have not created an A record on Alibaba Cloud DNS, the Please choose your domain page will not appear. You can manually add the website configuration by following the procedure described in [Website configuration](../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15580617357562_en-US.png)

5.  On the Please choose your domain page, choose the **domain name** and the **protocol type** for the website.
6.  \(Optional\) If you choose **HTTPS**, you must verify the certificate before you add the website configuration.

    **Note:** Alternatively, do not select **HTTPS**. After you have added the website configuration, upload the HTTPS certificate by following the procedure described in [Update HTTPS certificates](../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Update HTTPS certificates.md#)

    1.  Click **Verify Certificate**.
    2.  In the Verify Certificate dialog box, upload the certificate and private key file.

        -   If you have hosted your certificates on **Alibaba Cloud SSL Certificate Service**, click **Select Existing Certificate** in the Verify Certificate dialog box, and select the certificate that is associated with the domain name.
        -   Manually upload the certificate. Click **Manual Upload**, enter the **certificate name**, and copy the text content of the certificate and private key files to the **Certificate File** and **Private Key File** fields respectively.

            For more information, see [Update HTTPS certificates](../reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Update HTTPS certificates.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15580617357567_en-US.png)

    3.  Click **Verify** to verify the uploaded certificate.
7.  Click **Add domain protection now**.

    After you have added the website configuration, WAF automatically updates the CNAME record of the domain to redirect requests sent to your website to WAF for monitoring. This operation will take 10 to 15 minutes.

    **Note:** If you are required to add DNS records manually, follow the procedure described in [Step 2: Update the DNS settings](../reseller.en-US/Quick Start/Step 2: Update the DNS settings.md#) to complete the configuration.

8.  You can choose **Management** \> **Website Configuration** to view the domain name that you have added and the DNS status in the **DNS resolution status** column.
    -   Normal indicates that you have successfully configured WAF for your website. You can follow the procedure described in [Step 3: Configure WAF protection policies](../reseller.en-US/Quick Start/Step 3: Configure WAF protection polices.md#) to specify protection policies.
    -   **Exception** may be displayed after you have added the website configuration. Wait a few seconds and check the DNS status again, or check whether the DNS settings are configured correctly at your DNS service provider.

        If the DNS settings are not configured correctly, see [Step 2: Update the DNS settings](../reseller.en-US/Quick Start/Step 2: Update the DNS settings.md#). For more information, see [DNS resolution status exception](../reseller.en-US/FAQ/DNS resolution status exception.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15580617367570_en-US.png)


## Add website configurations manually {#manual-website-configuration .section}

**Prerequisites** 

-   You have obtained the domain name of the website that needs protection.
-   You have obtained the origin server IP address of the website.
-   Check whether you have configured other proxy services such as Alibaba Cloud CDN and Alibaba Cloud Anti-DDoS Pro, or whether you will need to configure such services.
-   If your website is deployed in a Mainland China region, make sure that you have obtained an ICP license.
-   For an HTTPS-based website, you must obtain the HTTPS certificate and the private key file, or host your certificate on Alibaba Cloud SSL Certificates Service.

**Procedure**

1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  On the top of the page, click **Mainland China** or **International**.
3.  Choose **Management** \> **Website Configuration** and select **DNS Proxy Mode**.
4.  Click **Add Domain**.

    WAF automatically lists all domain names that have an A record configured on Alibaba Cloud DNS under the current Alibaba Cloud account. If no A records have been created on Alibaba Cloud DNS, the Choose your domain page will not appear.

5.  On the Choose your domain page, click **Add other domains manually**.
6.  On the Fill in the website information page, complete the following configuration.

    |Parameter|Description|
    |---------|-----------|
    |**Domain name**|Enter the domain name that needs WAF protection. **Note:** 

    -   Supports wildcard domains, such as `*.aliyun.com`. WAF automatically matches all subdomains for the wildcard domain.
    -   If you enter a wildcard domain and a specific domain name, such as `*.aliyun.com` and `www.aliyun.com`, WAF will use the redirection rules and protections policies of the specific domain name.
    -   Currently, .edu domain names are not supported. If you need to use a .edu domain name, submit a ticket to Alibaba Cloud technical support.
 |
    |**Protocol type**|Select a protocol type. Valid values: **HTTP** and **HTTPS**. **Note:** 

    -   If your website supports HTTPS, select HTTPS and upload the certificate and the private key file after you add the website configuration. For more information, see [Update HTTPS certificates](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Update HTTPS certificates.md#).
    -   After you select HTTPS, click **Advanced settings** to enable HTTP force redirect and HTTP back-to-origin to ensure efficient access to your website. For more information, see [HTTPS advanced settings](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/HTTPS advanced settings.md#).
 |
    |**Server address**|Enter the origin server IP address of the website. IP addresses and other formats of addresses are supported. WAF will filter and redirect requests to the server address.     -   \(Recommended\) Select **IP** and enter the public IP address of the origin server, such as the IP address of the ECS or SLB instance.

**Note:** 

        -   Separate multiple IP addresses with commas \(,\). You can enter up to 20 server IP addresses.
        -   If you enter multiple IP addresses, WAF automatically performs health check and load balancing on these addresses when WAF redirects requests. For more information, see [Load balance across multiple origin IPs](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Load balance across multiple origin IPs.md#).
    -   Select **Other addresses** and enter the back-to-origin domain name of the server, such as an OSS CNAME address.

**Note:** 

        -   The back-to-origin domain name and the domain name of the protected website must be different.
        -   If you enter an OSS CNAME address for your origin server, you must associate a custom domain name with the OSS CNAME address in the OSS console after you set the website configuration. For more information, see [Attach a custom domain name](../../../../../reseller.en-US/Console User Guide/Manage buckets/Manage a domain/Attach a custom domain name.md#).
 |
    |**Server port**|Specify the server port. After you configure WAF for your website, WAF will redirect filtered requests to this port.     -   If you select HTTP, the default port is **80**.
    -   If you select HTTPS, the default port is **443**.
    -   If you need to use other ports, click **Custom** to add ports.

**Note:** For more information, see [Supported non-standard ports](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Supported non-standard ports.md#).

**Note:** The protocol and the port must be the same as those of the origin server IP address. You cannot change the port after it is specified.

 |
    |**Any layer 7 proxy \(e.g. Anti-DDoS/CDN\) enabled?**|Select yes or no based on the actual status of your website. If you need to configure a layer 7 proxy to redirect requests before WAF, select **yes**. Otherwise, WAF cannot obtain the real IP addresses of clients that initiate requests to your website.|
    |**Load balancing algorithm**|When multiple origin server addresses are specified, select **IP hash** or **Round-robin**. WAF will distribute requests to these servers based on the specified algorithm to balance the load.|
    |**Flow mark**|Enter an unoccupied **Header Field** name and a custom **Header Field Value** to mark the requests that are redirected to the origin server by WAF. WAF adds the specified header field into the filtered requests for your backend server to identify the requests that are redirected by WAF. **Note:** If the requests to your website already contain a specified header field, WAF overwrites the original field value with the specified value.

 |

7.  Click **Next** to complete the configuration.

    You can perform the following operations after you configure WAF.

    -   Enter required information on the **Change DNS Record** page by following the prompts. For more information, see [Configure DNS settings](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#).
    -   If you select HTTPS as the protocol type, upload the HTTPS certificate and the private key file. For more information, see [Update HTTPS certificates](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Update HTTPS certificates.md#).
    -   Choose **Management** \> **Website Configuration** to view the website configuration that you have added. You can **edit** or **delete** it based on your actual needs.

## Edit website configurations {#edit-website-configuration .section}

If the configuration of your website such as the server address, protocol type, or server port is changed, or you need to configure advanced HTTPS settings, edit the website configuration of your website.

**Procedure** 

1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  On the top of the page, select **Mainland China** or **International**.
3.  Choose **Management** \> **Website Configuration**, select **DNS Proxy Mode**, and click **Edit** to modify the website configuration for the specified website.
4.  On the Edit page, perform [step 6](#) described in the Add website configurations manually section to modify the configuration.

    **Note:** You cannot change the **domain name**. If you want to configure WAF for a different domain, we recommend that you add a domain and set a website configuration for it, and delete the configuration that you no longer need.

5.  Click **OK** to delete the configuration.

## Delete website configurations {#delete-website-configuration .section}

If you want to disable WAF for your website, you can restore the DNS settings to redirect requests to the origin server, and delete the website configuration in the WAF console.

**Procedure** 

1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  On the top of the page, select **Mainland China** or **International**.
3.  Choose **Management** \> **Website Configuration**, select **DNS Proxy Mode**, and click **Delete** to delete the website configuration.

    **Note:** You must restore the DNS settings before deleting the website configuration. Otherwise, the website may become inaccessible.

4.  In the prompt message, click **OK**. The website configuration has been deleted.

