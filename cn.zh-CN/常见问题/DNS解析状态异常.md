# DNS解析状态异常 {#concept_zth_yzk_q2b .concept}

在Web应用防火墙（WAF）中完成网站配置后，WAF自动执行以下检测：

-   DNS解析检测：每小时执行一次，检测网站的域名解析是否指向WAF CNAME地址。
-   流量检测：每数分钟执行一次，检测最近数分钟内该域名的访问流量是否经过WAF。

只有当两者都正常时，域名的DNS解析状态才正常。

您可以登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)，在**管理** \> **网站配置**页面查看域名的接入状态，即DNS解析状态。

正常接入的结果如下图：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15598/15438269127971_zh-CN.jpg)

如果DNS解析状态提示异常，则WAF可能没有正确接入。如果您确认已将域名解析到WAF的CNAME地址，并且业务访问也都正常，可以忽略此处的提示。

## DNS解析状态判断条件 {#section_yrq_yzk_q2b .section}

WAF根据以下条件判断域名的DNS解析状态：

**说明：** 满足其中一个条件就判断为接入正常，会提示已接入WAF防护。

-   条件1：接入的域名是通过CNAME解析过来的。
-   条件2：接入的域名有一定的流量。在五秒内至少有多于10个请求才判断为有一定流量。如果每分钟只有两、三个请求，则流量太低，判断为无流量。历史流量可在[攻击防护报表](../../../../intl.zh-CN/用户指南/防护统计/攻击防护报表.md#)下的CC攻击报表中查看。

推荐您使用CNAME而不是A记录的方式接入WAF，因为前者可以在机房故障等极端情况下切换到其他的节点或机房，实现灾备，使用A记录接入时则无法实现灾备。正常情况下，WAF也支持使用A记录接入。

## 常见DNS解析异常状态 {#section_x5b_f1l_q2b .section}

-   当您使用精确域名（不包含“\*”的域名，如example.abc.com）接入WAF时，如果既没有CNAME接入，又没有流量，则会显示以下异常状态：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15598/15438269127972_zh-CN.jpg)

-   当您使用泛域名（如\*.abc.com）接入WAF时，除了正常的解析状态，只会出现以下一种异常状态：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15598/15438269137973_zh-CN.jpg)

-   WAF前部署了CDN等代理

    假如接入架构为CDN\>WAF，则域名解析在CDN上，这时不会检测到WAF有CNAME接入。通常CDN回源WAF的流量会很低，可能会由于流量太小而引起接入状态异常。所以，如果确认配置没有问题，接入状态显示异常并不一定代表WAF没有正确接入。

    关于CDN结合Web应用防火墙的配置，请参考[CDN结合WAF](../../../../intl.zh-CN/用户指南/接入WAF/同时部署WAF和CDN.md#)。


## 如何手动测试WAF在正常防护网站 {#section_cts_g1l_q2b .section}

1.  访问WAF防护的网址（如www.abc.com），网页可以正常打开。
2.  在网址的URL后面加/alert\(xss\)（如www.abc.com/alert\(xss\)），继续访问。这是一个Web攻击的测试请求，如果弹出WAF阻拦该请求的405页面，则说明WAF防护在正常工作。

