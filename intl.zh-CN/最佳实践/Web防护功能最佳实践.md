# Web防护功能最佳实践 {#concept_trh_4l4_m2b .concept}

本文介绍了阿里云云盾Web应用防火墙的Web攻击防护最佳实践，主要从应用场景、防护策略、防护效果、规则更新四个方面进行介绍。

## 应用场景 {#section_ryv_pl4_m2b .section}

Web应用防火墙（Web Application Firewall，简称WAF）主要提供针对Web攻击的防护，例如SQL注入、XSS、远程命令执行、Webshell上传等攻击。关于Web攻击的详细信息，请参考[OWASP 2017 Top 10](https://www.owasp.org/index.php/Top_10-2017_Top_10)。

**说明：** 主机层服务的安全问题（例如Redis、MySQL未授权访问等）导致的服务器入侵不在WAF的防护范围之内。

## 防护策略 {#section_syv_pl4_m2b .section}

在将网站成功接入WAF防护后，登录[Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)，在**管理** \> **网站配置**页面选择已防护的网站，并单击**防护配置**，即可查看Web应用攻击防护的防护状态，如图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768198640_zh-CN.jpg)

Web应用攻击防护功能默认开启，并使用正常模式的防护规则策略。其中，

-   **状态**
    -   **开启**表示WAF的Web应用攻击防护模块已开启。
    -   **关闭**表示该防护模块处于关闭状态。
-   **模式**：分为防护和预警两种模式。
    -   **防护**模式表示当遭受Web攻击时，WAF自动拦截攻击请求，并在后台记录攻击日志。
    -   **预警**模式表示当遭受Web攻击时，WAF不会拦截攻击请求，仅在后台记录攻击日志。
-   **防护规则策略**：分为宽松、正常、严格三种模式，仅在启用防护模式后生效。
    -   **宽松**防护规则策略的防护粒度较粗，只拦截攻击特征比较明显的请求。
    -   **正常**防护规则策略的防护粒度较宽松且防护规则策略精准，可以拦截常见的具有绕过特征的攻击请求。
    -   **严格**防护规则策略的防护粒度最精细，可以拦截具有复杂的绕过特征的攻击请求。

**使用建议**：

-   如果您对自己的业务流量特征还不完全清楚，建议先切换到预警模式进行观察。一般情况下，建议您观察一至两周，然后分析预警模式下的攻击日志。
    -   如果没有发现任何正常业务流量被拦截的记录，则可以切换到防护模式启用拦截防护。
    -   如果发现攻击日志中存在正常业务流量，可以联系阿里云安全专家沟通具体的解决方案。
-   PHPMyAdmin、开发技术类论坛接入WAF防护可能会存在误拦截的问题，建议联系阿里云安全专家沟通具体的解决方案。
-   业务操作方面应注意以下问题：
    -   正常业务的HTTP请求中尽量不要直接传递原始的SQL语句、JAVA SCRIPT代码。
    -   正常业务的URL尽量不要使用一些特殊的关键字（UPDATE、SET等）作为路径，例如`www.example.com/abc/update/mod.php?set=1`。
    -   如果业务中需要上传文件，不建议直接通过Web方式上传超过50M的文件，建议使用OSS或者其他方式上传。
-   开启WAF的Web应用攻击防护功能后，不要禁用默认精准访问控制规则中的Web防护通用防护模块，如图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768208641_zh-CN.jpg)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768208642_zh-CN.jpg)


## 防护效果 {#section_dzv_pl4_m2b .section}

开启WAF的Web应用攻击防护功能后，您可以在**统计** \> **安全报表**页面，查看攻击的拦截日志，如图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768208643_zh-CN.jpg)

在安全报表页面，您可以查看昨天、当天、7天以及一个月内的攻击详情。同时，单击**查看攻击详情**，可以查看具体的攻击信息，如图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768208644_zh-CN.jpg)

该截图中的拦截日志即为一条已被WAF拦截的SQL注入攻击请求。

**说明：** 如果您发现WAF误拦截了正常业务流量，建议您先通过精准访问控制功能对受影响的URL[配置白名单策略](../../../../../intl.zh-CN/用户指南/防护配置/IP黑白名单配置.md#)，然后联系阿里云安全专家沟通具体解决方案。

## 规则更新 {#section_gzv_pl4_m2b .section}

对于互联网披露的已知漏洞和未披露的0day漏洞，云盾WAF将及时完成防护规则的更新，并发布防护公告。

您可以登录[Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)，前往**总览** \> **安全**页面，查看最新发布的防护公告，如图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15589/15543768208645_zh-CN.jpg)

该截图中公告栏展示了针对weblogic远程命令执行漏洞的防护规则的更新公告。

**说明：** Web攻击往往存在不止一种概念证明方法（Proof of Concept，简称PoC），阿里云安全专家会对漏洞原理进行深度分析从而确保发布的Web防护规则覆盖已公开和未公开的各种漏洞利用方式。

