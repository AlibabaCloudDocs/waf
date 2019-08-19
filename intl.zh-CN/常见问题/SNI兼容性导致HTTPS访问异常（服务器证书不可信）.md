# SNI兼容性导致HTTPS访问异常（服务器证书不可信） {#concept_mrv_5wl_q2b .concept}

本文介绍了因客户端不兼容SNI，导致业务接入Web应用防火墙后出现HTTPS访问异常的解决方法。

## 背景介绍 {#section_hhm_bxl_q2b .section}

随着IPv4地址的短缺，为了让多个域名复用一个IP地址，在HTTP服务器上引入了虚拟主机的概念。服务器可以根据客户端请求中不同的Host，将请求分配给不同的域名（虚拟主机）来处理。在一个被多个域名（虚拟主机）共享IP的HTTPS服务器中，当浏览器访问一个HTTPS站点时，会首先与服务器建立SSL连接。建立SSL连接的第一步是请求服务器的证书。服务器在发送证书时，不知道浏览器访问的是哪个域名，所以不能根据不同域名发送不同的证书。

SNI（Server Name Indication）是为了解决一个服务器使用多个域名和证书的SSL/TLS扩展。它的工作原理是：在与服务器建立SSL连接之前，先发送要访问站点的域名（Hostname），这样服务器会根据这个域名返回一个合适的证书。

目前，大多数操作系统和浏览器都已经很好地支持SNI扩展。OpenSSL 0.9.8 已经内置这一功能，新版的Nginx也支持SNI。

## 问题描述 {#section_ihm_bxl_q2b .section}

在接入Web应用防火墙后，如果您出现HTTPS访问异常问题，可能是由于客户端不支持SNI导致的。

当使用不支持SNI的浏览器访问Web应用防火墙的网站时，Web应用防火墙因不知道客户端请求的是哪个域名，无法调取对应的虚拟主机证书来跟客户端交互，只能使用内置的一个缺省证书去跟客户端握手，这时在客户端浏览器上会提示“服务器证书不可信”。

如果客户端不支持SNI，可能会出现如下现象：

-   在手机App客户端，iOS客户端可以正常访问，而Android客户端无法正常打开。
-   浏览器打开网站，显示证书不可信。

## 解决方案 {#section_khm_bxl_q2b .section}

您可以在客户端抓SSL握手的报文，来判断客户端是否支持SNI。以Chrome浏览器访问阿里云官网为例。

若在Client Hello报文里可以看到SNI扩展，则表示客户端支持SNI扩展。

![sni,扩展](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15617/15661929928024_zh-CN.png)

否则，客户端不支持SNI扩展。对于不支持SNI的客户端有以下建议：

-   建议您升级或使用新版本的浏览器（如Chrome、Firefox等）。
-   如果是微信、支付宝第三方回调，需要让其调用源站IP，绕过Web应用防火墙。

## SNI兼容性 {#section_nhm_bxl_q2b .section}

**说明：** SNI兼容TLS1.0及以上协议，但不被SSL支持。

-   SNI支持以下桌面版浏览器：
    -   Chrome 5及以上版本
    -   Chrome 6及以上版本（Windows XP）
    -   Firefox 2及以上版本
    -   IE 7及以上版本（运行在Windows Vista/Server 2008及以上版本系统中，在XP系统中任何版本的IE浏览器都不支持SNI）
    -   Konqueror 4.7及以上版本
    -   Opera 8及以上版本
    -   Safari 3.0 on Windows Vista/Server 2008及以上版本，Mac OS X 10.5.6 及以上版本
-   SNI支持以下库：
    -   GNU TLS
    -   Java 7及以上版本，仅作为客户端
    -   HTTP client 4.3.2及以上版本
    -   libcurl 7.18.1及以上版本
    -   NSS 3.1.1及以上版本
    -   OpenSSL 0.9.8j及以上版本
    -   OpenSSL 0.9.8f及以上版本，需配置flag
    -   Qt 4.8及以上版本
    -   Python3、Python 2.7.9及以上版本
-   SNI支持以下手机端浏览器：
    -   Android Browser on 3.0 Honeycomb及以上版本
    -   iOS Safari on iOS 4及以上版本
    -   Windows Phone 7及以上版本
-   SNI支持以下服务器：
    -   Apache 2.2.12及以上版本
    -   Apache Traffic Server 3.2.0及以上版本
    -   HAProxy 1.5及以上版本
    -   IIS 8.0及以上版本
    -   lighttpd 1.4.24及以上版本
    -   LiteSpeed 4.1及以上版本
    -   nginx 0.5.32及以上版本
-   SNI 支持以下命令行：
    -   cURL 7.18.1及以上版本
    -   wget 1.14及以上版本

