# Deploy WAF and CDN together {#concept_ig2_xfj_p2b .concept}

You can deploy Alibaba Cloud WAF and CDN \(Content Delivery Network\) together to speed up your website and protect against web attacks at the same time. We recommend that you use the following architecture: CDN \(entry layer, website speed up\) \> WAF \(intermediate layer, web attacks protection\) \> Origin.

## Procedure {#section_qnf_dhj_p2b .section}

Suppose you use Alibaba Cloud CDN. Follow these steps to deploy WAF and CDN together:

1.  See [Get started with Alibaba Cloud CDN](../../../../reseller.en-US/Quick Start/Quick start.md#) to implement a CDN for your domain name.
2.  Create a website configuration in Alibaba Cloud WAF.

    -   **Domain name**: Enter the CDN-enabled domain name. Wildcard is supported.
    -   **Server address**: Enter the public IP address of the ECS/Server Load Balancer instance, or the external server IP address of the origin server.
    -   **Any layer 7 proxy \(e.g. Anti-DDoS/CDN\) enabled?**: Check **yes**.
    For more information, see [Website configuration](reseller.en-US/User Guide/Access WAF/Website configuration.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15558/15451983667705_en-US.jpg)

3.  When the website configuration is successfully created, WAF generates a dedicated CNAME address for it.

    **Note:** For more information about how to view the WAF CNAME address, see [WAF deployment guide](reseller.en-US/User Guide/Access WAF/WAF deployment guide.md#).

4.  Modify the CDN configuration to change the origin site address to the WAF CNAME address.
    1.  Log on to the **Alibaba Cloud CDN console**.
    2.  Go to the Domain Names page, select the domain to be configured, and click **Configure**.
    3.  Under **Origin site settings**, click **Modify**.
    4.  Modify origin site information.

        -   **Type**: Select **Origin Site**.
        -   **Origin site address IP**: Enter the WAF CNAME address.
        -   **Use the same protocol as the back-to-source protocol**: Select Enable.
        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15558/15451983667706_en-US.jpg)

    5.  Under **Back-to-Source Settings**, make sure that **Back-to-Source host** is disabled.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15558/15451983667707_en-US.jpg)


After the operation is complete, the traffic goes through CDN, and the dynamic content continues to be checked and protected by WAF.

