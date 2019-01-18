# Intercept malicious crawlers {#concept_a4w_chl_q2b .concept}

This topic explains the features of malicious crawlers and describes how to use WAF to block them.

It is noteworthy that, professional crawlers constantly change their crawling methods to bypass anti-crawling policies set by the website administrators. It is impossible to achieve perfect protection by applying fixed rules. In addition, anti-crawling has a strong association with the characteristics of your own business. Therefore, you must regularly review and update the protection policies to achieve relatively ideal results.

## Distinguish malicious crawlers {#section_w5c_dhl_q2b .section}

Normal crawlers are usually labeled with marks similar to xxspider’s user-agent. They request in a regular manner, and the URLs and time are relatively scattered. If you perform an inverted nslookup or tracert on a legitimate crawler, you can always find the legitimate source address. For example, a Baidu crawler record is shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15615/15477944768008_en-US.png)

However, malicious crawlers may send a large number of requests to a specific URL/interface of a domain name during a specific period of time. It may be an HTTP flood attack disguised as a crawler, or a crawler that crawls targeted sensitive information disguising as a third party. When the number of requests sent by a malicious crawler is large enough, it can usually cause a sharp rise in CPU usage, failure to open the website, and service interruptions.

WAF performs [Risk warning](../../../../../reseller.en-US/User Guide/Protection reports/Risk warning report.md#) against malicious crawlers, and alerts you about yesterday’s crawler requests. You can configure one or more of the following rules based on your actual business situation, to block the corresponding crawler requests.

## Configure HTTP ACL policy to block specific crawlers {#section_y5c_dhl_q2b .section}

You can [configure the HTTP ACL policy](../../../../../reseller.en-US/User Guide/Protection configuration/HTTP ACL policy.md#) to use user-agent, URL, and other keywords to filter out malicious crawler requests. For example, the following configuration only allows Baidu crawler, and filters out other crawlers \(keywords are not case-sensitive\).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15615/15477944768009_en-US.png)

**Note:** Multiple conditions in a rule are connected by the “AND” logical relationship, that is, a request must satisfy all conditions of a rule for the rule to be effective.

You can use the following configurations to prevent all crawlers from accessing contents under the /userinfo directory.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15615/15477944768010_en-US.png)

## Configure custom HTTP flood policies to block malicious requests {#section_bvc_dhl_q2b .section}

Using [custom HTTP flood protection rules](../../../../../reseller.en-US/User Guide/Protection configuration/Customize HTTP flood protection.md#) allows you to set a few specific URLs blocking rules under certain access frequency.

