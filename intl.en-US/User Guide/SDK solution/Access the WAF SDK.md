# Access the WAF SDK {#concept_kvh_khq_p2b .concept}

WAF SDK is a programming package designed specifically for native Apps. It offers security protection such as trusted communications, anti-fake-orders detection, and so on. WAF SDK can effectively identify high-risk mobile phones, ModemPOOLs, and other characteristics.

## Scenarios {#section_q2p_khq_p2b .section}

After accessing the SDK, your App can get the same trusted communication technologies as the clients such as Tmall, Taobao, and Alipay. WAF SDK also shares Alibaba Group’s fingerprint database of malicious devices against black/grey industries and econnoisseurs, and fundamentally resolves the security issues at the App end.

WAF SDK can resolve the following **native App** side issues:

-   Malicious registration, account credential enumeration attacks, and brute-force attacks
-   Large volume traffic HTTP flood attacks against Apps
-   Malicious attacks against SMS/CAPTCHA interfaces
-   Bonus hunting and red envelopes snatching
-   Seckill and time-and-purchase-limited goods
-   Malicious check and brush votes \(such as air tickets or hotel booking information\)
-   Value consulting crawls \(such as price, credit information, financing, and fiction\)
-   Machine voting
-   Spams and malicious comments

## How to access WAF SDK {#section_s2p_khq_p2b .section}

Follow these steps to access WAF SDK:

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).
2.  Go to the **Management** \> **Website Configuration** page, and add the App domain to the protection list to enable WAF protection for it. For more information, see [Set up WAF console](../../../../intl.en-US/Quick Start/Step1: Automatically add a website configuration.md#).
3.  At your DNS service provider, add a CNAME record by using the WAF-generated Cname address as the record value. For more information, see [Update DNS settings](../../../../intl.en-US/Quick Start/Step 2: Update the DNS settings.md#).
4.  Integrate the SDK components provided by WAF on your App. This operation usually takes 1-2 days.

    **Note:** The SDK integration does not require any modification on the server side. WAF can filter out malicious traffic and only send the valid request back to the origin. The pressure of malicious requests is also handled by WAF.

    For more information about how to integrate the SDK components on your App, see the following documents:

    -   [iOS integration manual](intl.en-US/User Guide/SDK solution/iOS integration manual.md#)
    -   [Android integration manual](intl.en-US/User Guide/SDK solution/Android integration manual.md#)
5.  Contact WAF support to help test your integrated App.
6.  Release a new version of your App to enable the SDK protection.

