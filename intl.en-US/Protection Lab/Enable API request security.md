# Enable API request security

You can use the API security function to upload a custom API rule file to ensure only requests that comply with the rules are executed. This protects your website assets from threats such as tampering and replay attacks.

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   If the instance is deployed in **mainland China**, the instance must be of the **Business** or higher edition.
    -   If the instance is deployed **outside mainland China**, the instance must be of the **Enterprise** or higher edition.
    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

After you upload the API rule file, the API security function automatically parses the content of the file, and verifies access requests based on the rules. WAF either blocks API requests that do not comply with the rules or generates alerts for the requests.

Typically, API access requests that have inconsistent request paths or contain parameter values out of the valid range are identified as invalid.

**Note:** The API security function is now under public preview and is provided free of charge.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **Protection Lab** \> **API Request Security**.

4.  On the **API Request Security** page, click **Switch Domain Name** and switch to the domain name that you want to protect.

5.  Click **Import**.

6.  In the dialog box that appears, select the API rule file to be uploaded and click **Open**.

    **Note:** The file has the following restrictions:

    -   The file size does not exceed 128 KB.
    -   The file must be in the Swagger 2.0-compliant XML or JSON format.

        [Swagger](https://swagger.io/docs/specification/about/?spm=a2c4g.11186623.2.15.f37011db3xVmge) is a specification used to describe API definitions. It is widely used to define and describe APIs for backend services. For more information about Swagger extensions, see [Import Swagger files to create APIs]().

    After the API rule file is imported, the file content is automatically parsed and displayed in the rule list on the **API Request Security** page.

    ![API security rules](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4352563951/p120945.png)

    On the **API Request Security** page, you can:

    -   View the status of API security rules.

        After the file is imported, the status of the API security rule is **Enabled** and the protection status is **Warn**. In this case, WAF generates an alert if an invalid request is detected. You can view the alert information on the **API Request Security** tab on the **Security report** page.

        ![Security reports-API security](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5352563951/p120947.png)

    -   Modify the status.

        In the rule list, you can turn on or off the switch in the **Status** column to enable or disable the API rule. If you disable the API security rule \(**Disabled**\), WAF no longer detects requests of this API or generates alerts.

    -   Modify the protection status.

        In the **Protection Status** column, you can click either **Warn** or **Block**. If you click **Block**, WAF blocks all invalid access requests to this API.

    -   View API information.

        In the **Operation** column, click **Details** to view the API information. The information includes the URL, request method, parameters, parameter values, description, and whether the parameters are required.


