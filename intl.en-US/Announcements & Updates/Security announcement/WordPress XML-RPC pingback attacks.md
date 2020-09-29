# WordPress XML-RPC pingback attacks

This topic describes how to prevent WordPress pingback attacks by using WAF.

## Introduction to WordPress pingback attacks

WordPress is a blog platform that is written in PHP, and a pingback is a plug-in of WordPress. Attackers can use the pingback to initiate WordPress pingback attacks against a website.

![Discussion settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6525338951/p7627.png)

When WordPress pingback attacks occur, a large number of requests are displayed on the server log, and the User-Agent fields of these requests contain WordPress and pingback.

![User-Agent, WordPress, and pingback](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7525338951/p7628.png)

As a variant of HTTP flood attacks, WordPress pingback attacks typically cause the following problems: slow web page loading, high CPU utilization, and no response from servers.

## Use WAF to defend against WordPress pingback attacks

1.  Log on to the [WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.
3.  Click the **Access Control/Throttling** tab.
4.  In the **Custom Protection Policy** section, click **Settings**.
5.  Click **Custom Protection Policy** and add the following two rules.

    -   Block access requests that contain pingback in User-Agent.
        -   **Rule name**: Enter wp1.
        -   **Matching field**: Select User-Agent.
        -   **Logical operator**: Select Includes.
        -   **Matching content**: Enter pingback.
        -   **Action**: Select block.
    -   Block access requests that contain WordPress in User-Agent.
        -   **Rule name**: Enter wp2.
        -   **Matching field**: Select User-Agent.
        -   **Logical operator**: Select Includes.
        -   **Matching content**:Enter WordPress.
        -   **Action**: Select block.
    **Note:** You must add the two rules separately.


