# Billing methods

This topic describes the billing methods of Log Service for WAF. Log Service for WAF is billed based on the storage capacity and storage duration.

## Overview

Log Service for WAF is available for subscription WAF instances of the Pro or higher edition.

On the WAF buy page, you can set **Access Log Service** to YES. Then, specify **Log Storage Period** and **Log Storage Size**. The price is automatically calculated based on the specifications you choose. For more information about how to enable Log Service for WAF, see [t40708.md\#section\_iwk\_q33\_b9e](/intl.en-US/Log Management/Log service/Enable Log Service for WAF.md). For the prices of Log Service for WAF at different specifications, see [Log storage specifications](#section_pvh_41m_qfb).

## Log storage specifications

The following table lists the prices of Log Service for WAF at different log storage specifications.

|Log storage duration|Storage capacity|Recommended scenario|Instance outside mainland China|Instance in mainland China|
|Monthly subscription \(USD\)|Yearly subscription \(USD\)|Monthly subscription \(USD\)|Yearly subscription \(USD\)|
|--------------------|----------------|--------------------|-------------------------------|--------------------------|
|----------------------------|---------------------------|----------------------------|---------------------------|
|180 days|3TB|Average daily QPS is up to 80.|USD 450|USD 5,400|USD 225|USD 2,700|
|5TB|Average daily QPS is up to 120.|USD 750|USD 9,000|USD 375|USD 4,500|
|10TB|Average daily QPS is up to 260.|USD 1,500|USD 18,000|USD 750|USD 9,000|
|20TB|Average daily QPS is up to 500.|USD 3,000|USD 36,000|USD 1,500|USD 18,000|
|50TB|Average daily QPS is up to 1,200.|USD 7,500|USD 90,000|USD 3,000|USD 36,000|
|100TB|Average daily QPS is up to 2,600.|USD 15,000|USD 180,000|USD 7,500|USD 90,000|
|360 days|5TB|Average daily QPS is up to 60.|USD 750|USD 9,000|USD 375|USD 4,500|
|10TB|Average daily QPS is up to 120.|USD 1,500|USD 18,000|USD 750|USD 9,000|
|20TB|Average daily QPS is up to 260.|USD 3,000|USD 36,000|USD 1,500|USD 18,000|
|50TB|Average daily QPS is up to 600.|USD 7,500|USD 90,000|USD 3,000|USD 36,000|
|100TB|Average daily QPS is up to 1,200.|USD 15,000|USD 180,000|USD 7,500|USD 90,000|

**Upgrade of storage capacity**

If the log storage capacity that you purchase is exhausted, the system automatically sends you a notification. You can increase the capacity at any time by upgrading the log storage capacity specifications.

**Notice:** If you do not upgrade the log storage capacity, WAF stops writing new log data to the Logstore in Log Service. Existing log data in the Logstore is retained and is not automatically deleted until the storage period is exceeded. If Log Service for WAF expires and is not renewed within seven days, all log data in the Logstore is automatically deleted.

## Subscription duration

The subscription duration of Log Service for WAF depends on that of the WAF instance.

-   **New purchase**: If you purchase a subscription WAF instance, the price of Log Service for WAF is calculated based on the subscription duration of the WAF instance.
-   **Upgrade**: If you enable Log Service for WAF by upgrading the existing subscription WAF instance, the price of Log Service for WAF is calculated based on the remaining validity of the existing WAF instance. The remaining validity is accurate to minutes.

## Service expiration

If your WAF instance expires, Log Service for WAF also expires.

-   After Log Service for WAF expires, WAF stops writing log data to the Logstore.
-   Log data is retained for seven days after Log Service for WAF expires. If you renew Log Service for WAF within seven days, you can continue to use this feature. Otherwise, all log data is deleted.

