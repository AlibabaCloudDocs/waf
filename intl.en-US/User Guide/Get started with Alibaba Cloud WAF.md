# Get started with Alibaba Cloud WAF {#task_jtl_1sl_l2b .task}

To get started with Alibaba Cloud WAF, you create a website configuration to implement WAF for your site and configure the WAF protection policies for various scenarios.

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf). 

    In the upper right corner of the page, you can see the version and expiration time of your WAF instance and perform the Renew and Upgrade actions. For more information, see [Renewal and upgrade](../../../../../reseller.en-US/Pricing/Renewal and upgrade.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15551/15508237597108_en-US.png)

2.   Go to the **Management** \> **Website Configuration** page and select the region of your WAF instance \(Mainland China or International\).![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15551/15508237597110_en-US.png)

 
3.  On the Website Configuration page, click **Add Domain** to create a website configuration to associate your website with the WAF instance. For more information, see [Website configuration](reseller.en-US/User Guide/Implementation/Website configuration.md#). 

    **Note:** To add a website configuration to the WAF instance of Mainland China, the website to be protected must have an ICP license.

    You can also click **Edit** or **Delete** to manage the existing configurations.

4.  After the configuration is complete, use the WAF CNAME address to update the domain name's DNS settings to redirect web traffic to WAF for inspection. For more information, see [Implement Alibaba Cloud WAF](reseller.en-US/User Guide/Implementation/Deploy Alibaba Cloud WAF.md#). 
5.  With WAF implemented, go to the **Management** \> **Website Configuration** page, locate to the domain name to be configured, and click **Policies**. 
6.  On the domain name protection configuration page, configure the following scenario-based protection features as needed. 

    -   [Web Application Protection](reseller.en-US/User Guide/Configuration/Web application protection.md#)
    -   [Malicious IP Penalty](reseller.en-US/User Guide/Configuration/Malicious IP Penalty.md#)
    -   [HTTP Flood Protection](reseller.en-US/User Guide/Configuration/HTTP flood protection.md#)
    -   [HTTP ACL Policy](reseller.en-US/User Guide/Configuration/HTTP ACL policy.md#)
    -   [Blocked Regions](reseller.en-US/User Guide/Configuration/Blocked regions.md#)
    -   [New Intelligent Protection Engine](reseller.en-US/User Guide/Configuration/New intelligent protection engine.md#)
    -   [Website tamper-proofing](reseller.en-US/User Guide/Configuration/Website tamper-proofing.md#)
    -   [Data Risk Control](reseller.en-US/User Guide/Configuration/Data risk control.md#)
    -   [Data Leakage Prevention](reseller.en-US/User Guide/Configuration/Data leakage prevention.md#)
    Alibaba Cloud WAF inspects web traffic to your website based on the enabled features and rules, and only forwards valid traffic to your origin server.

7.  Go to the Reports page to view WAF protection records and network traffic statistics. 

    The following reporting features are available:

    -   [Overview](reseller.en-US/User Guide/Reporting/Business and security overview.md#) gives you a glimpse of the business and security environment of a WAF-enabled site.
    -   [Reports](reseller.en-US/User Guide/Reporting/WAF security reports.md#) allow you to view and understand all WAF protection actions with the Attack protection and Risk warning reports.
        -   Attack protection reports display the detailed records of Web application attacks, HTTP flood, and HTTP ACL events on the WAF-enabled websites.
        -   Risk warning reports display the detailed records of known hacker attacks, WordPress attacks, suspected attacks, robots scripts, bot attacks, and SMS abuses on the WAF-enabled websites.
    -   [Logs](reseller.en-US/User Guide/Reporting/Log search.md#) help you record all web requests to your website and enable you to search the stored logs for business analysis or security management.

        **Note:** You must first enable the **Log Query** function on the Website Configuration page for the domain name. WAF only collects the access logs for the specified domain name.

    -   [Data Visualization](reseller.en-US/User Guide/Reporting/Data visualization.md#) converts the WAF logs data into a visual big screen to let you monitor and understand the real-time attack and defense situations of your website.
8.  Go to the Setting page to view the [WAF instance information](reseller.en-US/User Guide/Setting/View product information.md#) and configure the [alarm settings](reseller.en-US/User Guide/Setting/Configure alarm settings.md#) or [rule groups](reseller.en-US/User Guide/Setting/Custom rule groups.md#). 
9.  For any technical questions about using Alibaba Cloud WAF, use DingTalk to scan the **Technical Support** code in the lower left corner to join the WAF Technical Support team. Our technical experts are ready to serve you. 

    **Note:** You can go to the [DingTalk official website](https://www.dingtalk.com/) to download and install DingTalk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15551/155082375912056_en-US.png)


