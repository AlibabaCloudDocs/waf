# Best practices for preventing HTTP flood attacks

This topic describes common types of HTTP flood attacks and how to defend against them by using protection policies offered by WAF.

## Overview

You can determine which protection policies to use based on the attack type.

-   [Volumetric and high-rate HTTP flood attacks](#section_cb2_fvm_2gb)
-   [Attacks from regions outside China and public clouds](#section_utg_mvm_2gb)
-   [Malformed packets](#section_xmy_wvm_2gb)
-   [API abuse](#section_yfn_2wm_2gb)
-   [Malicious scans](#section_str_3wm_2gb)
-   [App attacks](#section_fmz_jwm_2gb)
-   [Malicious crawlers](#section_f42_lwm_2gb)

## Volumetric and high-rate HTTP flood attacks

In volumetric HTTP flood attacks, a zombie server sends requests at a higher frequency than a normal server does. To prevent such attacks, the most effective measure is to limit the request rate of request sources. WAF provides the **Rate Limiting** function for this purpose. You can configure this function from the **Custom Protection Policy** page. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).

You can configure a rule, as shown in the following figure. The rule blocks all IP addresses that initiate more than 1,000 requests in a 30 second interval to any path under the domain name. The blocking period lasts for 10 hours. This rule is used to protect small and medium-sized websites.

![Rate limiting](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0728549951/p34768.png)

You can modify the protected path, adjust the threshold, and select the optimal action to best suit your protection requirements. For example, to prevent credential stuffing on logon endpoints, you can set **Matching field** to URL and **Matching content** to `/login.php`, and block IP addresses that send more than 20 requests to access the path within 60 seconds.

![Example rate limiting](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9628549951/p129834.png)

Note the following points when you configure HTTP flood protection policies:

-   **Captcha** and **Strict Captcha** in the **Action** drop-down list aim to verify whether requests originate from a human or an automation script. You can use these two actions to protect common and HTML5 web pages, but not native apps or APIs. To protect the native apps and APIs, set **Action** to **block**.
-   You can configure whitelist policies for APIs or IP addresses that may be mistakenly blocked by HTTP flood protection on the **Access Control/Throttling** tab. For more information, see [Configure the access control and throttling whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the access control and throttling whitelist.md).
-   Do not select the **Protection-emergency** mode for native apps or APIs in the **HTTP Flood Protection** section.

If you have purchased an instance of the WAF Enterprise edition, you can configure rate limiting by using custom statistical objects, IP addresses, and sessions. Blocking IP addresses may affect NAT. You can use cookies or parameters that identify users as statistical objects. In the following example, the request rate is calculated based on the cookie that is used to identify the user, and Captcha is used to verify the requests. Assume that the cookie format is as follows: `uid=12345`.

![Cookie ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1728549951/p34769.png)

## Attacks from regions outside China and public clouds

A large portion of HTTP flood attacks originate from regions outside China, on-premises data centers, and public clouds.

If your website targets users inside China, you can block requests from regions outside China to mitigate this type of attack. WAF provides the **Area-based IP Blacklist** function for this purpose. For more information, see [Configure an IP address blacklist](/intl.en-US/Website Protection Settings/Access control and throttling/Configure an IP address blacklist.md)

![封禁区域 ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0728549951/p34770.jpg)

If you need to block the crawler IP addresses of common IP libraries, such as the CIDR blocks of Alibaba Cloud, Tencent Cloud, and on-premises data centers, you can use the **Bot Threat Intelligence** function on the **Bot Management** tab.

**Note:** Many crawlers are deployed on ECS instances. Users do not access your services by using the source IP addresses of public clouds or on-premises data centers.

Example: You can use the following bot threat intelligence rule to block accesses from the crawler IP addresses of Tencent Cloud. For more information, see [Set a bot threat intelligence rule](/intl.en-US/Website Protection Settings/Bot management/Set a bot threat intelligence rule.md).

![Bot threat intelligence rule for Tencent Cloud](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9628549951/p129822.png)

## Malformed packets

Malicious requests in HTTP flood attacks are specially crafted and contain malformed packets. Malformed packets have the following features:

-   Abnormal or malformed User-Agent string: has characteristics of automation tools \(such as Python\), is in an incorrect format \(such as `Mozilla///`\), or is impossible to be used in normal requests \(such as `www.baidu.com`\). If abnormal or malformed User-Agent strings are detected, block the requests.
-   Unusual User-Agent string: Promotional HTML5 pages that target WeChat users are supposed to be accessed through WeChat. It is unusual if the User-Agent string indicates that the request is sent from a Windows desktop browser, such as Microsoft Internet Explorer 6.0. If unusual User-Agent strings are detected, block the requests.
-   Abnormal referer field: If a request does not have a referer field or has a referer field that identifies the addresses of illegitimate websites, block the request. However, when a user visits your homepage or your website for the first time, the request may not contain the referer field. If a URL can only be accessed by using redirects, you can decide whether to block the URL based on the referer field.
-   Abnormal cookie: Similar to the referer field, a normal request contains cookies that identify the requested websites, unless it is the first time for the user to visit your website. Malicious requests in HTTP flood attacks typically do not contain any cookie information. You can block access requests without cookies.
-   Missing HTTP headers: Normal requests contain authorization headers while malicious requests do not.
-   Incorrect request methods: If an API has only received POST requests before but is now overwhelmed by GET requests, you can block these GET requests.

You can analyze the features of requests and set Protection Type to **ACL** from the **Custom Protection Policy** page to block malicious requests. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).

Configuration examples:

-   Example 1: Block requests that do not contain cookies.

    ![Block requests that do not contain cookies ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0255122061/p34776.png)

-   Example 2: Block requests that do not contain authorization headers.

    ![拦截不带authorization ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9628549951/p34777.jpg)


## API abuse

We recommend that you use the data risk control function to protect important APIs from attacks. These APIs include logon, registration, voting, and SMS verification APIs.

Data risk control injects a JavaScript snippet into your website and collects information about user behaviors and environment variables to determine whether requests originate from a human or an automation script. Data risk control makes decisions based on CAPTCHA rather than the request rate or the source IP address. The function mitigates low-frequency attacks very effectively.

**Note:** Data risk control checks whether requests contain authentication parameters required by all normal requests to identify malicious requests. The function is not suitable for environments where JavaScript is not supported, such as APIs and native apps. To prevent false positives, we recommend that you test data risk control in the test environment before you enable it. Alternatively, you can use the observation mode and contact engineers before you enable the prevention mode.

For more information, see [Configure data risk control](/intl.en-US/Website Protection Settings/Bot management/Configure data risk control.md).

## Malicious scans

A large number of malicious scans pose a serious threat to the performance of your servers. Apart from rate limiting, you can also use the **Scan Protection** function to enhance security. Scan protection supports the following settings:

-   **Blocking IPs Initiating High-frequency Web Attacks**: automatically blocks client IP addresses that initiate high-frequency web attacks.
-   **Directory Traversal Prevention**: automatically blocks client IP addresses that initiate multiple directory traversal attacks in a short period of time.
-   **Scanning Tool Blocking**: automatically blocks access requests from IP addresses defined in the common scan tools or the Alibaba Cloud malicious IP library.
-   **Collaborative Defense**: automatically blocks access requests from IP addresses defined in the Alibaba Cloud malicious IP library.

For more information, see [Configure scan protection](/intl.en-US/Website Protection Settings/Access control and throttling/Configure scan protection.md).

![Scan protection ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9628549951/p74001.png)

## App attacks

In addition to the preceding measures, you can also use SDK to enhance protection.

After you integrate the SDK with your app, all incoming requests are verified before they are sent to your server. The device information and request signature are combined to determine whether the requests are from legitimate apps. Requests that do not originate from official apps are automatically blocked. This ensures that only valid requests are served. You do not need to analyze the patterns of invalid requests.

To use the SDK, you must enable **App Protection**. For more information, see [Configure application protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md).

## Malicious crawlers

For informational websites that offer services such as credit reports, apartment rentals, airline tickets, and e-book reading, malicious crawlers can significantly increase the bandwidth usage and server workload, and even cause data leaks. If the preceding measures cannot prevent against malicious crawlers, we recommend that you enable and use the **Bot Management** feature for more effective protection. For more information, see [Configure the bot management whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the bot management whitelist.md).

