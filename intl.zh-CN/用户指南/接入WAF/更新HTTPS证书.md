# 更新HTTPS证书 {#task_tgm_wwj_5fb .task}

要使Web应用防护墙（WAF）帮助您监控HTTPS业务流量，您必须在[网站配置](intl.zh-CN/用户指南/接入WAF/网站配置.md#)中勾选HTTPS协议，并上传HTTPS证书，保证HTTPS协议状态正常。如果证书发生变化，您也要在WAF控制台及时更新证书。

如果您已将证书文件上传到[云盾证书服务](https://yundunnext.console.aliyun.com/?p=casnext)进行统一管理，那么在以下步骤中，您可以选择一个已有证书进行更新。

否则，您需要准备好网站的证书和私钥文件，以完成以下操作。

一般情况下，您所需准备的证书相关内容包括：

-   \*.crt（公钥文件）或\*.pem（证书文件）
-   \*.key（私钥文件）

1.  登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)。 
2.  在页面上方选择地域：**中国大陆**、**海外地区**。 
3.  在**管理** \> **网站配置**页面，选择要操作的域名，单击其**HTTPS****协议状态**右侧的上传按钮（![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154382276531794_zh-CN.png)）。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154382276531793_zh-CN.png)

 
4.  在更新证书对话框中，选择**上传方式**并上传证书。 
    -   如果该域名所绑定的HTTPS证书已添加至[云盾证书服务](https://yundunnext.console.aliyun.com/?p=casnext)进行管理，您可以单击**选择已有证书**，直接选择想要上传的证书。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154382276531795_zh-CN.png)

    -   手动上传证书。单击**手动上传**，填写**证书名称**，并将该域名所绑定的证书文件和私钥文件中的文本内容分别复制粘贴到**证书文件**和**私钥文件**文本框中。

        **说明：** 

        -   对于.pem、.cer、.crt格式的证书，您可以使用文本编辑器直接打开证书文件，并复制其中的文本内容；对于其他格式（如.pfx、.p7b等）的证书，则需要将证书文件转换成.pem格式后，才能用文本编辑器打开并复制其中的文本内容。

            关于证书格式的转换方式，请参考[HTTPS证书转换成PEM格式](https://www.alibabacloud.com/help/faq-detail/40526.htm)。

        -   如果该HTTPS证书有多个证书文件（如证书链），需要将证书文件中的文本内容拼接合并后粘贴至**证书文件**文本框中。
        **证书文件文本内容样例**：

        ```
        -----BEGIN CERTIFICATE-----
        xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx8ixZJ4krc+1M+j2kcubVpsE2
        cgHdj4v8H6jUz9Ji4mr7vMNS6dXv8PUkl/qoDeNGCNdyTS5NIL5ir+g92cL8IGOkjgvhlqt9vc
        65Cgb4mL+n5+DV9uOyTZTW/MojmlgfUekC2xiXa54nxJf17Y1TADGSbyJbsC0Q9nIrHsPl8YKk
        vRWvIAqYxXZ7wRwWWmv4TMxFhWRiNY7yZIo2ZUhl02SIDNggIEeg==
        -----END CERTIFICATE-----
        ```

        **私钥文件文本内容样例**：

        ```
        -----BEGIN RSA PRIVATE KEY-----
        DADTPZoOHd9WtZ3UKHJTRgNQmioPQn2bqdKHop+B/dn/4VZL7Jt8zSDGM9sTMThLyvsmLQKBgQ
        Cr+ujntC1kN6pGBj2Fw2l/EA/W3rYEce2tyhjgmG7rZ+A/jVE9fld5sQra6ZdwBcQJaiygoIYo
        aMF2EjRwc0qwHaluq0C15f6ujSoHh2e+D5zdmkTg/3NKNjqNv6xA2gYpinVDzFdZ9Zujxvuh9o
        4Vqf0YF8bv5UK5G04RtKadOw==
        -----END RSA PRIVATE KEY-----
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154382276531796_zh-CN.png)

5.  单击**保存**，成功上传证书和私钥文件。 

HTTPS协议状态显示为**正常**。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154382276531803_zh-CN.png)

