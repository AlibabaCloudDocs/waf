# Overview

WAF integrates Log Service to provide the Log Service of WAF feature.

The feature collects and stores website access logs and attack protection logs in real time. It leverages the capabilities of Log Service, allows you to query and analyze log data, generate reports, and configure alerts, and delivers log data to downstream services for consumption. This way, Log Service for WAF provides an an easy approach to log query and search and allows you to focus more on log analysis.

## Limits

The following table lists the WAF editions that support Log Service for WAF and related limits, such as log storage duration.

|WAF edition|Support for Log Service for WAF|Log storage duration|Modification of log storage duration|Enabling method|
|-----------|-------------------------------|--------------------|------------------------------------|---------------|
|Pro edition \(subscription\)|√|180 days or 360 days. The duration is determined based on the configurations you specify when you enable Log Service for WAF.|×|Select **Log Service** when you buy a subscription instance or upgrade an instance. For more information, see [t40708.md\#section\_iwk\_q33\_b9e](/intl.en-US/Log Management/Log service/Enable Log Service for WAF.md).|
|Business edition \(subscription\)|√|180 days or 360 days. The duration is determined based on the configurations you specify when you enable Log Service for WAF.|√|
|Enterprise edition \(subscription\)|√|180 days or 360 days. The duration is determined based on the configurations you specify when you enable Log Service for WAF.|√|

## Benefits

Log Service for WAF offers the following benefits:

-   Compliance audits: This feature allows you to store website access logs for more than six months to meet classified protection requirements.
-   Flexible configuration: Website access logs and attack protection logs can be collected in real time with simple configuration. You can customize the log storage duration and capacity and select a website for log collection as required. You can also modify an existing report template or customize a report template to meet your business or security requirements.
-   Real-time log analysis: WAF provides the real-time log analysis feature and an out-of-the-box \(OOTB\) report center, and supports data interaction and mining. This allows you to identify and analyze various attacks on your website and access details in seconds.
-   Real-time alerting: You can customize real-time monitoring and alert rules based on specific metrics to respond to exceptions that occur in critical services in a timely manner.
-   Collaboration: This feature collaborates with other data solutions such as real-time computing, cloud storage, and visualization to further explore the value of data.

## Target users

-   Large-scale enterprises and organizations, such as financial entities and government agencies that need to comply with log storage requirements. The logs include host, network, and security logs for various assets in the cloud.
-   Organizations, such as large-scale real-estate, e-commerce, financial entities, and government agencies that have security operations centers \(SOCs\) and require centralized collection and management of security and alert logs.
-   Enterprises with advanced technologies, such as companies in the IT, gaming, or financial industry, which require in-depth analysis on logs collected from various assets in the cloud and automated alert handling.
-   All users who need to track business security events and generate weekly, monthly, and yearly reports, or users who need to meet classified protection requirements \(level 3 or higher\).

## Features

After you enable Log Service for WAF based on powerful features of Alibaba Cloud Log Service, you can analyze website access logs and attack protection logs. You can also display data on visual dashboards and use preset thresholds to configure monitoring and alert rules.

|Feature|Description|
|-------|-----------|
|[Query and analysis](/intl.en-US/Index and query/Overview.md)|You can enter a query and analysis statement to query and analyze collected log data in real time. The query and analysis statement consists of a search clause and an analytics clause, which are separated with a vertical bar \(`|`\).

For example, you can use the following statement to query the number of visits to a domain name:

```
* | select time_series(__time__,'15m','%H:%i','0') as time,COUNT_if(block_action='waf') as "wafmodule",COUNT_if(block_action='acl') as 
"aclmodule",COUNT_if(block_action='tmd') as "httpfloodmodule" GROUP by time order by time
```

For more information about query and analysis statements, see [Common query statements](#section_p7c_pz3_g7e). |
|[Analysis charts](/intl.en-US/Query and visualization/Analysis graph/Overview.md)|A query and analysis statement contains analytics syntax. After the statement is executed, analysis results are displayed in tables by default. You can also choose a line chart, column chart, or pie chart to display the results.|
|[Dashboard](/intl.en-US/Query and visualization/Dashboard/Overview.md)|Log Service for WAF provides dashboards for real-time data analysis. You can save analysis charts to the dashboard.

The full log service of Anti-DDoS Pro provides two default dashboards: access center and operations center.

You can also subscribe to dashboards and sends dashboard data to specific recipients by using emails or DingTalk messages. |
|[Monitoring and alerts](/intl.en-US/Query and visualization/Alarm/Overview.md)|You can configure alert rules based on the charts in a dashboard to monitor the service status in real time.|

## Usage notes

All log data of WAF is stored in a dedicated Logstore. Take note of the following points on the Logstore:

-   You cannot write data into the dedicated Logstore by using API operations or SDKs.

    **Note:** The dedicated Logstore has no limits on queries, statistics, alerts, and streaming consumption.

-   The dedicated Logstore is not billed. However, it runs normally on the condition that Log Service does not have overdue payments.
-   The built-in charts of the dedicated Logstore may be updated.

## Scenarios

-   Trace web attack detection logs and locate the source of security threats.
-   Monitor web requests in real time and view traffic trends.
-   Obtain information about the efficiency of security operations and respond to issues in a timely manner.
-   Generate and deliver security network logs to user-created data centers or compute centers.

## Common query statements

-   Query request blocking types.

    ```
    * | select count(*) as times,host,block_action group by host,block_action order by times desc
    ```

-   Query the QPS data.

    ```
    * | select time_series(__time__,'15m','%H:%i','0') as time,count(*)/900 as QPS group by time order by time
    ```

-   Query attacked domain names

    ```
    * and acl_blocks:1 | select count(*) as times,host group by host order by times desc
    ```

-   Query attacked URLs.

    ```
    * and acl_blocks:1 | select count(*)as times,host,request_path group by host,request_path order by times
    ```

-   Query request details.

    ```
    * | select date_format(date_trunc('second',__time__),'%H:%i:%s') as time,host,request_path,request_method,status,upstream_status,querystring limit 10
    ```

-   Query web attack types.

    ```
    * | SELECT web_attack_type,times,concat(try_cast(round((times*100.0/sum(times) over()),2)as varchar),'%') as pre from (SELECT COUNT(*) as times,web_attack_type
     from log GROUP by host) ORDER by times desc limit 10
    ```


