# Step 1: Create a WAF log analysis dashboard

After you perform log query and analysis by using the Log Service for WAF feature, you can create a dashboard based on the SQL statement. By default, the dashboard contains the chart that is generated based on the SQL statement.

-   Your domain name is added to WAF for protection. For more information, see [Change a DNS record](/intl.en-US/Website Access/Website access with CNAME/Change a DNS record.md).
-   The Log Service for WAF feature is enabled for your domain name. For more information, see [Enable Log Service for WAF](/intl.en-US/Log Management/Log service/Enable Log Service for WAF.md).

1.  Log on to the [WAF console](https://yundun.console.aliyun.com/?p=waf).

2.  Go to the advanced management page of Log Service for WAF.

    1.  In the top navigation bar, select **Mainland China** or **International**.

    2.  In the left-side navigation pane, choose **Log Management** \> **Log Service**.

    3.  In the upper-right corner of the Log Service page, click **Advanced Settings**.

    4.  In the dialog box that appears, click **OK**.

3.  In the project list, find the log project that you want to manage, and click the project name.

4.  Enter an SQL statement and click **Search & Analyze**.

5.  After the query is complete, click **Add to New Dashboard** on the **Graph** tab.

    ![Add a chart to a new dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1052023851/p76397.png)

6.  In the Add to New Dashboard dialog box, configure the following parameters and click **OK**.

    ![Add to New Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1052023851/p76398.png)

    |Parameter|Description|
    |---------|-----------|
    |**Operation**|Select **Create Dashboard**.|
    |**Dashboard Name**|Enter a dashboard name.|
    |**Chart Name**|Enter a name for the chart generated based on the SQL statements.|


After the dashboard is created, you are redirected to the new dashboard. By default, the dashboard contains the chart that is generated based on the SQL statement entered in Step 4. You can edit the chart or create more charts on the dashboard.

[Step 2: Configure log charts](/intl.en-US/Monitoring and Alarm/Best practices for configuring alerts in Log Service/Step 2: Configure log charts.md)

