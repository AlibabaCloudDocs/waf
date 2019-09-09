# 业务接入WAF配置 {#task_2118186 .task}

本文介绍通过DNS配置模式接入WAF时，如何在已添加网站配置后，配置域名解析，实现业务接入。

**说明：** 如果您通过包年包月方式开通WAF，且您的源站服务器部署在阿里云ECS（华北2地域），同时ECS实例拥有公网IP或已绑定弹性公网IP（EIP），则您可以使用透明代理模式接入WAF。

-   透明代理模式：将所配置的源站服务器公网IP的80端口接收到的HTTP协议的流量直接牵引到WAF，经WAF处理后再将正常的访问流量回注给源站服务器。

    该方式需要您授权WAF读取您的ECS实例信息。配置过程中只用在WAF控制台添加域名和勾选相应的服务器IP。具体操作请参见[使用透明代理模式接入WAF](cn.zh-CN/用户指南/使用透明代理模式接入WAF.md#)。

-   DNS配置模式：通过修改域名解析的方式，将被防护域名的访问流量指向WAF；WAF根据域名配置的源站服务器地址，将处理后的请求转发回源站服务器。

    该方式需要您在WAF控制台添加网站配置并更新域名的DNS设置。


通过DNS配置模式接入WAF时，您需要先[添加网站配置](cn.zh-CN/用户指南/使用DNS配置模式接入WAF/网站配置.md#)；成功添加网站配置后，您可以选择通过[（推荐）CNAME接入](#section_itl_ixa_92z)和[A记录接入](#section_wji_7qi_0xt)的方式更新域名DNS解析，将网站访问流量转发到WAF进行监控。

**说明：** 推荐您采用CNAME接入。在某些极端情况下（如节点故障、机房故障等），通过CNAME解析方式接入WAF，可以实现自动切换节点IP甚至直接将解析切回源站，从而最大程度保证业务的稳定运行，提供高可用性和灾备能力。

下文内容适用于为网站单独开启WAF防护，即该网站不接入CDN、DDoS高防等其它代理型服务。如果您需要将WAF与其它代理型服务结合部署，请参见以下文档：

-   [同时部署WAF和CDN](cn.zh-CN/用户指南/使用DNS配置模式接入WAF/同时部署WAF和CDN.md#)：介绍同时为网站部署CDN和Web应用防火墙的配置方法。
-   [同时部署WAF和DDoS高防](cn.zh-CN/用户指南/使用DNS配置模式接入WAF/同时部署WAF和DDoS高防.md#)：介绍同时为网站部署DDoS高防和Web应用防火墙的配置方法。

## （推荐）CNAME接入 {#section_itl_ixa_92z .section}

前提条件

-   已添加网站配置。具体请参见[网站配置](cn.zh-CN/用户指南/使用DNS配置模式接入WAF/网站配置.md#)。
-   获取WAF CNAME地址。
    1.  登录[云盾Web应用防火墙控制台](https://yundunnext.console.aliyun.com/?p=waf)。
    2.  在页面上方选择地域：**中国大陆**、**海外地区**。
    3.  前往**管理** \> **网站配置**页面，在**DNS配置模式**下，选择已添加的网站配置，将鼠标放置在域名上，即可出现**复制CName**按钮。

        ![复制CName](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15546/15680207237565_zh-CN.png)

    4.  单击**复制CName**，将该CNAME复制到剪贴板中。
-   具有在域名的DNS服务商处更新DNS记录的权限。
-   （可选）放行WAF回源段IP。源站服务器上已启用非阿里云安全软件（如安全狗、云锁）时，您需要在这些软件上设置放行WAF回源段IP，防止由WAF转发到源站的正常业务流量被拦截。具体请参见[放行WAF回源段IP](cn.zh-CN/用户指南/使用DNS配置模式接入WAF/放行WAF回源IP段.md#)。
-   （可选）进行本地验证。通过本地验证确保WAF转发规则配置正常后，再修改网站域名的DNS解析记录，防止因配置错误导致业务中断。具体请参见[本地验证](cn.zh-CN/用户指南/使用DNS配置模式接入WAF/本地验证.md#)。

操作步骤

以下操作以阿里云云解析DNS为例介绍修改域名CNAME解析记录的方法。如果您的域名的DNS解析托管在阿里云云解析DNS上，您可以直接参照以下步骤进行操作；若您使用阿里云以外的DNS服务，请参见以下步骤在域名的DNS服务商的系统上进行类似配置。

下文也提供了[花生壳配置示例](#)，介绍在花生壳修改域名解析的方法。

1.  登录[云解析DNS控制台](https://dns.console.aliyun.com/#/dns/domainList)。
2.  选择要操作的域名，单击其操作列下的**解析设置**。![解析设置,域名解析列表](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15680207237588_zh-CN.jpg)


3.  选择要操作的**主机记录**，单击其操作列下的**修改**。 

    关于域名的主机记录，以域名`abc.com`为例：

    -   **www**： 用于精确匹配www开头的域名，如`www.abc.com`。
    -   **@**： 用于匹配根域名`abc.com`。
    -   **\***： 用于匹配泛域名，包括根域名和所有子域名，如`blog.abc.com`、`www.abc.com`、`abc.com`等。
    ![解析设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15680207237589_zh-CN.jpg)

4.  在修改记录对话框中，完成以下操作： 

    -   **记录类型**：修改为**CNAME**。
    -   **记录值**：修改为已复制的WAF CNAME地址。
    -   其他设置保持不变。TTL值一般建议设置为10分钟。TTL值越大，则DNS记录的同步和更新越慢。
    关于修改解析记录：

    -   对于同一个主机记录，CNAME解析记录值只能填写一个，您需要将其修改为WAF CNAME地址。
    -   不同DNS解析记录类型间存在冲突。例如，对于同一个主机记录，CNAME记录与A记录、MX记录、TXT记录等其他记录互相冲突。在无法直接修改记录类型的情况下，您可以先删除存在冲突的其他记录，再添加一条新的CNAME记录。

        **说明：** 删除其他解析记录并新增CNAME解析记录的过程应尽可能在短时间内完成。如果删除A记录后长时间没有添加CNAME解析记录，可能导致域名无法正常解析。

        关于DNS解析记录互斥的详细说明，请参见[解析记录冲突的规则](https://help.aliyun.com/document_detail/39787.html)。

    -   如果必须保留MX记录（邮件服务器记录），您可以参见[业务接入WAF配置](../cn.zh-CN/用户指南/使用DNS配置模式接入WAF/业务接入WAF配置.md#)，使用A记录解析的方式将域名解析到WAF IP。
    ![修改记录](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15680207237590_zh-CN.jpg)

5.  单击**确定**，完成DNS配置，等待DNS解析记录生效。
6.  验证DNS配置。您可以Ping网站域名或使用[17ce](https://www.17ce.com/)等工具验证DNS解析是否生效。 

    **说明：** 由于DNS解析记录生效需要一定时间，如果验证失败，您可以等待10分钟后重新检查。

7.  查看DNS解析状态。 
    1.  登录[云盾Web应用防火墙控制台](https://yundunnext.console.aliyun.com/?p=waf)。
    2.  前往**管理** \> **网站配置**页面，在**DNS配置模式**下，查看域名的**DNS解析状态**。 
        -   **正常**：表示网站已成功接入WAF，网站访问流量由WAF监控。
        -   **异常**：如果DNS解析状态为异常，且收到**未检测到CNAME接入**、**无流量**、**检测失败**等提示，说明网站未正确接入WAF。

            如果您确认已将网站域名解析到WAF CNAME地址，可在一小时后再次查看DNS解析状态或者参见[DNS解析状态异常](../cn.zh-CN/常见问题/DNS解析状态异常.md#)排查异常原因。

            **说明：** 该提示仅说明网站是否正确接入WAF，不代表您的网站访问异常。

            ![dns解析状态](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15549/15680207237591_zh-CN.jpg)


花生壳配置示例

如果您的域名DNS托管在[花生壳](https://www.oray.com/)，您可以参照下图修改DNS解析设置。

![花生壳,cname记录](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15553/156802072332207_zh-CN.jpg)

启用源站保护

启用源站保护可以防止攻击者在获取源站服务器的真实IP后，绕过WAF直接攻击您的源站。建议您通过配置源站ECS的安全组或源站SLB的白名单，防止恶意攻击者直接攻击您的源站。具体请参见[源站保护配置](../cn.zh-CN/最佳实践/源站保护.md#)。

## A记录接入 {#section_wji_7qi_0xt .section}

A记录接入和CNAME接入的流程大体相同，区别在于以下两点：

-   前提条件：获取WAF CNAME后，执行以下步骤，获取WAF IP地址。
    1.  在Windows操作系统中，打开cmd命令行工具。
    2.  执行以下命令：`ping "已复制的WAF Cname地址"`。

        ![ping](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15553/156802072332229_zh-CN.png)

    3.  在返回结果中，记录WAF IP地址。
-   操作步骤：在步骤4修改记录时，执行以下操作，修改记录类型和记录值。
    -   **记录类型**：修改为**A**。
    -   **记录值**：修改为已获得的WAF IP地址。
    -   其他设置保持不变。

