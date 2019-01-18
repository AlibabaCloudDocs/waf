# 为什么不能直接访问WAF生成的CNAME域名？ {#concept_cnf_y1l_q2b .concept}

Web应用防火墙或高防IP生成的CNAME域名是用于DNS解析的，不能直接访问。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15600/15477936047988_zh-CN.png)

如果直接访问CNAME域名，可能显示504页面，或者本帮助页面。

