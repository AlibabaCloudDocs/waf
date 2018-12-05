# Deploy WAF and Anti-DDoS Pro together {#task_tpk_dfj_p2b .task}

Alibaba Cloud WAF and Anti-DDoS Pro and are fully compatible. You can use the following architecture to deploy WAF and Anti-DDoS Pro together: Anti-DDoS Pro \(entry layer, DDoS attack protection\) \> WAF \(intermediate layer, web attack protection\) \> Origin.

1.  Create a website configuration for your website in Alibaba Cloud WAF. 

    -   **Server address**: Check **IP** and enter the public IP address of the ECS instance/Server Load Balancer instance or external server IP address.
    -   **Any layer 7 proxy \(e.g. Anti-DDoS/CDN\) enabled?**: Check **yes**.
    For more information, see [Website configuration](intl.en-US/User Guide/Access WAF/Website configuration.md#).

2.  Create a web service access configuration for your website in Anti-DDoS Pro. The procedure is as follows: 
    1.  On the **Access** \> **Web Service** page, click **Add Domain**.
    2.  In the Fill in the domain name information task, do the following:

        -   **Domain name**: Enter the domain name to be protected.
        -   **Protocol**: Check the supported protocol.
        -   **Origin IP/Domain**: Check **Origin site domain** and enter the WAF CNAME address.

            **Note:** For more information about how to view the WAF CNAME address, see [WAF deployment guide](intl.en-US/User Guide/Access WAF/WAF deployment guide.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15557/154397512933576_en-US.png)

    3.  Click **Next**.
    4.  Complete the **Please choose Instance and ISP Line** task.
3.  Update the DNS settings of your domain name. Log on to the DNS host's system and add a CNAME record to redirect web traffic to the Anti-DDoS Pro CNAME address. 

    For more information, see [Access Anti-DDoS Pro through a CNAME record](https://www.alibabacloud.com/help/doc-detail/40532.htm).


All web requests to your website are redirected to Anti-DDoS Pro for cleanup and then redirected to WAF for inspection before they reach your origin server.

