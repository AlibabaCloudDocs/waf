# Perform redirect check with a local computer {#concept_t23_cy1_p2b .concept}

When you have created a website configuration in Alibaba Cloud WAF for your website and are going to update the DNS settings to redirect web traffic to WAF for inspection, we recommend that you perform a redirect check with a local computer to make sure that WAF can handle the traffic. Redirect check requires you to modify the local hosts file to make your local machine look directly at your Alibaba Cloud WAF instance. Therefore, you can test whether the WAF instance works properly.

## Modify the local hosts file {#section_kxn_ctb_p2b .section}

Modify the local hosts file \([What is the hosts file?](https://en.wikipedia.org/wiki/Hosts_(file))\) to forward local requests to WAF. For Windows systems, the procedure is as follows:

1.  Open the hosts file with Notepad. The hosts file locates in the C:\\Windows\\System32\\drivers\\etc\\hosts directory.
2.  In the last line, add the following content: `WAF_IP_address Domain_name_protected`.

    Suppose that you have created a website configuration for `www.aliyundemo.cn`, and Alibaba Cloud WAF assigns the following CNAME address to it: `xxxxxxxxxwmqvixt8vedyneaepztpuqu.alicloudwaf.com`.

    1.  Open the cmd command-line tool in Windows, and run the following command to obtain the WAF IP address: `ping xxxxxxxxxwmqvixt8vedyneaepztpuqu.alicloudwaf.com`. You can view the WAF IP address in the response.

        ![](images/7577_en-US.jpg)

    2.  Add the following line to hosts. The IP address is the WAF IP address obtained in the previous step, and the domain name is the protected domain name.

        ![](images/7578_en-US.jpg)

3.  Save changes to hosts. Ping the protected domain name in cmd.

    ![](images/7579_en-US.jpg)

    If WAF works properly, the IP address you see will be the WAF IP address configured in the previous step. If the origin IP address is displayed, try refreshing the local DNS cache. In Windows, you can run `ipconfig`/`flushdns` in cmd.


## Verify WAF forwarding {#section_rxn_ctb_p2b .section}

Once the changes in the hosts file are effective, you can access the protected domain name from your local computer. If WAF is configured correctly, the website is expected to be normally accessed.

In addition, you can verify the protection effect by constructing some simple attack commands. For example, you can add `/? alert(xss)` to the URL to construct a Web attack request for testing. As you try to access `www.aliyundemo.cn/? alert(xss)`, WAF is expected to return the following error page.

![](images/7580_en-US.jpg)

