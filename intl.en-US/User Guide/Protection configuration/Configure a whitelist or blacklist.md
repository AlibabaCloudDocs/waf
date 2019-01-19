# Configure a whitelist or blacklist {#concept_rbj_mbp_p2b .concept}

You can set a whitelist or blacklist by configuring HTTP ACL policies in WAF. The whitelist and blacklist are only effective on the specific domain that has the HTTP ACL policy configured.

## Procedure {#section_ckj_xlp_p2b .section}

Follow these steps to configure a whitelist or blacklist:

**Note:** Make sure that you have added your domain to the WAF protection list before proceeding with the following operations. For more information, see [WAF deployment guide](reseller.en-US/User Guide/Access WAF/WAF deployment guide.md#).

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  Go to the **Management** \> **Website Configuration** page, and select the region of your WAF instance \(Mainland China or International\).
3.  Select the domain to be configured, and click **Policies**.
4.  Enable **HTTP ACL Policy**, and click **Settings**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15478905827783_en-US.jpg)

5.  Click **Add Rule**.
    -   Whitelist configuration example. Use the following configuration to allow all requests from IP 1.1.1.1.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15478905827784_en-US.jpg)

        **Note:** If you want to allow all requests from this IP, do not select any “Proceed to …” protection option in the Add Rule dialog box. If any protection option is selected, some requests from this IP can still be blocked.

    -   Similarly, you can also follow this procedure to set blacklist for a specific domain.

## Note {#section_kd4_cmp_p2b .section}

-   A rule supports up to three matching conditions. All conditions in a rule must be matched to trigger the rule. If you want to whitelist or blacklist multiple discrete IP addresses/IP segments, you must configure multiple HTTP ACL rules. For example, to block access requests from 1.1.1.1, 2.2.2.2, and 3.3.3.3, you must configure three rules separately.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15478905827786_en-US.jpg)

-   The IP matching filed in HTTP ACL rules supports mask format \(for example, 1.1.1.0/24\), and the logical operator supports “does not have”. For example, you can use the following configuration to only allow requests from specific IP segment to one domain.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15478905827787_en-US.jpg)

-   Priority exists among multiple HTTP ACL rules. WAF applies the HTTP ACL rules according to the displayed sequence \(from top to bottom\) of HTTP ACL rules in the HTTP ACL Policy list. Additionally, you can click **Sort Rules** to change the priority among the HTTP ACL rules.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15478905827789_en-US.jpg)


