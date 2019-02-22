# HTTP flood protection {#concept_erx_gbp_p2b .concept}

HTTP Flood protection helps you block HTTP flood attacks against your website.

## Function description {#section_fqd_hcp_p2b .section}

HTTP Flood protection helps you block HTTP flood attacks in different modes, including Normal and Emergency. After adding your website to the WAF protection list, you can enable HTTP Flood protection and select an appropriate protection mode for the website. Upon identifying an HTTP flood attack, WAF disconnects from the client to protect your origin.

The Business and Enterprise editions support advanced HTTP flood protection. For more information, see [FAQ](#).

**Note:** The Emergency mode is applicable to web pages, but not to API/Native Apps, because it may result in a large number of false positives. For API/Native Apps, you can use [Custom HTTP Flood Protection](reseller.en-US/User Guide/Configuration/Custom HTTP flood protection.md#).

## Procedure {#section_iqd_hcp_p2b .section}

Follow these steps to configure HTTP flood protection mode:

**Note:** Make sure that you have added your domain to the WAF protection list before proceeding with the following operations. For more information, see [WAF deployment guide](reseller.en-US/User Guide/Implementation/Deploy Alibaba Cloud WAF.md#).

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  Go to the **Management** \> **Website Configuration** page, and select the region of your WAF instance \(Mainland China or International\).
3.  Select the domain to be configured and click **Policies**.
4.  Enable **HTTP Flood Protection** and select the protection mode:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15563/15508263647762_en-US.png)

    -   **Normal**: Used by default. In Normal mode, WAF only blocks extremely suspicious requests, and the amount of false positives is relatively small. We recommend that you use this mode when there is no apparent traffic exception to your website to avoid false positives.
    -   **Emergency**: When you find many HTTP flood attacks are not blocked in the Normal mode, you can switch to the Emergency mode. In Emergency mode, WAF imposes strict inspection rules against HTTP flood attacks, but it may cause false positives.
    **Note:** 

    -   If many attacks are still missed out in the Emergency mode, check if the source IP addresses are WAF’s back-to-Source IP addresses. If the origin is directly attacked, see [Protec your origin server](../../../../../reseller.en-US/Best Practices/Protect your origin server.md#) to only allow WAF’s back-to-Source IP addresses to access the server.
    -   For better protection effects and lower false positive rate, you can use the Business Edition or Enterprise Edition to customize or request security experts to customize targeted protection algorithms for your website.

## FAQ {#section_nqd_hcp_p2b .section}

**What is the difference between HTTP flood protection capability for different WAF editions?**

WAF is categorized based on the capacity to provide protection against the complex HTTP flood attacks.

-   **Pro Edition**: supports default protection modes \(Normal and Emergency\), and blocks HTTP flood attacks with obvious attack characteristics.
-   **Business Edition**: supports custom access control rules, and defends against HTTP flood attacks with certain attack characteristics. For more information, see [Custom HTTP flood protection](reseller.en-US/User Guide/Configuration/Custom HTTP flood protection.md#).
-   **Enterprise Edition**: offers protection rules customized by security experts to guarantee solid protection effects.

For more information on how to upgrade WAF, see [Renewal and upgrade](../../../../../reseller.en-US/Pricing/Renewal and upgrade.md#).

**Why must I upgrade WAF to the Business Edition to defend against certain HTTP flood attacks?**

Alibaba Cloud WAF identifies attacks by using human identification, big data analysis, model analysis, and other techniques, and blocks attacks accordingly. Different from program interaction, security attack and defense is the confrontation between people. Each website has its own performance bottleneck. If hackers find a type of attack to be ineffective, they may analyze the website and then start a targeted attack.  In this case, Alibaba Cloud Security experts can analyze the attack to provide a higher level protection and a better protect effect.

