# WAF security reports {#concept_kzf_bdq_p2b .concept}

Alibaba Cloud WAF provides security reports for you to view and understand all protection actions of WAF. You can view the attack protection and risk warning statistics.

## Background information {#section_lmw_l2m_vgb .section}

Alibaba Cloud WAF security reports include attack protection report and risk warning report.

-   The attack protection report gives you an overall view of all Web application attacks, HTTP flood attacks, and HTTP ACL events.
-   The risk warning report records and summarizes common attacks that occur on your network assets, and provides you with risk warning information. You can view the following risk warnings: known hacker attack, WordPress attack, suspected attack, robots script, crawler access, and SMS abuse.

## Procedure {#section_hgn_bdq_p2b .section}

Follow these steps to view WAF security reports:

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  Go to the **Reports** \> **Reports** page.
3.  Go to the Attack Protection or Risk Warning tab page to view the corresponding report.
    -   View attack protection report

        On the Attack Protection tab page, select the attack type to view the detailed records. You can view the following records:

        -   **Web Application Attack**: displays records of all Web attacks inspected by WAF. You can filter the records based on domain names, attack IP addresses, and attack time.

            **Note:** For more information about web attack protection, see [Web application attack protection](intl.en-US/User Guide/Protection configuration/Web application protection.md#).

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15574/155056845738968_en-US.jpg)

            By default, the records are displayed in details. You can also view the attack statistics. Attack statistics displays the distribution of security attack types, top 5 attacker source IP addresses, and top 5 attacker source regions.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15574/155056845738969_en-US.jpg)

        -   **HTTP Flood**: displays the records of HTTP flood attacks inspected by WAF. You can select the domain name and query time to view the corresponding records.

            **Note:** For more information about HTTP flood attack protection, see [HTTP flood protection](intl.en-US/User Guide/Protection configuration/HTTP flood protection.md#).

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15574/155056845738970_en-US.jpg)

            The real-time total QPS and attack QPS records are displayed at the top of the page, and all HTTP flood events are displayed at the bottom of the page. Alibaba Cloud WAF defines the HTTP flood attack as follows: attack duration \> 3 minutes and attack frequency \(per second\) \> 100.

        -   **HTTP ACL Event**: displays the ACL events for a domain name. You can select the domain name and query time to view the corresponding records.

            **Note:** For more information about the HTTP ACL events, see [HTTP ACL events](intl.en-US/User Guide/Protection configuration/HTTP ACL policy.md#).

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15574/155056845738971_en-US.jpg)

    -   View risk warning report

        On the Risk Warning tab page, select a risk type to view details. You can view the following risk records:

        -   **Hacker attack**

            Risk warning provides the hacker profiling function based on Alibaba Cloud big data analytics and the attack source tracing capability. This function identifies and records the malicious behaviors and activities of recognized hackers on your website. These behaviors include footprints, scans, and attacks. A hacker can be an individual or it can be a group of hackers, with real identities. When you receive such alarms, it means your website is hacked by a known hacker.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15574/15505684577802_en-US.png)

            Dots in the figure indicate the activity of hackers on the corresponding date. Click a specific dot to view the detailed attack record. Here,

            -   Different lines stand for different hackers. Click hacker information to view the characteristics of the hacker.
            -   The severity of the hazard is gauged by the color of the dot. Darker the color, more severe is the hazard.
            -   The size of the dots indicates the frequency of attacks during the day. Bigger dots indicate more attacks and smaller dots, lesser attacks.
            Defense: The attack displayed in the report is intercepted by WAF. You do not need to worry about it. We recommend that you pay attention to non-web services security on the server because the hackers may try various options \(for example, SSH and database port\) to penetrate into your website.

        -   **Wordpress**

            Risk warning detects WordPress attacks according to attack features described in [Prevent WordPress bounce attacks](https://www.alibabacloud.com/help/doc-detail/42198.htm). If the number of such warnings keeps increasing, your server may encounter this kind of HTTP Flood attacks these days.

            Defense: Configure [HTTP flood protection](intl.en-US/User Guide/Protection configuration/HTTP ACL policy.md#) according to the defense suggestions provided in the preceding document.

        -   **Suspected attack**

            Based on the exception detection algorithm of big data analytics, WAF screens suspicious access requests, which may include abnormal parameter names, types, sequences, special symbols, and statements, for you to perform further analysis and provide protection based on service features.

            The risk warnings highlight the abnormal portion. For example, the request shown in the following figure includes two repeated parameters and is not connected with the conventional “&” symbol.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15574/15505684577803_en-US.png)

            Defense: The alarm here reports a suspicious request, which may be a normal request of a special service or a variant attack. Analyze the alarm based on features of your service.

        -   **Robot Script**

            WAF supports detecting features of common machine script tools, such as Python2.2 and HttpClient. If you have not submitted a large number of requests through the test tool recently, the alarm number indicates the number of malicious requests received or detected from some machine script tools. It may also include the tools used to test the traffic pressure or initiate HTTP flood attacks.

            Defense: Check whether HTTP flood attacks exist by analyzing [logs](intl.en-US/User Guide/Protection reports/Log search.md#) and intercept malicious attacks based on protection algorithms such as [HTTP ACL Policy](intl.en-US/User Guide/Protection configuration/HTTP ACL policy.md#), [HTTP flood protection emergency mode](intl.en-US/User Guide/Protection configuration/HTTP flood protection.md#), and [blocked region](intl.en-US/User Guide/Protection configuration/Blocked regions.md#).

        -   **Bot Attack**

            WAF supports detecting crawler requests \(including valid crawlers such as Baidu spider\). If the number of this alarms is high, the number of requests increases abnormally on the server, and the CPU usage increases, the website may encounter malicious crawler requests or HTTP flood attacks that are masqueraded as crawlers.

            Defense: Based on logs and server performance analysis, check whether HTTP flood attacks or malicious crawler requests exist. For more information, see [Intercept malicious crawlers](../../../../../intl.en-US/FAQ/Intercept malicious crawlers.md#). WAF does not incept valid crawler \(for example, Baidu crawler\) requests.

        -   **SMS Abuse**

            WAF supports detecting requests on interfaces such as the short message registration interface and short message verification interface. If you receive more alarms, your short message interface is being abused \(causing high short message overhead\).

            Defense: Click **View Details** to view specific requests. You can analyze whether the invocation is normal service invocation based on the source IP address and interface to which most requests are sent. If not, we recommend that you use [Data Risk Control](intl.en-US/User Guide/Protection configuration/Data risk control.md#) and [Custom HTTP flood protection](intl.en-US/User Guide/Protection configuration/Custom HTTP flood protection.md#) to protect the abused interfaces.


