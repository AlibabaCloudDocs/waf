# 什么是Web应用防火墙

Web应用防火墙（Web Application Firewall，简称 WAF）为您的网站或App业务提供一站式安全防护。WAF可以有效识别Web业务流量的恶意特征，在对流量进行清洗和过滤后，将正常、安全的流量返回给服务器，避免网站服务器被恶意入侵导致服务器性能异常等问题，保障网站的业务安全和数据安全。

## 主要功能

-   提供Web应用攻击防护。
-   缓解恶意CC攻击，过滤恶意的Bot流量，保障服务器性能正常。
-   提供业务风控方案，解决业务接口被恶意滥刷等业务安全风险。
-   提供网站一键HTTPS和HTTP回源，降低源站负载压力。
-   支持对HTTP和HTTPS流量进行精准的访问控制。
-   支持超长时长的全量日志实时存储、分析和自定义报表服务，支持日志线上同步第三方平台，助力满足等保合规要求。

## 如何使用WAF

您购买WAF后，可以通过CNAME接入的方式把网站域名接入到WAF集群进行防护。您只需把域名解析到WAF提供的CNAME地址上，并配置源站服务器IP，即可启用WAF。启用WAF后，您网站所有的公网流量都会先经过WAF，恶意攻击流量在WAF上被检测过滤，而正常流量返回给源站IP，从而确保源站IP安全、稳定、可用。详细内容，请参见[网站接入](/intl.zh-CN/接入WAF/CNAME接入/网站接入.md)。

## 计费概述

WAF支持包年包月（预付费）的计费方式。包年包月计费方式支持按一个月、三个月、半年和一年购买。详细内容，请参见[计费方式](/intl.zh-CN/产品定价/计费方式.md)。

