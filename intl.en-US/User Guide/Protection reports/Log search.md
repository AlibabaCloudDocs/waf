# Log search {#task_bkt_22q_p2b .task}

When the Log search feature is enabled, Alibaba Cloud WAF helps you record all web requests to your website and enables you to search the stored logs for business analysis or security management.

You must upgrade Alibaba Cloud WAF Pro to the Business or Enterprise plan to use this feature. For more information, see [Renewal and upgrade](../../../../../intl.en-US/Pricing/Renewal and upgrade.md#).

**Note:** The international WAF instance must be upgraded to the Enterprise edition to use this feature.

With the log search function, you can easily complete the following O&M tasks:

-   Check the action \(block or allow\) WAF performs on a specific request.
-   Check the type of rule that terminated a request: web attack protection rule, HTTP flood attack protection rule, or custom access control rule.
-   Check the response time of a specific request to see if the origin server response timed out.
-   Use a combination of field filtering conditions to search for specific requests. For example, source IP address, URL keyword, cookie, referer, user-agent, X-forwarded-for, server response status code, and more.

**Note:** When you enable the Log search function, this constitutes your permission for Alibaba Cloud to record all of the web requests that are inspected by WAF \(POST data is not recorded\).

As a prerequisite, you must go to the Website Configuration page to enable the log search function for a specific domain name. Alibaba Cloud WAF starts recording request logs for the website only when the **Log search** switch is on. When Log search is enabled, you can go to the Logs page to search for logs of the domain name.

**Note:** You can view the request log for up to 100 domain names.

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf). 
2.  Go to the **Management** \> **Website Configuration** page and select the region of your WAF instance \(Mainland China or International\). 
3.  Select the domain name to be configured and enable **Log search** for it. 

    **Note:** You can also disable Log search on this page. When Log search is disabled, the request log is no longer recorded. Even if you enable Log search again, you cannot query the request log for the time during which the function is disabled.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15575/15505473727807_en-US.png)

4.  Go to the **Reports** \> **Logs** page. 
5.  Select the **domain name**, **Query time** and click **Search**. 

    **Note:** Only the latest 30 days' logs can be accessed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15575/15505473727809_en-US.png)

    You can also click **Advanced Search** to define more detailed search conditions.

    |Field|Description|
    |-----|-----------|
    |Source IP|The source IP address.|
    |URL Key Words|The requested URL.**Note:** This field supports the "/" symbol. For example, you can enter /NTIS/casier.

|
    |Cookie|The client-side cookie, which is included in the request header.|
    |Referer|The referer field in the HTTP request header.|
    |User-Agent|The user agent string in the request that identifies the client browser, operating system, and more.|
    |X-Forwarded-For|The XFF field in the request header.|
    |Server Response Code|The response status code that Alibaba Cloud WAF received from the origin server.**Note:** A three-digit number is supported. You can also specify the -symbol to search for requests that have no response status information. For example, the request was blocked.

|
    |Status Code Returned by WAF|The response status code that Alibaba Cloud WAF returned to the client.**Note:** A three-digit number is supported. You can also specify the -symbol to search for requests that have no response status information. For example, the request was blocked.

|
    |Request Unique ID|The request ID. If the request was blocked, you can find the request ID in the blocking page.|
    |Request Domain|When a wildcard domain name is enabled with the log search function, you can use this field to search for a specific domain name.|
    |Protection policies|You can use this option to specify the rule matching type, which includes Web Application Attack Protection, HTTP Flood Protection Policies, HTTP ACL Rules, Region Blocking, and Data Risk Control.|

6.  View the search result. 
    -   In the **Service Traffic** area, you can view access request volume trend charts for the search time range.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15575/15505473727811_en-US.png)

    -   In the **Request Logs** list, you can view the access request records that match the search conditions. The following figure shows the log for an access request that was blocked against the HTTP flood attack protection rule.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15575/15505473727813_en-US.png)

        **Descriptions of parameters in the Origin’s response info**

        -   **Status**: indicates the response status information that Alibaba Cloud WAF returns to the client.
        -   **Upstream\_status**: indicates the response status information that Alibaba Cloud WAF received from the origin server. If “-“ is returned, this indicates no response. For example, this request was blocked by Alibaba Cloud WAF or the origin server response timed out.
        -   **Upstream\_ip**: indicates the origin site IP address of this request. For example, when Alibaba Cloud WAF returns traffic back to an ECS instance, this parameter returns the IP address of the origin ECS instance.
        -   **Upstream\_time**: indicates the time the origin server took to respond to the WAF request. “-“ indicates the response timed out.
7.  Click **Log download** in the upper-right corner of the Log query page to add a download task for the currently retrieved log. On the View the downloaded file page, you can download the log file to your local client. 

    **Note:** You can download up to 20 million lines of logs at a time. If you want to export more than 20 million lines of logs, we recommend that you perform multiple download tasks.

     **Description of request log fields**

    |Field|Name|Description|
    |-----|----|-----------|
    |Time|Time|The UTC time of the request.|
    |Domain|Domain|The requested domain name.|
    |Source\_IP|Source IP|The source IP address.|
    |IP\_City|IP City|The city from which the request originated.|
    |IP\_Country|IP Country|The country from which the request originated.|
    |Method|Method|The HTTP method of the request.|
    |URL|Access request URL|The requested URL.|
    |Https|Access Request Protocol|The protocol specified in the request.|
    |Referer|Referer|The referer field in the HTTP header.|
    |User-Agent|User Agent|The user agent string in the request that identifies the client browser, operating system, and more.|
    |X-Forwarded-For|X-Forwarded-For|The x-forward-field in the request header that identifies the originating IP address of a client connecting to a web server through an HTTP proxy or load balancer.|
    |Cookie|Cookie|The cookie field in the request header that identifies the client cookie information.|
    |Attack\_Type|Attack Type| The event triggered by the request.

    -   0: indicates that no attack was found.
    -   1: indicates that the Web application attack protection rule was triggered.
    -   2: indicates that the HTTP flood protection rule was triggered.
    -   3: indicates that the HTTP ACL policy rule was triggered.
    -   4: indicates that the Blocked region rule was triggered.
    -   5: indicates that the Data risk control rule was triggered.
 |
    |Status|Response Status Code|The response status code that Alibaba Cloud WAF returned to the client.|
    |Upstream\_status|Status|The response status code that Alibaba Cloud WAF received from the origin site. "-" indicates that no response was received. For example, the request was blocked by WAF or the origin site timed out.|
    |Upstream\_IP|Upstream IP|The source IP address of the request. For example, when Alibaba Cloud WAF returns traffic to an ECS instance, this parameter indicates the IP address of the origin ECS instance.|
    |Upstream\_Time|Upstream Time|The time that the origin server took to respond to the request. "-" indicates that the response timed out.|


