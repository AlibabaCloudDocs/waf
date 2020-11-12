# Configure protection for an origin server

After you add your website to WAF, you can configure access control policies for your origin server to allow inbound traffic from only WAF back-to-origin CIDR blocks. This protects your website from direct-to-origin attacks. This topic describes how to configure security group rules and whitelist policies for an origin server that is deployed on an ECS and SLB instance.

The origin server is deployed on an ECS and SLB instance. All domain names whose origin server is deployed on the instance are added to and protected by WAF. For more information, see [Add websites](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).

## Precautions

After you add your website to WAF for protection, the traffic is always be forwarded, regardless of whether you configure protection for your origin server. If the IP address of your origin server is exposed, malicious parties can bypass WAF and launch direct-to-origin attacks. Therefore, you must configure protection for your origin server. For more information about how to determine whether the IP address of your origin server is exposed, see [FAQ](#section_9i9_p4l_gxg).

Risks may arise if you configure access control policies on the origin server. Take note of the following items before you configure protection for the origin server:

-   Make sure that all domain names whose origin server is deployed on an ECS or SLB instance are added to WAF.
-   If a WAF cluster fails, requests destined for your website are all directed to the origin server in bypass mode. This ensures service continuity. In this case, if you have configured ECS security group rules or SLB whitelist policies for the origin server, the origin server cannot be accessed over the Internet.
-   If back-to-origin CIDR blocks are added after WAF cluster scale-out and you have configured ECS security group rules and SLB whitelist policies for the origin server, HTTP 5xx errors may be frequently reported.

## Obtain the WAF back-to-origin CIDR blocks

**Note:** The WAF back-to-origin CIDR blocks are updated on a regular basis. Pay attention to update notifications and make sure that you add the updated back-to-origin CIDR blocks to the security group and whitelist policies in a timely manner to avoid service interruption.

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **System Management** \> **Product Information**.

4.  In the lower part of the **Product Information** page, find the **WAF IP Segments** section and click **Copy All IPs**.

    The **WAF IP Segments** section displays the latest back-to-origin CIDR blocks.

    ![WAF back-to-origin CIDR blocks](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1901549951/p7997.png)


## Configure ECS security group rules

If your origin server is deployed on an ECS instance, you must configure security group rules for the ECS instance after you obtain the WAF back-to-origin CIDR blocks. These security group rules allow inbound traffic only from the WAF back-to-origin CIDR blocks.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select the resource group and region of the ECS instance.

4.  On the **Instances** page, find the instance and choose **More** \> **Network and Security Group** \> **Configure Security Group** in the Actions column.

5.  Find the security group that you want to configure and click **Add Rules** in the Actions column.

6.  Click **Add Security Group Rule**.

7.  In the **Add Security Group Rule** dialog box, specify the following parameters and click **OK**.

    ![Security group rule-allow](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9801549951/p101182.png)

    |Parameter|Description|
    |---------|-----------|
    |**NIC Type**|The default NIC type is consistent with the network type of the ECS instance.     -   If the network type of the ECS instance is VPC, the default value is **Internal**.
    -   If the network type of the ECS instance is a classic network, set **NIC Type** to **Public**. |
    |**Rule Direction**|Select **Inbound**.|
    |**Action**|Select **Allow**.|
    |**Protocol Type**|Select **Custom TCP**.|
    |**Port Range**|Enter **80/443**.|
    |**Priority**|Enter **1**, which indicates the highest priority.|
    |**Authorization Type**|Select **IPv4 CIDR Block**.|
    |**Authorization Object**|Paste the back-to-origin CIDR blocks that you copy. CIDR blocks follow the 10.x.x.x/32 format. Separate multiple CIDR blocks with commas \(,\). You can add up to 10 CIDR blocks to each security group rule.

**Note:** We recommend that you put all WAF back-to-origin CIDR blocks into multiple security group rules. |
    |**Description**|Enter the description of the security group rule. Example: Allow inbound traffic from the WAF back-to-origin CIDR blocks.|

    The security group rule that you add takes the highest priority and allows all inbound traffic from the WAF back-to-origin CIDR blocks.

    **Warning:** Make sure that you add all WAF back-to-origin CIDR blocks to the security group rules. Otherwise, access exceptions may occur.

8.  Add another security group rule with the lowest priority and configure it to block all accesses.

    ![Security group rule-block](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9801549951/p101184.png)

    The following table lists the specific rule configurations.

    |Parameter|Description|
    |---------|-----------|
    |**NIC Type**|The default NIC type is consistent with the network type of the ECS instance.     -   When the network type of the ECS instance is VPC, the default value is **Internal**.
    -   When the network type of the ECS instance is a classic network, set **NIC Type** to **Public**. |
    |**Rule Direction**|Select **Inbound**.|
    |**Authorization Type**|Select **Forbid**.|
    |**Protocol Type**|Select **Custom TCP**.|
    |**Port Range**|Enter **80/443**.|
    |**Priority**|Enter **100**, which indicates the lowest priority.|
    |**Authorization Type**|Select **IPv4 CIDR Block**.|
    |**Authorization Object**|Enter **0.0.0.0/0**, which indicates all CIDR blocks.|
    |**Description**|Enter the description of the security group rule. Example: Block all inbound traffic, with a priority of 100.|


**Note:** If your origin server communicates with other IP addresses or applications, you must add another security group rule to allow access from them. Alternatively, you can add a security group rule to allow access from all ports and set it to the lowest priority.

## Configure SLB access control policies

If your origin server is deployed on an SLB instance, you must obtain the WAF back-to-origin CIDR blocks and configure an access control policy \(whitelist\) for the SLB instance. The policy allows the inbound traffic only from the WAF back-to-origin CIDR blocks.

1.  Log on to the [SLB console](https://slb.console.aliyun.com/).

2.  In the left-side navigation pane, click **Access Control**.

3.  Click **Create Access Control List**.

4.  In the **Create Access Control List** panel, configure the following configurations and click **OK**.

    ![Create Access Control List](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9801549951/p101223.png)

    |Parameter|Description|
    |---------|-----------|
    |**Access Control List Name**|Enter the name of the custom policy group. Example: WAF back-to-origin CIDR block|
    |**Resource Group**|Select the resource group to which the custom policy group belongs.|
    |**IP Version**|Select **IPv4**.|
    |**Add Multiple Addresses and Descriptions**|Paste all WAF back-to-origin CIDR blocks. Enter one entry in each line. Start a new line by pressing Enter.

**Note:** All copied WAF back-to-origin CIDR blocks are separated by commas \(,\). When you copy those CIDR blocks, we recommend that you use a text editor that supports extension replacement, such as Notepad or Word, to replace the commas \(,\) with line breaks \(\\n\). |

5.  In the left-side navigation pane, choose **Instances** \> **Server Load Balancers**.

6.  On the **Server Load Balancers** page, find the instance and click its ID.

7.  On the **Listener** tab, find the listener and choose ![More icon](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9801549951/p101229.png) \> **Set Access Control**.

8.  In the Access Control Settings panel, turn on **Enable Access Control**, configure the following parameters, and then click **OK**.

    |Parameter|Description|
    |---------|-----------|
    |**Access Control Method**|Select **Whitelist** to allow specified IP addresses to access the SLB instance.|
    |**Access Control List**|Select the access control list that you created for the WAF back-to-origin CIDR blocks.|


## What to do next

After you configure the ECS security group rules and SLB whitelist policies, test whether the origin server can be connected through ports 80 and 8080 to check whether the protection configurations are in effect.

If the origin server cannot be connected through these ports but your service is running normally, the protection configurations are in effect.

## FAQ

How do I determine whether the IP address of my origin server is exposed?

Use Telnet to establish a connection from a host that is not deployed on Alibaba Cloud to the service port of the public IP address of your origin server.

-   If the connection is established, the IP address of your origin server may be exposed. Malicious parties that obtain the public IP address can bypass WAF and launch attacks on your origin server.
-   If the connection fails, your origin server is secure.

For example, test the connectivity of ports 80 and 8080 of the origin server that is protected by WAF. If the connectivity is normal, your origin server is insecure.

![Reachable port of WAF](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9801549951/p8740.png)

