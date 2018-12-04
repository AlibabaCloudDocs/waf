# Whitelist Alibaba Cloud WAF IP addresses {#concept_wzd_by1_p2b .concept}

When a website is deployed with Alibaba Cloud WAF, all web traffic is redirected to WAF for inspection, and WAF returns the inspected traffic to origin server.

From the origin server’s perspective, all web requests arrive from a limited quantity of WAF IP addresses, which is suspicious. If the origin server has been installed with a security software such as FortiGate, the security software may trigger a blocking action against WAF IP address and web traffic returned by WAF. Therefore, you must whitelist all WAF IP addresses in the security software in origin server to avoid normal business interruption.

**Note:** We recommend that you uninstall other security software in origin server after Alibaba Cloud WAF is deployed.

## Procedure {#section_sb1_xrb_p2b .section}

You can view the IP addresses of Alibaba Cloud WAF in the Alibaba Cloud WAF console. The procedure is as follows.

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China**, **International**.
3.  Go to the **Management** \> **Website Configuration** page.
4.  Click **Alibaba Cloud WAF IP range** to view and copy all WAF IP addresses.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15547/15438899167574_en-US.png)

    You can see the following result:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15547/15438899167575_en-US.png)

5.  Open the security software in origin server, and add the copied WAF IP addresses to the IP whitelist.

## FAQs {#section_wb1_xrb_p2b .section}

**What is the Alibaba Cloud WAF IP address?**

Alibaba Cloud WAF acts as a reverse proxy between your client and origin server. In origin server’s eyes, all web requests originate from Alibaba Cloud WAF IP addresses and the real client IP addresses are written into the XFF \(X-Forwarded-For\) field of HTTP header.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15547/15438899167576_en-US.png)

**Why must I whitelist Alibaba Cloud WAF IP addresses?**

From origin server’s perspective, web requests from the Alibaba Cloud WAF IP addresses are more concentrated and in a very high frequency. The security software in origin server may determine that Alibaba Cloud WAF IP addresses are starting attacks, and trigger a blocking action against them. If Alibaba Cloud WAF IP addresses are blocked, the real client cannot get a response. Therefore, you must whitelist Alibaba Cloud WAF IP addresses once your website is deployed with WAF. Otherwise, normal web access may be affected, which leads to web pages cannot be opened or respond slowly.

We recommend that after deploying Alibaba Cloud WAF, you only allow web requests originate from WAF and block other requests to guarantee normal web business access and avoid direct-to-origin attacks. If the origin server IP address is disclosed, an attacker can bypass WAF to directly attack your origin server. For more information, see **Protect your origin server**.

