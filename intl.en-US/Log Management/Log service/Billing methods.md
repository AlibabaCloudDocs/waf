# Billing methods

This topic describes the billing methods of Log Service for WAF. Log Service for WAF is billed based on the storage capacity and the storage duration.

## Overview

Log Service for WAF is available for subscription WAF instances of the Pro or higher edition.

On the WAF buy page, you must set **Access Log Service** to YES. Then, specify **Log Storage Period** and **Log Storage Size**. The price of Log Service for WAF is automatically calculated based on the specifications you choose and the WAF instance you purchase. For more information about how to enable Log Service for WAF, see [Enable Log Service for WAF for a subscription WAF instance](/intl.en-US/Log Management/Log service/Enable Log Service for WAF.md). For more information about the prices of Log Service for WAF at different storage specifications, see [Storage specifications](#section_pvh_41m_qfb).

## Storage specifications

The following table lists the prices of Log Service for WAF at different storage specifications.

|Storage duration|Storage capacity|Recommended scenario|Instance outside mainland China|Instance inside mainland China|
|Monthly subscription fee \(USD\)|Yearly subscription fee \(USD\)|Monthly subscription fee \(USD\)|Yearly subscription fee \(USD\)|
|----------------|----------------|--------------------|-------------------------------|------------------------------|
|--------------------------------|-------------------------------|--------------------------------|-------------------------------|
|180 days|3 TB|Average daily QPS does not exceed 80.|USD 450|USD 5,400|USD 225|USD 2,700|
|5 TB|Average daily QPS does not exceed 120.|USD 750|USD 9,000|USD 375|USD 4,500|
|10 TB|Average daily QPS does not exceed 260.|USD 1,500|USD 18,000|USD 750|USD 9,000|
|20 TB|Average daily QPS does not exceed 500.|USD 3,000|USD 36,000|USD 1,500|USD 18,000|
|50 TB|Average daily QPS does not exceed 1,200.|USD 7,500|USD 90,000|USD 3,000|USD 36,000|
|100 TB|Average daily QPS does not exceed 2,600.|USD 15,000|USD 180,000|USD 7,500|USD 90,000|
|360 days|5 TB|Average daily QPS does not exceed 60.|USD 750|USD 9,000|USD 375|USD 4,500|
|10 TB|Average daily QPS does not exceed 120.|USD 1,500|USD 18,000|USD 750|USD 9,000|
|20 TB|Average daily QPS does not exceed 260.|USD 3,000|USD 36,000|USD 1,500|USD 18,000|
|50 TB|Average daily QPS does not exceed 600.|USD 7,500|USD 90,000|USD 3,000|USD 36,000|
|100 TB|Average daily QPS does not exceed 1,200.|USD 15,000|USD 180,000|USD 7,500|USD 90,000|

**Upgrade of storage capacity**

If the storage capacity that you purchase is exhausted, the system sends you a notification. You can increase the storage capacity at all times.

**Notice:** If you do not increase the storage capacity in this case, WAF stops writing log data to the Logstore in Log Service. Existing log data in the Logstore is retained. This data is not automatically deleted until the storage period elapses. If Log Service for WAF expires and is not renewed within seven days, all log data in the Logstore is automatically deleted.

## Subscription duration

The subscription duration of Log Service for WAF depends on the subscription of the WAF instance.

-   **New purchase**: If you purchase a subscription WAF instance, the price of Log Service for WAF is calculated based on the subscription duration of the WAF instance.
-   **Upgrade**: If you enable Log Service for WAF by upgrading an existing subscription WAF instance, the price of Log Service for WAF is calculated based on the remaining duration of the existing WAF instance. The remaining duration is accurate to minutes.

## Expiration of Log Service for WAF

If your WAF instance expires, Log Service for WAF also expires. If Log Service for WAF expires, it brings the following issues:

-   WAF stops writing log data to the Logstore.
-   Log data is retained for only seven days. If you renew Log Service for WAF within seven days, you can continue to use this feature. Otherwise, all log data is deleted.

