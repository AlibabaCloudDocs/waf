# Use custom rule groups to prevent false positives {#concept_kt4_1gt_bgb .concept}

When you find that normal requests to your site are mistakenly blocked by WAF, you can set custom rule groups to prevent this issue.

When a normal request to your site is blocked by WAF, you can identify the rule that causes the issue and create a custom rule group for the affected domain. You can then remove the specified rule to resolve the issue.

**Note:** Before you remove a rule, make sure that the requests blocked according to this rule are normal requests.

## Identify the ID of the protection rule that causes false positives {#section_wmq_1mt_bgb .section}

1.  Log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf).
2.  Select **Mainland China** or **International**.
3.  In the left-side navigation pane, choose **Reports** \> **Reports** and click **Attack Protection**.
4.  Click **Web Application Attack** and select the affected domain from the drop-down list. Then click **Attack Details**.
5.  You can select a time range or source IP to search for records you are interested in. The record contains the ID of the protection rule that causes false positives.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78570/155437578434042_en-US.png)


## Create custom group rules for a domain {#section_dd5_j4t_bgb .section}

1.  In the left-side navigation pane, choose **Management** \> **Website Configuration**. Select the affected domain and click **Policies** to view the protection configuration of this domain.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78570/155437578434043_en-US.png)

2.  In the left-side navigation pane, choose **Settings** \> **Custom Rule Groups**. Select the rule group associated with the affected domain and click **Copy**.
3.  Enter a rule group name and description. Click **OK** to create a custom rule group.
4.  Select the newly created rule group and click **Edit**.
5.  In the **Configure Rule Group** dialog box that appears, select the rule that has caused false positives from the rules list on the right side. Click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78570/155437578434044_en-US.png) to remove this rule from the rule group and click **Confirm**.

    **Note:** All protection rules are listed on the left side, and rules in the specified custom rule group are listed on the right side.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78570/155437578434045_en-US.png)

6.  On the **Custom Rule Groups** page, select the new rule group, click **Apply to Website**, and select the affected domain.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78570/155437578434046_en-US.png)


After the custom rule group is changed for the affected domain, the same requests sent to your domain are no longer blocked.

**Note:** If requests are still blocked, make sure you have identified the right ID of the protection rule that causes false positives and remove this rule from the custom rule group.

