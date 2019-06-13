# Custom rule groups {#concept_j4x_f35_1gb .concept}

A rule group is a combination of the built-in protection rules of Alibaba Cloud WAF that makes up an optional policy for a specific protection function. You can create and apply a custom rule group for a specific protection function of WAF to achieve dedicated protection effect.

**Note:** Custom rule group is included in the Enterprise subscription plan. Currently, this feature only applies to Web application protection. For more information about the default protection policy of Web application protection, see [Web application protection](intl.en-US/User Guide/Configuration/Web application protection.md#).

## View the build-in protection rules {#section_pwd_z45_1gb .section}

Before you create a custom rule group, we recommend that you get yourself familiar with the build-in protection rules of Alibaba Cloud WAF.

**Procedure** 

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China** or **International**.
3.  On the **Setting** \> **Customize Rule Groups** page, select the protection function to view. Currently, only **Web Application Protection** is supported.
4.  Click the **Built-in Rule Set** page tab to view the protection rules of Web application protection. Each rule consists of the following information:

    -   **Rule**: The name of this rule.
    -   **Rule ID**: The unique identifier of this rule.
    -   **Risk Level**: The risk level of the vulnerability that is defended against by this rule.
    -   **Application Type**: The application that is protected by this rule. Options: Common, Wordpress, Discuz, Tomcat, phpMyAdmin, and more.
    -   **Protection Type**: The type of the web attack that is defended against. Options: SQL Injection, Cross-site Script, Code Execution, CRLF, Local File Inclusion, Remote File Inclusion, Webshell, CSRF, and Others.
    -   **Description**: The description of this rule, including web attack description, code to inspect, and on which selector to run the inspection.

        **Note:** You can view the detailed description of a rule by placing the pointer on a description.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/77901/156042402433856_en-US.png)

5.  \(Optional\) Use filters and search to locate to a specific rule.
    -   You can filter rules by protection type, application type, and risk level.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/77901/156042402433857_en-US.png)

    -   You can search for rules by rule name or ID.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/77901/156042402533858_en-US.png)


## Add a custom rule group {#add .section}

You can create a custom rule group for a specific protection function \(only Web Application Protection is supported now\). When you are creating a custom rule group, you select built-in rules to add to the group to compose a dedicated protection policy.

**Procedure** 

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China** or **International**.
3.  On the **Setting** \> **Customize Rule Groups** page, select the protection function to be operated. Currently, only **Web Application Protection** is supported.

    The Customize Rule Groups page displays all rule groups of Web Application Protection, among which the rule group IDs of **1011**, **1012**, and **1013** are the default rule groups.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/77901/156042402533853_en-US.png)

4.  Add a custom rule group by creating one or coping an existing one.

    **Note:** You can add up to 10 custom rule groups for Web Application Protection.

    -   Create a custom rule group
        1.  Click **Add Rule Group**.
        2.  On the Add Rule Group page, complete the following configuration.
            -   **Rule Group Name**: Required. Name this rule group. We recommend that you use a name with an indicative meaning, because this name will display in the drop down box for you to select a protection policy.
            -   **Description**: Optional. Add a description for this rule group.
            -   **Rules**: Select rules from the left-side area of all built-in rules to add to the right-side area of this rule group’s rules.

                For more information about rules, see [Step 4 of View the built-in rules](#). You can locate to a specific rule by using filters and search. For more information, see [Step 5 of View the built-in rules](#).

        3.  Click **Confirm** to add the rule group.

            The newly created rule group is assigned with a rule group ID.

    -   Copy an existing rule group
        1.  Locate to the rule group to be copied and click **Copy**.
        2.  On the Add Rule Group page, enter a new name in **Rule Group Name**, and confirm the inherited rules. \(You cannot add or delete rules in this step.\)
        3.  Click **Confirm** to add the rule group.

            The newly copied rule group is assigned with a rule group ID. See [Edit a custom rule group](#) to add or delete rules in this rule group.


## Apply a custom rule group to websites {#apply .section}

When a rule group is added, you can enable it in the protection Policies of a specific website or enable it for bulk domains in the Customize Rule Groups page.

**Procedure**

Taking Web Application Protection as an example, you can follow these steps to enable or disable a custom rule group in website configuration.

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China** or **International**.
3.  On the **Management** \> **Website Configuration** page, select the domain name to be configured and click **Policies**.
4.  Under **Web Application Protection**, enable the protection.
5.  Expand the **Mode of protection policies** drop down box, and select the newly added rule group by name. \(In this example, select **custom**.\)

    To disable a custom rule group, you select a default policy in the **Mode of protecting policy** drop down box. In this example, select Strict rule group, Medium rule group, or Loose rule group.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/77901/156042402533861_en-US.png)


Taking Web Application Protection as an example, follow these steps to apply a custom rule group to bulk domains:

**Note:** To disable a rule group, we recommend that you go to the protection Polices page of the specific domain.

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China** or **International**.
3.  On the **Setting** \> **Customize Rule Groups** page, select the protection function to be operated. Currently, only **Web Application Protection** is supported.
4.  On the Customize Rule Groups tab page, locate to the rule group to be operated, and click **Apply to Website**.
5.  Check the website to apply the specified rule group and click **Confirm**.

    You can search for domains.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/77901/156042402533864_en-US.png)


## Edit a custom rule group {#edit .section}

When a custom rule group is successfully added, you can edit it to manage the rules or change its name and description. The default rule group cannot be edited.

**Procedure** 

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China** or **International**.
3.  On the **Setting** \> **Customize Rule Groups** page, select the protection function to be operated. Currently, only **Web Application Protection** is supported.
4.  Locate to the rule group to be operated, and click **Edit**.
5.  On the Edit Rule Group page, re-configure the rule group. For more information, see [Add a custom rule group](#).
6.  Click **Confirm** to update the rule group.

## Delete a custom rule group {#delete .section}

For an unnecessary custom rule group, you can delete it. Before deleting a rule group, you must make sure that the rule group has not been applied to any website. The default rule group cannot be deleted.

**Procedure** 

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf).
2.  On the top of the page, select the region: **Mainland China** or **International**.
3.  On the **Setting** \> **Customize Rule Groups** page, select the protection function to be operated. Currently, only **Web Application Protection** is supported.
4.  Locate to the rule group to be deleted, and click **Delete**.
5.  In the Tips dialog box, click **Confirm**.

    **Note:** If the group has been applied to websites, you must disable it from the website configuration to continue the deletion. For more information, see [Apply a custom rule group to websites](#).


