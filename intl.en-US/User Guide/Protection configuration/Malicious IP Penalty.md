# Malicious IP Penalty {#concept_kwp_j54_p2b .concept}

Malicious IP penalty helps you automatically block malicious IPs that attack your web assets repeatedly in a short period of time.

## Function description {#section_h22_k54_p2b .section}

Traditional web application firewall products function in the IP-URL dimension. After determining whether a request is an attack, they only block this request once. However, malicious attackers may scan and attack your website repeatedly. These attackers observe and detect your website’s vulnerabilities, study the protection policies, and plan attempts to bypass them.

To address this problem, Alibaba Cloud WAF provides the Malicious IP Penalty function. WAF detects and automatically blocks the malicious IP addresses, through which the website is attacked repeatedly.

WAF generates judging rules for malicious IP address through the database with a massive amount of malicious IP addresses. This database is backed with the machine learning function of Alibaba Cloud platform that keeps studying and analyzing the attacks and attack frequencies of the malicious IP addresses. When an IP address starts continuous attacks, WAF blocks all access requests from this IP address.

## Procedure {#section_k22_k54_p2b .section}

Follow these steps to enable malicious IP penalty:

**Note:** Make sure that you have added your domain to the WAF protection list before proceeding with the following operations. For more information, see [WAF deployment guide](reseller.en-US/User Guide/Access WAF/WAF deployment guide.md#).

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  Go to the **Management** \> **Website configuration** page, and select the region of your WAF instance \(Mainland China or International\).
3.  Select the domain to be configured, and click **Policies**.
4.  Enable **Malicious IP Penalty**. The default protection rule is: when WAF detects two Web attacks by an IP in less than 1 minute, it blocks the IP's access request for 6 minutes.

    **Note:** If you do not want to use malicious IP penalty, you can disable it on this page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15561/15478904497755_en-US.png)


## Test {#section_n22_k54_p2b .section}

Once the Malicious IP Penalty function is enabled, WAF scans the website to detect and automatically block the malicious attacks and access requests from them. This action can incur a higher cost to the hacker to start new attacks. The following is an actual effect test after malicious IP penalty is enabled.

With Malicious IP Penalty, WAF effectively blocks attacks from various automatic tools and scanners to safeguard your website.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15561/15478904497756_en-US.png)

