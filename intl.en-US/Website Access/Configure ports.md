# Configure ports

After you add a website to your Web Application Firewall \(WAF\) instance, you must configure HTTP or HTTPS port numbers to allow access to the website. Then, WAF can process requests that are sent over the configured ports to protect the website.

WAF forwards only the requests that are sent over the configured ports to the origin server. If requests are sent over an unconfigured port, WAF does not forward the requests to the origin server.

WAF protects services that use standard ports and non-standard ports. The non-standard ports include ports specified by WAF and ports that you customize. The number of supported ports and the allowed range of non-standard ports vary based on WAF editions. For more information, see [Ports that each WAF edition supports](/intl.en-US/Website Access/View the ports supported by WAF.md).

## Scenarios

You must configure HTTP or HTTPS ports in the following scenarios:

-   A website is added to WAF.
-   The HTTP or HTTPS ports that the website uses change.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Asset Center** \> **Website Access**.

4.  On the **Domain Names** tab, find the domain name of your website and click **Edit** in the Actions column.

5.  In the **Destination Server Port** section of the **Edit** page, click **Customize**.

6.  Click **HTTP** or **HTTPS** based on your business requirements. Then, enter the port number that you want to add and click **Save**.

    ![Server ports](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3901549951/p102177.png)

    **Note:** The port number that you enter must be within the allowed port range. Otherwise, the settings cannot be saved. You can click **View Allowed Port Range** to check whether the port number is within the allowed port range.

    ![Allowed Port Range](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4901549951/p102191.png)

7.  Click **Confirm**.


## References

[If my website receives requests over an unconfigured port, is the origin server threatened?]()

[Does WAF support custom server ports?]()

[What do I do if services on non-standard ports cannot be added to WAF of the Pro edition?]()

