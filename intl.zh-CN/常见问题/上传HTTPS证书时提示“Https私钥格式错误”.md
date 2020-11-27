# 上传HTTPS证书时提示“Https私钥格式错误”

## 问题描述

在Web应用防火墙上传HTTPS证书时提示“Https私钥格式错误”。

## 问题原因

证书的私钥可能被加密了。Web应用防火墙无法识别被加密的私钥。

## 解决方案

1.  查看私钥文件。如果私钥文件中包含如下图红框中标注的内容，则说明私钥被加密。

    ![私钥加密](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3957385951/p8006.png)

2.  执行以下命令并输入密码，解密私钥文件。

    ```
    openssl rsa -in [$keyName] -text
    #[$keyName]表示私钥文件名称。
    ```

    如果返回结果如下图所示，则说明私钥解密成功。

    ![私钥解密](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3957385951/p8007.png)

3.  在Web应用防火墙重新上传解密后的私钥内容。

