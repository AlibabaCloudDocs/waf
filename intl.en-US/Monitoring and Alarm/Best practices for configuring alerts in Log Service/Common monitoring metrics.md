# Common monitoring metrics

This topic describes the common metrics that you can use to query and analyze logs collected by Log Service for WAF. You can use these metrics to configure alerts and monitor exceptions in your workload as needed. This topic also provides the recommended alert thresholds of metrics and suggestions on handling metric exceptions.

|Metric|Description|Recommended threshold|Suggestion|
|------|-----------|---------------------|----------|
|**200**|The server has processed the request and returned the requested data.|Before you initialize your workloads, set the alert threshold to 90% for status code 200. You can adjust the threshold as needed.|If the percentage of code 200 is lower than the specified threshold, identify the reason. For example, this is because the percentage of another status code has increased.|
|**request\_time\_msec**|Time period between the time when the client sends a request and the time when the client receives a response.|Set the alert thresholds based on the time required for actual service requests.|If it takes a long time to receive responses from a domain name, check the network connectivity between the client and WAF and that between WAF and the origin servers, and make sure that the origin servers respond properly.|
|**upstream\_response\_time**|The time period between the time when WAF sends data to the origin server and the time when WAF receives a response from the origin server.|
|**ssl\_handshake\_time**|The time required for an SSL handshake between the client and WAF during an HTTPS request.|
|**status:302 and block\_action:tmd**/**status:200 and block\_action:tmd**|The status code indicates whether CAPTCHA is triggered. Code 302 indicates that CAPTCHA is triggered, and code 200 indicates that CAPTCHA is not triggered and the HTTP flood protection is triggered.|When you initialize your workloads, we recommend that you set the alert threshold for status code percentage to a value from 5% to 10%. You can adjust the threshold based on the traffic blocked by WAF.|-   If the alert threshold is reached, find out whether the domain name is under HTTP flood attacks and customize rules to block the attacks.
-   Check for server exceptions, such as, a large number of 5xx status codes or 4xx status codes. |
|**status:200 and block\_action:antifraud**|A request is blocked by data risk control.|Test the alert rule before you apply it. If you receive this alert frequently, contact the Alibaba Cloud R&D team to adjust the alert threshold.|
|**status:404**|The server cannot find the requested resources.|Query the source IP addresses that trigger the alert. -   If only one IP address triggers the alert, a malicious user may have started a path traversal on your server.
-   If multiple IP addresses trigger the alert, check whether the server works properly and whether any files are missing. |
|**status:405**|A request is blocked by either web application protection rules or HTTP ACL policy rules.|Use the log analysis feature to analyze the blocked request and the rule that is used to block the request, and find out whether this is a false positive.|
|**status:444**|A request is blocked by custom HTTP flood protection rules.|-   If the alert threshold is reached, find out whether the domain name is under HTTP flood attacks and customize rules to block the attacks.
-   If the blocked request is not an attack but an API call, you can adjust the threshold or allow API calls on specified servers. |
|**status:499**|After a client sends a request, the server does not return data. After the maximum wait time of the client is reached, the client disconnects, and the server returns this status code.|-   Check for exceptions on the origin server, such as, slow responses and a large number of slow queries on the database.
-   Check whether attacks have consumed all resources on the origin server. |
|**status:500**|A request cannot be processed due to the 500 Internal Server Error.|We recommend that you check the loads and database status of the origin server.|
|**status:502**|The server is used as a gateway or a proxy and receives invalid responses from the upstream server due to a 502 Bad Gateway error. The origin server does not respond due to low quality performance of the back-to-origin network or the fact that back-to-origin requests are blocked by access control policies configured for the origin server.|-   Check the back-to-origin network quality, the access control policies on the origin server, and the loads and database status of the origin server.
-   Check whether the origin server has blocked requests from the back-to-origin IP address of WAF. |
|**status:503**|The service is unavailable due to overloads or maintenance needs.|Check for exceptions on the origin server.|
|**status:504**|The server serves as a gateway or proxy but fails to receive requests from the upstream server in time. The 504 Gateway Timeout error occurred.|Possible causes include: -   The server fails to respond due to overload.
-   The origin server does not reset after it discards requests.
-   The protocol-based communication fails. |

