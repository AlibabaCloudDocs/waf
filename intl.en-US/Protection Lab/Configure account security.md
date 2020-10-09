---
keyword: [website protection, account security, protection against credential stuffing, brute-force attack, weak password]
---

# Configure account security

Web Application Firewall \(WAF\) supports the account security feature. This feature monitors the endpoints related to user authentication, such as registration and logon endpoints. It also detects events that may threaten user credentials. The events include credential stuffing, brute-force attacks, account registration launched by bots, weak password sniffing, and SMS interface abuse. If you want to use the account security feature, add endpoints that you want to monitor to WAF. You can view detection results in WAF security reports.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   The instance must be of the **Pro** or higher edition. For more information, see [Editions and features](/intl.en-US/Product Introduction/Editions and features.md).
    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

## Background

Before you enable account security, obtain the interface information that is required for configurations. For example, the domain name, the URL where visitors submit user credentials, and the parameters that specify the username and password. Each WAF instance allows you to enable account security for a maximum of three endpoints.

## Add an endpoint

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Lab** \> **Account Security**.

4.  On the **Account Security** page, click **Add Endpoint**.

    If you are using **Account Security** for the first time, skip this step.

    **Note:** Each WAF instance allows you to enable account security for a maximum of three endpoints. If you have already added three endpoints, **Add Endpoint** is dimmed.

5.  Configure the endpoint parameters and click **Save**.

    ![Add an endpoint](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1010240061/p135925.png)

    |Parameter|Description|
    |---------|-----------|
    |**Endpoint to be Detected**|Select the domain name for which you want to enable account security. Then, enter the URI to which user credentials are submitted. Do not enter the URI of the logon page. For example, do not enter `/login.html`. Instead, enter the URI to which the username and password are submitted. |
    |**Request Method**|Select the request method for the endpoint. Valid values: **POST**, **GET**, **PUT**, **DELETE**.|
    |**Account Parameter Name**|Enter the username.|
    |**Password Parameter Name**|Enter the password. If passwords are not required to access the endpoint, leave this parameter empty.|
    |**Protective Action**|Select the action to manage requests that compromise account security. Valid values:     -   **Report**
    -   **Block** |

    Configuration examples:

    -   If the URI of the logon page is `/login.do` and the body of the POST request is `username=Jammy&pwd=123456`, set **Account Parameter Name** to `username` and **Password Parameter Name** to `pwd`. Keep other settings the same as those in the preceding figure.
    -   If the parameters that specify user credentials are included in the URL of a GET request, for example, `/login.do? username=Jammy&pwd=123456`, set **Request Method** to **GET**. Keep other settings the same as those in the preceding figure.
    -   If passwords are not required to access the endpoint, for example, a registration endpoint, set **Account Parameter Name** and leave **Password Parameter Name** empty.
    -   If a mobile number is required to access the endpoint, enter the mobile number for the account parameter. Assume that the URL is `/sendsms.do? mobile=13811111111`. In this case, set **Endpoint to be Detected** to `/sendsms.do` and **Account Parameter Name** to `mobile`, and leave **Password Parameter Name** empty.
    After you add the endpoint, WAF automatically dispatches detection tasks. If the network traffic of the endpoint meets the detection conditions, account risks are reported within a few hours.

    **Note:** After account security is enabled, all requests destined for websites are checked by the account security rule. You can configure a whitelist in data security to allow the requests that match conditions to bypass the account security rule. For more information, see [Configure the data security whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the data security whitelist.md).


## View account security reports

If you want to view account security reports, find the endpoint on the **Account Security** page, and click **View Report** in the Actions column. You can also view security reports on the **Security report** page in the WAF console.

The following procedure describes how to view security reports on the **Security report** page.

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, click **Security report**.

4.  On the **Web Security** tab, click **Account Security** and select the domain name, URI, and data range \(**Yesterday**, **Today**, **7 Days**, or **30 Days**\) to check for account security risks.

    ![Account Security tab ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4833219951/p77282.png)

    The following table describes the fields in an account security report.

    |Field|Description|
    |-----|-----------|
    |**Endpoint**|The URI where account risks are detected by WAF.|
    |**Domain**|The domain name to which the URI belongs.|
    |**Malicious Requests Occurred During**|The time period during which account risks are detected.|
    |**Blocked Requests**|The number of requests blocked based on WAF protection rules during the time period displayed in the **Malicious Requests Occurred During** field. The WAF protection rules indicate those effective rules, including rules for web application protection, precise access control, HTTP flood protection, and blocked regions. The proportion of blocked requests indicates the account security status of the endpoint. |
    |**Total Requests**|The total number of requests sent to the endpoint during the time period displayed in the **Malicious Requests Occurred During** field.|
    |**Alert Triggered By**|The reason why the alert is triggered. Possible reasons:     -   A request fits the behavior model of credential stuffing or brute-force attacks.
    -   The traffic baseline of the endpoint is abnormal during the displayed time period.
    -   A large number of requests sent to the endpoint match the rules described in the threat intelligence library during the displayed time period.
    -   Weak passwords are detected in a large number of requests sent to the endpoint during the displayed time period. In this case, credential stuffing and brute-force attacks may occur. |


## References

The account security feature only detects account risks. Due to the variations of businesses and technologies, we recommend that you select security services as required to better safeguard your business. For more information, see [Account security best practices](/intl.en-US/Website Protection Settings/Best practices for protection settings/Account security best practices.md).

