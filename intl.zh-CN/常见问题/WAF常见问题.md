# WAF常见问题

本文汇总了您在购买和使用Web应用防火墙（WAF）时的常见问题。

-   售前咨询问题
    -   [非阿里云服务器能否使用WAF？](#section_gh5_30i_8dd)
    -   [WAF支持云虚拟主机吗？](#section_4ot_vhn_lr7)
    -   [WAF是否支持防护HTTPS业务？](#section_lhx_wwx_2dy)
    -   [WAF是否支持自定义端口？](#section_1kb_tmq_etu)
    -   [WAF的QPS限制规格是针对整个WAF实例汇总的QPS，还是配置的单个域名的QPS上限？](#section_gti_77s_y1g)
    -   [WAF哪些版本支持短信防刷？](#section_i9n_4eq_fxi)
    -   [WAF是否支持HTTPS双向认证？](#section_8vh_d8q_l7q)
    -   [WAF是否支持Websocket、HTTP 2.0或SPDY协议？](#section_o0b_5z7_sfp)
    -   [WAF支持哪些SSL协议？](#section_lda_atd_b8h)
    -   [WAF是否支持接入采用NTLM协议认证的网站？](#section_qz6_ku4_9as)
-   网站接入配置问题
    -   [WAF中的源站IP可以填写ECS内网IP吗？](#section_f39_s8b_788)
    -   [WAF能够保护在一个域名下的多个源站IP吗？](#section_kiv_2vu_kn4)
    -   [WAF配置多个源站时如何负载？](#section_hnl_jl2_b0f)
    -   [WAF是否支持健康检查？](#section_531_5ry_lzh)
    -   [WAF是否支持会话保持？](#section_g2y_ez7_zxn)
    -   [修改WAF的源站IP是否有延迟？](#section_vfn_2gs_sdr)
    -   [WAF的回源IP段是多少？](#section_wj9_s6i_6qj)
    -   [WAF是否会自动将WAF回源IP段加入安全组？](#section_og6_h6h_pf4)
    -   [WAF回源是否需要放行所有客户端IP？](#section_7zd_nhc_56u)
    -   [WAF的独享IP是否能够防御DDoS攻击？](#section_s10_fsh_yxt)
    -   [WAF能和CDN或DDoS高防一起接入吗？](#section_1jz_tnq_me3)
    -   [WAF是否支持跨账号使用CDN+高防+WAF的架构？](#section_g02_y48_bsv)
    -   [跨账号迁移网站配置时需要注意什么？](#section_isn_6f4_2po)
-   网站防护配置问题
    -   [WAF如何防御CC攻击？](#section_w3y_x9e_ik6)
    -   [在WAF管理控制台更改配置后大约需要多久生效？](#section_toy_4ti_4db)
    -   [WAF自定义防护策略（ACL访问控制）中的IP字段是否支持填写网段？](#section_2c3_w4b_mzi)
    -   [为什么URL匹配字段包含双斜杠（//）的自定义防护策略规则不会生效？](#section_cup_65t_0x5)
-   网站防护分析问题
    -   [WAF管理控制台中能查看CC攻击的攻击者IP吗？](#section_lcj_2l0_ng8)
    -   [如何查询WAF使用的带宽流量？](#section_tgu_d2s_02g)

## 非阿里云服务器能否使用WAF？

可以，WAF支持云外机房用户接入。WAF可以保护任何公网路由可达的服务器，不论是阿里云、其他的云服务、IDC机房等环境，都可以使用WAF。

**说明：** 在中国内地地域接入的域名必须按照工信部要求完成ICP备案，否则不支持接入。

## WAF支持云虚拟主机吗？

支持，WAF的所有版本都支持独享虚拟主机，直接开通WAF进行配置即可。

对于共享虚拟主机，由于使用的是共享IP，源站由多个用户共同使用，不建议单独配置WAF。

## WAF是否支持防护HTTPS业务？

支持，WAF的所有版本都支持HTTPS业务，并且支持泛域名接入。

只需根据提示将SSL证书及私钥上传，WAF即可防护HTTPS业务流量。配置HTTPS业务接入后，WAF会先解密访问请求，检查请求包，再重新加密，并转发正常的请求到源站。

## WAF是否支持自定义端口？

WAF企业版及旗舰版支持自定义非标准端口（企业版最多支持10个非标准端口；旗舰版最多支持50个非标准端口）。

**说明：** 不是任意端口都支持自定义，非标准端口必须在支持范围内，详细信息请参见[支持的自定义端口范围](/intl.zh-CN/接入WAF/支持的自定义端口范围.md)。

## WAF的QPS限制规格是针对整个WAF实例汇总的QPS，还是配置的单个域名的QPS上限？

Web应用防护墙QPS限制规格针对整个WAF实例。

例如，您的WAF配置防护了三个域名，则这三个域名累加的QPS不能超过规定上限。如果超过已购买的WAF实例的QPS限制，将触发限速，可能导致随机丢包。

## WAF哪些版本支持短信防刷？

WAF所有版本都支持短信防刷。更多信息，请参见[套餐规格与功能说明](/intl.zh-CN/产品简介/套餐规格与功能说明.md)。

## WAF是否支持HTTPS双向认证？

WAF暂时不支持HTTPS双向认证。

## WAF是否支持Websocket、HTTP 2.0或SPDY协议？

WAF支持WebSocket协议，且企业版及以上规格支持HTTP 2.0。目前暂不支持SPDY协议。

## WAF支持哪些SSL协议？

-   中国内地的WAF实例支持以下SSL协议：
    -   TLS v1.0
    -   TLS v1.1
    -   TLS v1.2
-   海外地区的WAF实例支持以下SSL协议：
    -   TLS v1.1
    -   TLS v1.2

`ssl_ciphers`套件样例：

```
"ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES128-SHA256:DHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:DES-CBC3-SHA:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!MD5:!PSK:!RC4"
```

## WAF是否支持接入采用NTLM协议认证的网站？

不支持。如果网站使用NTLM协议认证，经WAF转发的访问请求可能无法通过源站服务器的NTLM认证，客户端将反复出现认证提示。建议您使用其他方式进行网站认证。

## WAF中的源站IP可以填写ECS内网IP吗？

不可以。WAF通过公网进行回源，不支持直接填写内网IP。

## WAF能够保护在一个域名下的多个源站IP吗？

可以，一个WAF域名配置中最多支持配置20个源站IP地址。

## WAF配置多个源站时如何负载？

如果您配置了多个源站IP地址，WAF会自动采用轮询的方式对访问请求进行负载均衡。

## WAF是否支持健康检查？

WAF默认启用健康检查。WAF会对所有源站IP进行接入状态检测，如果某个源站IP没有响应，WAF会将访问请求转发至其他源站IP。

**说明：** 源站IP无法响应时，WAF将为该源站IP自动设置一个静默时间。静默时间结束后，新的访问请求可能仍然会被转发至该源站IP。关于WAF的健康检查工作原理，请参见负载均衡SLB服务的[健康检查概述](/intl.zh-CN/用户指南/健康检查/健康检查概述.md)。

## WAF是否支持会话保持？

WAF支持会话保持，但默认不开启。如果您需要使用，请[工单](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80)联系技术支持团队，申请开启会话保持。

## 修改WAF的源站IP是否有延迟？

有。修改WAF已防护的源站IP后，大约需要一分钟生效。

## WAF的回源IP段是多少？

您可以在[Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)的**系统管理** \> **产品信息**页面查询WAF的回源IP段。更多信息，请参见[放行WAF回源IP段](/intl.zh-CN/接入WAF/CNAME接入/放行WAF回源IP段.md)。

## WAF是否会自动将WAF回源IP段加入安全组？

WAF不会自动将WAF回源IP段添加到安全组。如果您的源站部署了其他防火墙或主机安全防护软件，建议您将WAF回源IP段添加至相应的白名单中。

建议您配置源站保护策略，对您的源站进行安全防护。详细信息，请参见[设置源站保护](/intl.zh-CN/接入WAF/CNAME接入/设置源站保护.md)。

## WAF回源是否需要放行所有客户端IP？

根据您的业务情况，您可以只放行WAF回源IP段，也可以放行所有客户端IP。

对于Web业务，建议您只放行WAF回源IP，实现源站保护。

## WAF的独享IP是否能够防御DDoS攻击？

可以。

-   WAF给每个用户提供独立的IP，该IP同样适用DDoS防护的黑洞策略，和ECS、SLB服务器一致。
-   WAF的黑洞阈值和当前地区ECS的默认阈值相同。

## WAF能和CDN或DDoS高防一起接入吗？

WAF完全兼容CDN和DDoS高防服务。同时接入WAF、CDN和DDoS高防的最佳部署架构为：客户端 \> DDoS高防 \> CDN \> WAF \> 负载均衡 \> 源站。

WAF与DDoS高防或CDN一起接入时，只要将WAF提供的CNAME地址配置为DDoS高防或CDN的源站即可。这样就可以实现流量在经过DDoS高防或CDN之后，被转发到WAF，再通过WAF最终转发至源站，从而对源站进行全面的安全防护。更多信息，请参见以下文档：

-   [同时部署WAF和CDN](/intl.zh-CN/接入WAF/云产品接入WAF/同时部署WAF和CDN.md)
-   [同时部署WAF和DDoS高防](/intl.zh-CN/接入WAF/云产品接入WAF/同时部署WAF和DDoS高防.md)

## WAF是否支持跨账号使用CDN+高防+WAF的架构？

支持，您可以跨账号使用CDN、高防、WAF产品组合成抵御DDoS攻击和Web应用攻击的安全架构。

## 跨账号迁移网站配置时需要注意什么？

为了防止网站配置迁移误操作导致业务流量转发出现问题，在您删除网站配置后，有一段时间的域名保护期。如果您需要将WAF的网站配置迁移到另一个账号下，在原账号中删除网站配置后，您需要等待30分钟后才能在另一个账号的WAF实例中添加该域名的网站配置。

如果您需要快速添加该网站配置，请[工单](https://workorder-intl.console.aliyun.com/?#/ticket/add/?productId=80)或在钉钉服务群中申请解除该域名的保护期。待保护期解除后，您就可以在新的账号中添加该域名的网站配置。

## WAF如何防御CC攻击？

WAF提供多种CC安全防护模式，您可以根据实际情况进行选择。详细信息，请参见[设置CC安全防护](/intl.zh-CN/网站防护配置/访问控制/限流/设置CC安全防护.md)。

如果您希望同时有好的防护效果和低误杀率，建议您选择WAF企业版和旗舰版，由安全专家定制针对性的防护算法。详细信息，请参见[设置自定义防护策略](/intl.zh-CN/网站防护配置/访问控制/限流/设置自定义防护策略.md)。

## 在WAF管理控制台更改配置后大约需要多久生效？

一般情况下，更改后的配置在一分钟内即可生效。

## WAF自定义防护策略（ACL访问控制）中的IP字段是否支持填写网段？

支持。

## 为什么URL匹配字段包含双斜杠（//）的自定义防护策略规则不会生效？

由于WAF的规则引擎在处理URL匹配字段时会进行标准化处理，默认将连续的正斜杠（/）进行压缩，因此无法正确匹配包含双斜杠（//）URL的自定义防护策略规则。

如果您需要对包含双斜杠（//）的URL设置ACL访问控制，您可以直接设置该URL对应的单斜杠路径作为匹配条件。例如，如果需要将`//api/sms/request`作为URL匹配字段的条件值，您只需在匹配内容中填写`/api/sms/request`，WAF即可针对包含该内容的请求进行访问控制。

## WAF管理控制台中能查看CC攻击的攻击者IP吗？

可以。您可以开通WAF日志服务，然后使用日志查询功能查询CC攻击的攻击者IP信息。更多信息，请参见[开启WAF日志服务](/intl.zh-CN/日志管理/日志服务/开启WAF日志服务.md)、[使用日志查询](/intl.zh-CN/日志管理/日志服务/使用日志查询.md)。

## 如何查询WAF使用的带宽流量？

您可以在[Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)的**总览**页面查看已使用的带宽流量情况。

