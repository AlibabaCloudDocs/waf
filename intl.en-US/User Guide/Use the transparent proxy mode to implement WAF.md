# Use the transparent proxy mode to implement WAF {#task_jc3_4cf_zgb .task}

The transparent proxy mode is a more efficient method to configure Alibaba Cloud WAF \(Web Application Firewall\) for your site. This topic describes how to use the transparent mode to implement WAF.

To use the transparent proxy mode, you must meet the following requirements:

-   The billing method of WAF instances must be Subscription.
-   The origin server must be deployed on Alibaba Cloud Elastic Compute Service \(ECS\). The ECS instance can only be created in the China \(Beijing\) region.
-   The ECS instance where the origin server is deployed must have a public IP address, or is associated with an EIP address.

    **Note:** The transparent proxy mode does not support redirecting ECS traffic through a public IP address of a Server Load Balancer \(SLB\) instance.


You can configure WAF for a website by using the transparent proxy mode or the DNS proxy mode.

**Note:** You can only choose one of these modes. If you choose the transparent proxy mode, you must clear the website configuration that you have set for the DNS proxy mode. If you choose the DNS proxy mode, you must clear the website configuration that you have set for the transparent proxy mode.

-   Transparent proxy mode: This mode directs HTTP requests that are received on port 80 of the specified origin server to WAF. WAF processes the requests and then redirects the requests to the origin server.

    To use this mode, you must authorize WAF to access the ECS instance where your origin server is deployed. To configure this mode, add a domain and specify the IP address of the server that hosts your website in the WAF console. For more information about how to configure this mode, see the following section.

-   DNS proxy mode: This mode directs requests that are sent to the protected domain to WAF based on the specified DNS record. WAF then processes and redirects the requests to the specified origin server.

    This mode requires you to add a website configuration in the WAF console and update DNS settings of the domain. For more information, see [Website configuration](intl.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#) and [Update DNS settings](intl.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#).


1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  In the left-side navigation pane, click **Management** \> **Website Configuration**.
3.  Select **Transparent Proxy Mode**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134541/155892896339912_en-US.png)


4.  Click **Authorize**. 

    **Note:** If this is the first time that you have used the transparent proxy mode, you must authorize WAF to access the ECS instance. If you have already authorized WAF, skip this step and perform [step 6](#).

5.  On the Cloud Resource Access Authorization page, click **Confirm Authorization Policy**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134541/155892896339913_en-US.png)

 You will be directed to the Add Domain Name page after you authorize WAF. Perform [step 7](#).
6.  Click **Add Domain Name**.
7.  On the Add Domain Name page, specify the **domain** that needs protection. In the left-side **Destination Server IP Addresses** list, select the origin server IP address of the domain. 

    **Note:** HTTP requests that are received on port 80 of the selected IP address will be directed to WAF for analysis and processing. WAF detects the HTTP requests based on the protection policy that you have set, and then redirects the requests to the origin server.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134541/155892896339914_en-US.png)

8.  Verify that the configuration is correct and click **Confirm**. The domain has been added. After a domain is added, request redirection is triggered automatically. You can view the **status** of the server IP addresses that you have specified on the **Destination Server IP Addresses** page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134541/155892896339915_en-US.png)

    Status description:

    -   **Traffic Routed**: This status indicates that all requests received on port 80 of the specified IP address are redirected automatically to WAF.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134541/155892896339916_en-US.png)

    -   **Routing Traffic**: This status indicates that requests are being redirected.
    -   **Route Failed**: This status indicates that an error occurred while redirecting requests.
    -   **Deleting**: This status indicates that the IP address is being removed.
    If you no longer need to redirect requests for a server IP address, you can **delete** it on the **Destination Server IP Addresses** page.

    **Note:** To disable request redirection, you must delete the website configuration on the Website Configurations page and the server IP address on the Destination Server IP Address page.


After you configure WAF for your website by using the transparent proxy mode, specify the protection policy for your domain. For more information, see [WAF features](intl.en-US/User Guide/Overview.md#configure).

