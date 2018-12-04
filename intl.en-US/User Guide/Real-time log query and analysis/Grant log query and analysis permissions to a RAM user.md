# Grant log query and analysis permissions to a RAM user {#task_omb_rgl_qfb .task}

If you want to use the WAF log query and analysis service with a RAM user, you must grant required permissions to the RAM user using the Alibaba Cloud account.

The following permissions are required for enabling and using the WAF log query and analysis service.

|Operation|Required account type and permissions|
|:--------|:------------------------------------|
|Enable Log Service \(the service remains enabled after this operation\)|Alibaba Cloud account|
|Authorize WAF to write log data to the exclusive logstore in Log Service in real-time \(the authorization remains valid after this operation\)| -   Alibaba Cloud account
-   RAM user that has the `AliyunLogFullAccess` permission
-   RAM user that has specific permissions

 |
|Use the log query and analysis service| -   Alibaba Cloud account
-   RAM user that has the `AliyunLogFullAccess` permission
-   RAM user that has specific permissions

 |

Grant permissions to RAM users as required.

|Scenario|Permission|Procedure|
|--------|----------|---------|
|Grant permissions on all Log Service operations to a RAM user.|`AliyunLogFullAccess`|For more information, see [RAM users](../../../../reseller.en-US/User Guide/Access control RAM/Grant RAM sub-accounts permissions to access Log Service.md#).|
|Grant the log viewing permission to a RAM user after you enable the WAF log query and analysis service and complete the authorization on the Alibaba Cloud account.|`AliyunLogReadOnlyAccess`|For more information, see [RAM users](../../../../reseller.en-US/User Guide/Access control RAM/Grant RAM sub-accounts permissions to access Log Service.md#).|
|Grant the RAM user permissions on enabling and using the WAF log query and analysis service. This RAM user is not granted other administrative permissions on Log Service.|Custom authorization policy|For more information, see the following procedure.|

1.  Log on to the [RAM console](https://partners-intl.console.aliyun.com/#/ram). 
2.  On the Policies page, select the Custom Policy tab. 
3.  In the upper-right corner of the page, click **Create Authorization Policy**. 
4.  Click **Create Authorization Policy**. In the template, specify the **Authorization Policy Name**, and then enter the following in the **Policy Content** field. 

    **Note:** Replace `${Project}` and `${Logstore}` in the following policy content with the names of the exclusive project and logstore in WAF Log Service.

    ```
    
    {
      "Version": "1",
      "Statement": [
      	{
          "Action": "log:GetProject",
          "Resource": "acs:log:*:*:project/${Project}",
          "Effect": "Allow"
        },
        {
          "Action": "log:CreateProject",
          "Resource": "acs:log:*:*:project/*",
          "Effect": "Allow"
        },
    	{
          "Action": "log:ListLogStores",
          "Resource": "acs:log:*:*:project/${Project}/logstore/*",
          "Effect": "Allow"
        },
        {
          "Action": "log:CreateLogStore",
          "Resource": "acs:log:*:*:project/${Project}/logstore/*",
          "Effect": "Allow"
        },
    	{
          "Action": "log:GetIndex",
          "Resource": "acs:log:*:*:project/${Project}/logstore/${Logstore}",
          "Effect": "Allow"
        },
        {
          "Action": "log:CreateIndex",
          "Resource": "acs:log:*:*:project/${Project}/logstore/${Logstore}",
          "Effect": "Allow"
        },
        {
          "Action": "log:UpdateIndex",
          "Resource": "acs:log:*:*:project/${Project}/logstore/${Logstore}",
          "Effect": "Allow"
        },
        {
          "Action": "log:CreateDashboard",
          "Resource": "acs:log:*:*:project/${Project}/dashboard/*",
          "Effect": "Allow"
        },
    	{
          "Action": "log:UpdateDashboard",
          "Resource": "acs:log:*:*:project/${Project}/dashboard/*",
          "Effect": "Allow"
        },
    	{
          "Action": "log:CreateSavedSearch",
          "Resource": "acs:log:*:*:project/${Project}/savedsearch/*",
          "Effect": "Allow"
        },
    	{
          "Action": "log:UpdateSavedSearch",
          "Resource": "acs:log:*:*:project/${Project}/savedsearch/*",
          "Effect": "Allow"
        }
      ]
    }
    ```

5.  Click **Create Authorization Policy**. 
6.  Go to the Users page, find the RAM user, and then click **Authorize**. 
7.  Add the authorization policy that you created and click **OK**. This RAM user can enable and use the WAF log query and analysis service, and cannot use other features of Log Service.

