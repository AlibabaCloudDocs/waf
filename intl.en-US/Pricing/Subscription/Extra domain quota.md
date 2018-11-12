# Extra domain quota {#concept_zsf_cvd_n2b .concept}

## What is the default domain quota? {#section_pbn_cvd_n2b .section}

After you activate Alibaba Cloud WAF, you can deploy it for one domain name to provide protection. By default, a total of ten subdomains \(including the root domain\) of one domain name can be configured with a WAF instance. A subdomain can be a wildcard domain.

Taking `abc.com` for example, you can enable WAF protection for up to ten subdomains, such as `www.abc.com`, `\*.abc.com`, `mail.abc.com`, `user.pay.abc.com`, and `x.y.z.abc.com`. The root domain `abc.com` is also regarded as one of the ten subdomains.

## What is an extra domain quota? {#section_rbn_cvd_n2b .section}

If you want to enable WAF protection for more than one domain names or more than 10 subdomains, you can buy an extra domain quota. Assume that you have already configured `abc.com` or its subdomains with your WAF instance. When you try to add `xyz.com` \(another domain name\) to the WAF protection list, you will receive a system prompt informing you that the domain quota is exceeded.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15541/15419900087289_en-US.png)

In this case, you must upgrade the service to purchase an extra domain quota. For more information, see [Renewal and upgrade](intl.en-US/Pricing/Renewal and upgrade.md#).

On the Upgrade page, select the number of extra domains you want and complete the payment.

