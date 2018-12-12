# Billing method {#concept_rbc_jqf_qfb .concept}

Web Application Firewall \(WAF\) Log Service is billed based on the log storage period and the log storage size of your choice.

WAF Log Service is activated on a subscription basis.

**Note:** To activate WAF Log Service, you must buy a WAF subscription.

In the WAF purchase page, enable Activate Log Service and select the log storage period and the log storage size. Then, the price is automatically calculated based on the **log store specification** of your choice and the **validity** of the WAF instance.

## Log storage specification {#section_pvh_41m_qfb .section}

The detailed pricing for each log storage specification for WAF Log Service is shown in the following table.

|Log storage period|Log storage size|Recommended scenarios|For International region instances|For Mainland China region instances|
|Monthly subscription|Yearly subscription|Monthly subscription|Yearly subscription|
|------------------|----------------|---------------------|----------------------------------|-----------------------------------|
|--------------------|-------------------|--------------------|-------------------|
|180 days|3 TB|Average daily QPS is up to 80.|4,50|5,400|225|2,700|
|5 TB|Average daily QPS is up to 120.|750|9,000|375|4,500|
|10 TB|Average daily QPS is up to 260.|1,500|18,000|750|9,000|
|20 TB|Average daily QPS is up to 500.|3,000|36,000|1,500|18,000|
|50 TB|Average daily QPS is up to 1,200.|7,500|90,000|3,000|36,000|
|100 TB|Average daily QPS is up to 2,600.|15,000|180,000|7,500|90,000|
|360 days|5 TB|Average daily QPS is up to 60.|750|9,000|375|4,500|
|10 TB|Average daily QPS is up to 120.|1,500|18,000|750|9,000|
|20 TB|Average daily QPS is up to 260.|3,000|36,000|1,500|18,000|
|50 TB|Average daily QPS is up to 600.|7,500|90,000|3,000|36,000|
|100 TB|Average daily QPS is up to 1,200.|15,000|180,000|7,500|90,000|

**Upgrade storage capacity**

If you have no log storage left, a notification appears to remind you to expand the storage size. You can expand the log storage size at any time.

**Notice:** If log storage is full, WAF stops writing new log entries to the exclusive logstore in Log Service. A log entry stored in the logstore is deleted based on the specified period. If the WAF Log Service instance expires and you do not renew it within seven days, all log entries in the logstore are deleted.

## Validity {#section_c3w_ncm_qfb .section}

The validity of the WAF Log Service instance is based on your WAF subscription.

-   **Buy**: When you buy a WAF subscription and enable Log Service, the price of Log Service is calculated based on the validity of the subscription.
-   **Upgrade**: When you enable Log Service by upgrading an existing WAF subscription, the price of Log Service is calculated based on the remaining validity of the existing WAF instance. The remaining validity is accurate to minutes.

**Service expiration**

If your WAF instance expires, WAF Log Service expires at the same time.

-   When the service expires, WAF stops writing log entries to the exclusive logstore in Log Service.
-   The log entries recorded by WAF Log Service are retained within seven days after the service expires. If you renew the service within seven days after the service expires, you can continue to use WAF Log Service. Otherwise, all stored WAF log entries are deleted.

