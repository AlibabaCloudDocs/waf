# WordPress xmlrpc PingBack反射攻击防护最佳实践 {#concept_hhz_pqc_p2b .concept}

本文用于在遭受WordPress反射攻击时，通过Web应用防火墙防御WordPress反射攻击。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15593/15538237787626_zh-CN.jpg)

## 什么是WordPress反射攻击 {#section_jnf_qqc_p2b .section}

WordPress是一种使用PHP语言开发的博客平台，pingback是WordPress的一个插件。黑客可以利用pingback对网站发起WordPress反射攻击。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15593/15538237787627_zh-CN.png)

在遭受WordPress攻击后，您可以在服务器日志上看到大量User-Agent中包含WordPress、pingback字样的请求。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15593/15538237797628_zh-CN.png)

WordPress反射攻击是CC攻击的变种，可以造成网页加载极其缓慢、服务器CPU 飙升、失去响应等情况。

## 如何使用Web应用防火墙进行防御 {#section_mnf_qqc_p2b .section}

1.  登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)。
2.  前往**管理** \> **网站配置**页面。
3.  选择需要防护的域名，单击其操作列下的**防护配置**。
4.  在**精准访问控制**下，单击**前去配置**。
5.  单击**新增规则**，分别添加以下两条精准访问控制规则。

    -   阻断User-Agent中包含pingback的访问。
        -   **规则名称**：wp1
        -   **匹配字段**：User-Agent
        -   **逻辑符**：包含
        -   **匹配内容**：pingback
        -   **匹配动作**：阻断
    -   阻断User-Agent中包含WordPress的访问。
        -   **规则名称**：wp2
        -   **匹配字段**：User-Agent
        -   **逻辑符**：包含
        -   **匹配内容**：WordPress
        -   **匹配动作**：阻断
    **说明：** 两条规则要分开添加。


