# Add websites

This topic describes how to add your website to Web Application Firewall \(WAF\) after you purchase a WAF instance.

-   WAF is activated, and the number of second-level domain names and subdomains that you add to a WAF instance does not reach the upper limit.

    **Note:** The total number of domain names that you can add to a WAF instance depends on the specifications of the instance and the number of extra domain packages that you purchase. For more information, see [Extra domain quota](/intl.en-US/Billing and Service Activation/Subscription/Extra domain quota.md).

-   If your domain name is protected by a WAF instance in mainland China, you must complete ICP filing for your domain name. If you do not complete ICP filing but still add your domain name to WAF, an error may occur and the system prompts you to complete ICP filing.

You can use one of the following methods to add your website:

-   [Configure WAF to automatically add website configurations](#section_06w_k6n_iiw): You need only to select the domain name that you want to add and the network protocol type on the **Add Domain Name** page. WAF automatically reads information about the domain name assets under your Alibaba Cloud account. Then, WAF adds website configurations, such as the domain name, server address, and standard ports \(80 and 443\), and changes the DNS record of the domain name.

    **Note:** The account that you use to add domain names must have management permissions on Alibaba Cloud DNS resources. Otherwise, WAF cannot automatically change the DNS record. If the automatic change operation fails, you can manually change the DNS record of the domain name after the domain name is added.

-   [Manually add website configurations](#section_i0l_fp0_t66): If your website does not support the first method, you can manually add the website configurations, such as the domain name, protocol, server address, and server port. After you manually add the website configurations, you must manually change the DNS record of the domain name of your website to redirect requests destined for your website to WAF for protection.

## Configure WAF to automatically add website configurations

The **Add Domain Name** page appears only when an eligible domain name exists. If the page appears, you can select the domain name that you want to add to WAF. The website is automatically added to WAF.

Eligible domain names contain only valid domain names that are configured in Alibaba Cloud DNS.

**Procedure**

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Asset Center** \> **Website Access**.

4.  On the **Domain Names** tab, click **Website Access**.

5.  On the **Add Domain Name** page, select the domain name that you want to add and a protocol type in the domain name list, and click **Add domain protection now**.

    **Note:** The **Add Domain Name** page appears only when an eligible domain name exists. If the **Add Domain Name** page is not displayed, we recommend that you manually add the website configurations. For more information, see [Step 6](#step_81i_fn8_dsd).

    ![Add Domain Name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1145248951/p96929.png)

    If you select **https**, you must complete certificate verification before you add the website configurations.

    Perform the following operations to verify a certificate:

    1.  Select a domain name and **https** and click **Verify Certificate** in the **HTTPS Certificate** column.

    2.  In the **Verify Certificate** dialog box, specify **Upload Type** and upload the HTTPS certificate.

        For more information, see [Upload HTTPS certificates](#step5).

    3.  Click **Confirm** after the HTTPS certificate is uploaded.

        -   If the certificate verification succeeds, click **Add domain protection now**.
        -   If the certificate verification fails, verify the certificate again based on error messages, such as **The certificate and key do not match**, until the verification succeeds.
    WAF automatically adds the website configurations and changes the DNS record.

    **Note:** If you want to add ports other than 80 and 443, manually edit the domain name after the domain name is automatically added. For more information, see [References](#section_l50_3ox_mix).

    Possible issues and solutions:

    -   **Domain name was added, but you need to manually change the DNS record.**

        Possible causes: The account that you use to add the domain name does not have management permissions on Alibaba Cloud DNS resources, or the uploaded HTTPS certificate does not match your domain name.

        **Note:** Assume that your website uses **HTTPS** and the certificate verification succeeds. If the uploaded certificate and the website do not match, the certificate detection still fails, and WAF does not automatically change the DNS record. In this case, you must upload a valid and correct certificate and then manually change the DNS record. For more information, see [Upload HTTPS certificates](#section_jo2_hwu_mbj).

        Click **manually access the DNS**. In the **Manual Configuration** dialog box, change the DNS record. For more information, see [Change a DNS record](/intl.en-US/Website Access/Website access with CNAME/Change a DNS record.md).

    -   **The maximum number of domain names has been reached.**

        Click **extra domain package** to purchase an extra domain package. Add the domain name again.

    -   **No ICP filing records are found for the domain name.**

        If your domain name is protected by a WAF instance in mainland China, you must complete ICP filing for your domain name. Complete ICP filing for your domain name.


## Manually add website configurations

The following steps describe how to manually add a website in CNAME mode.

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Asset Center** \> **Website Access**.

4.  On the **Domain Names** tab, click **Website Access**.

5.  On the **Add Domain Name** page, click **Manually Add Other Websites**.

    **Note:** The **Add Domain Name** page appears only when an eligible domain name exists. If the **Add Domain Name** page is not displayed, skip this step. For more information, see [Configure WAF to automatically add website configurations](#section_06w_k6n_iiw).

6.  On the **Add Domain Name** page, specify **Domain Name**, select **CNAME Record** for **Access Mode**, and complete the wizard.

    The domain name must meet the following requirements:

    -   The domain name can be exact match domains, such as `www.aliyun.com`, and wildcard domains, such as `*.aliyun.com`.
        -   If you use a wildcard domain, WAF automatically matches all subdomains of the wildcard domain.
        -   If you configure both a wildcard domain and an exact match domain, WAF uses the forwarding rules and protection policies of the exact match domain.
    -   The domain name cannot be `.edu` domain names. To add `.edu` domain names, submit a [ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80) to request technical support.
    **CNAME** wizard:

    1.  **Enter your website information**.

        Configure the website parameters that are described in the following table and click **Next**.

        ![Enter your website information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7601543061/p66025.png)

        |Parameter|Description|
        |---------|-----------|
        |**Protection Resource** \(applicable only to the Exclusive edition\)|If you are using a WAF instance of the Exclusive edition, select a protection resource. **Note:** This **Protection Resource** option is available only for the WAF Exclusive edition.

Valid values:

        -   **Shared Cluster**: This is the default value.
        -   **Exclusive Cluster**: You can customize an exclusive cluster to deliver service-specific protection. For more information, see [Create an exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md).
        -   **Static Back-to-Origin in Hybrid Cloud Scenarios** |
        |**Protocol Type**|Select a protocol type. Valid values:         -   **HTTP**
        -   **HTTPS**: If your website uses HTTPS, select **HTTPS** and upload the certificate and private key file after you add the website configurations. For more information, see [Upload HTTPS certificates](#section_jo2_hwu_mbj).

After you select **HTTPS**, click **Advanced Settings** to show more options.

![HTTPS ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2145248951/p7688.png)

**Advanced Settings** supports the following features:

            -   **Enforce HTTPS Routing**: If this feature is enabled, the HTTP requests are delivered through HTTPS port 443. You must clear HTTP before you turn on Enforce HTTPS Routing.

If you want a client to access your website by using HTTPS, enable this feature. This enhances access security.

**Note:** Before you enable this feature, make sure that your website supports HTTPS services. After this feature is enabled, requests are delivered over HTTPS.

            -   **Enable HTTP**: If this feature is enabled, WAF forwards requests over HTTP. The default port is 80.

This feature implements HTTPS access to your website without making changes to the origin server. This reduces the workload of the origin server. If your website does not support HTTPS, turn on Enable HTTP.

        -   **HTTP2**: This option is available only when you use the WAF Business or Enterprise edition and select **HTTPS**. |
        |**Destination Server \(IP Address\)**|Enter the address of the origin server. You can select **IP** or **Destination Server \(Domain Name\)**. WAF filters and redirects requests to this address.         -   **IP**: Enter the public IP address of the origin server.

Separate multiple IP addresses with commas \(,\). You can enter up to 20 IP addresses. Do not use line breaks.

**Note:** If you enter multiple IP addresses, WAF automatically performs health checks and load balancing on these addresses before redirecting requests.

            -   If the origin server is an Alibaba Cloud ECS instance, enter the public IP address of the instance.
            -   If the ECS instance is connected to an SLB instance, enter the public IP address of the SLB instance.
            -   If your origin server is not deployed on Alibaba Cloud, we recommend that you ping the domain name to query the public IP address of the origin server, and then enter the public IP address.
        -   **Destination Server \(Domain Name\)**: Enter the domain name of the origin server, such as an OSS bucket.

The domain name of the origin server must be different from the protected domain name.

**Note:** If you enter a domain name of an OSS bucket, you must bind this domain name to the bucket in the OSS console. For more information, see [Bind custom domain names](/intl.en-US/Console User Guide/Manage buckets/Manage a domain/Bind custom domain names.md). |
        |**Destination Server Port**|Specify the port that you use to forward website requests. WAF redirects the filtered requests only through the port that you specify. If other ports are enabled, no security threats are posed to the origin server.

**Note:** **Protocol Type** and **Destination Server Port** must be the protocol and port that the origin server uses to provide web services. WAF does not support port translation. For example, if the origin server provides web services through HTTP port 80, HTTP and port 80 must be configured for your domain name.

Default ports:

        -   **HTTP 80**: This port is used when HTTP is selected.
        -   **HTTPS 443**: This port is used when HTTPS is selected.

**Note:** HTTP/2 uses the same port as HTTPS does.

Customize ports: Click **Customize** and specify custom ports based on **HTTP** or **HTTPS** that you select.

![Customize ports](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2145248951/p97012.png)

Click **View Allowed Port Range** to query all supported ports. Separate multiple ports with commas \(,\).

**Note:**

        -   WAF Enterprise and Exclusive each supports a maximum of 50 different server ports, including ports 80, 8080, 443, and 8443. WAF Pro and Business each supports a maximum of 10 ports, including ports 80, 8080, 443, and 8443.
        -   For more information about ports supported by the shared cluster, see [Supported custom ports](/intl.en-US/Website Access/Supported custom ports.md).
        -   If you are using the WAF Exclusive edition, you can select ports only from the **Server Ports** section on the **Exclusive Cluster Settings** page. For more information, see [Create an exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md). |
        |**Load Balancing Algorithm**|If multiple origin IP addresses are configured, select a value. Valid values:         -   **IP hash**: Requests from a specific IP address are redirected to the same origin server. This is the default value.

**Note:** If the IP addresses of origin servers are not scattered on different network segments when this algorithm is selected, unbalanced loads may occur.

        -   **Round Robin**: All requests are distributed to origin servers in turn.
        -   **Least time**: You can use the intelligent DNS resolution feature and the upgraded Least-time back-to-origin algorithm to minimize the latency when requests are forwarded to origin servers.

**Note:** You can select **Least time** only when intelligent load balancing is enabled. For more information, see [Intelligent load balancing](/intl.en-US/Billing and Service Activation/Subscription/Intelligent load balancing.md).

After the settings take effect, WAF distributes back-to-origin requests to the IP addresses of multiple origin servers to achieve load balancing. |
        |**Does a layer 7 proxy \(DDoS Protection/CDN, etc.\) exist in front of WAF**|If you need to configure a Layer 7 proxy in front of WAF, select **Yes**. Otherwise, WAF cannot obtain the actual IP addresses of clients. For more information, see the following topics:         -   [Deploy WAF and Anti-DDoS Pro together](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and Anti-DDoS Pro together.md)
        -   [t15558.md\#](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and CDN together.md)
If you do not need to configure a Layer 7 proxy in front of WAF, select **No**. |
        |**Request Tag**|Enter a **Header Field Name** that is not occupied and a custom **Header Field Value** to mark website requests forwarded by WAF. WAF adds the specified header field and value to the filtered requests. This allows your origin server to identify and collect the requests redirected by WAF, which in turn implements precise protection and effect analysis.

**Note:** If a request already contains the specified header field, WAF overwrites the original field value with the specified value. |
        |**Resource Group**|Select the resource group to which the domain name belongs from the resource group list. **Note:** You can use Resource Management to create resource groups and manage resources under your Alibaba Cloud account by department or project. For more information, see [Create a resource group](). |

    2.  **Change the DNS record**.

        Change the DNS record as prompted and click **Next**. After you change the DNS record, the domain name is mapped to WAF. For more information, see [Change a DNS record](/intl.en-US/Website Access/Website access with CNAME/Change a DNS record.md).

    3.  **Complete the settings**.

        Configure back-to-origin CIDR blocks of WAF as prompted and click **Completed. Return to the website list.** to go to the **Website Access** page. For more information, see [Allow access from WAF back-to-origin CIDR blocks](/intl.en-US/Website Access/Website access with CNAME/Allow access from WAF back-to-origin CIDR blocks.md).


## What to do next

After you add the website, the requests destined for the website are protected by WAF. You can also configure website protection configurations for better protection.

WAF provides multiple protection features to protect your website against different types of attacks. Among the features, only **RegEx Protection Engine** and **HTTP Flood Protection** are enabled by default. The RegEx Protection Engine feature protects your website against common web attacks, such as SQL injection, XSS, and webshell upload. The HTTP Flood Protection feature protects your website against HTTP flood attacks. You need to manually enable other features and configure protection rules. For more information, see [Overview](/intl.en-US/Website Protection Settings/Overview.md).

## Upload HTTPS certificates

If your domain name uses **HTTPS**, you must upload the valid and correct HTTPS certificate associated with the domain name in the WAF console. This ensures that WAF protects HTTPS requests.

You can upload an HTTPS certificate by using the following methods:

-   Manual uploading:

    You must prepare the following files for your website before you upload the certificate:

    -   The certificate file in the CRT or PEM format
    -   The private key file in the KEY format
-   Selecting an existing certificate: You can select the certificate that is associated with the domain name. For more information, see [SSL Certificates Service](/intl.en-US/Product Introduction/What is SSL Certificates Service?.md).

**Procedure**

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Asset Center** \> **Website Access**.

4.  On the **Domain Names** tab, find the domain name that you want to manage, and click the ![Upload](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3145248951/p31794.png) icon in the **Origin Server** column.

    **Note:** The ![Upload](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3145248951/p31794.png) icon is displayed only when you select HTTPS for your domain name that you add to WAF.

    ![HTTPS status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3145248951/p31793.png)

5.  In the **Upload Certificate** or **Update Certificate** dialog box, specify **Upload Type** to upload an HTTPS certificate.

    **Note:** If a certificate has been uploaded, the **Update Certificate** dialog box is displayed. The **Update Certificate** and **Upload Certificate** dialog boxes have the same configuration items.

    -   **Manual Upload**: Specify **Certificate Name**, and copy the content in the certificate file to the **Certificate File** field and the content in the private key file to the **Private Key File** field.

        ![Select Manual Upload](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3145248951/p31796.png)

        For more information about the certificate file, see the following descriptions:

        -   If the certificate file is in the PEM, CER, or CRT format, you can use a text editor to open the certificate file and copy its text content.
        -   If the certificate file is in another format, such as PFX or P7B, you must covert the certificate file format to PEM. Then, you can use a text editor to open the certificate file and copy its text content. For information about how to convert the format of a certificate file, see [How do I convert an HTTPS certificate to the PEM format?]().
        -   If the domain name is associated with multiple certificate files, for example, a certificate chain, you must merge the text content in the certificate files and then copy the merged content to the **Certificate File** field.
    -   **Select Existing Certificate**: Select the certificate to be uploaded from the **Certificate** drop-down list.

        ![Select Existing Certificate](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3145248951/p31795.png)

        The **Certificate** drop-down list is a collection of certificates that are issued in the SSL Certificates Service console. You can select the certificate associated with the domain name in this list. You can click **Cloud Security - Certificates Service** to go to the SSL Certificates Service console to manage certificates.

    -   **Purchase Certificate**: Click **Buy Now** to go to the configuration page of SSL Certificates Service to purchase a certificate for the domain name.

        ![Select Purchase Certificate](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3145248951/p99119.png)

        The certificate that you purchase is automatically uploaded to WAF.

        **Note:** You can purchase only a DV certificate on this page. If you want to purchase a different type of certificate, go to the buy page of SSL Certificates Service. For more information, see [Select and purchase certificates](/intl.en-US/.md).

6.  Click **Confirm**.


## References

You can go to the **Website Access** page to view the added domain name on the **Domain Names** tab and perform the following operations as required:

-   Upload HTTPS certificates: If your website uses HTTPS, make sure that the correct certificate and private key file are uploaded to WAF. This ensures that WAF protects HTTPS requests. To upload the HTTPS certificate and private key for the domain name, you can click the ![Upload](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3145248951/p97136.png) icon in the **Origin Server** column.

    For more information, see [Upload HTTPS certificates](#section_jo2_hwu_mbj).

-   Enable Log Service for WAF: Click **Log Service** in the **Quick Access** column to enable the Log Service for WAF feature. This feature collects logs of your website. The logs can be used for query, analysis, dashboard data visualization, and alerting.

    For more information, see [Enable log collection](/intl.en-US/Log Management/Log service/Enable log collection.md).

    **Note:** Log Service for WAF is a value-added service provided by WAF. You can use this feature only after you enable it. For more information, see [Enable Log Service for WAF](/intl.en-US/Log Management/Log service/Enable Log Service for WAF.md).

-   Configure protection resources: Click the ![Configure protection resources](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3145248951/p97139.png) icon next to **Protection Resource** in the **Quick Access** column. Then, configure protection resources for the domain name.

    The following protection resource types are supported:

    -   **Shared Cluster and Shared IP**

        **Note:** By default, websites that are automatically added to WAF use protection resources of the **Shared Cluster and Shared IP** type.

    -   **Shared Cluster and Exclusive IP**: For more information, see [Exclusive IP addresses](/intl.en-US/Billing and Service Activation/Subscription/Exclusive IP addresses.md).
    -   **Shared Cluster and Load Balancing Among Multiple WAF Nodes**: For more information, see [Intelligent load balancing](/intl.en-US/Billing and Service Activation/Subscription/Intelligent load balancing.md).
    -   **Exclusive Cluster**: For more information, see [Create an exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md).
-   View attack monitoring reports: Click **View Report** in the **Attack Monitoring** column to navigate to the **Security report** page. On this page, you can view the protection report of the domain name. For more information, see [View security reports](/intl.en-US/.md).
-   Configure protection policies: Click **Config** in the **Actions** column to navigate to the **Website Protection** page. On the page that appears, you can configure the **Web Security**, **Bot Management**, and **Access Control/Throttling** modules. For more information, see [Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md).
-   Edit a domain name: Click **Edit** in the **Actions** column to modify the website configurations, such as the protocol type, server address, and server port. You cannot change the domain name.
-   Delete a domain name: Click **Delete** in the **Actions** column to delete a domain name.

    **Warning:** Before you delete a domain name, change the DNS record to map the domain name to the IP address of the origin server. Otherwise, requests to the domain name cannot be forwarded after the domain name is deleted.


## FAQ

What do I need to know about migrating website configurations across accounts?

To prevent traffic forwarding errors caused by misoperations during website configuration migration, a 30-minute protection period is configured for your website. To migrate the website configurations to another account, you must delete the website configurations from the current account. Then, wait for 30 minutes until you can add the website configurations to the WAF instance of another account.

If you want to immediately migrate the website configurations, submit a [ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80). Alternatively, apply for a protection period cancellation for this domain name in the DingTalk group. After the protection period is canceled, you can add the website configurations to the WAF instance of another account.

