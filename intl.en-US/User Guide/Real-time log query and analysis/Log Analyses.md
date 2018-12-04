# Log Analyses {#concept_a1q_4kq_32b .concept}

The Real-time Log Query and Analysis Service page in the Web Application Firewall \(WAF\) console is integrated with the Log Analyses feature and the Log reports feature. After [enabling the WAF log collection feature](reseller.en-US/User Guide/Real-time log query and analysis/Log collection.md#) for a domain, you can perform real-time query and analysis, view or edit dashboards, and set up monitoring and alarms in the Real-time Log Query and Analysis Service page.

## Procedure {#section_zdf_5c2_j2b .section}

1.  Log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf), and choose **App Market** \> **App Management**.
2.  Click on the Real-time Log Query and Analysis Service area to open the Log Service page.
3.  Select the domain and check that the **Status** switch on the right is turned on.
4.  Click **Log Analyses**.

    The current page is integrated with the Querying and analyzing page. A query statement is automatically inserted. For example, `matched_host: "www.aliyun.com"` is used to query all log entries that is related to the domain in the statement.

5.  Enter a query and analysis statement, select a log time range, and then click **Search & Analysis**.

## More operations {#section_xgc_bsn_qfb .section}

The following operations are available in the Log Analyses page.

-   **Customize query and analysis**

    Log Service provides rich query and analysis syntax for querying log entries in a variety of complex scenarios. For more information, see the [Custom query and analysis](#) in this topic.

-   **View the distribution of log entries by time period**

    Under the query box, you can view the distribution of log entries that are filtered by time period and query statement. A histogram is used to indicate the distribution, where the horizontal axis indicates the time period, and the vertical axis indicates the number of log entries. The total number of the log entries in the query results is also displayed.

    **Note:** You can hold down the left mouse button and drag the histogram to select a shorter period. The `time picker` automatically updates the time period, and the query results are also updated based on the updated time period.

-   **View raw log entries**

    In the **Raw Logs** tab, each log entry is detailed in a single page, which includes the time when the log entry is generated, the content, and the properties in the log entry. You can click **Display Content Column** to configure the display mode \(**Full Line** or **New Line**\) for long strings in the Content column. You can click **Column Settings** to display specific fields, or click the Download Log button to download the query results.

    Additionally, you can click a value or a property name to add a query criterion to the query box. For example, if you click the value `GET` in the `request_method: GET` filed, the query statement in the query box is updated to:

    ```
    <The original query statement> and request_method: GET
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447521315_en-US.png)

-   **View analysis graphs**

    Log Service enables you to display the analysis results in graphs. You can select the graph type as needed in the Graph tab. For more information, see [Analysis graph](reseller.en-US/User Guide/Query and visualization/Analysis graph/Graph description.md#section_pn5_ymv_tdb).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447521319_en-US.png)

-   **Perform quick analysis**

    The Quick Analysis feature in the Raw Logs tab provides you with an one-click interactive experience, which gives you a quick access to the distribution of log entries by a single property within a specified time period. This feature can reduce the time used for indexing key data. For more information, see [Quick analysis](reseller.en-US/User Guide/Index and query/Query/Quick analysis.md#section_lly_xvj_5cb) in the following section.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447521324_en-US.png)


## Customize query and analysis {#section_ncn_mvt_j2b .section}

The log query statement consists of the query \(Search\) and the analysis \(Analytics\). These two parts are divided by a vertical bar \(`|`\):

```
$Search | $Analytics
```

|Type|Description|
|:---|:----------|
|Query \(Search\)|A keyword, a fuzzy string, a numerical value, a range, or other criteria can be used in the query criteria. A combined condition can also be used. If the statement is empty or only contains an asterisk \(`*`\), all log entries are displayed.|
|Analysis \(Analytics\)|Performs computing and statistics to the query results or all log entries.|

**Note:** Both the query part and the analysis part are optional.

-   When the query part is empty, all log entries within the time period are displayed. Then, the query results are used for statistics.
-   When the analysis part is empty, only the query results are returned without statistics.

**Query syntax**

The query syntax of Log Service supports **full-text index** and **field search**. You can enable the New Line display mode, syntax highlighting, and other features in the query box.

-   **Full text index**

    You can enter keywords without specifying properties to perform the query by using the full-text index. You can enter the keyword with double quotation marks \(""\) surrounded to query log entries that contain the keyword. You can also add a space or `and` to separate keywords.

    **Examples**

    -   **Multiple-keywords query**

        The following statements can be used to query all log entries that contain `www.aliyun.com` and `error`.

        `www.aliyun.com error` or `www.aliyun.com and error`.

    -   **Criteria query**

        The following statement can be used to search for all log entries that contain `www.aliyun.com`, `error` or `404`.

        ```
        www.aliyun.com and (error or 404)
        ```

    -   **Prefix query**

        The following statement can be used to query all log entries that contain `www.aliyun.com` and start with `failed_`.

        ```
        www.aliyun.com and failed_*
        ```

        **Note:** An asterisk \(`*`\) can be added as a suffix, but it`` cannot be added as a prefix. For example, the statement cannot be `*_error`.

-   **Field search**

    You can perform a more accurate query based on specified fields.

    The field search supports comparison queries for fields of numeric type. The format is `field name:value` or `field name>=value`. Moreover, you can perform combination queries using `and` or `or`, which can be used in combination with the full text index.

    **Note:** The log entries that record access, operation, and attack on the domain name in WAF Log Service can also be queried by fields. For more information about the meaning, type, format, and other information of the fields, see [Fields in the WAF log entries](reseller.en-US/User Guide/Real-time log query and analysis/Fields in the log entry.md#).

    **Examples**

    -   **Multiple-fields query**

        The following statement can be used to query all log entries that record the CC attack on the `www.aliyun.com` domain and are intercepted by WAF .

        ```
        matched_host: www.aliyun.com and cc_blocks: 1
        ```

        If you want to query all log entries that record access from a specific client whose IP address is `1.2.3.4` to `www.aliyun.com`, and access is blocked by the 404 error, you can use the following statement.

        ```
        real_client_ip: 1.2.3.4 and matched_host: www.aliyun.com and status: 404
        ```

        **Note:** In this example, the `matched_host`, `cc_blocks`, `real_client_ip`, and `status` fields are the fields defined in the WAF log.

    -   **Numeric fields query**

        The following statement can be used to query all log entries where the response time exceeds five seconds.

        ```
        request_time_msec > 5000
        ```

        Range query is also supported. For example, you can query all log entries where the response time exceeds five seconds and is no more than 10 seconds.

        ```
        request_time_msec in (5000 10000]
        ```

        **Note:** The following query statement has the same function.

        ```
        request_time_msec > 5000 and request_time_msec <= 10000
        ```

    -   **Field existence query**

        You can perform a query based on the existence of a field.

        -   The following statement can be used to search for all log entries where the `ua_browser` field exists.

            ```
            ua_browser: *
            ```

        -   The following statement can be used to search for all log entries where the `ua_browser` field does not exist.

            ```
            not ua_browser: *
            ```


For more information about the query syntax that is supported by Log Service, see[Index and query](reseller.en-US/User Guide/Index and query/Overview.md).

**Syntax for analysis**

You can use the SQL/92 syntax for log analysis and statistics.

For more information about the syntax and functions supported by Log Service, see[Syntax description](../../../../reseller.en-US/User Guide/Index and query/Syntax description.md#).

**Note:** 

-   The `from table name` part that follows the SQL standard syntax can be omitted from the analysis statement. In WAF Log Service, `from log` can be omitted.
-   The first 100 results are returned by default, and you can modify the number of results that are returned by using the [LIMIT syntax](../../../../reseller.en-US/User Guide/Index and query/Analysis grammar/LIMIT syntax.md#).

## Examples of query and analysis {#section_syk_r14_qfb .section}

**Time-based log query and analysis**

Each WAF log entry has a `time` field, which is used to represent the time when the log entry is generated. The format of the value in this field is `<year>-<month>-<day>T<hour>:<minute>:<second>+<time zone>`. For example, `2018-05-31T20:11:58+08:00` is 20:11:58 `UTC+8` \(Beijing Time\), May 15, 2018.

In addition, each log entry has a built-in field `__time__`, which is also used to indicate the time when the log entry is generated. This field is used for calculation when performing statistics. The format of this field is a [Unix timestamp](https://en.wikipedia.org/wiki/Unix_time), and the value of this field indicates the number of seconds that have elapsed since 00:00:00 Coordinated Universal Time \(UTC\), January 1, 1970. Therefore, if you want to display a calculated result, you must convert the format first.

-   **Select and display the time**

    You can query the log based on the `time` field. For example, you can search for the last 10 log entries that record the CC attacks on `www.aliyun.com` and are intercepted by WAF. Then, you can display the time field, the source IP field, and the client field.

    ```
    matched_host: www.aliyun.com and cc_blocks: 1 
    | select time, real_client_ip, http_user_agent
        order by time desc
        limit 10
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447521335_en-US.png)

-   **Calculate using time.**

    You can use the `__time__` field to calculate using time. For example, you can calculate the number of days that have elapsed since the domain suffered a CC attack.

    ```
    matched_host: www.aliyun.com and cc_blocks: 1 
    round((to_unixtime(now()) - __time__)/86400, 1) as "days_passed", real_client_ip, http_user_agent
          order by time desc
          limit 10
    ```

    **Note:** In this example, `round((to_unixtime(now()) - __time__)/86400, 1)` is used to calculate the number of days that have elapsed since the domain had a CC attack. First, use `now()` to get the current time, and convert the current time into a Unix timestamp using `to_unixtime`. Then, subtract the converted time with the value of the built-in field `__time__` to get the number of seconds that have elapsed. Finally, divide it by `86400` \(the total number of seconds in a day\) and apply the `round(data, 1)` function to keep one decimal place. The result is the number of days that have elapsed since each attack log entry is generated.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447521341_en-US.png)

-   **Perform group statistics based on a specific time**

    You can query the log based on the trend of CC attacks on the domain within a specified time period.

    ```
    matched_host: www.aliyun.com and cc_blocks: 1 
    | select date_trunc('day', __time__) as dt, count(1) as PV 
          group by dt 
    	  order by dt
    ```

    **Note:** In this example, the built-in field `__time__` is used by the `date_trunc('day', ..)` function to align the time of the entries by day. Each log entry is assigned to a group based on the day when the log entry is generated. The total number of log entries in each group is counted using count\(1\). Then, these entries are ordered by the group. You can use other values for the first parameter of the `date_trunc` function to group the log entries based on other time units, such as `second`, `minute`, `hour`, `week`, `month`, and `year`. For more information about this function, see [Date and time functions](../../../../reseller.en-US/User Guide/Index and query/Analysis grammar/Date and time functions.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447521342_en-US.png)

    **Note:** You can also display the results with a line chart.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447521343_en-US.png)

-   **Perform group statistics based on time.**

    If you want to analyze the log based on time using more flexible groupings, complex calculations are required. For example, you can query the log based on the trend of CC attacks on the domain within every five minutes.

    ```
    matched_host: www.aliyun.com and cc_blocks: 1 
    | select from_unixtime(__time__ - __time__% 300) as dt, 
             count(1) as PV 
          group by dt 
    	  order by dt 
    	  limit 1000
    ```

    **Note:** In this example, the built-in field is used for aligning the time by using the formula `__time__ - __time__% 300`, and the `from_unixtime` function converts the format of the result. Then, each entry is assigned to a group that indicates a time period of five minutes \(300 seconds\), and the total number of log entries in each group is counted using count\(1\). Finally, the query results are ordered by group and the first 1,000 results are returned, which include the log entries that are generated within 83 hours before the specified time period.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447521344_en-US.png)

    **Note:** You can also display the results with a line graph.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447521345_en-US.png)


The `date_parse` and `date_format` functions are used to convert the time format. For more information about the functions that can be used to parse the time field, see [Date and time functions](../../../../reseller.en-US/User Guide/Index and query/Analysis grammar/Date and time functions.md#).

**Client IP address-based log query and analysis**

The WAF log contains the field `real_client_ip`, which reflects the real client IP address. In cases where the user accesses your website through a proxy server, or the IP address in the request header is wrong, you cannot get the real IP address of the user. However, the `remote_addr` field forms a direct connection to the client, which can be used to get the real IP address.

-   **Classify attackers by country**

    You can query the log based on the distribution of CC attackers by country.

    ```
    matched_host: www.aliyun.com and cc_blocks: 1 
    | SELECT ip_to_country(if(real_client_ip='-', remote_addr, real_client_ip)) as country, 
             count(1) as "number of attacks" 
    		 group by country
    ```

    **Note:** In this example, the function `if(condition, option1, option2)` returns the real client IP address. If `real_client_ip` is `-`, the function returns the value of `remote_addr`. Otherwise, the function returns `real_client_ip`. Then, use the `ip_to_country` to get the country information from the IP address of the client.

    ![](images/21346_en-US.png)

    **Note:** You can also display the results with a world map.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447621347_en-US.png)

-   **Distribution of visitors by province**

    If you want to get the distribution of visitors by province, you can use the `ip_to_province` function to get the province information from the IP addresses.

    ```
    matched_host: www.aliyun.com and cc_blocks: 1 
    | SELECT ip_to_province(if(real_client_ip='-', remote_addr, real_client_ip)) as province, 
             count (1) as "number of attacks" 
    		 group by province
    ```

    **Note:** In this example, the `ip_to_province` function is used to get the country information from the real IP address of the client. If the IP address is not in the Mainland of China, the function returns the province or state of the IP address in the country field. However, if you choose to display the results with a map of China, IP addresses that are not in the Mainland of China are not displayed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447621348_en-US.png)

    **Note:** You can also display the results with a map of China.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41248/154389447621349_en-US.png)

-   **Heat map that indicates the distribution of attackers**

    You can use the `ip_to_geo` function to get the geographic information \(the latitude and the longitude\) from the real IP addresses of the clients. This information can be used to generate a heat map to indicate the density of attacks.

    ```
    matched_host: www.aliyun.com and cc_blocks: 1 
    | SELECT ip_to_geo(if(real_client_ip='-', remote_addr, real_client_ip)) as geo, 
             count (1) as "number of attacks" 
    		 group by geo
    		 limit 10000
    ```

    **Note:** In this example, the `ip_to_geo` function is use to get the latitude and the longitude from the real IP addresses of the clients. The first 10,000 results are returned.

    Select Amap and click **Show Heat Map**.


The `ip_to_provider` function can be used to get the IP provider name, and the `ip_to_domain` function can be used to determine whether the IP is a public IP or a private IP. For more information about the functions that can be used to resolve IP addresses, see [IP functions](../../../../reseller.en-US/User Guide/Index and query/Analysis grammar/IP functions.md#).

