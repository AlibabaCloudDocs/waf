# DNS resolution status exception {#concept_zth_yzk_q2b .concept}

When a website configuration is created in Alibaba Cloud WAF, WAF automatically performs the following checks:

-   **Domain to CNAME**: Performed every hour to detect whether the domain name has been resolved to the WAF CNAME address.
-   **Web traffic**: Performed every several minutes to detect whether the web traffic to the domain name passes through WAF.

When one of the checks is ok, the DNS resolution status is Normal, which indicates that Alibaba Cloud WAF is perfectly implemented for the website.

To view the **DNS resolution status**, log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf) and go to the **Management** \> **Website Configuration** page.

The **Normal** status displays as follows.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15598/15439928727971_en-US.jpg)

If the DNS resolution status is **Exception**, then Alibaba Cloud WAF may not be correctly configured. This topic explains how does WAF determine the DNS resolution status and lists common exception statuses.

## How does WAF determine the DNS resolution status {#section_yrq_yzk_q2b .section}

Alibaba Cloud WAF determines the DNS resolution status by the following conditions. When one of the conditions is met, the DNS resolution status is normal.

-   Condition A: The domain name is resolved to the WAF CNAME address.
-   Condition B: Web traffic of the domain name passes through WAF. When at least 10 requests are detected in the last five seconds, it is ok. Two or three requests per minute is regarded as no traffic. To view the history of web traffic, you can check the Attack protection report of HTTP flood. For more information, see [Attack protection reports](../../../../intl.en-US/User Guide/Protection reports/Attack protection reports.md#).

We recommend that you use a CNAME record to redirect web traffic to WAF. Using CNAME supports node switch or even redirecting traffic back to source in case of node failure or machine failure, which improves your business’s availability and failure recovery capacity. If CNAME record conflicts with your current DNS settings, you can use an A record to do traffic redirection.

## Common exception statues {#section_x5b_f1l_q2b .section}

-   For a fully qualified domain name \(FQDN, such as example.abc.com\), if both the Domain to CNAME and Web traffic checks fail, the exception status displays as follows.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15598/15439928727972_en-US.jpg)

-   For a wildcard domain name \(for example, \*.abc.com\), the exception status displays as follows.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15598/15439928727973_en-US.jpg)

-   When the website is deployed with CDN or other proxy servers in front of WAF, the domain name is resolved to CDN and other proxy server rather than WAF. As a result, the Domain to CNAME check fails. In addition, the CDN-returned traffic received by WAF is low, which may result to the Web traffic check fails. In this case, the exception message does not definitely indicate that WAF is ill-configured.

    For more information about how to deploy WAF and CDN together, see [Deploy WAF and CDN together](../../../../intl.en-US/User Guide/Access WAF/Deploy WAF and CDN together.md#).


## Manually test if WAF is working {#section_cts_g1l_q2b .section}

1.  Visit a domain name that is configured in Alibaba Cloud WAF, for example, www.aliyundemo.cn. The webpage can be accessed normally.
2.  Add the /alert\(xss\) string to the end of the domain name to assemble a testing URL and visit this URL \(in this example, www.aliyundemo.cn/alert\(xss\). If you receive a 405 page telling you that this request is blocked by Alibaba Cloud WAF, then WAF is protecting the website.

