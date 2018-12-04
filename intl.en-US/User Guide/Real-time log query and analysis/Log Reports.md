# Log Reports {#reference_emx_xkq_32b .reference}

The Log Reports page is integrated with the Dashboard page of Log Service. On this page, you can view default dashboards. You can filter business and security data about your website by modifying the time range or adding filters.

## View reports {#section_mvp_4qn_j2b .section}

1.  Log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf), and choose **App Market** \> **App Management**.
2.  Click the Real-time Log Query and Analysis Service area to open the Log Service page.
3.  \[DO NOT TRANSLATE\]****
4.  Select a domain and check that the **Status** switch on the right is turned on.
5.  Click **Log Reports**.

    The page that appears is integrated with the Dashboard page of Log Service. A **filter** is automatically added to display all log entries that are recorded for the domain you selected. In this example, the filter is `matched_host: www.aliyun.com`.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41421/154389449221411_en-US.png)


After you enable the WAF log collection feature, Log Service creates three dashboards by default: the Operation Center, Access Center, and Security Center.

**Note:** For more information about the default dashboards, see [Default dashboards](#).

|Dashboard|Description|
|:--------|:----------|
|Operation Center|Displays operation details such as the proportion of valid requests and the statistics of attacks, traffic details such as the peak of both inbound and outbound throughput and the number of requests received, operation trends, attack overview, and other information.|
|Access Center|Displays basic access details such as the number of page views \(PV\) and the number of unique visitors \(UV\), the access trend, the distribution of visitors, and other information.|
|Security Center|Displays basic index information of attacks, attack types, attack trend, attacker distribution, and other information.|

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41421/154389449221419_en-US.png)

**Note:** Dashboards displays various reports using the layout that is predefined in WAF Log Service. The following table describes the graph types supported for reports. For more information about the graph types supported by Log Service, see [Graph description](../../../../reseller.en-US/User Guide/Query and visualization/Analysis graph/Graph description.md#).

|Type|Description|
|:---|:----------|
|Number|Graphs of this type display important metrics, such as the valid request ratio and the peak of attacks.|
|Line chart and area chart|Graphs of these types display the trend of important metrics within a specified time period, such as the trend of inbound throughput and the trend of attack interceptions.|
|Map|Graphs of this type display the geographical distribution of visitors and attackers, for example, by country. Heat maps are also supported to illustrate the distribution of attackers.|
|Pie chart|Graphs of this type display a distribution, such as the distribution of attackers and the distribution of client types.|
|Table|Graphs of this type display a table that contains information, such as information of attackers.|
|Map|Graphs of this type display the geographical distribution of data.|

## Time selector {#section_uf1_hwn_j2b .section}

The data in all graphs on the dashboard page are generated based on different time ranges. If you want to unify the time ranges, configure the **time selector**.

1.  On the **Log Reports** page, click **Please Select** and
2.  select a time range in the pane that appears. You can select a relative time, a time frame, or customize a time range.

**Note:** 

-   After you set a time range, the time range is applied to all reports.
-   If you set a time range, a temporary view is generated on the current page. When you view reports next time, the default time range is used.
-   To change the time range for a single report in the dashboard, click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41421/154389449221432_en-US.png) in the upper-right corner.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41421/154389449221420_en-US.png)

## Data drilldown {#section_vlj_ttv_qfb .section}

The drilldown operation is enabled for some graphs on the dashboard page, which provides you a quick access to the detailed data.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41421/154389449221475_en-US.png)

The drilldown operation is available for graphs marked with a ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41421/154389449221474_en-US.png) icon in the upper-right corner. You can click a number with an underline to view the detailed underlying data. For example, to quickly find the domains that are attacked and the number of attacks, click the number in the **Attacked Hosts** graph of the **Security Center** report.

**Note:** Alternatively, switch to the **Raw Log** tab to find the relevant log entries.

## Description of values in default dashboards {#section_qyt_prn_j2b .section}

-   **Operation Center**: Displays operation details such as the proportion of valid requests and the statistics of attacks, traffic details such as the peak of both inbound and outbound throughput and the number of requests received, the operation trend, the attack overview, and other information.

    |Graph|Type|Default time range|Description|Example|
    |:----|:---|:-----------------|:----------|:------|
    |Valid Request Ratio|Single value|Today \(time frame\)|Displays the percentage of valid requests in all requests. A valid request is a request that is neither an attack nor a request that is blocked by a 400 error.|95%|
    |Valid Request Traffic Ratio|Single value|Today \(time frame\)|Displays the percentage of the traffic generated by valid requests in the traffic generated by all requests.|95%|
    |Peak Attack Size|Single value|Today \(time frame\)|Displays the peak of attack traffic, which is measured in Bps.|100 B/s|
    |Attack Traffic|Single value|1 hour \(relative\)|Displays the total attack traffic, which is measured in B.|30 B|
    |Attack Count|Single value|1 hour \(relative\)|The total number of attacks.|100|
    |Peak Network In|Single value|Today \(time frame\)|Displays the peak inbound throughput, which is measured in KB/s.|100 KB/s|
    |Peak Network Out|Single value|Today \(time frame\)|Displays the peak outbound throughput, which is measured in KB/s.|100 KB/s|
    |Received Requests|Single value|1 hour \(relative\)|Displays the total number of valid requests.|7,800|
    |Received traffic|Single value|1 hour \(relative\)|Displays the total inbound traffic that is generated by valid requests, which is measured in MB.|1.4 MB|
    |Traffic Out|Single value|1 hour \(relative\)|Displays the total outbound traffic that is generated by valid requests, which is measured in MB.|3.8 MB|
    |Network Traffic In And Attack|Area chart|Today \(time frame\)|Displays the trends of throughput generated by valid requests and attacks, which is measured in Kbit/s.|-|
    |Request And Interception|Line chart|Today \(time frame\)|Displays the trends of valid requests and requests that are intercepted, which is measure in Kbit/h.|-|
    |Access Status Distribution|Flow chart|Today \(time frame\)|Displays the trends of requests with different status codes \(404, 304, 200, and other status codes\), which is measured in Kbit/h.|-|
    |Attack Source \(World\)|World map|1 hour \(relative\)|Displays the distribution of attackers by country.|-|
    |Attack Source \(China\)|Map of China|1 Hour \(Relative\)|Displays the distribution of attackers in China by province.|-|
    |Attack Type|Pie chart|1 hour \(relative\)|Displays the distribution of attacks by attack type.|-|
    |Attacked Hosts|Tree map|1 hour \(relative\)|Displays the domains that are attacked and the number of attacks.|-|

-   **Access center**: Displays basic access details such as the number of PV and the number of UV, the access trend, the distribution of visitors, and other information.

    |Graph|Type|Default time range|Description|Example|
    |:----|:---|:-----------------|:----------|:------|
    |PV|Single value|1 hour \(relative\)|Displays the total number of PV.|100,000|
    |UV|Single value|1 hour \(relative\)|Displays the total number of UV.|100|
    |Traffic In|Single value|1 hour \(relative\)|Displays the total inbound traffic, which is measured in MB.|300 MB|
    |Peak Network In Traffic|Single value|Today \(time frame\)|Displays the peak inbound throughput, which is measured in KB/s.|0.5 KB/s|
    |Peak Network Out Traffic|Single value|Today \(time frame\)|Displays the peak outbound throughput, which is measured in KB/s.|1.3 KB/s|
    |Traffic Network Trend|Area chart|Today \(time frame\)|Displays the trends of inbound and outbound throughput, which are measured in KB/s.|-|
    |PV/UV Trends|Line chart|Today \(time frame\)|Displays the trends of PV and UV, which is measured in Kbit/h.|-|
    |Access Status Distribution|Flow chart|Today \(time frame\)|Displays the trends of requests with different status codes \(404, 304, 200, and other status code\), which is measured in Kbit/h.|-|
    |Access Source|World map|1 hour \(relative\)|Displays the distribution of attackers by country.|-|
    |Traffic In Source \(World\)|World map|1 hour \(relative\)|Displays the distribution \(by country\) of inbound traffic from requests.|-|
    |Traffic In Source \(China\)|Map of China|1 hour \(relative\)|Displays the distribution \(by province\) of inbound traffic from requests in China.|-|
    |Access Heatmap|Amap|1 hour \(relative\)|Displays the heat map that indicates the source distribution of requests by geographical position.|-|
    |Network Provider Source|Pie chart|1 hour \(relative\)|Displays the source distribution of requests by Internet service provider that provides network for the source, such as China Telecom, China Unicom, China Mobile, and universities.|-|
    |Referer|Table|1 hour \(relative\)|Displays the first 100 referer URLs which the hosts are most often redirected from, and displays the information of hosts and redirection frequency.|-|
    |Mobile Client Distribution|Pie chart|1 hour \(relative\)|Displays the distribution of requests from mobile clients, by client type.|-|
    |PC Client Distribution|Pie chart|1 hour \(relative\)|Displays the distribution of requests from PC clients, by client type.|-|
    |Request Content Type Distribution|Pie chart|1 hour \(relative\)|Displays the distribution of request sources by content type, such as HTML, form, JSON, and streaming data.|-|
    |Accessed Sites|Tree map|1 Hour \(Relative\)|Displays the addresses of 30 domains that are visited most.|-|
    |Top Clients|Table|1 hour \(relative\)|Displays the information of 100 clients that visit your domains most. The information includes the client IP address, the region and city, network information, the request method, inbound traffic, the number of incorrect accesses, the number of attacks, and other information.|-|
    |URL With Slowest Response|Table|1 hour \(relative\)|Displays the information of 100 URLs that have the longest response times. The information includes the website address, the URL, the average response time, the number of accesses, and other information.|-|

-   **Security Center**: Displays basic details of attacks, attack types, the attack trend, the distribution of attackers, and other information.

    |Chart|Type|Default time range|Description|Example|
    |:----|:---|:-----------------|:----------|:------|
    |Peak Attack Size|Single value|1 hour \(relative\)|Displays the peak of the throughput when your website is suffering attacks, which is measured in Bps.|100 B/s|
    |Attacked Hosts|Single value|Today \(time frame\)|Displays the number of domains that are attacked.|3|
    |Source Country Of Attack|Single value|Today \(time frame\)|Displays the number of countries that are attack sources.|2|
    |Attack Traffic|Single value|1 hour \(relative\)|Displays the total amount of traffic that is generated by attacks, which is measured in B.|1 B|
    |Attacker UV|Single value|1 hour \(relative\)|Displays the number of unique clients that are attack sources.|40|
    |Attack type distribution|Flow chart|Today \(time frame\)|Displays the distribution of attacks by attack type.|-|
    |Intercepted Attack|Single value|1 hour \(relative\)|Displays the number of attacks that are intercepted by WAF.|100|
    |CC Attack Interception|Single value|1 hour \(relative\)|Displays the number of CC attacks that are intercepted by WAF.|10|
    |Web Attack Interception|Single value|1 hour \(relative\)|Displays the number of Web application attacks that are intercepted by WAF.|80|
    |Access Control Event|Single value|1 hour \(relative\)|Displays the number of requests that are intercepted by the HTTP ACL policies of WAF.|10|
    |CC Attack \(World\)|World map|1 hour \(relative\)|Displays the distribution of CC attackers by country.|-|
    |CC Attack \(China\)|China map|1 hour \(relative\)|Displays the distribution of CC attackers by province in China.|-|
    |Web Attack \(World\)|World map|1 Hour \(Relative\)|Displays the distribution of Web application attacks by country.|-|
    |Web Attack \(China\)|Map of China|1 hour \(relative\)|Displays the distribution of Web application attacks by province in China.|-|
    |Access Control Attack \(World\)|World Map|1 hour \(relative\)|Displays the distribution by country of requests that are intercepted by the HTTP ACL policies of WAF.|-|
    |Access Control Attack \(China\)|Map of China|1 Hour \(Relative\)|Displays the distribution by province in China of requests that are intercepted by the HTTP ACL policy of WAF.|-|
    |Attacked Hosts|Tree map|1 hour \(relative\)|Displays the websites that are attacked most.|-|
    |CC Attack Strategy Distribution|Pie chart|1 hour \(relative\)|Displays the distribution of security policies being activated for CC attacks.|-|
    |Web Attack Type Distribution|Pie chart|1 hour \(relative\)|Displays the distribution of Web attacks by attack type.|-|
    |Top Attackers|Table|1 hour \(relative\)|Displays IP addresses, provinces, and network providers of the first 100 clients that launch the recent attacks, and displays the number of attacks and the amount of traffic generated by these attacks.|-|
    |Attacker Referer|Table|1 Hour \(Relative\)|Displays the information in referers of attack requests, which includes referer URLs, referer hosts, and the number of attacks.|-|


