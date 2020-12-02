# Step 3: Configure log alerts

After you create a log analysis dashboard, you can configure log alerts on the dashboard. You must associate the alerts with existing log charts and set the alert trigger conditions based on the parameters in the charts. You can customize an alert message template.

A log analysis dashboard is created. For more information, see [Step 1: Create a WAF log analysis dashboard](/intl.en-US/Monitoring and Alarm/Best practices for configuring alerts in Log Service/Step 1: create a WAF log analysis dashboard.md).

The practices provide 13 default alert configuration examples. For more information, see [WAF log charts and alert configuration examples](/intl.en-US/Monitoring and Alarm/Best practices for configuring alerts in Log Service/WAF log charts and alert configuration examples.md).

We recommend that you learn how to configure charts before you create a chart based on the examples. In addition, you can configure alerts and notification methods during chart creation. For more information, see [Step 2: Configure log charts](/intl.en-US/Monitoring and Alarm/Best practices for configuring alerts in Log Service/Step 2: configure log charts.md).

1.  Enter the customized WAF log analysis dashboard.

    For more information, see [Step 1: Create a WAF log analysis dashboard](/intl.en-US/Monitoring and Alarm/Best practices for configuring alerts in Log Service/Step 1: create a WAF log analysis dashboard.md).

2.  In the upper-right corner of the dashboard, choose **Alerts** \> **Create**.

    ![Create an alert](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7152023851/p76410.png)

3.  In the Create Alert pane, set the parameters in **Alert Configuration**, and click **Next**.

    ![Create an alert](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8152023851/p76411.png)

    |Parameter|Description|
    |---------|-----------|
    |**Alert Name**|The name of the alert. The name must be 1 to 64 characters in length.|
    |**Associated Chart**|The charts with which an alert is associated. The **Search Period** parameter specifies the time range of log data that WAF reads when you query data. You can select a relative time or a time frame. For example, if you set **Search Period** to 15 minutes \(relative\) and start the query at 14:30:06, WAF reads the log data that was written from 14:15:06 to 14:30:06. If you set **Search Period** to 15 minutes \(time frame\) and start the query at 14:30:06, WAF reads the log data that was written from 14:15:00 to 14:30:00.

To associate the alert with more than one chart, click **Add** and configure the new charts. You can add up to three charts. The number before the chart name is the sequence number of the chart in alert configuration. You can use the sequence number to associate a chart with a conditional expression in the trigger condition. |
    |**Frequency**|The time interval at which the server checks log data according to the alert configuration.**Note:** Currently, the server samples and checks only the first 100 data entries each time the specified time interval arrives. |
    |**Trigger Condition**|The conditional expression that determines whether the alert is triggered. When the condition is met, the system sends an alert notification based on the specified **Frequency** and **Notification Interval**. By default, the charts are numbered from 0. In a trigger condition, you can use `$0` to indicate the first chart. For example, you can set a trigger condition to `$0.domainnum>=10`, and this indicates that an alert is triggered if the `domainnum` parameter in the first chart is greater than or equal to 10.

If two conditions are jointed with two consecutive ampersands \(`&&`\), both the conditions must be met to trigger the alert. If two conditions are jointed with two consecutive vertical bars \(`||`\), either of the condition can trigger the alert.

**Note:** For more syntaxes of conditional expressions, see [Syntax of trigger conditions in alert rules](/intl.en-US/Query and visualization/Alarm/Relevant syntax and fields for reference/Syntax of trigger conditions in alert rules.md). |
    |**Advanced**|
    |**Notification Trigger Threshold**|The threshold for sending an alert notification based on the specified notification interval when the cumulative number of times that the trigger condition is met exceeds this threshold. If the trigger condition is not met, the overall count does not change.The default value of Notification Trigger Threshold is 1. That is, each time the specified trigger condition is met, the server checks whether the specified notification interval arrives.

You can also specify this parameter to enable the server to send an alert notification after the trigger condition is met multiple times. For example, if you set this parameter to 100, the server checks whether the specified notification interval arrives only after the trigger condition is met 100 times. If the specified notification trigger threshold is reached and the specified notification interval arrives, the server sends an alert notification. Then, the overall count is reset. If the server fails to check log data due to exceptions such as a network failure, the overall count does not change. |
    |**Notification Interval**|The time interval at which the server sends an alert notification.If the trigger condition is met several times that exceed the specified notification trigger threshold and the specified notification interval arrives, the server sends an alert notification. If you set this parameter to 5 minutes, you can receive up to one alert notification every 5 minutes for the alert. The default value is No Interval.

**Note:** By setting Notification Trigger Threshold and Notification Interval, you can control the number of alert notifications that you receive. |

    **Note:** After you specify **Notification Trigger Threshold**, **Notification Interval**, and **Frequency**, the system checks whether the trigger conditions are met at the specified frequency and sends notifications if **Notification Trigger Threshold** is exceeded within a **Notification Interval**.

4.  In the Create Alert pane, complete the settings for **Notifications**, and click **Submit**.

    ![Note](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8152023851/p76420.png)

    Multiple common alert notification methods are supported, such as **SMS**, **Voice**, **Email**, and **WebHook-DingTalk Bot**. You must select a notification method on the right of **Notifications** and complete the configuration. You can select and configure multiple notification methods.

    -   SMS: Set **Phone Number** to receive alerts and the **Content** of the notification. You can specify variables to be included in the notification. Click **View all variables** to view the description of each variable.

        ![SMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8152023851/p76413.png)

    -   Voice: Set **Phone Number** to receive alerts and the **Content** of the notification.

        ![Voice](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8152023851/p76414.png)

    -   Email: Set **Recipients** email addresses, **Subject**, and **Content**.

        ![Email](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8152023851/p76415.png)

    -   WebHook-DingTalk Bot: Set **Request URL** to the webhook URL of the DingTalk bot to receive alerts, and specify **Content**.

        ![WebHook-DingTalk Bot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9152023851/p76416.png)

5.  Repeat Steps 2 to 4 to create and configure more alerts.


