# 自定义TLS配置

已接入WAF防护的网站域名，如果网站使用的是HTTPS协议传输数据，WAF支持对该域名自定义TLS协议版本和加密套件，更灵活地满足您对于更高安全性（例如等保合规场景）或更高的TLS通信兼容性（例如兼容客户端旧版本的TLS协议）的需求。

-   已开通WAF企业版及以上版本。
-   网站域名使用的是HTTPS协议且已上传了HTTPS证书。

您可以为已接入的域名指定TLS协议版本和加密套件，WAF将对使用了不在指定范围内的TLS协议版本和加密套件的访问流量进行拦截，有效保证网站的通信安全。

如果网站使用的是HTTP协议传输数据，则无需配置TLS，您可以直接跳过本文。

## 适用版本

WAF各版本对TLS协议版本和加密套件的支持情况，说明如下：

|WAF版本|TLS协议版本|加密套件|
|-----|-------|----|
|高级版|不支持|不支持|
|企业版|支持**说明：** 支持选择以下TLS版本：

-   TLS 1.0及以上（包括1.0、1.1、1.2）
-   TLS 1.1及以上（包括1.1、1.2）
-   TLS 1.2及以上（仅包括1.2）

|支持**说明：** 仅支持选择**全部加密套件**和**强加密套件**两种模板。加密套件具体信息，请参见[配置TLS](#section_54v_2a0_1lq)中的步骤4。 |
|旗舰版、独享版|支持**说明：** 支持选择以下TLS版本：

-   TLS 1.0及以上（包括1.0、1.1、1.2）
-   TLS 1.1及以上（包括1.1、1.2）
-   TLS 1.2及以上（仅包括1.2）

支持同时开启TLS 1.3。

|支持**说明：** 支持选择**全部加密套件**、**强加密套件**、**自定义加密套件**三种模板。加密套件具体信息，请参见[配置TLS](#section_54v_2a0_1lq)中的步骤4。 |

## 配置TLS

1.  登录[Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)。

2.  在左侧导航栏，选择**资产中心** \> **网站接入**。

3.  在**网站接入**页面，定位到需要配置TLS的域名，单击**TLS配置**。

    **说明：** 仅使用了HTTPS协议的网站域名需要配置TLS。如果网站域名使用的是HTTP协议或者使用HTTPS协议但是未上传HTTPS证书，此处您将不会看到**TLS配置**按钮。

4.  在**TLS安全策略配置**页面，对TLS协议版本和加密套件进行自定义配置。

    |配置项|说明|
    |---|--|
    |**域名**|需要自定义配置TLS的网站域名。此项已自动填写，无需您手动设置。|
    |**TLS协议版本**|选择网站使用的TLS版本。可选项：    -   **支持TLS 1.0及以上版本，兼容性最高，安全性较低**：选择该项表示对TLS 1.0及以上所有版本生效。
    -   **支持TLS 1.1及以上版本，兼容性较好，安全性较好**：选择该项表示对TLS 1.1及以上所有版本生效，使用TLS 1.0将无法访问该网站。
    -   **支持TLS 1.2及以上版本，兼容性较好，安全性最高**：选择该项表示对TLS 1.2及以上所有版本生效，使用TLS 1.0和1.1将无法访问该网站。 |
    |开启TLS 1.3|支持同时开启TLS 1.3。|
    |**加密套件**|选择您需要使用的加密套件类型。可选项：    -   **全部加密套件，兼容性最高，安全性较低**，支持以下强加密套件和弱加密套件：
        -   强加密套件：
            -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256
            -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384
            -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_CBC\_SHA256
            -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_CBC\_SHA384
            -   TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256
            -   TLS\_ECDHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384
            -   TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256
            -   TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384
            -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_CBC\_SHA
            -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_CBC\_SHA
        -   弱加密套件：
            -   TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA
            -   TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA
            -   TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256
            -   TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384
            -   TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256
            -   TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256
            -   TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA
            -   TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA
            -   SSL\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA
    -   **强加密套件，兼容性最低，安全性较高**，支持以下强加密套件：
        -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256
        -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384
        -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_CBC\_SHA256
        -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_CBC\_SHA384
        -   TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256
        -   TLS\_ECDHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384
        -   TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256
        -   TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384
        -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_CBC\_SHA
        -   TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_CBC\_SHA
    -   **协议版本的自定义加密套件，请谨慎选择，避免影响业务** |

5.  单击**保存**，配置即可生效。

    WAF会对使用了不在指定范围内的TLS协议版本和加密套件的访问流量进行拦截。


