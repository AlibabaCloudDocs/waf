# Load balance across multiple origin IPs {#concept_nfq_4bj_p2b .concept}

You can specify a maximum of 20 origin IP addresses in a website configuration.

When multiple origin IP addresses are specified, WAF performs load balance across them when returning the inspected web traffic. WAF also performs health check on all origin IPs. When one IP is inaccessible, WAF stops assigning requests to that IP until it can be accessed again.

Suppose you have three origin IPs: 1.1.1.1, 2.2.2.2, and 3.3.3.3. You can configure your website as follows.

**Note:** If you have other layer-7 proxies enabled together with WAF, such as DDoS protection or CDN, make sure that you select **yes** for **Any layer 7 proxy \(e.g. Anti-DDoS/CDN\) enabled?** in website configuration

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15556/15439928497702_en-US.jpg)

When multiple origin IPs are specified, select a load balancing algorithm, such as IP HASH or Round-robin.

**Note:** If you use IP hash, make sure that the origin IP addresses are discrete. Otherwise, load balancing may not work properly.

