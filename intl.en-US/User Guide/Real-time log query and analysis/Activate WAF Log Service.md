# Activate WAF Log Service {#concept_p1p_3mg_qfb .concept}

After purchasing a Web Application Firewall instance, you can activate the real-time log query and analysis service for your websites on the App Management page in the console.

## Scope {#section_ovc_vng_qfb .section}

With WAF Log Service, you can collect multiple log entries in real time from your websites that are protected by WAF. You can also perform real-time log query and analysis and display results in dashboards. WAF Log Service fully meets the business protection needs and operational requirements of your websites. You can select the log storage period and the log storage size as needed when enabling WAF Log Service.

**Note:** At the moment, WAF Log Service is only available to WAF subscription instances \(Pro, Business, or Enterprise edition\).

## Enable WAF Log Service {#section_vmk_ppg_qfb .section}

1.  Log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf).
2.  Choose **App Market** \> **App Management**, and select the region where your WAF instance is located.
3.  Click **Upgrade** in Real-time Log Query and Analysis Service.
4.  On the page that is displayed, enable **Log Service**, select the log storage period and the log storage size, and then click **Buy Now**.

    **Note:** For more information about the billing of WAF Log Service, see [WAF Log Service Billing methods](reseller.en-US/User Guide/Real-time log query and analysis/Billing method.md#).

5.  Return to the WAF console and choose **App Market** \> **App Management**, and then click **Authorize** in Real-time Log Query and Analysis Service.
6.  Click **Agree** to authorize WAF to write log entries to your exclusive logstore.

    WAF Log Service is then enabled and authorized.

7.  Return to the WAF console and choose **App Market** \> **App Management** and then, click **Configure** in Real-time Log Query and Analysis Service.
8.  On the Log Service page, select the domain name of your website that is protected by WAF, and turn on the **Status** switch on the right to enable WAF Log Service.

    Log Service collects all web log recorded by WAF in real time. These log entries can be queried and analyzed in real time.


