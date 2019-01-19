# Custom HTTP flood protection {#task_nkw_hbp_p2b .task}

The Business and Enterprise editions of Alibaba Cloud WAF support customizing HTTP flood protection rules to apply rate-based access control.

The frequency of certain URLs can be restricted from accessing your server by applying custom protection rules in the console. For example, you can define the following rule: when a single source IP address accesses www.yourdomain.com/login.html for more than 20 times within 10 seconds, then block this IP address for one hour.

You must upgrade WAF to the Business or Enterprise edition to use this function. For more information, see [Renewal and upgrade](../../../../../reseller.en-US/Pricing/Renewal and upgrade.md#).

Make sure that you have added your domain to the WAF protection list before proceeding with the following operations. For more information, see [WAF deployment guide](reseller.en-US/User Guide/Access WAF/WAF deployment guide.md#).

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf). 
2.  Go to the **Management** \> **Website Configuration** page, and select the region of your WAF instance \(Mainland China or International\). 
3.  Select the domain to be configured, and click **Policies**. 
4.  Enable **HTTP Flood Protection** \(**Normal** mode\) and Custom Rules, and click **Settings**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15564/15478905197764_en-US.png)

 
5.  Click **New Rule** to add a rule. The parameters include: 

    |Configuration|Description|
    |-------------|-----------|
    |**Name**|The name of this rule.|
    |**URI**|The URI path to be protected. For example, /register. The path can contain parameters connected by “?”. For example, you can use /user? action=login.|
    |**Matching rule**|     -   **Exact Match**: The request URI must be exactly the same as the configured URI here to get counted.
    -   **URI Path Match**: When the request URI starts with the URI value configured here, the request is counted. For example, /register.html is counted if you use /register as the URI.
 |
    |**Interval**|The cycle for calculating the number of visits. It works in sync with **Visits from one single IP address**.|
    |**Visits from a single IP address**|The number of visits allowed from a single source IP address to the URL during the **Interval**.|
    |**Blocking type**|The action to be performed after the condition is met. The operations can be Block or Human-Machine Identification.    -   **Block**: blocks accesses from the client after the condition is met.
    -   **Man-Machine Identification**: accesses the client with redirection after the condition is met. Only the verified requests are forwarded to the origin.
|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15564/15478905197765_en-US.png)

    Consider the configurations in the preceding figure: a single IP address can access the target address \(Exact Match\) more than 20 times in 10 seconds, after which the IP is blocked for 600 minutes.

    Since WAF collects data from multiple servers in the cluster to calculate the frequency of access from a single IP, a certain delay may exist in the statistical process.


Once the rule is added successfully, you can **Edit** or **Delete** the rule.

