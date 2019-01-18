# HTTPS访问异常问题 {#concept_wml_wdl_q2b .concept}

接入WAF后出现HTTPS访问异常（HTTP是正常的），如页面打不开、提示证书不可信、部分接口调用失败、部分机型/操作系统/APP访问报错等问题，您可以参照本文提供的排错方法来排查问题。

## 确认控制台已勾选HTTPS并已上传证书 {#section_rdt_wdl_q2b .section}

使用WAF防护HTTPS业务时，必须在WAF控制台上勾选HTTPS，并且上传与服务器完全一样的证书/密钥。即使WAF与高防、SLB、CDN等其他产品一起使用时，也要在WAF上传证书/密钥。WAF的证书是独立于其他产品。

**说明：** 在控制台上传证书成功后，可能需要最多5分钟的时间来使配置完全生效，在此期间可能出现访问异常的现象。您可以[绑定hosts](../../../../../intl.zh-CN/用户指南/接入WAF/本地验证.md#)，确保配置已经生效之后，再将DNS解析切换过来。

## 确认证书链完整（常见错误） {#section_sdt_wdl_q2b .section}

多数情况下，证书服务商会提供给您多个证书（其中包含服务器的证书以及一个或多个CA根证书），这些证书组合成一个完整的证书链。以阿里云的证书为例，您收到的证书链如下图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15608/15477937667999_zh-CN.png)

请确保在WAF中上传了完整的证书链而不是只有部分证书。请将多个证书文本内容联合到一起，并**确保服务器证书在上面，根证书在下面**。以下是您需要上传的证书内容的一个样例。

```
-----BEGIN CERTIFICATE-----
MIIFdDCCBFygAwIBAgIQFmr88Z0mn6rEleGaC6UVEzANBgkqhkiG9w0BAQsFADCB
Obc3E+7h0u6cUXaQAmFNZ2a...
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIFYjCCBEqgAwINMTYwNjA3MDAwMDAwmlTaWduLCBJbmMuMRLnN5bWNiLmNvbS9
wY2EzLWc1Lm1hbnRlY1BLSS0yLTU...
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIG/TCCBeWgAwIBAgIQLMUH03pBzhUCrOR0SsKM+DANBgkqhkiG9w0BAQsFADB+
NzIDMgUHVibGljIFByaW1...
-----END CERTIFICATE-----
```

如果证书链不完整，可能会出现打开页面提示证书不可信，某些安卓手机、操作系统或App访问报错、异常等情况（可能部分环境下访问是正常的）。

您也可以借助网上的第三方检测工具（如[GeoCerts™ SSL Checker](https://www.geocerts.com/ssl_checker)）来检查当前的证书链是否完整。

**说明：** 这种方式只能检测当前解析到的域名状态。假如您已经将解析回源而没有解析到WAF，是无法检测WAF上的证书状态的。

## SNI问题 {#section_ydt_wdl_q2b .section}

如果出现特定的一些客户端或应用程序不能正常访问HTTPS业务，提示 “SSL handshake failed/error”或者证书不可信，则很可能是客户端不支持SNI引起的。这些客户端或应用程序可能是旧版本的安卓，低版本JAVA开发的一些调用程序（特别是使用SSL协商的程序）、XP系统的IE浏览器、某些老款手机，以及第三方的支付回调接口等。

目前绝大部分的浏览器和应用程序、微信、支付宝回调接口等都已全面支持SNI。如果您将解析切换回源站就恢复正常，切换到WAF就异常，则可能是这个问题。建议升级相关的客户端，或者将回调接口直接解析回源。

更多信息，请参考[SNI 兼容性导致HTTPS访问异常（服务器证书不可信）](intl.zh-CN/常见问题/SNI兼容性导致HTTPS访问异常（服务器证书不可信）.md#)。

## Windows Server 2003/IIS6服务器 {#section_zdt_wdl_q2b .section}

Windows Server 2003/IIS6服务器在接入WAF后，访问HTTPS业务会出现白屏和502现象。这是因为系统TLS版本和加密套件过旧，安全性太弱，与WAF默认的HTTPS回源算法不兼容。目前，我们不再支持对2003系统的HTTPS回源，微软官方也已不建议使用2003系统搭建HTTPS站点。为了您的通信安全，请升级至2008或以上的操作系统。

## DH密钥太短导致链接失败 {#section_a2t_wdl_q2b .section}

因为过短的DH（Diffie-Hellman）密钥存在安全问题，WAF已经停止对短密钥的支持。同样的，当您使用较新版本的火狐浏览器（如51.0.1）不经过WAF访问源站，也会看到相应的报错信息。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15608/15477937668000_zh-CN.png)

请升级相关组件（如JDK版本），**确保服务器DH算法的key位数为2048 bit 或更大**。

**说明：** Key的长度是服务器加密算法决定的，与证书无关。如果您不知道如何操作，请联系您的服务器开发人员，或搜索相关的解决方案。您可以根据以下报错信息来查找相关解决方案：`SSL routines:ssl3_check_cert_and_algorithm:dh key too small`。

## 需要HTTP跳转的业务也需要勾选HTTP {#section_c2t_wdl_q2b .section}

如在源站服务器做了访问HTTP强制跳转到HTTPS的设置，则必须在WAF上勾选HTTP和HTTPS。否则，HTTP请求到了WAF后，无法正常转发回源站，也会报错。

