# Blocked regions {#task_vfm_vdl_l2b .task}

Use this feature to add specific areas of Mainland China, Hong Kong, Macao and Taiwan, and up to 247 countries in the world to the region blacklist. All requests from the specified areas are blocked.

To enable the Blocked Regions feature, you must upgrade WAF to Enterprise Edition or above. For more information about the upgrade, see [Renewal and upgrade](../../../../../reseller.en-US/Pricing/Renewal and upgrade.md#).

To enable and specify blocked regions, follow these steps:

**Note:** Ensure that you have added the target domain in WAF for protection. For more information, see [CNAME access guide](reseller.en-US/User Guide/Access WAF/WAF deployment guide.md#).

1.  Log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf). 
2.  Go to the **Management** \> **Website Configuration** page, and select the region of your WAF instance \(Mainland China or International\). 
3.  Select the domain to be configured, and click **Policies**. 
4.  Enable the **Blocked Regions** option. 

    **Note:** To make the Area Blocking polices be effective, ensure that the system default rule is enabled in HTTP ACL Policy.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15566/15469628207072_en-US.png)

5.  Click **Settings**, select the **Mainland China** or **International** scope, and select the areas that you want to block. Then, click **OK**. 

    **Note:** When you select the **International** scope, you can quickly find the country or area through the initial letter of the country name or the quick search.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15566/15469628207073_en-US.png)


After you confirm the settings, all requests from the IP addresses in the blocked areas are blocked by WAF.

**Note:** The source area information of the IP is based on the [Alibaba Taobao IP address Library](http://ip.taobao.com/).

