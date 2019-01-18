# Modify local hosts file to test WAF {#concept_ak3_nxk_q2b .concept}

## Location of the hosts file {#section_tdw_nxk_q2b .section}

C:\\Windows\\System32\\drivers\\etc\\hosts

## Hosts file functionality {#section_udw_nxk_q2b .section}

The hosts file specifies the correspondence between the domain name and IP address. If a domain name has an IP address specified in the hosts file, the system will not resolve its IP address through the domain name system \(DNS\) when accessing this domain name, but will directly access the specified IP address instead.

Therefore, if your website is deployed with Anti-DDoS Pro or WAF services, you can modify the local hosts file to direct the website to the WAF without changing the online business flow. This allows you to test whether or not the business services work normally after they pass through WAF.

## Procedure {#section_m5z_4xk_q2b .section}

1.  Find the IP address allocated by WAF.

    When the domain name is configured, WAF generates a CNAME record for resolution purposes. Use the ping command to get the IP address of the CNAME record, and this IP address is the WAF IP. Use www.abc.com as an example.

    1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf) and go to the **Management** \> **Website Configuration** page to view the WAF CNAME address.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15597/15477825727967_en-US.jpg)

    2.  Use the ping command to get the IP address of the CNAME record.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15597/15477825727968_en-US.png)

2.  Locate to the C:\\Windows\\System32\\drivers\\etc\\ folder.
3.  Open the hosts file in Notepad, and point the domain name to the WAF IP address.

    The hosts file format is `<IP> <domain name>`. For example, point www.abc.com to `xx.xx.xx.xxx.xx.xx.xx.xxx www.abc.com`.

4.  Save the modified hosts file to the C:\\Windows\\System32\\drivers\\etc\\ folder.

