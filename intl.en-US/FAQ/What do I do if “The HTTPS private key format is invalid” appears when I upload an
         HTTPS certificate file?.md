# What do I do if “The HTTPS private key format is invalid” appears when I upload an HTTPS certificate file?

## Problem description

The system prompts "The HTTPS private key format is invalid" when you upload an HTTPS certificate file to WAF.

## Cause

The private key of the certificate may be encrypted. WAF cannot identify the encrypted private key.

## Solution

1.  View the private key file. If the private key file contains the content that is marked in the red box in the following figure, the private key is encrypted.

    ![Private key encryption](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9880746061/p8006.png)

2.  Run the following command and enter a password to decrypt the private key:

    ```
    openssl rsa -in [$keyName] -text
    #[$keyName] indicates the name of the private key file.
    ```

    If the following result is returned, the private key is decrypted.

    ![Private key decryption](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0980746061/p8007.png)

3.  Re-upload the decrypted private key file to WAF.

