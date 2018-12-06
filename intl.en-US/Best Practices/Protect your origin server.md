# Protect your origin server {#task_p5p_h3c_p2b .task}

If the IP address of your origin server is disclosed, an attacker may exploit it to bypass Alibaba Cloud WAF and start direct-to-origin attacks against your origin server. To prevent such attacks, you can configure a security group \(ECS origins\) or whitelist \(SLB origins\) in your origin server.

**Note:** You are not required to do the configuration described in this topic. But we recommend that you do so to eliminate the possible risk arises from IP exposure.

**You can verify if such a risk exists in your origin server as follows.**

Use Telnet to establish a connection from a non-Alibaba Cloud host to the listener port of your origin server’s public IP address. Check if the connection is successful. If the connection succeeds, your origin server faces an exposure risk. Once a hacker obtain the public IP address, he or she can bypass WAF to reach your origin server. If the connection fails, your origin server is secure.

For example, test the connection to port 80 and 800 of your WAF-enabled origin server IP. If the connection is successfully established, your origin server is insecure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15587/15440750158740_en-US.png)

**Note**

Configuring a security group has certain risks. Consider the following:

-   Make sure that all domain names hosted in your origin server \(ECS or SLB instance\) are deployed with Alibaba Cloud WAF.
-   In case of an Alibaba Cloud WAF cluster failure, where the WAF-inspected traffic is returned to origin server through a standby route, the access to your site will be affected if the security group policy is enabled in origin server.
-   In case of an expansion of the Alibaba Cloud WAF IP addresses, 5xx error pages may be frequently returned to a visitor if the security group policy is enabled in origin server.

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf). 
2.  Go to the **Management** \> **Website Configuration** page. 
3.  Click **Alibaba Cloud WAF IP range** to view the WAF IP addresses.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15587/15440750157608_en-US.jpg)

 
4.  In the Alibaba Cloud WAF IP range dialog box, click **Copy IP list**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15587/15440750157609_en-US.jpg)

 
5.  Configure the access control in your origin server to only allow the WAF IP addresses. 
    -   **For an ECS origin**

        1.  Go to the [ECS instance list](https://ecs.console.aliyun.com/#/server/region/cn-beijing), locate the origin instance, and click **Manage**.
        2.  In the left-side navigation pane, click Security Groups.
        3.  Locate to the security group to be operated and click **Add Rules**.
        4.  Click **Add Security Group Rule** and complete the following configuration to allow the WAF IP addresses with the highest priority.
            -   **NIC**: Internet Network
            -   **Rule Direction**: Ingress
            -   **Action**: Allow
            -   **Protocol Type**: Customized TCP
            -   **Authorization Type**: Ipv4 CIRD Block
            -   **Port Range**: 80/443
            -   **Authorization Objects**: Paste the copied WAF IP addresses in step 4.
            -   **Priority**: 1
        5.  Add another security group rule and configure it as follows to block all accesses with the lowest priority.
            -   **NIC**: Internet Network
            -   **Rule Direction**: Ingress
            -   **Action**: Forbid
            -   **Protocol Type**: Customized TCP
            -   **Port Range**: 80/443
            -   **Authorization Type**: Ipv4 CIRD Block
            -   **Authorization Object**: 0.0.0.0/0
            -   **Priority**: 100
        **Note:** If the origin instance interacts with other IPs or applications, you must add corresponding rules to allow accesses from them.

    -   **For an SLB origin**

        The configuration in an SLB instance is similar as ECS. You add the WAF IP addresses to the whitelist. For more information, see [Configure access control](../../../../intl.en-US/Archives/User Guide (Old Console)/Access control/Manage access control.md#).

        -   Create an access control list
        -   Add the WAF IP addresses to the IP whitelist
        -   Enable the IP whitelist

