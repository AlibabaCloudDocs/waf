# Consul Service API远程命令执行漏洞 {#concept_f2s_gd2_p2b .concept}

2018年11月27日，Consul在官方博客中发布了关于Consul工具在特定配置下可能导致远程命令执行（RCE）漏洞的公告，并描述了防护该漏洞的配置方案。

Consul是HashiCorp公司推出的一款开源工具，用于实现分布式系统的服务发现与配置。与其他分布式服务注册与发现的方案相比，Consul提供的方案更为“一站式”。Consul内置了服务注册与发现框架、分布一致性协议实现、健康检查、Key/Value存储、多数据中心方案，不再需要依赖其他工具（例如ZooKeeper等），使用方式也相对简单。

Consul使用Go语言编写，因此具有天然的可移植性（支持Linux、Windows和Mac OS X系统）；且安装包中仅包含一个可执行文件，便于部署，可与Docker等轻量级容器无缝配合。

## 漏洞名称 {#section_urn_xp4_m2b .section}

Hashicorp Consul Services API远程命令执行漏洞

## 漏洞描述 {#section_l12_zp4_m2b .section}

在特定配置下，恶意攻击者可以通过发送精心构造的HTTP请求在未经授权的情况下在Consul服务端远程执行命令。关于该Consul漏洞的更多详细信息，请查看[HashiCorp官方公告](https://www.hashicorp.com/blog/protecting-consul-from-rce-risk-in-specific-configurations)。

**漏洞复现过程** 

1.  验证Consul服务端存在该远程命令执行漏洞。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/218967/155790426047331_zh-CN.png)

2.  构造HTTP PUT请求，实现在Consul服务端远程执行命令。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/218967/155790426147320_zh-CN.png)


## 影响范围 {#section_kch_bq4_m2b .section}

启用了脚本检查参数（-enable-script-checks）的所有版本。

## 防护建议 {#section_x4q_cq4_m2b .section}

您可以通过选择以下适合的方案防护该Consul漏洞：

-   禁用Consul服务器上的脚本检查功能
-   如果您需要使用Consul的脚本检查功能，请升级至0.9.4、1.0.8、1.1.1、1.2.4中的一个版本（这些版本中包含-enable-local-script-checks参数），将Consul配置中的-enable-script-checks更改为-enable-local-script-checks。
-   确保Consul HTTP API服务无法通过外网访问或调用
-   启用Web应用防火墙的精准访问控制功能，配置以下防护规则。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/218967/155790426147322_zh-CN.png)


## 更多信息 {#section_yls_mn4_m2b .section}

安全管家服务可以为您提供包括安全检测、安全加固、安全监控、安全应急等一系列专业的安全服务项目，帮助您更加及时、有效地应对漏洞及黑客攻击，详情请关注[安全管家服务](https://www.aliyun.com/product/sos)。

