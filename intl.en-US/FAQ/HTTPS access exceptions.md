# HTTPS access exceptions {#concept_wml_wdl_q2b .concept}

This topic provides troubleshooting methods for HTTPS access exceptions after the website is connected to WAF \(HTTP access is normal\). The symptoms include failure to open the page, the system prompts that the certificate cannot be trusted, failure to call some ports, and access errors for certain machine types, operation systems, and Apps.

## HTTPS enabled and certificate uploaded? {#section_rdt_wdl_q2b .section}

When using WAF to protect HTTPS services, you must select HTTPS in the WAF console and upload the certificate/key that is exactly the same as that of the server. Even when WAF is used in sync with Anti-DDoS Pro, SLB, CDN, and other products, you must upload the certificate/key in the WAF console. WAF certificate is independent of other products.

**Note:** Once you upload the certificate in the console, it may take up to five minutes for the configuration to be effective. During this period, you may still encounter access exceptions. You can [bind hosts](../../../../../reseller.en-US/User Guide/Access WAF/Perform redirect check with a local computer.md#), and switch DNS resolution once WAF is configured and effective.

## Is certificate chain complete? {#section_sdt_wdl_q2b .section}

In most cases, the certificate service provider provides you with multiple certificates \(including the server certificate and one or more CA root certificates\), which together form a complete certificate chain. Taking Alibaba Cloud certificate as an example, the certificate chain you may receive is shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15608/15477937747999_en-US.png)

Make sure that you upload the complete certificate chain in WAF \(as shown in the preceding figure\). Also, pay attention to the sequence of the certificate when you upload them. Such as **the server certificate must be at the top, and the root certificate must be at the bottom** and, combine text content of the multiple certificates. The following is an example of the certificate content you need to upload.

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

If the certificate chain is incomplete, the page may prompt that the certificate cannot be trusted, and some Android mobile phones, operation systems, or Apps may encounter access errors or exceptions \(the access may be normal in some environments\).

You can also use third-party inspection tools available on the Internet \(for example, [GeoCerts™ SSL Checker](https://www.geocerts.com/ssl_checker)\) to check if the current certificate chain is complete.

**Note:** This method can only check the domain name status that can be resolved. If you already resolve the domain name to the origin rather than WAF, you cannot check the certificate status in WAF.

## SNI Problem {#section_ydt_wdl_q2b .section}

If only some specified clients or applications cannot normally access the HTTPS service, the system prompts “SSL handshake failed/error”, or “the certificate cannot be trusted”, it may be because the client does not support SNI. These clients or applications may be old Android devices, calling programs \(especially programs using SSL protocol\) developed with an older version of JAVA, IE browser running on a Windows XP, some old version mobile phones, and some third-party payment callback interfaces.

Currently, most browsers, applications, and WeChat and Alipay callback interfaces support SNI. It may be the SNI compatibility problem if the access returns to normal when you resolve the domain name to the origin, and you encounter exceptions if you resolve the domain name to the WAF. You can upgrade the client, or directly resolve the callback interface to the origin.

For more information, see [HTTPS access exceptions arising from SNI compatibility \(Certificate not trusted\)](reseller.en-US/FAQ/HTTPS access exceptions arising from SNI compatibility ("Certificate not trusted").md#).

## Windows Server 2003/IIS6 server {#section_zdt_wdl_q2b .section}

Access HTTPS service from Windows Server 2003 or IIS6 server that is connected to WAF may cause a white screen or 502 error. Because the TLS version and encryption suite of these systems are too old, the security performance is too weak, and it is not compatible with WAF’s default HTTPS back-to-source algorithm. WAF does not support HTTPS back-to-source requests for Windows Server 2003, and Microsoft officially suggests not to use Windows Server 2003 to build HTTPS sites. For your communication security, we recommend that you upgrade your operating system to Windows Server 2008 or later.

## Link failure caused by short DH key {#section_a2t_wdl_q2b .section}

Short DH \(Diffie-Hellman\) keys are known for security problems. WAF does not support short keys anymore. Likewise, you can see similar errors when you use a later version of the Firefox browser \(for example, 51.0.1\) to access the origin, even when you are not using WAF.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15608/15477937748000_en-US.png)

We recommend that you upgrade the related components \(such as JDK version\), to make sure that **the server’s DH key algorithm is 2048 bits or more**.

**Note:** Length of a key is determined by the server’s encryption algorithm, and has nothing to do with the certificate. If you do not know how to operate, contact your server developer, or search for the related solutions. You can find the related solutions based on the following error messages: `SSL routines:ssl3_check_cert_and_algorithm:dh key too small`.

## HTTP enabled for services requiring HTTP redirect? {#section_c2t_wdl_q2b .section}

If you have set on the origin to force redirect HTTP access requests to HTTPS, then you must select both HTTP and HTTPS in WAF. Otherwise, these HTTP requests cannot be normally forwarded to the origin after they are redirected to WAF, and the system throws an error.

