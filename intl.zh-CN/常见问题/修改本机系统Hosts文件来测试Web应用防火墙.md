# 修改本机系统Hosts文件来测试Web应用防火墙 {#concept_ak3_nxk_q2b .concept}

## 系统hosts文件位置 {#section_tdw_nxk_q2b .section}

C:\\Windows\\System32\\drivers\\etc\\hosts

## 系统hosts文件作用 {#section_udw_nxk_q2b .section}

Hosts文件中指定了域名和IP地址的对应关系。如果一个域名在hosts文件中指定了IP地址，在访问此域名时，系统将不会通过DNS（Domain Name System）来解析它的IP地址，而是直接访问所指定的IP地址。

因此，如果网站配置完高防IP或者Web应用防火墙之后，在不变更线上业务流向的情况下，可以通过修改本地hosts文件，将网站指向Web应用防火墙，来测试业务经过Web应用防火墙后是否正常。

## Host文件修改步骤 {#section_m5z_4xk_q2b .section}

1.  找到已分配的Web应用防火墙（WAF）IP地址。

    配置完域名后，WAF会生成一个解析用的CNAME域名。使用Ping命令可得到该域名的IP地址，即WAF IP。

    1.  登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)，在**管理** \> **网站配置**页面找到已分配的CNAME域名。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15597/15477825647967_zh-CN.jpg)

    2.  使用Ping命令得到该域名的IP地址。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15597/15477825647968_zh-CN.png)

2.  定位到C:\\Windows\\System32\\drivers\\etc\\目录。
3.  使用记事本打开hosts文件，进行编辑。把域名指向WAF IP地址。

    Hosts文件的格式为`IP 域名`。例如，添加以下记录，将cdn.aliyundemo.cn指向xx.xx.xx.xxx：`xx.xx.xx.xxx cdn.aliyundemo.cn`。

4.  将修改后的hosts文件保存到C:\\Windows\\System32\\drivers\\etc\\目录下。

