# Best practices for HTTP flood protection {#concept_hzx_cvm_2gb .concept}

This topic describes common scenarios of HTTP flood attacks and introduces related protection strategies offered by WAF. By using WAF, you can effectively protect your site from HTTP flood attacks.

## Frequent HTTP flood attacks {#section_cb2_fvm_2gb .section}

During HTTP flood attacks, the request rate of a single zombie server is typically far higher than that of a normal user. The most effective way to defend against this type of attack is to restrict the request rate of the source IP.

You can create [custom HTTP flood protection rules](../../../../reseller.en-US/User Guide/Configuration/Custom HTTP flood protection.md#) to implement restrictions on the request rate. Example:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156514763134768_en-US.jpg)

This rule uses **prefix match** to select all paths under the domain. If an IP address sends more than 1,000 requests to the domain within 30 seconds, the IP address is blocked for 10 hours. This rule can be used to protect small and medium-sized websites.

You can modify the protected paths, adjust the blocking threshold, and change the blocking type based on your need to achieve better protection. For example, to prevent user enumeration, you can use prefix match to select the logon path, such as "/login.php", and block IPs that send more than 20 requests to access the path within 60 seconds.

Note the following points when you use HTTP flood protection:

-   The **Human-machine Identification****blocking type** can verify whether requests are sent from Web browsers or automation scripts. You can use this blocking type to protect Web and HTML5 applications, but not native apps or API services. To protect native apps and API services, set the **blocking type** to **block**.
-   For APIs or IP addresses that may be mistakenly blocked by HTTP flood protection, you can use [HTTP ACL Policy](../../../../reseller.en-US/User Guide/Configuration/HTTP ACL policy.md#) to whitelist these source IPs.
-   Do not enable the emergency mode for native apps or API services.

We recommend that you use **Anti-Bot Service** for more targeted protection and flexible handling methods.

For example, blocking IP addresses may affect NAT. Anti-Bot Service allows you to use cookies or request parameters to calculate the request rate. You can also use slider captcha to verify the identity of the requester. In the following example, the request rate is calculated based on the user's cookie. Slider captcha is used to verify the identity of the user. Assume that the cookie format is as follows: uid=12345.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156514763134769_en-US.jpg)

## Attacks originating from international regions and public clouds {#section_utg_mvm_2gb .section}

A large portion of HTTP flood attacks originate from international regions, data centers, and public clouds. If your website targets Chinese users, you can block requests from international regions to mitigate this attack.

WAF provides the [Blocked Regions](../../../../reseller.en-US/User Guide/Configuration/Blocked regions.md#) feature for this purpose.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156514763234770_en-US.jpg)

If you need to block IP addresses from data centers or public clouds, such as Alibaba Cloud or Tencent Cloud, contact customer service through **DingTalk**.

## Abnormal or unusual packets {#section_xmy_wvm_2gb .section}

Malicious requests in HTTP flood attacks are arbitrarily constructed and contain abnormal or unusual packets compared with normal requests. Most malicious requests have the following features:

-   Abnormal user-agent. For example, the user-agent field shows characteristics of automation tools \(such as Python\), has an incorrect format \(such as Mozilla///\), or is obviously exceptional \(such as www.baidu.com\). Block the request if these features are detected.
-   Unusual user-agent. For example, promotional HTML5 pages targeting WeChat users are supposed to be accessed through WeChat. It is unusual if the user-agent field indicates that the request is sent from a Windows desktop browser, such as MSIE 6.0. Block the request if these features are detected.
-   Unusual referer. For example, the referer field does not exist or indicates the address of an illegitimate site. We recommend that you block this request. However, the user may be visiting your home page for the first time. If the page can only be accessed through redirects, it is unusual that the referer field is void.
-   Unusual cookie: Similar to the referer field, a normal request usually contains a cookie that is related to the user, unless it is the user's first visit to your site. In many situations, malicious requests in HTTP flood attacks do not contain any cookie information.
-   Missing HTTP headers: For example, normal requests usually contain the authorization header while malicious requests usually do not.
-   Incorrect request method: For example, if an API has only received POST requests before and is now overwhelmed by GET requests, then you can directly block GET requests.

To handle these requests, you can analyze their features and add [HTTP ACL policies](../../../../reseller.en-US/User Guide/Configuration/HTTP ACL policy.md#) to block the malicious requests.

![](images/34776_en-US.jpg "Example 1: Block requests that do not contain cookies")

![](images/34777_en-US.jpg "Example 2: Block requests that do not contain authorization headers")

## API abuses {#section_yfn_2wm_2gb .section}

We recommend that you use [Data Risk Control](../../../../reseller.en-US/User Guide/Configuration/Data risk control.md#) to protect important APIs from abuses. These APIs include logon, registration, voting, and SMS verification APIs.

Data Risk Control injects a JavaScript snippet into your webpage and collects information about user behavior and environment variables to determine whether the request is sent from a real user or an automation script. Data Risk Control makes decisions based on human identification. The request rate and source IP address are not taken into account. The service is very effective in mitigating low-frequency attacks.

**Note:** Data Risk Control depends on the authorization headers contained in normal requests to identify malicious requests. The service is not applicable to environments where JavaScript is not supported, such as API services and native apps. To prevent false positives, we recommend that you test out Data Risk Control first before you enable it in the production environment. You can contact customer service for the test methods.

## Malicious scans {#section_str_3wm_2gb .section}

A large number of malicious scans pose a serious threat to the performance of your servers. Apart from restricting scans based on frequency, you can also use Malicious IP Blocking to enhance protection.

Scan requests displaying common attack patterns are automatically blocked by WAF based on default protection rules. Malicious IP Blocking can directly block IP addresses that frequently trigger protection rules.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156514763234778_en-US.jpg)

## Fake apps {#section_fmz_jwm_2gb .section}

To protect your business from fake apps, you can use a number of different mitigations such as custom HTTP flood protection, blocked regions, and HTTP ACL policies. You can also integrate with Alibaba Cloud Security SDK for enhanced protection capability.

After you integrate the SDK with your app, all incoming requests must be verified before they are sent to the server. The device information and request signature are combined to determine if the request is sent from a legitimate app. Requests that do not originate from the official app are automatically blocked. This ensures that only requests from legitimate clients are served. You do not need to analyze the patterns of illegitimate requests.

To use the security SDK, you must activate Anti-Bot Service. For more information, see [SDK instructions](../../../../reseller.en-US/User Guide/App protection/Solution overview.md#).

## Web crawlers {#section_f42_lwm_2gb .section}

For informational websites offering services such as credit reports, apartment rentals, airline tickets, and e-book reading, Web crawlers can significantly increase bandwidth usage, slow down the server's performance, and even cause data leakage. The aforementioned approaches may not be very effective in preventing Web crawlers. We recommend that you use **Anti-Bot Service** for more advanced protection.

