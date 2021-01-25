# Best practices for using custom rule groups to provide enhanced protection

If you find that RegEx Protection Engine of WAF blocks normal requests to your website, you can customize protection rule groups to avoid this issue.

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   If the instance is deployed in **mainland China**, the instance must be of the **Business** edition or higher.
    -   If the instance is deployed **outside mainland China**, the instance must be of the **Enterprise** edition or higher.
    For more information, see [Purchase a WAF instance](/intl.en-US/Billing and Service Activation/Subscription/Purchase a WAF instance.md).

-   Your website is added to WAF. For more information, see [Add websites](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).

To address this issue, you must identify the protection rule that causes the issue, create a custom rule group for the affected domain name, and then remove the protection rule from the custom rule group.

## Procedure

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, click **Security report**.

4.  Identify the ID of the protection rule that causes false positives.

    1.  On the **Web Security** tab, click **Web Intrusion Prevention**, select the target domain name, and select **Regular Protection** in the lower part of the page to view attack records.

        ![The ID of the protection rule that causes false positives ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3728549951/p34042.png)

    2.  In the attack record list, find the false positive record and record the rule ID. You can search for the record by using the attack IP address.

5.  In the left-side navigation pane, choose **System Management** \> **Protection Rule Group**.

6.  Create a custom rule group and remove the protection rule from the rule group.

    1.  In the rule group list on the **Web Application Protection** tab, find the rule group that applies to the affected domain name.

        **Note:** To find the rule group, search for the affected domain name in the **Website** column.

        ![Website](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3728549951/p129926.png)

    2.  Click **Copy** in the Action column. Assume that the **Medium rule group** causes the issue.

    3.  On the **Copy Rule Group** page, modify **Rule Group Name**, turn on **Automatic Update**, and click **Save**. You can change the rule group name to medium rule group-remove false positive rule.

        ![Copy rule group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3728549951/p129927.png)

        After you copy the rule group, you can view it in the rule group list.

        ![Rule group that you copy](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3728549951/p129929.png)

    4.  Find the rule group that you copy and click **Edit** in the Action column.

    5.  On the **Edit Rule Group** page, search for the rule that causes false positives by using the **rule ID**, select the rule, and then click **Remove Selected Rules**.

        **Note:** Before you remove a protection rule from a custom rule group, make sure that you select the exact rule that blocks normal requests.

        ![Edit rule group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3728549951/p129928.png)

    6.  Click **Save**.

7.  Apply the custom rule group to your website.

    1.  Find the rule group that you copy and click **Apply to Website** in the Action column.

    2.  On the **Apply to Website** page, add the affected domain name to the **Websites Added to WAF** section and click **Save**.

        ![Apply to website](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3728549951/p129930.png)

    After you apply the custom rule group, you can go to the **Website Protection** page and view the **RegEx Protection Engine** settings. The **Protection Rule Group** changes to the custom rule group that you apply. For more information, see [Configure the protection rules engine](/intl.en-US/Website Protection Settings/Web security/Configure the protection rules engine.md).

    ![Custom rule groups](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3728549951/p34119.png)

    When the website receives the same access requests again, WAF does not block the requests.

    **Note:** If the requests are still blocked, make sure you identify the correct ID of the protection rule that causes false positives and remove this rule from the custom rule group.


