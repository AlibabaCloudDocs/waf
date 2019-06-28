# Web application protection {#task_pxh_dxj_p2b .task}

Web application protection provides different levels of protection policies, including loose, normal, and strict, to prevent common Web application attacks such as SQL injection and XSS attacks.

After you add your domain to the WAF protection list, you can enable Web application protection for this domain, and select a protection policy. This feature takes effect immediately after you enable it. You can disable it at any time.

Before you perform the following operations, make sure that you have added the domain to WAF for protection. For more information, see [Use WAF CNAME to add domains for protection](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#).

1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  In the left-side navigation pane, choose **Management** \> **Website Configuration**. On the Website Configuration page, select the region of your WAF instance. The options include Mainland China and International.
3.  In the domain list, find the domain to be configured, and click **Policies** in the Operation column.
4.  Enable **Web Application Protection**, and select a mode. 

    **Note:** You can disable this feature on this page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15560/15616850327731_en-US.png)

    -   **Prevention mode**: detects and blocks attacks.
    -   **Detection mode**: detects attacks and generates alerts.
5.  In the **Policy** drop-down list, select a protection policy. 
    -   By default, the **Normal** policy is selected.
    -   In the normal policy mode, if many normal requests are blocked or many uncontrollable user inputs are detected, such as rich text editors and technology forums, we recommend that you use the **Loose** policy.
    -   If you require stricter protection against path traversal, SQL injections, and command execution attacks, we recommend that you use the **Strict** policy.
6.  Click **Settings** on the right of Decoding Settings. In the **Decoding Settings** dialog box, select the data formats to be decoded and analyzed by the Web application protection feature. If this feature often blocks normal requests with data of a specific format, open the **Decoding Settings** dialog box, clear the check box of this format, and click **OK**. 

    **Note:** To ensure high performance, the feature decodes and analyzes the request data of all formats by default. You cannot clear URL decoding, JavaScript Unicode decoding, hex decoding, comment processing, or space compression.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15560/156168503249550_en-US.png)


