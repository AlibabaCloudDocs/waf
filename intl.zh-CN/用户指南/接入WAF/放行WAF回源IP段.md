# 放行WAF回源IP段 {#concept_wzd_by1_p2b .concept}

网站成功接入WAF后，所有网站访问请求将先流转到WAF进行监控，经WAF实例过滤后再返回到源站服务器。流量经WAF实例返回源站的过程称为回源。

WAF实例的IP数量有限，且源站服务器收到的所有请求都来自这些IP。在源站服务器上的安全软件（如安全狗、云锁）看来，这种行为很可疑，有可能触发屏蔽WAF回源IP的操作。因此，在接入WAF防护后，您需要在源站服务器的安全软件上设置放行所有WAF回源IP。

**说明：** 强烈推荐您在接入WAF防护后，卸载源站服务器上的其他安全软件。

## 操作步骤 {#section_sb1_xrb_p2b .section}

WAF控制台提供了最新的回源IP段列表，您可以参照以下步骤进行操作：

1.  登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)。
2.  在页面上方，选择地域：**中国大陆**、**海外地区**。
3.  前往**管理** \> **网站配置**页面。
4.  单击页面上方的**Web应用防火墙回源IP网段列表**，直接查看和复制所有WAF回源IP段。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15547/15438229517574_zh-CN.png)

    您会看到如下结果：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15547/15438229517575_zh-CN.png)

5.  打开源站服务器上的安全软件，将复制的IP段添加到白名单。

## 常见问题 {#section_wb1_xrb_p2b .section}

**什么是回源IP?**

回源IP是WAF用来代理客户端请求服务器时用的源IP，在服务器看来，接入WAF后所有源IP都会变成WAF的回源IP，而真实的客户端地址会被加在[HTTP头部的XFF字段](../../../../intl.zh-CN/最佳实践/获取访问者真实IP.md#)中。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15547/15438229517576_zh-CN.png)

**为何要放行回源IP段？**

由于来源的IP变得更加集中，频率会变得更快，服务器上的防火墙或安全软件很容易认为这些IP在发起攻击，从而将其拉黑。一旦拉黑，WAF的请求将无法得到源站的正常响应。因此，在接入WAF后，您应确保源站已将WAF的全部回源IP放行（加入白名单），不然可能会出现网站打不开或打开极其缓慢等情况。

建议在部署WAF后，您在源站上只允许来自WAF的访问请求，这样既可保证访问不受影响，又能防止源站IP暴露后被黑客直接攻击。更多信息，请参考[源站保护](../../../../intl.zh-CN/最佳实践/源站保护.md#)。

