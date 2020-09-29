# Intelligent load balancing

Web Application Firewall \(WAF\) provides intelligent load balancing. By leveraging the intelligent multi-node access technology, WAF ensures that access requests to your website are automatically scheduled among multiple nodes or lines to achieve disaster recovery. This ensures high service availability and low-latency access.

**Note:** Only subscription WAF instances support intelligent load balancing. Instances deployed in mainland China must be of the Pro edition or higher. Instances deployed outside mainland China must be of the Business edition or higher.

Intelligent load balancing is best suited to the following services to achieve high availability and low-latency access:

-   Active geo-redundancy services: Multiple nodes are deployed on the cloud or in on-premises data centers deployed across regions. These nodes provide services simultaneously and work as backups for each other to achieve disaster recovery.
-   Co-location multi-active services: Multiple nodes are deployed on the cloud or in on-premises data centers deployed in the same region. These nodes provide services simultaneously and work as backups for each other to achieve disaster recovery.
-   Co-location single-active services: A single node is deployed on the cloud or in an on-premises data center in the same region to provide services.

    **Note:** Co-location single-active services do not have automatic disaster recovery capabilities. However, you can enable intelligent load balancing to achieve high service availability, automatic disaster recovery, and low-latency access.


## How intelligent load balancing works

After intelligent load balancing is enabled, a WAF instance has a minimum of three protection nodes that are deployed in different regions to achieve automatic disaster recovery. In addition, the intelligent DNS resolution feature and the upgraded back-to-origin algorithm are used to achieve the lowest latency when traffic is forwarded to origin servers.

**Note:**

-   After intelligent load balancing is enabled in mainland China, a WAF instance has three protection nodes, with one node deployed in the China \(Beijing\) region, one in the China \(Hangzhou\) region, and one in the China \(Shenzhen\) region.
-   After intelligent load balancing is enabled outside mainland China, a WAF instance has eight protection nodes that are deployed in different regions, including India \(Mumbai\), China \(Hong Kong\), Germany \(Frankfurt\), UAE \(Dubai\), and Singapore \(Singapore\).

![How intelligent load balancing works](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2869177951/p89086.png)

The following table lists the capabilities of your WAF instance after you enable intelligent load balancing.

|Capability|Before this feature is enabled|After this feature is enabled|
|----------|------------------------------|-----------------------------|
|Disaster recovery|-   Access protection based on multiple single-active nodes
-   Unified failover for disaster recovery

|-   Access protection based on multi-node load balancing
-   Automatic failover based on intelligent DNS resolution |
|Access acceleration|N/A|Shortest link due to the closest protection node and origin server|

## Benefits

Intelligent load balancing brings you the following benefits:

-   Active geo-redundancy services

    -   Automatic disaster recovery among multiple lines to achieve fault recovery
    -   Distributed health check to balance loads among multiple lines
    -   Upgraded least-time back-to-origin algorithm to ensure low latency
    ![Benefits of active geo-redundancy services](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3869177951/p89101.png)

-   Co-location multi-active services

    -   Automatic disaster recovery among multiple lines to achieve fault recovery
    -   Distributed health check to balance loads among multiple lines
    ![Co-location multi-active services](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3869177951/p89104.png)

-   Co-location single-active service

    -   Automatic disaster recovery among multiple lines to achieve fault recovery
    -   Distributed health check to balance loads among multiple lines
    ![Co-location single-active services](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3869177951/p89105.png)


## Enable intelligent load balancing

To enable intelligent load balancing, set the **GSLB** parameter to Yes when you purchase a subscription WAF instance. You can also set the **GSLB** parameter to Yes when you upgrade a subscription WAF instance.

Intelligent load balancing is charged on a monthly basis during the service period of your WAF instance.

-   WAF instances in mainland China: USD 180/month
-   WAF instances outside mainland China: USD 800/month

