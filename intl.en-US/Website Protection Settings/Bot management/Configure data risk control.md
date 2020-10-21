---
keyword: [Web Application Firewall, WAF, website protection, data security, data risk control, crawler]
---

# Configure data risk control

After you add a website to Web Application Firewall \(WAF\), you can enable data risk control. Data risk control helps you protect crucial website services, such as registrations, logons, campaigns, and forums, against attacks. You can customize data risk control rules based on your requirements.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:
    -   The instance is billed on a subscription basis.
        -   The instance is deployed in **mainland China**.

            **Note:** Instances deployed **outside mainland China** do not support data risk control.

        -   The **Bot Management** feature is enabled.
-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background information

Data risk control is based on Alibaba Cloud big data. It uses industry-leading engines for risk decision-making and integrates human-machine identification technologies to protect crucial services in different scenarios against attacks. To use data risk control, you only need to add your website to WAF, without the need to configure the server or client.

Data risk control is suitable for a wide array of scenarios, including but not limited to: spam registration,SMS verification code abuse, credential stuffing, brute-force attacks, fraud in flash sales, second kills, bargain manipulation, red envelope lucky draws, ticket snapping by using bots, vote rigging, and spamming.

The following figure shows how data risk control protects your website. For more information about scenarios and protection effects of data risk control, see [Examples](#section_5xy_y13_yja).

## Compatibility

Data risk control is supported only by web pages or HTML5 environments. In some cases, the JavaScript plug-in inserted into web pages may be incompatible with the web pages and this causes errors during CAPTCHA verification. Web pages that may encounter incompatibility with data risk control include:

-   Static web pages that can be accessed by using their URLs, such as HTML details page, shared pages, website homepages, and documents. Web pages that are redirected by modifying `location.href` or by using the `window.open` method and the anchor tag \(<a\>\).
-   Web pages where you can rewrite service code and submit requests by using request methods or custom methods, such as submitting forms, rewriting XMLHttpRequest \(XHR\), and sending custom Ajax requests.
-   Service code that makes use of webhooks.

After you enable data risk control, we recommend that you choose the warn mode and use data risk control together with Log Service for WAF to run a compatibility test. For more information, see [Overview](/intl.en-US/Log Management/Log service/Overview.md).

If data risk control is incompatible with your website, use [Alibaba Cloud Human-Machine Validation](https://promotion.aliyun.com/ntms/act/captchaIntroAndDemo.html) together with WAF to protect your website.

To protect native applications, we recommend that you use the Anti-Bot SDK. For more information, see [Configure application protection](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Configure application protection.md).

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Bot Management** tab, find the **Data Risk Control** section, and then click **Settings**.

    ![Data Risk Control](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4428549951/p74243.png)

    |Parameter|Description|
    |---------|-----------|
    |**Status**|Enable or disable data risk control. After you enable data risk control for a website, WAF inserts a JavaScript plug-in into specific or all web pages of the website. Reactive elements in the web pages are returned to visitors as compressed files that are not in the GZIP format. Even if your website uses non-standard ports, no further configurations are required. **Note:**

    -   You must enable data risk control before you set the mode and configure protection rules.
    -   When data risk control is enabled, all requests destined for your website are checked by the function. You can configure a Bot Management rule so that the requests that match the rule bypass the check. For more information, see [Configure a whitelist for Bot Management](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Bot Management.md). |
    |**Mode**|The mode for data risk control. Valid values:     -   **Strict Interception**: If WAF detects that your website is under attack, requests are required to pass a strict multi-factor authentication.
    -   **Block**: If WAF detects that your website is under attack, requests are required to pass a multi-factor authentication.
    -   **Warn**: If WAF detects that the website is under attack, requests are forwarded to your website but events related to the requests are recorded. You can view detailed information in risk reports.

**Note:** The Mode parameter is set to Warn by default. In this mode, data risk control does not block requests. However, WAF inserts a JavaScript plug-in into static web pages to analyze client behaviors. |

6.  Add a protection request for data risk control.

    1.  On the **Data Risk Control** page, click the **Protection Request** tab and click **Add Protection Request**.

    2.  In the **Add Protection Request** dialog box, enter the URL that you want to protect in the **Protection Request URL** field.

        For more information, see [Introduction to a protected URL in a protection request](#section_wpl_d2z_pbe).

        ![Add a protection request for data risk control](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4428549951/p74258.png)

    3.  Click **Confirm**.

    A newly added protection request takes effect in about 10 minutes. You can view the newly added protection requests in the request list, and modify or delete them based on your requirements.

7.  Specify the web page into which you want to insert the JavaScript plug-in.

    Some code of web pages may be incompatible with the JavaScript plug-in. In this case, we recommend that you insert the JavaScript plug-in into specific pages that are compatible with the plug-in.

    **Note:** When the JavaScript plug-in is inserted into specific web pages, data risk control may fail to obtain all visitor behaviors. This affects the effectiveness of data risk control.

    1.  On the **Data Risk Control** page, click the **Insert JavaScript into Webpage** tab.

    2.  Select **Insert JavaScript into Specific Webpage** and click **Add Webpage**.

        ![Insert the JavaScript plug-in into specific web pages](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4428549951/p74259.png)

        **Note:** You can insert the JavaScript plug-in into a maximum of 20 web pages.

    3.  In the **Add URL** dialog box, enter the URL into which you want to insert the JavaScript plug-in and click **Confirm**. The URL must start with a forward slash \(/\).

        ![Add a URL](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4428549951/p74260.png)

    After you add the URL, data risk control inserts the JavaScript plug-in into all web pages under this URL.


After data risk control is enabled, you can use Log Service for WAF to monitor the protection effect. For more information, see [View protection results](#section_mr1_oeq_rlg).

## Introduction to a protected URL in a protection request

A protected URL in a protection request is the endpoint where operations are performed on a service. It is not the URL of the web page. As shown in the following figure, the URL of the registration page is `www.abc.com/new_user`. The endpoint where you can obtain verification codes is `www.abc.com/getsmscode`, and the endpoint where you can register is `www.abc.com/register.do`.

In this example, you must add protection requests to protect the endpoints `www.abc.com/getsmscode` and `www.abc.com/register.do`. This way, WAF protects these URLs from SMS interface abuse and spam registration. If you set the protected URL to `www.abc.com/new_user`, regular visitors are also required to pass CAPTCHA verification, which may adversely affect the user experience.

Usage notes of protected URLs

-   The protected URL must be exact. Fuzzy match is not supported.

    If you set the protected URL to `www.test.com/test`, data risk control filters only requests that are sent to this URL. Data risk control does not filter requests sent to the sub-directories of this URL.

-   Data risk control protects website directories.

    If you set the protected URL to `www.abc.com/book/*`, data risk control filters the requests that are sent to all web pages under `www.abc.com/book`. We recommend that you do not set data risk control to monitor the entire website. If you set the protected URL to `www.abc.com/*`, regular visitors need to pass CAPTCHA verification to visit the website homepage. This adversely affects the user experience.

-   Requests that are sent to a protected URL always trigger CAPTCHA verification. Make sure that the protected URL is not directly requested by regular visitors in normal cases. Otherwise, regular visitors must pass multi-factor authentication before they can visit the URL.
-   Data risk control does not apply to websites that provide API calling services. API calls are directly initiated machine actions and cannot pass the CAPTCHA verification of data risk control. However, if the API operation is called after regular visitors click a button on a page, you can implement data risk control.

## View protection results

You can use Log Service for WAF to view the protection results.

-   Allowed requests

    The following figure shows a request that passes data risk control verification. The URL of a request from a regular visitor that passes data risk control verification includes a parameter that starts with u\_a. The request is forwarded to the origin server by WAF and the origin server returns a response to the visitor.

    ![Logs, data risk control, and passed verification](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4428549951/p7083.png)

-   Blocked requests

    The following figure shows a request that is blocked by data risk control. Typically, a request directly sent to the URL of a service does not start with u\_a, or starts with a forged u\_a parameter. WAF blocks this type of request, and the origin server does not return responses.

    ![Logs, data risk control, block](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5428549951/p7084.png)


After you enable Log Service for WAF, choose **Advanced Search** \> **URL Key Words** and set the endpoints to be protected by data risk control. This function helps you monitor the status of data risk control and records blocked requests. For more information, see [Use full logs](/intl.en-US/Log Management/Use full logs.md).

## Examples

User Tom has a website and the website domain name is `www.abc.com`. Regular visitors can register as website members at `www.abc.com/register.html`. Tom notices that attackers can use malicious scripts to submit registration requests and create accounts. These accounts are used to participate in prize draws held by the website. The registration requests are highly similar to normal requests, and the request rate is maintained at a normal level. The HTTP flood protection policy fails to identify this type of malicious request.

Sample configurations

Tom configures WAF for the website and enables data risk control for the domain name `www.abc.com`. The URL of the most crucial registration service is `www.abc.com/register.html`. Therefore, Tom sets the protected URL to this URL.

Protection results

After the configurations take effect, data risk control inserts a JavaScript plug-in into all web pages of the website to monitor and analyze the behaviors of each visitor that visits `www.abc.com`, including the homepage subpages. Data risk control then determines whether a visitor behavior is normal. Data risk control also determines whether a source IP address is malicious based on the Alibaba Cloud big data reputation library.

When a visitor sends a registration request to `www.abc.com/register.html`, WAF determines whether the visitor is a potential attacker based on the visitor behavioral data generated from the time the visitor visits the website to the time the visitor submits the registration request. For example, if a visitor directly submits a registration request without performing other operations in advance, the request is identified as suspicious.

-   If data risk control determines that the request is from a regular visitor based on previous visitor behaviors, the visitor can register accounts without verification.
-   If data risk control identifies a request as potentially malicious, or the source IP address has a record of sending malicious requests, CAPTCHA is triggered to verify the identity of the visitor. Only visitors that pass the verification can register accounts.
    -   If CAPTCHA verification captures suspicious visitor behaviors, such as using scripts to simulate real visitor behaviors to pass CAPTCHA verification, data risk control requires two-factor authentication to verify the visitor identity until the visitor passes verification and is identified as a regular visitor.
    -   If the visitor fails the verification, data risk control blocks the request.

During this process, data risk control is enabled for the entire website \(`www.abc.com`\). Data risk control inserts a JavaScript plug-in into all web pages of the website to analyze visitor behaviors. However, protection and verification are enabled for only `www.abc.com/register.html` where visitors submit registration requests. Data risk control is triggered only after a registration request is submitted.

