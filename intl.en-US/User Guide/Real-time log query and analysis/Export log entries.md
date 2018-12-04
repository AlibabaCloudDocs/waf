# Export log entries {#concept_pm4_cq3_kfb .concept}

The WAF log query and analysis service enables you to export log query results to a local file.

You can export the log entries on the current page to a CSV file, or export all log entries to a TXT file.

## Procedure {#section_clk_gvk_kfb .section}

1.  Log on to the [Alibaba Cloud Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf) and choose **App Market** \> **App Management**.
2.  Click the log query and analysis service area to open the Log Service page.
3.  On the Raw Logs tab of the Log Service page, click the download button ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41483/154389455021448_en-US.png) on the right.

    **Note:** The download button does not appear if no result is found for a query.

4.  In the Download Log dialog box that appears, select **Download Log in Current Page** or **Download all logs in the CLI console**.
    -   **Download Log in Current Page**: Click **OK** to download the raw log entries on the current page to a CSV file.
    -   **Download all logs in the CLI console**

        1.  For more information about installing the command-line interface \(CLI\), see the [CLI guide](https://aliyun-log-cli.readthedocs.io/en/latest/README_CN.html#安装).
        2.  Go to the [Security Management](https://usercenter.console.aliyun.com/#/manage/ak) page, and find the AccessKey ID and AccessKey Secret of the current user.
        3.  Click **Copy Command** and paste the command into CLI, replace the `AccessID obtained in step 2` and `AccessKey obtained in step 2` with the AccessKey ID and AccessKey Secret of the current user, and then run the command.
        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41483/154389455021457_en-US.png)

        All raw log entries recorded by WAF are automatically downloaded and saved to the **download\_data.txt** file in the directory where the command is run.


