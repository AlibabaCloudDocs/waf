# Allow access from WAF back-to-origin CIDR blocks

WAF uses specified back-to-origin CIDR blocks to forward normal traffic back to an origin server. To allow inbound traffic from the back-to-origin CIDR blocks, you must configure the security software or access control policies of the origin server when you add a website to WAF.

If you use security software such as FortiGate for your origin server, you must add the WAF back-to-origin CIDR blocks to the whitelist of the security software. This prevents normal traffic forwarded by WAF to the origin server from being blocked by access control policies.

For security purposes, we recommend that you configure access control policies for the origin server to allow only inbound traffic from the WAF back-to-origin CIDR blocks. This prevents attackers from bypassing WAF and directly attacking the origin server. For more information, see [Configure protection for an origin server](/intl.en-US/Website Access/Website access with CNAME/Configure protection for an origin server.md).

## Obtain the WAF back-to-origin CIDR blocks

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **System Management** \> **Product Information**.

4.  In the lower part of the **Product Information** page, find the **WAF IP Segments** section and click **Copy All IPs**.

    The **WAF IP Segments** section displays the latest back-to-origin CIDR blocks.

    ![WAF back-to-origin CIDR blocks](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1901549951/p7997.png)


## What to do next

After you obtain the WAF back-to-origin CIDR blocks, you must add them to the IP address whitelist of your security software on the origin server.

**Warning:** If you do not add the WAF back-to-origin CIDR blocks to the IP address whitelist of the origin server, normal requests sent by WAF may be rejected. This may cause a service interruption.

## FAQ

-   [Does WAF automatically add its back-to-origin CIDR blocks to security groups?]()
-   [Do I need to allow accesses from all client IP addresses?]()

