---
keyword: [bot management, application protection, native application]
---

# Configure application protection

Application protection provides secure connections and anti-bot protection for native applications. This function identifies proxies, emulators, and requests with invalid signatures. This topic describes how to configure and enable application protection in the Web Application Firewall \(WAF\) console after you integrate the Anti-Bot SDK into an application.

## Prerequisites

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   **App Protection** is enabled. This feature is a value-added service.
    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   You have integrated the Anti-Bot SDK into the target application. For more information, see [Overview](/intl.en-US/Website Protection Settings/Bot management/Integrated App protection/Overview.md).

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Settings** \> **Website Protection**.

4.  In the upper part of the **Website Protection** page, select the domain name for which you want to configure the whitelist.

    ![Switch Domain Name](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8038549951/p77231.png)

5.  Click the **Bot Management** tab, find the **App Protection** section, and then click **Settings**.

    **Note:** After application protection is enabled, all service requests are checked by the function. You can configure a Bot Management rule so that the requests that match the rule bypass the check. For more information, see [Configure a whitelist for Bot Management](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Bot Management.md).

    ![App Protection](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8428549951/p96117.png)

6.  Create a path protection rule.

    1.  On the **App Protection** page, find the **Interface Protection** section, and click **Add Rule**.

    2.  In the **Add Rule** dialog box that appears, set the following parameters.

        ![Add Rule-Interface Protection](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8428549951/p96118.png)

        **Note:** In the test phase, we recommend that you set **Path** to a forward slash \(`/`\) and **Matching** to **Prefix Match** to match all paths. You can set **Action** to **Monitor**. If the target domain name is a test domain name, you can set Action to **Block**. This allows you to debug the application without affecting your online workloads.

        |Parameter|Description|
        |---------|-----------|
        |**Rule Name**|The name of the rule that you want to create.|
        |**Path Protection Settings**|The path that you need to protect. The following parameters are required:         -   **Path**: The path that you need to protect. A forward slash \(/\) indicates all paths.

**Note:** Signature verification may fail when the body of a POST request exceeds 8 KB. We recommend that you disable SDK protection for API operations that do not require protection, for example, the API operation that is used to upload large images. If you do need to enable SDK protection for an API operation, use a user-defined field.

        -   **Matching**: **Prefix Match**, **Precise Match**, and **Regular Expression Match** are supported.

If you set the value to Prefix Match, all endpoints under the specified path are considered matches. If you set the value to Precise Match, only the specified path is considered a match. If you set the value to Regular Expression Match, paths specified by the regular express are considered matches.

        -   **Parameter**: The parameters that need to be matched if the protected path contains invariable parameters. WAF can use these parameters to filter endpoints more precisely. The parameters are the parts following the question mark \(?\) in the request URL.
Example: The protected URL contains `domain name/? action=login&name=test`. In this case, set **Path** to a forward slash \(/\), **Matching** to Prefix Match, and **Parameter** to name, login, name=test, and action=login. |
        |**Protection Policy**|Protection policy that you want to use.         -   **Invalid Signature**: This policy is selected by default and cannot be cleared. The system checks whether the signatures of requests sent to the specified path are correct. The rule is matched if a signature is incorrect.
        -   **Simulator**: If this policy is selected, the system checks whether the user uses an emulator to initiate requests to the specified path. The rule is matched if a request is initiated from an emulator.
        -   **Proxy**: If this policy is selected, the system checks whether the user uses a proxy to initiate requests to the specified path. We recommend that you select this option. The rule is matched if a request is initiated from a proxy. |
        |**Action**|The action to be performed on requests that match the rule.         -   **Monitor**: records the request but does not block the request.
        -   **Block**: blocks the request and returns a 405 HTTP status code.
**Note:** Before the SDK integration or debugging is completed, do not set Action to Block for domain names used in a production environment. Otherwise, valid requests may be blocked because the SDK is not properly integrated into the application. In the test phase, you can set Action to Monitor to debug the SDK-integrated application based on log data. |
        |**User-defined Field**|When a user-defined field is used, the system verifies the request signature based on the specified request field and field value. By default, the system verifies the signature based on the request body. The verification may fail if the length of the request body exceeds 8 KB. In this case, you can specify a user-defined field to replace the default field for signature verification.

If you select User-defined Field, you can choose Header, Parameter, or Cookie, and then specify the field that is used to verify the request signature. For example, you can choose **Cookie** and then enter DG\_ZUID. This replaces the default body field with the DG\_ZUID field in the request cookie as the field used for signature verification. |

    3.  Click **Confirm**.

7.  Enable version protection.

    You can configure version protection to block requests from non-official applications. You can also use this function to verify the validity of an application.

    **Note:** A version protection policy is required only when you need to verify the validity of an application.

    1.  On the **App Protection** page, find the **Version Protection** section and turn on **Allow Specified Version Requests**.

    2.  In the **Add Rule** dialog box that appears, set the following parameters.

        ![Add a rule-version protection](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9428549951/p96119.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule Name**|The name of the rule that you want to create.|
        |**Valid Version**|The valid versions of an application.         -   **Enter the legal package name**: Enter the name of the valid application package, for example, com.aliyundemo.example.
        -   **Package Signature**: Contact Alibaba Cloud technical support to obtain the package signature. This parameter is optional if the package signature does not need to be verified. In this case, the system verifies only the package name.

**Note:** The **Package Signature** is not the signature of the application certificate.

Click **Add Valid Version** to add more valid versions. You can add a maximum of five valid versions. Package names must be unique. Currently, both iOS and Android applications are supported. You can enter multiple valid versions to match the package names. |
        |**Disposal Method for Illegal Version**|        -   **Monitor**: records the request but does not block the request.
        -   **Block**: blocks the request and returns a 405 HTTP status code. |

    3.  Click **Confirm**.

8.  Enable application protection. In the **App Protection** section, turn on **Status**.

    **Note:** We recommend that you integrate the Anti-Bot SDK into the application, debug the application, and release the new version before you enable application protection to make sure that the protection settings take effect.


