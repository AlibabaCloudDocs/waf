# 同时部署WAF和DDoS高防 {#task_tpk_dfj_p2b .task}

Web应用防火墙（WAF）与DDoS高防完全兼容。您可以参照以下架构为源站同时部署WAF和DDoS高防：DDoS高防IP（入口层，实现DDoS防护）\> Web应用防火墙（中间层，实现应用层防护）\> 源站。

1.  在Web应用防火墙中添加网站配置。 

    -   **服务器地址**：勾选**IP**并填写ECS公网IP、SLB公网IP，或云外机房服务器的IP。
    -   **WAF前是否有七层代理（高防/CDN等）**：勾选**是**。
    具体操作请参考[网站配置](intl.zh-CN/用户指南/接入WAF/网站配置.md#)。

2.  在高防IP中添加网站配置。操作步骤如下： 
    1.  在**接入** \> **网站**页面，单击**添加域名**。
    2.  在填写域名信息任务中， 完成以下配置：

        -   **防护网站**：填写被防护网站的域名。
        -   **协议类型**：勾选源站支持的协议类型。
        -   **源站IP/域名**：勾选**源站域名**并填写Web应用防火墙生成的CNAME地址。

            **说明：** 关于如何查看WAF生成的CNAME地址，请参考[WAF接入指南](intl.zh-CN/用户指南/接入WAF/WAF接入指南.md#)。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15557/154382326133576_zh-CN.png)

    3.  单击**下一步**。
    4.  完成任务**选择实例与线路**。
3.  变更域名的DNS解析。登录域名的DNS系统，添加一条CNAME记录，将网站域名的解析地址指向DDoS高防生成的CNAME地址。 

    具体操作请参考[DDoS高防CNAME接入流程](https://www.alibabacloud.com/help/doc-detail/40532.htm)。


完成上述配置后，网站流量先经过DDoS高防，再转发到Web应用防火墙。

