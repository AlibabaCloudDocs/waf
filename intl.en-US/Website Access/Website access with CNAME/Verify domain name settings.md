---
keyword: [hosts, local computer, access, Web Application Firewall]
---

# Verify domain name settings

After you add a domain name to WAF and before you change the DNS record to redirect requests to WAF for protection, we recommend that you change the DNS record on a local computer to verify domain name settings in WAF. This example in this topic is performed on a Windows machine. The example describes how to verify the domain name settings on your local computer.

A domain name of your website is added to WAF in CNAME mode. For more information, see [Add domain names](/intl.en-US/Website Access/Website access with CNAME/Add websites.mdsection_i0l_fp0_t66).

You can modify the hosts file to configure address-to-name mapping of your local computer. The DNS record takes effect only on the local computer. During the verification, you must resolve the domain name of your website to the IP address of WAF on the local computer. If you can access the domain name that you add to WAF from a local computer, the domain name settings in WAF are correct. The step on a local computer prevents access exceptions caused by invalid domain name settings.

## Procedure

The following procedure describes how to verify domain name settings on a local computer that runs Windows.

1.  Open File Server Resource Manager on the local computer.

2.  In the address bar, enter C:\\Windows\\System32\\drivers\\etc\\hosts and open the hosts file with Notepad or Notepad++.

3.  Append the following content to the hosts file:

    ```
    <WAF IP address> <Protected domain name>
    ```

    where, `<Protected domain name>` is the domain name that you add to WAF. `<WAF IP address>` is the WAF IP address that is mapped to the domain name. Separate `<WAF IP address>` and `<Protected domain name>` with a space.

    To obtain the WAF IP address, perform the following steps:

    1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

    2.  In the top navigation bar, select the resource group to which the instance belongs and the region, **Mainland China** or **International**, in which the instance is deployed.

    3.  In the left-side navigation pane, choose **Asset Center** \> **Website Access**.

    4.  On the Domain Names tab of the Website Access page, move the pointer over the domain name, view and copy the CNAME of the domain name.

        ![CNAME](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7801549951/p97144.png)

    5.  Open Command Prompt in Windows.

    6.  Run the following command to obtain the WAF IP address:

        ```
        ping <CNAME that you have copied>
        ```

    7.  Record the WAF IP address in the command output.``

    Assume that you add the domain name `test.wafqa3.com` to WAF and the WAF IP address is `47. ***. ***.213`. Append the following content to the hosts file:

    ```
    47.***. ***.213 test.wafqa3.com
    ```

4.  Save changes to the hosts file and run the `ping <Protected domain name>` command to verify that your changes are in effect.

    If your changes are in effect, the IP address in the command output is the WAF IP address that is mapped to the domain name.``

    If the IP address of the origin server is displayed, try refreshing the local DNS cache. You can run the `ipconfig` or `flushdns` command to refresh the DNS cache. Then, run the ping command again until the changes take effect.

5.  In the address bar of your local browser, enter the protected domain name.

    -   If you can access the website, the domain name settings added to the WAF console are correct and in effect. In this case, you can restore the hosts file and change the DNS record to redirect traffic to WAF for protection. For more information, see [Change a DNS record](/intl.en-US/Website Access/Website access with CNAME/Change a DNS record.md).
    -   If you are unable to access your website, the domain name settings may be invalid. We recommend that you check the domain name settings in the WAF console and perform the verification again after troubleshooting. For more information, see [Add websites](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).
6.  Simulate simple web attack commands to verify whether WAF works properly.

    For example, in the address bar of your browser, enter `<Protected domain name>/alert(xss)`, a web attack request, and verify whether WAF blocks the attack.

    If the request is blocked, the following page appears.

7.  After the verification is complete, delete the record added in Step 3 from the hosts file.

    **Note:** Delete the record after the verification is complete. Otherwise, exceptions may occur when the local computer sends requests to the protected domain name.


## Contact technical support

If you cannot identify any faults in domain name settings, contact technical support for help with the following ways:

-   Log on to the [WAF console](https://yundun.console.aliyun.com/?p=waf). In the lower part of the left-side navigation pane, click **Meet Expert**, scan the DingTalk code to join the WAF DingTalk group, and contact Alibaba Cloud security experts for assistance.
-   Submit a [ticket](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80).

