# Web应用防火墙常见问题 {#concept_rws_35k_q2b .concept}

-   [非阿里云内的服务器能否使用Web应用防火墙？](#)
-   [Web应用防火墙支持云虚拟主机吗？](#)
-   [Web应用防火墙如何防护CC攻击？](#)
-   [Web应用防火墙是否支持HTTPS的业务防护？](#)
-   [Web应用防火墙是否支持自定义端口？](#)
-   [Web应用防火墙QPS限制规格是针对整个Web应用防火墙实例汇总的QPS，还是配置的单个域名的QPS上限？](#)
-   [Web应用防火墙哪些版本支持短信防刷？](#)
-   [Web应用防火墙中的源站IP可以填写ECS内网IP吗？](#)
-   [Web应用防火墙能和CDN或高防IP一起接入吗？](#)
-   [Web应用防火墙能够保护在一个域名下的多个源站IP吗？](#)
-   [Web应用防火墙配置多个源站时如何负载？](#)
-   [Web应用防火墙是否支持健康检查？](#)
-   [Web应用防火墙是否支持会话保持？](#)
-   [修改Web应用防火墙的源站IP是否有延迟？](#)
-   [在Web应用防火墙管理控制台中，更改配置后大约需要多少时间生效？](#)
-   [Web应用防火墙的回源IP段是多少？](#)
-   [Web应用防火墙是否会自动将WAF的回源IP段加入安全组？](#)
-   [Web应用防火墙回源是否需要放行所有客户端IP？](#)
-   [Web应用防火墙管理控制台中能查看CC攻击的攻击者IP吗？](#)
-   [如何查询Web应用防火墙使用的带宽流量？](#)
-   [Web应用防火墙的精准访问控制中IP字段是否支持填写网段？](#)
-   [Web应用防火墙IP的DDoS攻击相关说明？](#)
-   [Web应用防火墙是否支持HTTPS双向认证？](#)
-   [Web应用防火墙是否支持Websocket、HTTP 2.0或SPDY协议？](#)
-   [Web应用防火墙支持的SSL协议有哪些？](#)
-   [Web应用防火墙是否支持跨账号使用CDN+高防+WAF架构？](#)
-   [匹配条件中的URL匹配字段包含双斜杠“//”的精准访问控制规则为何不生效？](#)
-   [Web应用防火墙是否支持接入采用NTLM协议认证的网站防护？](#section_wgn_qt3_mgb)

## 非阿里云内的服务器能否使用Web应用防火墙？ {#section_tfb_j5k_q2b .section}

Web应用防火墙支持云外机房用户接入。Web应用防火墙可以保护任何公网路由可达的服务器，不论是在阿里云、或是其他的云、IDC机房等环境，都可以使用Web应用防火墙服务。

**说明：** 在大陆地区接入的域名必须按照工信部要求进行ICP备案。

## Web应用防火墙支持云虚拟主机吗？ {#section_ufb_j5k_q2b .section}

Web应用防火墙的所有版本都支持独享虚拟主机，直接开通Web应用防火墙进行配置即可。

对于共享虚拟主机，由于使用的是共享IP，源站是多个用户在使用，不建议单独配置Web应用防火墙。

## Web应用防火墙如何防护CC攻击？ {#section_vfb_j5k_q2b .section}

Web应用防火墙提供不同的CC安全防护模式：正常和攻击紧急。您可以根据实际情况进行选择。具体请参考[选择CC防护模式](../../../../../intl.zh-CN/用户指南/防护配置/CC安全防护.md#)。

如果您希望同时有好的防护效果和低误杀率，建议您选择Web应用防火墙企业版和旗舰版，自定义或让安全专家为您定制针对性的防护算法。配置方法请参考[自定义CC防护](../../../../../intl.zh-CN/用户指南/防护配置/自定义CC防护.md#)。

## Web应用防火墙是否支持HTTPS的业务防护？ {#section_wfb_j5k_q2b .section}

Web应用防火墙的所有版本都支持HTTPS业务，并且支持泛域名接入。

只需根据提示将SSL证书及私钥上传，Web应用防火墙即可防护HTTPS业务流量。配置HTTPS业务接入后，Web应用防火墙会解密访问请求，检查请求包，再重新加密，并转发回给源站。

## Web应用防火墙是否支持自定义端口？ {#section_xfb_j5k_q2b .section}

Web应用防火墙企业版及旗舰版支持自定义非标准端口（企业版最多支持10个非标准端口；旗舰版最多支持50个非标准端口）。

**说明：** 不是任意端口都支持自定义，非标准端口必须在支持范围内，详情请参考[非标端口支持](../../../../../intl.zh-CN/用户指南/使用DNS配置模式接入WAF/非标端口支持.md#)。

## Web应用防火墙QPS限制规格是针对整个Web应用防火墙实例汇总的QPS，还是配置的单个域名的QPS上限？ {#section_yfb_j5k_q2b .section}

Web应用防护墙QPS限制规格是针对整个Web应用防火墙实例。例如，您的Web应用防火墙配置防护了三个域名，则这三个域名累加的QPS不能超过规定上限。如果超过已购买的Web应用防火墙实例的QPS限制，将触发限速，可能导致随机丢包。

## Web应用防火墙哪些版本支持短信防刷？ {#section_zfb_j5k_q2b .section}

Web应用防火墙所有版本都支持短信防刷。关于Web应用防火墙各版本功能，请查看[Web应用防火墙各版本功能介绍](../../../../../intl.zh-CN/产品定价/开通WAF/WAF各版本功能说明.md#)。

## Web应用防火墙中的源站IP可以填写ECS内网IP吗？ {#section_agb_j5k_q2b .section}

Web应用防火墙中是通过公网进行回源的，不支持直接填写内网IP。

## Web应用防火墙能和CDN或高防IP一起接入吗？ {#section_bgb_j5k_q2b .section}

Web应用防火墙完全兼容CDN和高防IP服务。同时接入WAF、CDN和高防IP的最佳部署架构如下：**客户端 \> DDoS高防IP \> CDN \> Web应用防火墙 \> 负载均衡 \> 源站**

Web应用防火墙与高防IP或CDN一起接入时，只要将Web应用防火墙提供的CNAME配置为高防IP或CDN的源站即可。这样，即可实现流量在经过高防IP或CDN之后，被转发至Web应用防火墙，再通过Web应用防火墙最终转发至源站，从而对源站进行全面的安全防护。

具体配置方法，请查看[高防IP结合WAF](../../../../../intl.zh-CN/用户指南/使用DNS配置模式接入WAF/同时部署WAF和DDoS高防.md#)及[CDN结合WAF](../../../../../intl.zh-CN/用户指南/使用DNS配置模式接入WAF/同时部署WAF和CDN.md#) 。

## Web应用防火墙能够保护在一个域名下的多个源站IP吗？ {#section_cgb_j5k_q2b .section}

支持，一个Web应用防火墙域名防护最多支持20个回源IP。

## Web应用防火墙配置多个源站时如何负载？ {#section_dgb_j5k_q2b .section}

如果您配置了多个回源IP，Web应用防火墙会自动采用轮询的方式对访问请求进行负载均衡。

## Web应用防火墙是否支持健康检查？ {#section_egb_j5k_q2b .section}

Web应用防火墙默认启用健康检查。Web应用防火墙会对所有源站IP进行接入状态检测，如果某个源站IP没有响应，Web应用防火墙会将访问请求转发至其它源站IP。

**说明：** 源站IP无法响应时，Web应用防火墙将为该源站IP自动设置一个静默时间。静默时间结束后，新的访问请求可能仍然会被转发至该源站IP。关于WAF的健康检查工作原理，参考SLB服务的[健康检查原理](../../../../../intl.zh-CN/历史文档/用户指南（旧版控制台）/监听/健康检查/健康检查介绍.md#)。

## Web应用防火墙是否支持会话保持？ {#section_fgb_j5k_q2b .section}

Web应用防火墙支持会话保持，默认不开启。如果您需要使用，请通过工单联系技术支持团队申请开启。

## 修改Web应用防火墙的源站IP是否有延迟？ {#section_ggb_j5k_q2b .section}

修改Web应用防火墙已防护的源站IP后，大约一分钟之内即可生效。

## 在Web应用防火墙管理控制台中，更改配置后大约需要多少时间生效？ {#section_hgb_j5k_q2b .section}

一般情况下，更改后的配置在一分钟内即可生效。

## Web应用防火墙的回源IP段是多少？ {#section_igb_j5k_q2b .section}

您可以登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf) 中，在**管理** \> **网站配置**页面查看详细的Web应用防火墙回源IP段。详情请参考[如何查看Web应用防火墙回源IP段](intl.zh-CN/常见问题/如何查看Web应用防火墙回源IP段？.md#)。

## Web应用防火墙是否会自动将WAF的回源IP段加入安全组？ {#section_jgb_j5k_q2b .section}

Web应用防火墙不会自动将高防回源IP段添加到安全组。如果您的源站部署了其它防火墙或主机安全防护软件，建议您将WAF回源IP段添加至相应的白名单中。

您可以参考[源站保护](../../../../../intl.zh-CN/最佳实践/源站保护.md#)，对您的源站进行安全防护配置。

## Web应用防火墙回源是否需要放行所有客户端IP？ {#section_kgb_j5k_q2b .section}

根据您的业务情况，您可以只放行WAF回源IP段，也可以放行所有客户端IP。

对于Web业务，建议您只放行WAF回源IP，实现[源站保护](../../../../../intl.zh-CN/最佳实践/源站保护.md#)。

## Web应用防火墙管理控制台中能查看CC攻击的攻击者IP吗？ {#section_lgb_j5k_q2b .section}

Web应用防火墙旗舰版支持在业务分析页面的全量日志检索中查看CC攻击的攻击者IP信息。

## 如何查询Web应用防火墙使用的带宽流量？ {#section_mgb_j5k_q2b .section}

您可以在Web应用防火墙控制台的总览页面查看已使用的带宽流量情况。

## Web应用防火墙的精准访问控制中IP字段是否支持填写网段？ {#section_ngb_j5k_q2b .section}

Web应用防火墙支持在精准访问控制规则的IP字段中输入IP网段。

## Web应用防火墙IP的DDoS攻击相关说明？ {#section_pgb_j5k_q2b .section}

-   Web应用防火墙给每个用户提供独立的IP，该IP同样适用DDoS防护的黑洞策略，和ECS、SLB服务器一致。
-   Web应用防火墙的黑洞阈值和当前地区ECS的默认阈值相同。

DDoS攻击可以通过购买[DDoS高防IP](https://www.alibabacloud.com/product/ddos-pro)服务进行防护。

## Web应用防火墙是否支持HTTPS双向认证？ {#section_rgb_j5k_q2b .section}

Web应用防火墙暂时不支持HTTPS双向认证。

## Web应用防火墙是否支持Websocket、HTTP 2.0或SPDY协议？ {#section_sgb_j5k_q2b .section}

Web应用防火墙已支持WebSocket协议，但目前暂不支持HTTP 2.0及SPDY协议。

## Web应用防火墙支持的SSL协议有哪些？ {#section_tgb_j5k_q2b .section}

**支持的SSL协议**：

-   TLSv1
-   TLSv1.1
-   TLSv1.2

**SSL\_ciphers 套件样例**：

```
"ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES128-SHA256:DHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:DES-CBC3-SHA:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!MD5:!PSK:!RC4"
```

## Web应用防火墙是否支持跨账号使用CDN+高防+WAF架构？ {#section_vgb_j5k_q2b .section}

支持，您可以跨账号使用CDN、高防、WAF产品组合成抵御DDoS和Web攻击的安全架构。

## 匹配条件中的URL匹配字段包含双斜杠“//”的精准访问控制规则为何不生效？ {#section_wgb_j5k_q2b .section}

由于WAF的规则引擎在处理URL匹配字段时会进行标准化处理，默认将连续的斜杠“/”进行压缩，因此无法正确匹配包含双斜杠“//”URL的精准访问控制规则。

如果您需要对指定包含双斜杠“//”的URL进行访问控制，您可以直接设置该URL对应的单斜杠路径作为匹配条件。例如，你需要将`//api/sms/request`作为URL匹配字段的条件值，您只需在匹配内容中填写`/api/sms/request`，WAF即可针对包含该URI的请求进行访问控制。

## Web应用防火墙是否支持接入采用NTLM协议认证的网站防护？ {#section_wgn_qt3_mgb .section}

Web应用防火墙不支持接入使用NTLM协议认证的网站，经WAF转发的访问请求可能无法通过源站服务器的NTLM认证，客户端将反复出现认证提示。

建议您的网站采用其他方式进行认证。

