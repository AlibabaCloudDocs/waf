# Business overview {#task_wnz_t4l_l2b .task}

The Overview page of the Web Application Firewall \(WAF\) console displays the overall threat information of all your websites protected by WAF. The information includes an overview of attack protection and threats and detailed analysis of your business, attacks, and threats.

Take the following steps to view the business, attacks, and threats on all websites protected by WAF:

1.  Log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf).
2.  Choose **Reports** \> **Overview**. In the upper-left corner, select the region of your WAF instance. The options include Mainland China and International.
3.  Select one or all domain names and a time period. You can select real-time, 1 day, 7 days, 30 days, or customize a time period. 

    **Note:** The overall business information for the last 30 days is available. You can customize a time period within the last 30 days.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15616850687091_en-US.jpg)

4.  On the Overview page, you can view the business, attack protection, and threat information of the specified websites in the area as shown in the following figure: 
    -   **Overall information**: Displays the total number of requests received by the domain name, the number of Web attacks, the number of HTTP flood attacks, the number of requests blocked by access control, and the number of requests blocked by region blocking policies. You can click the unfold button below to view the trend of the data within the specified time period.

        **Note:** If you select all domains, after you click the unfold button, the top five domains of each indicator and the corresponding data are displayed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/156168506849556_en-US.png)

    -   **Attacks and events**: WAF classifies the blocked attacks into events and displays the events below the domain drop-down list. You can quickly learn about the attacks and threats on your websites.

        **Note:** If you select all domains, the numbers of attacks and events on all domains are provided. You can click a domain to view the corresponding events.

        WAF classifies the attacks into events based on the attack type, severity level, frequency, and time. The event types include invalid requests, HTTP flood attacks, Web attacks, requests blocked by precise access control, requests blocked by region blocking policies, and requests blocked by continuous attack protection.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/156168506849557_en-US.png)

        You can click an event to view details and the related data of the event type. For example, in the HTTP flood attacks area, you can view the top five source IP addresses, the top five UserAgents, the top five referrers, the top five requested URLs, and the number of blocked attacks on each of these URLs. You can also refer to the protection suggestions provided below the data.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/156168506849558_en-US.png)

    -   **Business trend graph**: This graph shows how the number of requests, queries per second \(QPS\), bandwidth consumed by the requests, and status code vary with time within the specified time period. The data at each minute is provided.

        **Note:** Click the icons below the graph to hide or show the corresponding records.

        -   **Requests**: This tab shows the trend of the total number of requests, the number of blocked Web attacks, the number of blocked HTTP flood attacks, the number of requests blocked by precise access control, and the number of requests blocked by region blocking policies.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15616850687092_en-US.jpg)

        -   **QPS**: This tab shows the total requests per second, the blocked Web attacks per second, the blocked HTTP flood attacks per second, the requests blocked by precise access control per second, and the requests blocked by region blocking policies per second.

            **Note:** Click **Average** or **Peak** in the upper-right corner of the graph to switch between the average QPS and peak QPS.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/156168506849561_en-US.png)

        -   **Bandwidth**: This graph shows the inbound bandwidth and the outbound bandwidth in bit/s.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15616850687093_en-US.jpg)

        -   **Status code**: Displays the trends of HTTP response status codes such as 5XX, 405, 499, 302, and 444.

            **Note:** In the upper-right corner, click **WAF to Client** to view the status codes from the WAF instance to the client, or click **Origin Server to WAF** to view the status codes from the origin server to the WAF instance.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15616850687094_en-US.jpg)

    -   **Event distribution**: In the **Attack Distribution** area, the attack events distribution is displayed.

        **Note:** You can click an event in the graph to view the event details and related data of the event type.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15616850687095_en-US.jpg)

    -   **Browser distribution**: On the **Browser Distribution** tab page, a pie chart shows the distribution of browsers used by the request sources.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15616850687096_en-US.jpg)

    -   **Top UserAgents**: On the **UA Top** tab page, the most frequently used UserAgents and the numbers of corresponding requests are listed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15616850687097_en-US.jpg)

    -   **Most frequently requested URLs**: On the **URL Requests** tab page, the most frequently requested URLs and the number of corresponding requests are listed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/15616850697098_en-US.jpg)

    -   **Top source IP addresses**: On the **Top IP** tab page, the source IP addresses with the most requests and the number of corresponding requests are listed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15572/156168506949563_en-US.png)


