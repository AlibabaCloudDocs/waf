# 查看Web应用防火墙回源IP段 {#concept_onw_pcl_q2b .concept}

为了防止您的Web应用防火墙回源IP段被源站拦截或限速，您可以将Web应用防火墙的回源IP段添加至您源站的安全组、防火墙，或其它主机安全防护软件的白名单中。

参照以下步骤，查看Web应用防火墙回源IP段。

1.  登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)。
2.  在页面上方，选择地域：**中国大陆**、**海外地区**。
3.  前往**设置** \> **产品信息**页面。
4.  在产品信息页面底部，查看**回源IP段**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15607/15585441097997_zh-CN.png)


您可将对应的WAF回源IP段添加至您源站的安全组、防火墙，或其它主机安全防护软件的白名单中，对您的源站进行防护部署。详细配置方法，请参考[源站防护](../../../../intl.zh-CN/最佳实践/源站保护.md#)。

