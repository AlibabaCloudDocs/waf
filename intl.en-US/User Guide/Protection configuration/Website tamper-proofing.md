# Website tamper-proofing {#task_b2x_lll_l2b .task}

Website tamper-proofing allows you to lock specific web pages and manually cache the intact content as the server response to prevent malicious tampering. When a locked web page is requested, Alibaba Cloud WAF \(WAF\) responds with the cached content.

**Note:** Make sure that you have implemented WAF for your website before performing this configuration. For more information, see [Implement Alibaba Cloud WAF](reseller.en-US/User Guide/Access WAF/WAF deployment guide.md#).

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf). 
2.  Go to the **Management** \> **Website Configuration** page and select the region of your WAF instance \(Mainland China or International\). 
3.  Locate to the domain name to be configured and click **Policies**. 
4.  Enable **Website Tamper-proofing** and click **Settings**. 

    **Note:** If you no longer need the website tamper-proofing feature, you can disable it on this page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15569/15502015097087_en-US.png)

5.  Click **New Rule** and complete the configuration in the Add New URL dialog box. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15569/15502015097088_en-US.png)

    -   **Service Name**: Name this rule.
    -   **URL**: Specify the exact path of the web page to be protected. Wildcard characters \(such as`/*`\) or parameters \(such as `/abc? xxx=`\) are not supported. WAF can protect all text, HTML, and pictures under this path against tampering.
6.  When the rule is successfully added, turn on the **Protection Status** switch to enable it, that it, lock the specified web page and cache the latest content as the server response. If you do not enable the rule, the settings do not take effect. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15569/15502015107089_en-US.png)

7.  When the locked web page is updated, you must click **Update Cache** to cache the latest content. If you do not perform this operation, WAF always returns the last cached content. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15569/15502015107090_en-US.png)


