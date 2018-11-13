# 独享IP包 {#concept_qp5_k5n_42b .concept}

如果您有重要的域名需要使用额外分配WAF IP进行防护，您可以选用独享IP包。

## 什么是独享IP包 {#section_zcb_n5n_42b .section}

Web应用防火墙（WAF）开通后，每个WAF实例默认拥有一个WAF IP，该WAF IP可用于接入多个域名进行防护。通过购买独享IP包，您可为当前WAF实例开启额外的独享IP，用于接入单个域名实现独享防护。

**说明：** 一个独享 IP仅可以绑定一个域名。

通过独享IP包为域名开启独享防护，帮助您避免一个域名遭受大流量DDoS攻击导致其他域名也无法访问。默认情况下，接入WAF实例防护的所有域名都使用同一个WAF IP。因此，当其中一个域名遭受大流量DDoS攻击导致WAF IP进入黑洞时，该WAF实例所防护的其他域名也无法访问。通过购买额外的独享IP包，您可以为重要域名分配独享IP，避免重要域名的访问因其他域名的WAF IP进入黑洞而受到影响。

## 如何购买独享IP包 {#section_kpn_55n_42b .section}

对于按照包年包月模式开通的Web应用防火墙实例，您可以在购买实例时选购额外的独享IP包。

**说明：** 对于已经购买的Web应用防火墙实例，您可以通过[升级WAF实例](intl.zh-CN/产品定价/续费与升级.md#ol_ut4_hdn_42b)来选购额外的独享IP包。

## 如何分配和启用独享IP包 {#section_fdb_n5n_42b .section}

登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)，定位到**管理** \> **网站配置**页面，找到需要分配独享IP的域名，单击打开该域名的**独享IP**开关。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15542/15420727567433_zh-CN.png)

启用独享IP后，该域名的CNAME将自动解析至新的独享IP。您可以通过Ping该域名的CNAME确认该域名是否已自动解析到新的WAF IP。

**说明：** 如果域名是通过A记录而不是CNAME进行解析，该域名的解析无法完成自动切换。您需要通过Ping该域名的CNAME获得新的WAF IP，并尽快将该域名的DNS手动解析至新的独享IP。

