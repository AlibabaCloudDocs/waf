# Business and security overview {#concept_wnz_t4l_l2b .concept}

The Alibaba Cloud WAF Overview page gives you a glimpse of the business and security environment of a WAF-enabled site.

## View business overview {#section_u1m_z4l_l2b .section}

Follow these steps to view the business overview page:

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  Go to the **Reports** \> **Overview** page and select the region of your WAF instance \(Mainland China or International\).
3.  On the Business tab page, select a domain name and time period to display the business summary of the specified domain name during the time period. The time period options include Real-time, 6 Hours, 1 Day, 7 Days, 30 Days, or Custom.

    **Note:** The business statistics for the last 30 days can be viewed. You can use Custom to specify a time period within the last 30 days to view the record.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297091_en-US.jpg)

    The business overview includes the following information:

    -   **QPS**: This graph displays all queries per second and the number of suspicious requests that hit the Web Attack, HTTP Flood, HTTP ACL, Data Risk Control, or Region Blocking Interception rules, in queries/second. The sampling interval is one minute. You can choose the data type \(Average or Peak\) to display or click the legend icon below the graph to clear or display the corresponding record.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297092_en-US.jpg)

    -   **Bandwidth**: This graph displays the inbound and outbound bandwidth, in bit/s. The sampling interval is one minute. You can click the legend icon below the graph to clear or display the corresponding record.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297093_en-US.jpg)

    -   **Abnormal**: This graph displays the number of HTTP error codes, such as 404, 502, 503, 504, 5XX, and No Response. The sampling interval is one minute. Next to the chart, a pie chart is provided showing the proportion of each error code. You can click the legend icon below the graph to clear or display the corresponding record.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297094_en-US.jpg)

    -   **Request source region TOP5** or **Request source IP TOP10**: This bar chart displays the top 5 regions that most requests originate from or the top 10 client IP addresses that send most requests. Next to the bar chart, a world map is provided showing the corresponding IP location record. You can place the pointer over a blue dot to view details.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297095_en-US.jpg)

    -   **Mobile OS distribution** and **PC browser distribution**: These two pie charts display the system distribution of access requests from mobile or PC clients.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297096_en-US.jpg)

    -   **Top 5 URLs Ordered by Response Time**: This bar chart displays the top 5 URLs with the longest response time and their response time in ms.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297097_en-US.jpg)

    -   **Request Counts**: This bar chart displays the top 5 most frequently accessed paths and the corresponding request count.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297098_en-US.jpg)


## View security overview {#section_fbm_z4l_l2b .section}

Follow these steps to view the security overview page:

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  Go to the **Reports** \> **Overview** page and select the region of your WAF instance \(Mainland China or International\).
3.  Go to the Security tab page to view the following security summary information:
    -   **Attack Protection**: These bar charts show statistics for the Web Application Attack, HTTP Flood Attack, and HTTP ACL Policy Event over the last 30 days. You can place the pointer on a record to view details, or click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297099_en-US.jpg) icon to go to the corresponding [Attack protection report](intl.en-US/User Guide/Protection reports/View the attack protection report.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297100_en-US.jpg)

    -   **Risk Warning**: This area lists the new security risks that WAF finds on your site and the latest security risks in your industry. Protection suggestions are also provided. You can click **View reports** to go to the corresponding [Risk warning report](intl.en-US/User Guide/Protection reports/Risk warning report.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297101_en-US.jpg)

    -   **Message**: This area lists WAF protection rule updates for the latest vulnerabilities. You can click **View** to view the corresponding vulnerability announcement.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15505406297102_en-US.jpg)


