---
keyword: [non-standard ports, custom ports, HTTP, HTTPS, Web Application Firewall]
---

# View allowed port range

Web Application Firewall \(WAF\) protects services at specific non-standard ports and services at standard ports 80, 8080, 443, and 8443. You can customize server ports when you configure WAF. Then, WAF redirects traffic destined for your website at the custom server ports.

-   Your website is added to the WAF console.

    This topic describes how to customize server ports when you edit a domain name in the WAF console . Alternatively, you can customize server ports when you manually add a website to WAF for protection. For more information, see [Manually add website configurations](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).

-   To use ports other than 80, 8080, 443, and 8443, make sure that the WAF instance that you purchase meets the following specification requirements:
    -   If the instance is billed on a subscription basis, the instance must be of the **Business** edition or higher. For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).

WAF forwards traffic on only the customized ports of the origin server. For ports that are not configured, WAF does not forward any traffic on these ports.

## Limits

Port range

If you use WAF of the **Business** or **Enterprise** edition,the following ports are available:

**Note:** The query results displayed in the WAF console prevail. For more information, see [Allowed Port Range](#step_y8z_w5d_05d).

-   **HTTP-compliant**:

    80, 81, 82, 83, 84, 86, 87, 88, 89, 97, 800, 808, 1000, 1090, 3333, 3501, 3601, 5000, 5222, 6001, 6666, 7000, 7001, 7002, 7003, 7004, 7005, 7006, 7009, 7010, 7011, 7012, 7013, 7014, 7015, 7016, 7018, 7019, 7020, 7021, 7022, 7023, 7024, 7025, 7026, 7070, 7081, 7082, 7083, 7088, 7097, 7510, 7777, 7800, 8000, 8001, 8002, 8003, 8008, 8009, 8020, 8021, 8022, 8025, 8026, 8077, 8078, 8080, 8081, 8082, 8083, 8084, 8085, 8086, 8087, 8088, 8089, 8090, 8091, 8106, 8181, 8334, 8336, 8686, 8800, 8888, 8889, 8999, 9000, 9001, 9002, 9003, 9021, 9023, 9027, 9037, 9080, 9081, 9082, 9180, 9200, 9201, 9205, 9207, 9208, 9209, 9210, 9211, 9212, 9213, 9898, 9908, 9916, 9918, 9919, 9928, 9929, 9939, 9999, 10000, 10001, 10080, 12601, 28080, 33702, and 48800

    **Note:** Only the WAF instances deployed in mainland China support port **48800**.****

-   **HTTPS-compliant**:

    443, 4443, 5443, 6443, 7443, 8443, 8553, 8663, 9443, 9553, 9663, and 18980

    **Note:** Only WAF instances deployed in the regions in mainland China support port **18980**.


Port quantity

The total number of ports that each WAF instance uses for all websites has the following limits:

-   A WAF instance of the **Business** edition supports a maximum of 10 ports, including ports 80, 8080, 443, and 8443.
-   A WAF instance of the **Enterprise** edition supports a maximum of 50 ports, including ports 80, 8080, 443, and 8443.

**Note:** A WAF instance of the Exclusive edition supports more non-standard ports. You can use HTTP ports, HTTPS ports, and HTTP/2 ports as back-to-origin ports. For more information, see [Create an exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md).

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Asset Center** \> **Website Access**.

4.  On the Domain Names tab of the Website Access page, find the domain name and click **Edit** in the Actions column.

5.  On the **Edit** page, click **Customize** in the **Destination Server Port** section.

6.  Click **HTTP** or **HTTPS**. Then, enter the ports that you want to add and click **Save**.

    ![Server ports](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3901549951/p102177.png)

    **Note:** The ports that you entered must be within the allowed port range. Otherwise, the settings cannot be saved. You can click **View Allowed Port Range** to check whether the specified ports are within the allowed port range.

    ![Allowed Port Range](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4901549951/p102191.png)

7.  Click **Confirm**.


