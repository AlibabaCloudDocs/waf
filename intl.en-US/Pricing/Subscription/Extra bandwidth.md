# Extra bandwidth {#concept_i22_std_n2b .concept}

Different subscription plans of Alibaba Cloud WAF are allocated a certain amount of bandwidth. If the allocated bandwidth of your WAF subscription does not suit your business requirements, you can purchase extra bandwidth.

## What is a bandwidth limit for WAF? {#section_fsq_std_n2b .section}

WAF bandwidth indicates the normal business flow capacity of a WAF instance, in Mbps. 100 Mbps of bandwidth corresponds to 4,000 QPS, and so forth. QPS \(Query Per Second\) indicates the quantity of requests in one second. For example, an HTTP GET request is a query.

**Note:** WAF bandwidth is calculated exclusively by WAF and has noting to do with the bandwidth or traffic limit of other Alibaba Cloud products such as CDN, SLB, and ECS.

Each WAF subscription has a certain bandwidth limit, and the higher plan has the larger bandwidth. Besides, when used to access origin servers inside Alibaba Cloud \(such as ECS or SLB instances\), the WAF subscription offers more bandwidth than is used to access non-Alibaba Cloud servers. For example, the WAF Business edition has a bandwidth limit of 100 Mbps \(when the origin server is inside Alibaba Cloud\) and 30 Mbps \(when the origin server is outside Alibaba Cloud\).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15540/15419878527286_en-US.png)

## How to select bandwidth? {#section_hsq_std_n2b .section}

We recommend that you evaluate the normal business flow capacity of both the inbound and outbound traffic of all websites that you want to enable WAF protection before purchasing. Make sure that the bandwidth of your WAF subscription is larger than the total inbound flow capacity and total outbound flow capacity.

**Note:** Generally, outbound traffic is greater than inbound traffic.

You can evaluate your business traffic by using ECS traffic statistics or other monitoring tools on your origin server.

**Note:** The traffic here indicates your normal business traffic. For example, if you enable WAF protection for all your websites that provide external services, in the case of normal access \(the websites are not attacked\), WAF forwards traffic to the origin ECS. If the websites are attacked by HTTP flood attacks or DDoS attacks, WAF filters out corrupted traffic and passes valid traffic back to the origin ECS. Therefore, the inbound and outbound traffic you view on the ECS console is your normal business traffic. If the origin servers consist of multiple ECS instances, you must calculate the traffic sum of all corresponding ECS instances.

**Examples**

Suppose you want to configure three websites with WAF protection. The normal traffic in the outbound direction of each website does not exceed 10 Mbps, and the total traffic does not exceed 30 Mbps. In this case, you can subscribe to the WAF Business Edition \(with a bandwidth limit of 30 Mbps\).

**Note:** You can also extend the default bandwidth by adding certain amount of extra bandwidth to your WAF subscription.

## What happens if the bandwidth is exceeded? {#section_jsq_std_n2b .section}

If your normal business flow capacity exceeds the bandwidth limit of your WAF subscription, you will receive an alarming message on the WAF console, informing that all your business traffic forwarding configured in WAF will be affected.

Your websites may be subject to traffic restrictions or random packet loss, and your normal business may be unavailable, slow, or delayed for a certain period of time.

In this case, you can upgrade your WAF, or purchase extra bandwidth.

## What is extra bandwidth? {#section_ksq_std_n2b .section}

If the business flow capacity of your website is high, you can purchase extra bandwidth to avoid exceeding the bandwidth limit.

For example, your current traffic requirement is 50 Mbps \(non-Alibaba Cloud server\), and you have purchased the WAF Business Edition \( the bandwidth limit is 30 Mbps\), you can purchase an additional 20 Mbps of extra bandwidth to meet your business needs.

You can [Upgrade WAF](reseller.en-US/Pricing/Renewal and upgrade.md#ol_ut4_hdn_42b) to increase the extra bandwidth to meet higher business requirement.

**Note:** You can also add certain amount of extra bandwidth to your WAF subscription when purchasing WAF.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15540/15419878527287_en-US.png)

