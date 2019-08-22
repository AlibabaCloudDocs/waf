# Best practices for HTTP flood protection {#concept_hzx_cvm_2gb .concept}

This topic describes common scenarios of HTTP flood attacks and introduces related protection strategies offered by Web Application Firewall \(WAF\). By using WAF, you can effectively protect your site from HTTP flood attacks.

## Volumetric and high-frequency HTTP flood attacks {#section_cb2_fvm_2gb .section}

In a volumetric HTTP flood attack, a zombie server sends requests more frequently than a normal server does. In this case, the most effective measure is to restrict the request rate or forbid the requests from suspicious request sources.

You can create [custom HTTP flood protection rules](../../../../dita-oss-bucket/SP_197/DNwaf1852814/EN-US_TP_15564.md#) to restrict the request rate. The following is an example.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156644529434768_en-US.jpg)

This rule sets **Matching rules** to URI Path Match and sets URI to a forward slash \(/\) to select all paths under the domain. If an IP address sends more than 1,000 requests to the domain within 30 seconds, WAF blocks this IP address for 10 hours. This rule can be used to protect small and medium-sized websites.

You can modify the protected paths, adjust the protection threshold, and change the blocking type based on your needs for better protection. For example, to prevent credential stuffing on the logon interface, you can set Matching rules to URI Path Match and set URI to /login.php, and block IP addresses that send more than 20 requests to access the path within 60 seconds.

Note the following points when you use HTTP flood protection:

-   The **human-machine identification** **blocking type** aims to verify whether requests are sent from Web browsers or automation scripts. You can use this blocking type to protect Web and HTML5 applications, but not native apps or APIs. To protect native apps and APIs, set **Blocking type** to **Block**.
-   For APIs or IP addresses that may be mistakenly blocked by HTTP flood protection, you can use [HTTP ACL policies](../../../../dita-oss-bucket/SP_197/DNwaf1852814/EN-US_TP_15565.md#) to whitelist these request sources.
-   Do not enable the emergency mode for native apps or APIs.

We recommend that you use **Anti-Bot Service** for more targeted protection and flexible handling methods.

For example, blocking IP addresses may affect NAT. Anti-Bot Service allows you to use the parameters related to user information in the cookies or requests to calculate the request rate. You can also use slider CAPTCHA to verify the identity of the requester. This helps reduce false positives. In the following example, the request rate is calculated based on the cookie that is used to identify the user, and slider CAPTCHA is used to verify the user identity. Assume that the cookie format is as follows: uid=12345.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156644529534769_en-US.jpg)

## Attacks from regions outside mainland China and public clouds {#section_utg_mvm_2gb .section}

A large portion of HTTP flood attacks originate from regions outside mainland China, data centers, and public clouds. If your website targets users in mainland China, you can block requests from regions outside mainland China to mitigate this attack.

WAF provides the [blocked regions](../../../../dita-oss-bucket/SP_197/DNwaf1852814/EN-US_TP_15566.md#) feature for this purpose.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156644529634770_en-US.jpg)

If you need to block IP addresses from data centers or public clouds, such as Alibaba Cloud or Tencent Cloud, contact customer service through **DingTalk**.

## Abnormal or unusual packets {#section_xmy_wvm_2gb .section}

Malicious requests in HTTP flood attacks are arbitrarily constructed and contain abnormal or unusual packets compared with normal requests. Most malicious requests have the following features:

-   Abnormal or malformed user agent. For example, the user agent has characteristics of automation tools \(such as Python\), has an incorrect format \(such as Mozilla///\), or is impossible to be used in normal requests \(such as www.baidu.com\). Block the request if these features are detected.
-   Unusual user agent. For example, promotional HTML5 pages targeting WeChat users are supposed to be accessed through WeChat. It is unusual if the user agent field indicates that the request is sent from a Windows desktop browser, such as MSIE 6.0. Block the request if these features are detected.
-   Unusual referer. For example, the referer field does not exist or indicates the address of an illegitimate site. We recommend that you block this request. However, if the user is visiting your home page or visiting your website for the first time, the request may not contain the referer field. If a URL can only be accessed through redirects, you can decide whether to block the URL based on the referer.
-   Unusual cookies. Similar to the referer field, a normal request contains cookies that are related to the business of the requested website, unless it is the user's first visit to your site. In many situations, malicious requests in HTTP flood attacks do not contain any cookie information.
-   Missing HTTP headers. For example, normal requests contain the authorization header while malicious requests do not.
-   Incorrect request methods. For example, if an API has only received POST requests before but is now overwhelmed by GET requests, then you can block these GET requests.

You can analyze the features of requests and use [HTTP ACL policies](../../../../dita-oss-bucket/SP_197/DNwaf1852814/EN-US_TP_15565.md#) to block malicious requests.

![](images/34776_en-US.jpg "Example 1: Block requests that do not contain cookies")

![](images/34777_en-US.jpg "Example 2: Block requests that do not contain authorization headers")

## API abuse {#section_yfn_2wm_2gb .section}

We recommend that you use [data risk control](../../../../dita-oss-bucket/SP_197/DNwaf1852814/EN-US_TP_15568.md#) to protect important APIs from abuse. These APIs include logon, registration, voting, and SMS verification APIs.

Data risk control injects a JavaScript snippet into your webpage and collects information about user behavior and environment variables to determine whether the request is sent from a real user or an automation script. Data risk control makes decisions based on CAPTCHA rather than the request rate or the source IP address. The feature is very effective in mitigating low-frequency attacks.

**Note:** Data risk control identifies malicious requests by checking whether requests contain the authentication parameters that normal requests must contain. The service is not applicable to environments where JavaScript is not supported, such as APIs and native apps. To prevent false positives, we recommend that you test data risk control first before you enable it in the production environment. You can also use the detection mode first, and then contact customer services before you enable the prevention mode.

## Malicious scans {#section_str_3wm_2gb .section}

A large number of malicious scans pose a serious threat to the performance of your servers. Apart from restricting scans based on frequency, you can also enhance security by using features such as [IP blocking](../../../../dita-oss-bucket/SP_197/DNwaf1852814/EN-US_TP_145404.md#), [directory scan protection](../../../../dita-oss-bucket/SP_197/DNwaf1852814/EN-US_TP_145405.md#), and [threat intelligence](../../../../dita-oss-bucket/SP_197/DNwaf1852814/EN-US_TP_145406.md#).

Scan requests with attack signatures are automatically blocked by WAF based on default protection rules. The malicious IP blocking feature directly blocks IP addresses that frequently trigger protection rules.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156644529741299_en-US.png)

Directory scan protection automatically blocks client IP addresses that launch multiple directory traversal attacks within a short period of time.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156644529834778_en-US.jpg)

Threat intelligence automatically blocks access requests from common vulnerability scanners or from IP addresses in the Alibaba Cloud library of identified port scan attackers.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81368/156644529941300_en-US.png)

## Fake apps {#section_fmz_jwm_2gb .section}

To protect your business from fake apps, you can use features such as custom HTTP flood protection, region blocking, and HTTP ACL policies. You can also use the Alibaba Cloud Security SDK for enhanced protection.

After you integrate the SDK with your app, all incoming requests are verified before they are sent to your server. The device information and request signature are combined to determine whether a request is sent from a legitimate app. Requests that do not originate from the official app are automatically blocked. This ensures that only requests from legitimate clients are served. You do not need to analyze the patterns of illegitimate requests.

To use the SDK, you must activate Anti-Bot Service. For more information, see [SDK instructions](../../../../dita-oss-bucket/SP_56/DNantibot1855834/EN-US_TP_16083.md#).

## Web crawlers {#section_f42_lwm_2gb .section}

For informational websites offering services such as credit reports, apartment rentals, airline tickets, and e-book reading, Web crawlers can significantly increase the bandwidth usage and server load, and even cause data leakage. If the preceding approaches cannot prevent Web crawlers, we recommend that you use **Anti-Bot Service** for more effective protection.

