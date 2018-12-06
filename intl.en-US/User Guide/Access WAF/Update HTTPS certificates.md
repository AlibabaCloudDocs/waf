# Update HTTPS certificates {#task_tgm_wwj_5fb .task}

To let Alibaba Cloud WAF inspect HTTPS traffic for your web business, you must include HTTPS in the protocol type in [website configuration](intl.en-US/User Guide/Access WAF/Website configuration.md#), and upload a valid HTTPS certificate to WAF. If the certificate changes, you must update the certificate in the Alibaba Cloud WAF console in a timely manner.

If you have uploaded the certificate file to [Alibaba Cloud SSL Certificate Service](https://yundunnext.console.aliyun.com/?p=casnext) for integrated management, then in the following steps, you can reuse it directly instead of uploading it again.

Otherwise, you must have the certificate and private key files prepared, to complete the following operations.

In general, the following files are required:

-   \*.crt（Public key）or \*.pem（Certificate）
-   \*.key（Private key）

1.  Log on to the [Alibaba Cloud WAF console](https://yundun.console.aliyun.com/?p=waf). 
2.  On the top of the page, select the region: **Mainland China**, **International**. 
3.  On the **Management** \> **Website Configuration** page, locate the domain name to be operated, and click the Update Certificate button \(![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154407458031794_en-US.png)\) next to the **HTTPS** **Protocol Status**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154407458031793_en-US.png)

 
4.  In the Update Certificate dialog box, select an **Upload method**. 
    -   If the HTTPS certificate to be uploaded is hosted in [Alibaba Cloud SSL Certificate Service](https://yundunnext.console.aliyun.com/?p=casnext), you can check **Select existing certificate** and select it for upload.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154407458031795_en-US.png)

    -   Manual upload. Click **Manual upload**, enter a **Certificate name**, and paste the text context of the certificate file and private key file respectively to the **Certificate file** and **Private key file** boxes.

        **Note:** 

        -   For certificates in general formats, such as PEM, CER, and CRT, you can open the certificate file directly by using a text editor tool to copy the text content. For certificates in other formats, such as PFX and P7B, convert the certificate file to the PEM format, and then copy the text content from the converted certificate file.
        -   If the HTTPS certificate has multiple certificate files, such as a certificate chain file, merge the text contents from the multiple certificate files and paste them into the **Certificate file** box.
        **Example of the text content of a certificate file**:

        ```
        -----BEGIN CERTIFICATE-----
        xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx8ixZJ4krc+1M+j2kcubVpsE2
        cgHdj4v8H6jUz9Ji4mr7vMNS6dXv8PUkl/qoDeNGCNdyTS5NIL5ir+g92cL8IGOkjgvhlqt9vc
        65Cgb4mL+n5+DV9uOyTZTW/MojmlgfUekC2xiXa54nxJf17Y1TADGSbyJbsC0Q9nIrHsPl8YKk
        vRWvIAqYxXZ7wRwWWmv4TMxFhWRiNY7yZIo2ZUhl02SIDNggIEeg==
        -----END CERTIFICATE-----
        ```

        **Example of the text content of a private key file**:

        ```
        -----BEGIN RSA PRIVATE KEY-----
        DADTPZoOHd9WtZ3UKHJTRgNQmioPQn2bqdKHop+B/dn/4VZL7Jt8zSDGM9sTMThLyvsmLQKBgQ
        Cr+ujntC1kN6pGBj2Fw2l/EA/W3rYEce2tyhjgmG7rZ+A/jVE9fld5sQra6ZdwBcQJaiygoIYo
        aMF2EjRwc0qwHaluq0C15f6ujSoHh2e+D5zdmkTg/3NKNjqNv6xA2gYpinVDzFdZ9Zujxvuh9o
        4Vqf0YF8bv5UK5G04RtKadOw==
        -----END RSA PRIVATE KEY-----
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154407458031796_en-US.png)

5.  Click **Save** to complete the procedure. 

The HTTPS protocol status displays as **Normal**.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63378/154407458031803_en-US.png)

