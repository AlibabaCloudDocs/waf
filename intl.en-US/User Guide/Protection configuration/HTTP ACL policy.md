# HTTP ACL policy {#concept_gy3_jbp_p2b .concept}

With HTTP ACL policy, you can customize access control rules to filter HTTP requests by client IP, request URL, and commonly used HTTP fields.

## Function description {#section_gzv_php_p2b .section}

HTTP ACL Policy supports customizing HTTP access control to filter HTTP requests based on a combination of criteria of commonly used HTTP fields, such as IP, URL, Referer, UA, and parameters. This feature applies to different business scenarios, such as anti-leech protection and website admin console protection.

**HTTP ACL policy rule**

Each HTTP ACL policy rule consists of a **Matching condition** and **Action**. When creating a rule, you define the matching condition by configuring matching fields, logical operators, and the corresponding match content, and select the action to be triggered in a match case.

**Matching condition**

A match condition is composed of matching fields, logical operators, and matching content. The matching content does not support regular expression descriptions, but is allowed to be set to null.

The following table lists all matching fields supported by HTTP ACL policy rules.

**Note:** For WAF Pro instances, only IP, URL, Referer, User-Agent are supported in matching fields, and a maximum of 20 rules are allowed for each domain name. For WAF Business or Enterprise instances, all the listed matching fields are supported, and you can define up to 100 or 200 rules for each domain name respectively.

|Matching field|Description|Supported logical operators|
|IP|The client IP address.| -   Has
-   Does not have

 |
|URL|The requested URL.| -   Includes
-   Does not include
-   Equals to
-   Does not equal to

 |
|Referer|The address of the previous web page with a link to the current request page.| -   Includes
-   Does not include
-   Equals to
-   Does not equal to
-   Length less than
-   Length equals
-   Length more than
-   Does not exist

 |
|User-Agent |The user agent string that identifies information about the client's browser.| -   Includes
-   Does not include
-   Equals to
-   Does not equal to
-   Length less than
-   Length equals
-   Length more than

 |
|Params|The parameters in the request URL, which start after "?". For example, the parameter of the URL www.abc.com/index.html? action=login is action=login.| -   Includes
-   Does not include
-   Equals to
-   Does not equal to
-   Length less than
-   Length equals
-   Length more than

 |
|Cookie|The cookie in the request URL.| -   Includes
-   Does not include
-   Equals to
-   Does not equal to
-   Length less than
-   Length equals
-   Length more than
-   Does not exist

 |
|Content-Type|The Media type of the body of the request \(used with POST and PUT requests\).| -   Includes
-   Does not include
-   Equals to
-   Does not equal to
-   Length less than
-   Length equals
-   Length more than

 |
|X-Forwarded-For|The x-forward-for field in the request URL. X-Forwarded-For \(XFF\) identifies the originating IP address of a client connecting to a web server through an HTTP proxy or load balancer.| -   Includes
-   Does not include
-   Equals to
-   Does not equal to
-   Length less than
-   Length equals
-   Length more than
-   Does not exist

 |
|Content-Length|The length of the request body in octets \(8-bit bytes\).| -   Value less than
-   Value equals
-   Value more than

 |
|Post-Body|The response content of the request.| -   Includes
-   Does not include
-   Equals to
-   Does not equal to

 |
|Http-Method|The request method, such as GET, POST.| -   Equals to
-   Does not equal to

 |
|Header|The customized header field.| -   Includes
-   Does not include
-   Equals to
-   Does not equal to
-   Length less than
-   Length equals
-   Length more than
-   Does not exist

 |

**Note:** Each rule allows a combination of three conditions at most. Multiple conditions in a rule are connected by “AND”, that is, a request must satisfy all the conditions to match the rule.

**Action**

The following actions can be performed after a rule is matched:

-   **Block**: blocks the request that matches the condition.
-   **Allow**: allows the request that matches the condition.
-   **Warn**: allows the request that matches the condition and triggers an alarm.

**Note:** After specifying **Allow** or **Warn**, you can further decide whether to proceed to perform Web application protection, HTTP flood protection, new intelligent protection, regional blocking, and data risk control.

**Sort rules**

Matching rules follow a specific order. The rule with the higher ranking is matched first.

You can adjust the order of the rules to achieve the optimal protection performance.

## Procedure {#section_m1w_php_p2b .section}

Follow these steps to add a HTTP ACL policy rule for the protected domain name:

**Note:** Before you perform the following operations, make sure that you have added the domain to WAF for protection. For more information, see [WAF deployment guide](reseller.en-US/User Guide/Access WAF/WAF deployment guide.md#).

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  Go to the **Management** \> **Website Configuration** page, and select the region of your WAF instance \(Mainland China or International\).
3.  Select the domain to be configured, and click **Policies**.
4.  Enable **HTTP ACL Policy**, and click **Settings**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15565/15478907517768_en-US.png)

5.  Click **Add Rule**, configure the expected rule, and click **OK**.

    **Note:** For more information about the configuration, see [HTTP ACL policy rule](#). For more information about configuration examples, see [Configuration examples](#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15565/15478907517769_en-US.png)

6.  For a created rule, you can either **Edit** its content or **Delete** it. If multiple rules are created, you can click **Sort Rules** to change the default order of them. By using **Move up**, **Move down**, **Move to top**, and **Move to bottom**, you decide which rule is matched first.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15565/15478907517770_en-US.jpg)


## Configuration examples {#section_u1w_php_p2b .section}

HTTP ACL Policy supports various configuration methods. You can work out the best rules based on your business characteristics. You can also use HTTP ACL policy to fix certain Web vulnerabilities.

Some examples are as follows.

**Configure IP blacklist and whitelist**

Use the following configuration to block all access from 1.1.1.1.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15565/15478907517771_en-US.jpg)

Use the following configuration to allow all access from 2.2.2.0/24.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15565/15478907527772_en-US.jpg)

**Note:** Do not check **Proceed to execute web application attack protection** or **Proceed to execute HTTP flood attack protection**.

For more information, see [Set up IP whitelist and blcaklist](reseller.en-US/User Guide/Protection configuration/Configure a whitelist or blacklist.md#).

**Block malicious requests**

The following figure shows an example of WordPress bounce attack, featuring that the UA contains WordPress.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15565/15478907527773_en-US.png)

Use the following configuration to defend against this type of attack.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15565/15478907527774_en-US.png)

**Block specific URLs**

If a large number of IP addresses are requiring a specific but nonexistent URL, you can use the following configuration.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15565/15478907527775_en-US.png)

**Anti-Leech**

You can configure a Referer-based access condition. For example, if you find abc.blog.sina.com is using a large quantity of pictures on your site, you can use the following configuration.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15565/15478907527776_en-US.png)

