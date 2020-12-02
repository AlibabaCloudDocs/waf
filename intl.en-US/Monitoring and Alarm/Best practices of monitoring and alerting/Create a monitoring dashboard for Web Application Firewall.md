# Create a monitoring dashboard for Web Application Firewall

This topic describes how to create and customize real-time monitoring dashboards and add charts to the dashboards for Web Application Firewall \(WAF\) in the Cloud Monitor console. By using custom dashboards and charts, you can view detailed information about how your workloads are protected by WAF in a visualized manner.

Cloud Monitor is a service that monitors Internet applications and Alibaba Cloud resources. It allows you to view monitoring data in custom dashboards. You can aggregate monitoring data of different products and instances running the same type of workloads by using one dashboard.

You can configure dashboards for WAF in the Cloud Monitor console. Cloud Monitor allows you to monitor the following WAF data metrics.

|Metric|Dimension|Unit|Description|Remarks|
|------|---------|----|-----------|-------|
|**4XX\_ratio**|Domain name|%|The percentage of the 4xx HTTP status codes per minute \(405 excluded\).|The value is a decimal number.|
|**5XX\_ratio**|Domain name|%|The percentage of the 5xx HTTP status codes per minute.|The value is a decimal number.|
|**acl\_blocks\_5m**|Domain name|PCS|The number of requests blocked by access control within the last five minutes.|None.|
|**acl\_rate\_5m**|Domain name|%|The percentage of requests blocked by access control within the last five minutes.|The value is a decimal number.|
|**cc\_blocks\_5m**|Domain name|PCS|The number of requests blocked by HTTP flood protection within the last five minutes.|None.|
|**cc\_rate\_5m**|Domain name|%|The percentage of requests blocked by HTTP flood protection within the last five minutes.|The value is a decimal number.|
|**waf\_blocks\_5m**|Domain name|PCS|The number of requests blocked by web intrusion prevention within the last five minutes.|None.|
|**waf\_rate\_5m**|Domain name|%|The percentage of requests blocked by web intrusion prevention within the last five minutes.|The value is a decimal number.|
|**QPS**|Domain name|CPS|QPS|None.|
|**qps\_ratio**|Domain name|%|The growth rate of QPS every minute on the minute.|The value is a percentage.|
|**qps\_ratio\_down**|Domain name|%|The decrease rate of QPS every minute on the minute.|The value is a percentage.|

1.  Log on to the [Cloud Monitor console](https://cloudmonitor.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Dashboard** \> **Custom Dashboard**.

3.  In the Create Dashboard dialog box, specify a name for the dashboard and click **Create**.

    ![Create a view group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5497449951/p66113.png)

    After the dashboard is created, you are redirected to the Dashboards page. You can select a dashboard from the **Dashboards** drop-down list to view or manage the dashboard.

4.  Click **Add View**. On the Add View panel, set the following parameters.

    1.  **Chart Type**: Supported chart types are Line, Area, Table, Heat Map, and Pie Chart.

        For more information, see [t6140.md\#](/intl.en-US/Dashboard/Use dashboards/Add a monitoring chart.md).

    2.  **Select Metrics**: Click the **Dashboards** tab and select **WAF**. Then, select a metric from the **Metrics** drop-down list and select resources from the **Resource** drop-down list.

        -   **Metrics**: Select a metric that you want to monitor. For more information, see [Table 1](#table_eu3_2ri_rrt).
        -   **Resource**: Select a domain name that you want to monitor.

            **Note:** Only the domain names for which data is generated over the last 12 hours are displayed in the resource list.

            ![Select domain names](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9498741851/p74461.png)

            Click **AddMetrics** if you want to add more metrics.

    3.  Click **Save** to create the chart.

    ![Add View](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9498741851/p74462.png)

    You have created the WAF monitoring chart.

5.  To add more charts to the dashboard, repeat Step 4. For more information, see [Add a monitoring chart](/intl.en-US/Dashboard/Use dashboards/Add a monitoring chart.md) and [Manage dashboards](/intl.en-US/Dashboard/Use dashboards/Manage dashboards.md).


