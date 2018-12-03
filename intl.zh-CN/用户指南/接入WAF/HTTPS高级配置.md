# HTTPS高级配置 {#task_kmv_qz3_p2b .task}

WAF提供灵活的HTTPS配置功能，帮助您在不改造源站的情况下，一键实现全站HTTPS和强制客户端使用HTTPS连接。

1.  登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)。 
2.  在页面上方选择地域：**中国大陆**、**海外地区**。 
3.  在**管理** \> **网站配置**页面，选择要操作的域名，单击其操作列下的**编辑**。 
4.  在**协议类型**下勾选**HTTPS**，并单击打开**高级设置**菜单。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15554/15438232397688_zh-CN.jpg)

 
    -   **开启HTTP回源**

        如果您的网站不支持HTTPS回源，请**开启HTTP回源**（默认回源端口是80端口），通过WAF实现HTTPS访问。使用该设置后，客户端可以通过HTTP和HTTPS方式访问站点。

        **说明：** 使用HTTP回源，可以无需在源站服务器上做任何改动，也不需要配置HTTPS。但是，该配置的前提是**在WAF上传正确的证书和私钥**（证书可以在阿里云证书免费申请）。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15554/15438232397689_zh-CN.jpg)

    -   **开启HTTPS的强制跳转**

        如果您需要强制客户端使用HTTPS来访问（从安全性考虑，推荐这样做），您可以**开启HTTPS的强制跳转**。

        **说明：** 开启HTTPS强制跳转前必须先取消HTTP协议。

        选择开启HTTPS的强制跳转后，部分浏览器将被缓存设置为使用HTTPS请求访问网站，请确保您的网站支持HTTPS业务。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15554/15438232397690_zh-CN.jpg)

        开启HTTPS强制跳转后，HTTP请求将显示为HTTPS，默认跳转到443端口。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15554/15438232397691_zh-CN.jpg)


