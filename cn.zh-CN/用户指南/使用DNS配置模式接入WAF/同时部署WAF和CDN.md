# 同时部署WAF和CDN {#task_1797345 .task}

云盾Web应用防火墙（WAF）可以与CDN（如网宿、加速乐、七牛、又拍、阿里云CDN等）结合使用，为开启内容加速的域名提供Web攻击防御。

您可以参照以下架构为源站同时部署WAF和CDN：CDN（入口层，内容加速）\> Web应用防火墙（中间层，实现应用层防护）\> 源站。

## 使用阿里云CDN {#section_5xq_cmq_f5u .section}

1.  参见[CDN快速入门](../../../../intl.zh-CN/快速入门/入门概述.md#)，将要防护的域名（即加速域名）接入CDN。
2.  在Web应用防火墙中创建网站配置。 

    -   **域名**：填写要防护的域名。
    -   **服务器地址**：填写SLB公网IP、ECS公网IP，或云外机房服务器的IP。
    -   **WAF前是否有七层代理（高防/CDN等）**：勾选**是**。
    具体操作请参见[网站配置](intl.zh-CN/用户指南/使用DNS配置模式接入WAF/网站配置.md#)。

    ![网站配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15558/15663502367705_zh-CN.jpg)

3.  成功创建网站配置后，Web应用防火墙为该域名生成一个专用的CNAME地址。 

    **说明：** 关于如何查看WAF生成的CNAME地址，请参见[WAF接入指南](intl.zh-CN/用户指南/使用DNS配置模式接入WAF/业务接入WAF配置.md#)。

4.  将CDN配置中的源站修改为Web应用防火墙分配的CNAME地址。 

    1.  登录[阿里云CDN控制台](https://cdn.console.aliyun.com/#/DomainList/list)。
    2.  在域名管理页面，选择要操作的域名，单击**管理**。
    3.  在**源站信息**下，单击**修改配置**。
    4.  修改源站信息。 

        -   **类型**：选择**源站域名**。
        -   **域名**：填写WAF生成的CNAME地址。
        -   **端口**：选择**80端口**。
        ![回源设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15558/15663502367706_zh-CN.jpg)

    5.  前往回源配置页面，在回源配置页签下，确认**回源HOST**未开启。 

        ![回源设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15558/15663502367707_zh-CN.jpg)

    完成上述配置后，流量经过CDN，其中动态内容将继续通过Web应用防火墙进行安全检测防护。


