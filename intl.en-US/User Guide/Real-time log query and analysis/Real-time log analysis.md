# Real-time log analysis {#concept_n1p_p4d_2gb .concept}

Integrated with Log Service, WAF provides access logs and attack logs, and allows you to analyze logs in real time.

The real-time log analysis feature in WAF collects and stores access logs in real time and provides the following capabilities based on **Log Service**: log querying, analysis, reporting, alerting, forwarding, and computing. The service makes it easy to search log data so that you can focus on log analysis.

## Target users {#section_qm3_dpd_2gb .section}

-   Large enterprises and institutions that need to meet compliance requirements regarding the use of cloud hosts, networks, and the storage of security logs, such as financial companies and government agencies.
-   Enterprises that have private security operations centers \(SOCs\) and need to collect security logs for centralized operations and management, such as large real estate, e-commence, financial companies, and government agencies.
-   Enterprises that have strong technical capabilities and need to perform in-depth analysis on logs of cloud resources, such as IT, gaming, and financial companies.
-   Small and medium-sized enterprises and institutions that need to meet compliance requirements regarding their business on the cloud or need to generate business reports on a regular basis, such as monthly, quarterly, and annual reports.

## Benefits {#section_mds_fpd_2gb .section}

-   Compliance: Stores the website's access logs for more than six months to help the website meet the compliance requirements.
-   Simple configuration: You can easily configure the service to collect access logs and attack logs on your site.
-   Real-time analysis: Integrated with Log Service, the service supports real-time log analysis and offers a ready-to-use report center. You can easily gain information about the details of attacks, and visits to your site.
-   Real-time alarms: Near real-time monitoring and custom alarms based on specific metrics are available to ensure a timely response to critical service failures.
-   Collaboration: The service can be integrated with real-time computing, cloud storage, visualization, and other data solutions to help you gain valuable insights into your data.

## Prerequisites and limits {#section_mxf_3pd_2gb .section}

To use the real-time analysis feature in WAF, you must meet the following prerequisites:

-   You have activated [Log Service](../../../../reseller.en-US/Quick Start/5-minute quick start.md#).
-   You have activated [WAF Enterprise Edition](../../../../reseller.en-US/Pricing/Subscription/Activate Alibaba Cloud WAF.md#) and enabled the log analysis module.

All log data in WAF is stored in an exclusive logstore that has the following limits:

-   Users cannot use APIs or SDKs to write data to the logstore or change attributes of the logstore, such as the storage period.

    **Note:** The logstore supports common features, including log querying, reporting, alerting, and stream computing.

-   The logstore is free of charge on condition that Log Service is available and your account has no overdue payments.
-   The system reports may be updated at irregular intervals.

## Scenarios {#section_yyw_kpd_2gb .section}

-   Analyze log data to track attacks and identify threats.
-   Monitor Web requests in real time to predict traffic trends.
-   Quickly learn about the efficiency of security operations and obtain timely feedback.
-   Transfer network logs to user-created data centers or computing centers.

