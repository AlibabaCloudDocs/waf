# Data risk control {#concept_dcf_3hl_l2b .concept}

Data risk control helps you protect critical business interfaces \(such as registration, login, activity, and forum\) on your website against fraud.

## Function description {#section_gnl_jhl_l2b .section}

Based on Alibaba Cloud's big data capabilities, Data risk control leverages industry-leading risk decision engines and human-machine identification technologies to protect critical businesses from fraud in different situations. By implementing Alibaba Cloud WAF \(WAF\) for your website, you can access data risk control without any modification to the server or client.

Data risk control is applicable to \(but not limited to\) the following scenarios:

-   Zombie accounts
-   SMS verification code floods
-   Credential stuffing and brute force cracking
-   Malicious snatching, flash sales, bonus hunting, and snatching of red packets
-   Ticket scalping by machines, vote cheating, and malicious voting
-   Spam messages

## Procedure {#section_lnl_jhl_l2b .section}

Follow these steps to enable and configure data risk control:

**Note:** Make sure you have implemented Alibaba Cloud WAF for your website before doing this configuration. For more information, see [Implement Alibaba Cloud WAF](reseller.en-US/User Guide/Access WAF/WAF deployment guide.md#).

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  Go to the **Management** \> **Website Configuration** page and select the region of your WAF instance \(Mainland China or International\).
3.  Locate to the domain name to be configured and click **Policies**.
4.  Under **Data Risk Control**, turn on the Status switch and confirm enabling this feature.

    **Note:** When enabled, Data risk control will inject JavaScript code into your webpage for detecting malicious behaviors, and disable all gzip compression settings. Even if your website uses a non-standard port, no additional configuration is required in data risk control. The JavaScript can be inserted into all webpages \(default\) or specific webpages. For more information, see [Insert JavaScript into specific webpages](#).

5.  Select a protection **Mode**:

    -   **Warning**: Allow all requests and record suspicious requests in logs.
    -   **Protection**: For suspicious requests, ask the client to finish the slider verification to continue.
    **Note:** The warning mode is used by default. Data risk control does not block any request, but injects JavaScript code into webpages to analyze behaviors on the client.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15568/15504702937077_en-US.png)

6.  Click **Settings** to add protection requests or specify the webpages to insert JavaScript.
    -   Add a protection request
        1.  On the **Protection Request** tab page, click **Add Protection Request**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15568/155047029338854_en-US.png)

        2.  In the Add Protection Request dialog box, enter the exact **Protection Request URL** to be protected.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15568/15504702937079_en-US.png)

            **What is the Protection Request URL**

            Protection Request URL is the interface address where business actions are performed instead of the webpage's address. Take the following registration page as an example.

            In this example, the registration page is `www.abc.com/new_user` where users can submit a registration request. To submit a registration request, users must perform the SMS verification and agree to registration. The business interfaces that work in this scenario are `www.abc.com/getsmscode` and `www.abc.com/register.do`.

            In this case, you can add two protection requests to protect URL `www.abc.com/getsmscode` and `www.abc.com/register.do` against SMS interface abuse and zombie registration.

            If you configure the request URL as `www.abc.com/new_user`, a validation slider will pop up when a user accesses the registration page. This will affect the user experience.

            **Note on specifying the Protection Request URL**

            -   The request URL must be an exact URL. A fuzzy match is not supported.

                For example, if `www.test.com/test` is specified, the protection only applied to the www.test.com/test interface. Any subdomain page \(for example www.test.com/test/abc\) is not affected.

            -   You can use /\* to apply data risk control to all paths under a web directory.

                For example, if `www.test.com/book/*` is specified, the protection applied to all paths under `www.test.com/book`. We recommend that you do not apply data risk control to full site \(for example, use `www.abc.com/*` as the protection request URL\). Because users will be required to finish the slider verification even on the homepage, which may reduce the user experience.

            -   We recommend that you do not configure a URL that is normally accessed directly by users without a series of previous visits. Because the user experience will be affected if the user is required to complete the slider verification without a series of previous visits.
            -   Data risk control does not apply to the direct API call scenario, and such calls may be blocked by data risk control. Because API calls are directly initiated machine actions, these calls cannot pass the human-machine identification of data risk control. If the API service is called by a user operation \(such as clicking a button in the console\), data risk control can be applied.
        3.  Click **Confirm**.

            The successfully added protection request takes effect in about ten minutes.

    -   Specify a webpage to insert the Data risk control JavaScript

        In case not all your webpages are compatible with the Data risk control JavaScript, you can insert JavaScript into specific webpages.

        **Note:** Not inserting Data risk control JavaScript into all webpages may weaken the protection effectiveness, because data risk control cannot perceive all user behaviors.

        1.  On the Insert JavaScript into Webpage tab page, click **Insert JavaScript into Specific Webpage**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15568/155047029338852_en-US.png)

        2.  Click **Add Webpage**.

            **Note:** You can add up to 20 webpages.

        3.  In the Add URL dialog box, enter a specific URI \(starting with “/?\) under the domain name to protect, and click **Confirm**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15568/155047029338853_en-US.png)

            Data risk control only inserts the JavaScript into the specified paths.


After data risk control is enabled, you can use the logs feature of Alibaba Cloud WAF to view the protection results. For more information about a log example, see [Data risk control logs](#).

## Use case {#section_znl_jhl_l2b .section}

A user, Tom, has a website with the domain name `www.abc.com`. Common users can register as members at `www.abc.com/register.html`.

Recently, Tom found out that hackers frequently submit registration requests by using malicious scripts. The hackers register a large number of zombie accounts to participate in the prize draw activity that Tom organizes. \(These hackers are known as econnoisseurs.\) These requests are similar to normal requests, where the frequency is not high. Traditional HTTP flood protection methods have problems identifying malicious requests of this kind.

Tom adds the website to WAF for protection, and enables data risk control for the domain name `www.abc.com`. As the business at `www.abc.com/register.html` is the most important to Tom, he configures specific request protection for this URL.

From the moment the configuration takes effect, WAF will do the following:

-   Observes and analyzes whether the behaviors of users who access the domain name `www.abc.com` \(including the homepage and its subpaths\) are abnormal. WAF refers to Alibaba Cloud's reputation database to determine whether this source IP address is risky.
-   A user submits a registration request to `www.abc.com/register.html`. Because this URL is configured for request protection in WAF, WAF will determine if the user is suspicious based on user behavior and reputation from the moment the user accesses the webpage to when the user submits the registration request. For example, if a user doesn't perform any prior actions but directly submits a registration request, the user is suspicious.
    -   If WAF finds the request to be suspicious or this client IP address has a bad record, a validation slider pops up for user authentication. The authenticated user can continue to register.
        -   If the user passes the slider validation in a suspicious way \(for example, use scripts to simulate a real person's sliding process\), WAF will continue to perform other validation tests.
        -   If the user cannot pass the validation, WAF will block this request.
    -   If WAF finds this is a common user based on the preceding behaviors, he or she can finish the registration process without any intervention.

Data risk control is enabled for the entire domain name \(`www.abc.com`\) during the process. This means that **WAF will insert JavaScript into all the pages with this domain name to determine whether the client is trusted**. The real protection and validation are targeted at the interface `www.abc.com/register.html`. WAF will intervene when this interface is requested. If the preceding behaviors of the client are trusted, WAF will not intervene. Otherwise, the user must pass the validation to continue the operation.

## Data risk control logs {#logs .section}

You can use the [Logs](reseller.en-US/User Guide/Protection reports/Log search.md#) feature of Alibaba Cloud WAF to troubleshoot the monitoring and blocking situations of data risk control. For example,

-   The following figure shows the log that the user passed the validation test of data risk control.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15568/15504702937083_en-US.png)

    When a common user who has passed the data risk control validation requests a URL, the URL has a parameter that begins with ua. This request will be sent to the origin and get a normal response.

-   The following figure shows the blocking logs of data risk control.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15568/15504702937084_en-US.png)

    If the user directly requests this interface, the URL typically does not have a parameter that begins with ua \(or a parameter with forged ua\). The request will be blocked by WAF, and the origin response cannot be seen in the corresponding logs.


You can use the **Logs** feature to configure and enable the data risk control interface in **Advanced Search** \> **URL Key Words**. You can use this interface to troubleshoot the blocking logs.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15568/15504702947085_en-US.png)

