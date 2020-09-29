---
keyword: [protection rule group, web application protection, RegEx Protection Engine, Web Application Firewall]
---

# Customize protection rule groups

You can use default protection rule groups provided by Web Application Firewall \(WAF\) to customize your rule groups for a specific protection feature, such as web application protection, known as RegEx Protection Engine. If the default protection rule groups cannot meet your business requirements, we recommend that you customize protection rule groups to protect your website.

-   A WAF instance is purchased. The instance must meet the following requirements:

    -   The instance is billed on a subscription basis.
    -   If the instance is deployed in **mainland China**, the instance must be of the **Business** edition or higher.
    -   If the instance is deployed **outside mainland China**, the instance must be of the **Enterprise** edition or higher.
    For more information, see [Purchase a WAF instance](/intl.en-US/Pricing/Subscription/Purchase a WAF instance.md).

-   Your website is added to the WAF console. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add domain names.md).

You can customize protection rule groups only for the **RegEx Protection Engine** feature. For more information, see [Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md).

## Use a custom rule group

To use a custom rule group, you must complete the following steps:

1.  [Create a rule group](#section_yuu_ino_24x): Create a custom rule group for a specific protection feature.
2.  [Apply the rule group](#section_ex7_5rn_tok): Apply the created rule group to your website.

## Create a rule group

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **System Management** \> **Protection Rule Group**.

4.  On the **Protection Rule Group** page, click the tab of the protection feature that you want to manage.

    **Note:** You can skip this step because only the **RegEx Protection Engine** feature supports protection rule groups. You are directly redirected to the **Web Application Protection** tab.

    The **Web Application Protection** tab displays the default and custom rule groups.

    -   Default rule group: The name of a default rule group can be **Loose rule group**, **Medium rule group**, or **Strict rule group**.

        You can click the number in the **Built-in Rule Number** column to view information about the built-in rules.

        ![Number of built-in rules](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5628549951/p128584.png)

        **Note:** Default rule groups cannot be edited or deleted.

    -   Custom rule group: You can create a rule group on the Protection Rule Group page.
5.  Click **Create Rule Group**.

    **Note:** You can create a maximum of 10 rule groups for the web application protection feature.

6.  Specify the parameters in the **Create Rule Group** wizard.

    1.  **Specify rule information**. Configure the following parameters and click **Next: Apply to Websites**.

        ![Create Rule Group](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5628549951/p99765.png)

        |Parameter|Description|
        |---------|-----------|
        |**Rule Group Name**|Enter a name for the rule group. The rule group name is used to identify the rule group. We recommend that you enter an informative name. |
        |**Rule Group Template**|Select a rule group template from which you want to select rules for the rule group. Valid values:         -   **Strict rule group**: contains 1,068 rules by default.
        -   **Medium rule group**: contains 1,039 rules by default.
        -   **Loose rule group**: contains 1,031 rules by default.
Different rule group templates contain different rules. After you select the rule group template and turn on the Automatic Update switch, each time a rule in the rule group template is updated, the rule is also updated in the created rule group. |
        |**Description**|Enter a description for the rule group.|
        |**Automatic Update**|If you turn on this switch, each time a rule in the rule group template is updated, the rule is also updated in the created rule group. **Note:** Some custom rule groups do not support the automatic update feature. In this case, we recommend that you create rule groups to replace these rule groups. |
        |**Select Rule**|Select a rule for the rule group.The **Selected Rules** tab lists all rules in the rule group template that you select. You must select rules that are not applicable or may cause false positives, and then click **Remove Selected Rules**.

You can use the filter or search feature to find rules you want to manage. You can filter rules by **Protection Type**, **Application Type**, or **Risk Level** or enter a rule name or ID to search for a rule.

        -   **Risk Level**: indicates the risk level of web attacks. Valid values: **High**, **Medium**, and **Low**.
        -   **Protection Type**: indicates the type of web attacks. Valid values: **SQL Injection**, **Cross-site Script**, **Code Execution**, **CRLF**, **Local File Inclusion**, **Remote File Inclusion**, **Webshell**, **CSRF**, and **Others**.
        -   **Application Type**: indicates the type of the protected web application. Valid values: **Common**, **Wordpress**, **Dedecms**, **Discuz**, **Phpcms**, **Ecshop**, **Shopex**, **Drupal**, **Joomla**, **Metinfo**, **Struts2**, **Spring Boot**, **Jboss**, **Weblogic**, **Websphere**, **Tomcat**, **Elastic Search**, **Thinkphp**, **Fastjson**, **ImageMagick**, **PHPwind**, **phpMyAdmin**, and **Others**. |

        **Note:** If you do not want to apply a rule group immediately after you create it, click **Save**. You can edit the group again after you complete the step.

    2.  **Apply to a website**. Select the website to which you want to apply the new rule group from the **Websites not Added to WAF** section and add them to the **Websites Added to WAF** section.

        **Note:** You must apply one rule group to each website.

        ![Apply to Website](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5628549951/p103158.png)

    3.  Click **Save**.

    You can view the new rule group in the rule group list and select the website to which you want to apply the rule group. For more information, see [Apply the rule group](#section_ex7_5rn_tok).

    After you create the rule group, you can view the creation time of a rule group in the **Updated On** column on the **Protection Rule Group** page and determine whether to update the rule group.


## Apply the rule group

After you create a custom rule group, you can apply it by using one of the following methods:

-   On the **Protection Rule Group** page, apply the rule group to a website. The following steps are provided for this scenario.
-   On the **Website Protection** page, select a custom rule group from the Protection Rule Group drop-down list in the RegEx Protection Engine card.

    ![Protection Rule Group](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5628549951/p100333.png)

    For more information, see [Configure the RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md).


1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

3.  In the left-side navigation pane, choose **System Management** \> **Protection Rule Group**.

4.  On the **Protection Rule Group** page, click the tab of protection feature you want to manage.

    **Note:** You can skip this step because only the **web application protection** feature supports the rule group. You are directly redirected to the **Web Application Protection** tab.****

5.  In the **Protection Rule Group** list on the **Web Application Protection** tab, find the rule group that you want to apply and click **Apply to Website** in the Action column.

6.  On the **Apply to Website** page, select the website to which you want to apply the rule group from the **Websites not Added to WAF** section, add them to the **Websites Added to WAF** section, and then click **Save**.

    **Note:** You must apply one rule group to each website.

    ![Apply to Website](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5628549951/p33864.png)

    After you complete the operation, you can view the website in the **Website** column on the **Protection Rule Group** page.

    ![Website](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5628549951/p103185.png)


## Related operations

You can perform the following operations to manage the created rule group on the **Protection Rule Group** page:

-   **Copy**: allows you to copy the configurations of the rule group.

    The following figure shows the Copy Rule Group page. On this page, you can modify **Rule Group Name**, **Description**, and **Automatic Update**, but cannot modify **Rule Group Template** and rule settings. If you need to modify the rule settings, we recommend that you copy the rule group and modify the rule settings in the copied rule group.

    ![Create Rule Group-Copy](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5628549951/p99766.png)

    **Note:** Some custom rule groups cannot be copied because they do not support the automatic update feature. In this case, we recommend that you create rule groups to replace these rule groups.

    ![Rule groups that cannot be copied](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5628549951/p103172.png)

-   **Edit**: allows you to modify the name, description, and rule settings of the rule group. Default rules cannot be edited.
-   **Delete**: allows you to delete the rule group. Default rules cannot be deleted.

    Before you delete a custom rule group, make sure that it is not applied to any website. If the rule group is applied to a website, apply a different rule group to the website before you delete the rule group.


