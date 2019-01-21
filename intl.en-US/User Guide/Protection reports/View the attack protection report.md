# View the attack protection report {#task_t3q_p4l_l2b .task}

Alibaba Cloud WAF provides security reports for you to view and understand all protection actions of WAF. The security reports include attack protection report and risk warning report. The attack protection report gives you an overall view of all Web application attacks, HTTP flood attacks, and HTTP ACL events. The risk warning report records and summarizes common attacks that occur on your network assets, and provides you with risk warning information. This topic describes how to view the attack protection report. For more information about how to use the risk warning report, see [View the risk warning report](reseller.en-US/User Guide/Protection reports/Risk warning report.md#).

Follow these steps to view the attack protection report:

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf). 
2.  Go to the **Reports** \> **Reports** page. 
3.  On the Attack Protection tab page, select the attack type to view the detailed records. 
    -   **Web Application Attack**: displays records of all Web attacks inspected by WAF. You can filter the records based on domain names, attack IP addresses, and attack time.

        **Note:** For more information about web attack protection, see [Web application attack protection](reseller.en-US/User Guide/Protection configuration/Web application protection.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15573/15480425917104_en-US.jpg)

        By default, the records are displayed in details. You can also view the attack statistics. Attack statistics displays the distribution of security attack types, top 5 attacker source IP addresses, and top 5 attacker source regions.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15573/15480425917105_en-US.jpg)

    -   **HTTP Flood**: displays the records of HTTP flood attacks inspected by WAF. You can select the domain name and query time to view the corresponding records.

        **Note:** For more information about HTTP flood attack protection, see [HTTP flood protection](reseller.en-US/User Guide/Protection configuration/HTTP flood protection.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15573/15480425917106_en-US.jpg)

        The real-time total QPS and attack QPS records are displayed at the top of the page, and all HTTP flood events are displayed at the bottom of the page. Alibaba Cloud WAF defines the HTTP flood attack as follows: attack duration \> 3 minutes and attack frequency \(per second\) \> 100.

    -   **HTTP ACL Event**: displays the ACL events for a domain name. You can select the domain name and query time to view the corresponding records.

        **Note:** For more information about the HTTP ACL events, see [HTTP ACL events](reseller.en-US/User Guide/Protection configuration/HTTP ACL policy.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15573/15480425917107_en-US.jpg)


