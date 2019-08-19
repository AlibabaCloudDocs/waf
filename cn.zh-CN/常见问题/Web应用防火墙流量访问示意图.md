# Web应用防火墙流量访问示意图 {#concept_kvh_qgl_q2b .concept}

本文介绍了Web应用防火墙的流量访问示意流程。

下图展示了Web应用防火墙的流量访问示意流程。

![流量访问,waf](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15613/15662058938656_zh-CN.png)

流程说明如下：

**说明：** Web应用防火墙的IP均在云上，即Web应用防火墙的VIP能够通过Banff查看流量。Web应用防火墙的VIP是一个LVS集群，您可以将Web应用防火墙的VIP理解为SLB的VIP，并在VNET上查到Web应用防火墙的VIP以及VIP后端的WAF Engine的IP地址。

1.  Client请求访问Web应用防火墙的VIP地址。
2.  Web应用防火墙的VIP将请求转发给LVS集群后方一台服务器（A）进行处理。
3.  服务器（A）将报文解析到7层，判断是否为恶意访问或者攻击。
    -   如果是正常访问，则转发给源站。
    -   如果是恶意访问，则阻断业务，直接将报文返回给Client并结束。
4.  源站收到转发的报文后进行处理，处理完成后将报文返回给服务器（A）。

    **说明：** 请注意步骤3和4中服务器（A）的角色变化。

    -   对于Client而言，服务器（A）为服务端。
    -   对于源站而言， 服务器（A）为客户端。
5.  服务器（A）将报文通过LVS的IP地址，返回给Client并结束。

