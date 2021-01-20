---
keyword: [non-standard ports, custom ports, HTTP, HTTPS, Web Application Firewall, WAF]
---

# View the ports supported by WAF

Web Application Firewall \(WAF\) protects services that use standard ports and non-standard ports. The standard ports include ports 80, 8080, 443, and 8443. You can also use non-standard ports that are specified by WAF. You can customize server ports when you configure WAF for your website. WAF receives and redirects traffic on the server ports that you specify.

After you configure WAF for your website, WAF forwards traffic to the origin server only on the specified ports.

## Precautions

WAF protects services that use standard ports and non-standard ports. The non-standard ports include ports specified by WAF and ports that you customize. The number of supported ports and the allowed range of non-standard ports vary based on WAF editions. For more information, see [Ports that each WAF edition supports](/intl.en-US/Website Access/View the ports supported by WAF.md). Take note of the following items:

-   To protect websites that use non-standard ports, you must use a WAF instance of the **Business** edition or higher.
-   The maximum number of ports that a WAF instance supports is the total number of standard and non-standard ports that the instance supports.
-   You can use non-standard ports only when you use a WAF instance of the Exclusive edition or when you add your website to a WAF instance of the Enterprise edition in transparent proxy mode. In other cases, you can use only the non-standard ports that are specified by WAF.

## View the supported ports in the WAF console

You can view the supported ports in the WAF console.

1.  In the left-side navigation pane of the WAF console, choose **Asset Center** \> **Website Access**.
2.  Find the domain name for which you want to configure ports and click **Edit** in the Actions column.
3.  On the **Edit** page, find the **Destination Server Port** section, click **Customize**, and then enter port numbers based on your business requirements.

For more information, see [Configure ports]().

## Ports that each WAF edition supports

Subscription WAF instances of the Business edition or higher allow you to configure non-standard ports.

The following table lists the ports that each WAF edition supports. The supported ports in the console shall prevail. For more information about how to view the supported ports in the console, see [Configure ports]()

|WAF edition|Maximum number of ports supported by each WAF instance|Supported standard port \(default\)|Supported non-standard port \(custom\)|
|-----------|------------------------------------------------------|-----------------------------------|--------------------------------------|
|Pro|4|-   HTTP ports: 80 and 8080
-   HTTPS ports: 443 and 8443

|Not supported.**Note:** The Pro edition of WAF does not support non-standard ports regardless of the access mode, CNAME or transparent proxy, that you use. |
|Business|10 \(This is the total number of standard ports and non-standard ports.\)|-   HTTP ports: 80 and 8080
-   HTTPS ports: 443 and 8443

|The non-standard ports that you can use are the same regardless of the access mode, CNAME or transparent proxy, that you use. You can use the following non-standard ports that are specified by WAF:-   HTTP ports:

81, 82, 83, 84, 86, 87, 88, 89, 97, 800, 808, 1000, 1090, 3333, 3501, 3601, 5000, 5222, 6001, 6666, 7000, 7001, 7002, 7003, 7004, 7005, 7006, 7009, 7010, 7011, 7012, 7013, 7014, 7015, 7016, 7018, 7019, 7020, 7021, 7022, 7023, 7024, 7025, 7026, 7070, 7071, 7081, 7082, 7083, 7088, 7097, 7510, 7777, 7800, 8000, 8001, 8002, 8003, 8008, 8009, 8020, 8021, 8022, 8025, 8026, 8077, 8078, 8081, 8082, 8083, 8084, 8085, 8086, 8087, 8088, 8089, 8090, 8091, 8106, 8181, 8334, 8336, 8686, 8800, 8888, 8889, 8999, 9000, 9001, 9002, 9003, 9021, 9023, 9027, 9037, 9080, 9081, 9082, 9180, 9200, 9201, 9205, 9207, 9208, 9209, 9210, 9211, 9212, 9213, 9898, 9908, 9916, 9918, 9919, 9928, 9929, 9939, 9999, 10000, 10001, 10080, 12601, 28080, 33702, and 48800

**Note:** Only WAF instances that are deployed in mainland China support port 48800.

-   HTTPS ports:

4443, 5443, 6443, 7443, 8553, 8663, 9443, 9553, 9663, and 18980

**Note:** Only WAF instances that are deployed in mainland China support port 18980. |
|Enterprise|50 \(This is the total number of standard ports and non-standard ports.\)|-   HTTP ports: 80 and 8080
-   HTTPS ports: 443 and 8443

|The non-standard ports that you can use vary based on the access mode, CNAME or transparent proxy, that you use. The following list describes the differences:-   **Transparent proxy mode**: You can use non-standard ports from 0 to 65535.
-   **CNAME mode**: You can use non-standard ports that are specified by WAF.
    -   HTTP ports:

81, 82, 83, 84, 86, 87, 88, 89, 97, 800, 808, 1000, 1090, 3333, 3501, 3601, 5000, 5222, 6001, 6666, 7000, 7001, 7002, 7003, 7004, 7005, 7006, 7009, 7010, 7011, 7012, 7013, 7014, 7015, 7016, 7018, 7019, 7020, 7021, 7022, 7023, 7024, 7025, 7026, 7070, 7071, 7081, 7082, 7083, 7088, 7097, 7510, 7777, 7800, 8000, 8001, 8002, 8003, 8008, 8009, 8020, 8021, 8022, 8025, 8026, 8077, 8078, 8081, 8082, 8083, 8084, 8085, 8086, 8087, 8088, 8089, 8090, 8091, 8106, 8181, 8334, 8336, 8686, 8800, 8888, 8889, 8999, 9000, 9001, 9002, 9003, 9021, 9023, 9027, 9037, 9080, 9081, 9082, 9180, 9200, 9201, 9205, 9207, 9208, 9209, 9210, 9211, 9212, 9213, 9898, 9908, 9916, 9918, 9919, 9928, 9929, 9939, 9999, 10000, 10001, 10080, 12601, 28080, 33702, and 48800

**Note:** Only WAF instances that are deployed in mainland China support port 48800.

    -   HTTPS ports:

4443, 5443, 6443, 7443, 8553, 8663, 9443, 9553, 9663, and 18980

**Note:** Only WAF instances that are deployed in mainland China support port 18980. |

**Note:** The Exclusive edition of WAF supports additional non-standard ports, in addition to the ports in the preceding table. This edition also allows you to customize HTTP ports, HTTPS ports, and HTTP/2 ports as back-to-origin ports. For more information, see [Create an exclusive cluster](/intl.en-US/System Management/Create an exclusive cluster.md).

## References

[If my website receives requests over an unconfigured port, is the origin server threatened?]()

[Does WAF support custom server ports?]()

[What do I do if services on non-standard ports cannot be added to WAF of the Pro edition?]()

