# Big data deep learning engine best practices {#concept_1113021 .concept}

Alibaba Cloud web application firewall \(WAF\) provides comprehensive protection for your website by combining multiple web attack detection engines. WAF uses a combination of rule engine, semantic analysis engine, and deep learning engine to fully take the advantages of Alibaba Cloud's powerful intelligence, data analysis system, and expert vulnerability mining experience. Based on Alibaba Cloud's attack data analysis, 0day vulnerabilities are captured. Then, security experts actively mine and analyze the vulnerabilities, and finally summarize the vulnerabilities as protection rules and policies. The rules and policies of WAF are updated every week, exceeding the industry average speed. WAF commits to providing users with the fastest and most comprehensive protection capabilities.

With the development of the Internet, web attack methods are constantly evolving. Traditional single-means protection methods cannot meet the security needs of complex Internet services. Only collaborative protection by multiple detection engines can achieve the best protection effect.

Alibaba Cloud WAF uses a combination of rule engine, semantic analysis engine, and deep learning engine to defend against web attacks.

-   **Rule engine**: Uses protection policy rules based on the expert experience accumulated by Alibaba Group over the years.
-   **Semantic analysis engine**: Makes up the weak description of context-independent grammar features in the regular syntax field in traditional rule engine, reducing the security risks caused by false positives and vulnerabilities of rules.
-   **Deep learning engine**: Conducts classification training for hundreds of millions of attack data on Alibaba Cloud every day through a neural network system built by Alibaba Cloud's powerful algorithm team through supervised learning. Finally, the model detects and intercepts unknown 0day vulnerabilities in real time, making up for other defense engines to detect unknown 0day vulnerabilities.

## Deep learning engine protection practice {#section_itw_lsn_0r9 .section}

Generally, the rules engine uses strong descriptive rules. For requests with obvious attack features, the protection effect of regular rules is the best. However, in the face of attacks without obvious features \(such as XSS feature requests\), even if you enable the strict protection mode for web application attacks, it may still have potential security risks due to the inability to detect them.

For example, you can enable the big data deep learning engine feature in WAF to identify and intercept attack requests without obvious features that cannot be identified by strict rules for web application attack protection.

In this case, the following XSS attack requests are not blocked by web application attack protection rules.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/895635/156679024951287_en-US.png)

After enable the [Big Data Deep Learning Engine](../../../../reseller.en-US/User Guide/Configuration/Big data deep learning engine.md#) feature, the XSS attack request that exceeds the regular rule engine's detection capability is successfully blocked.

Additionally, you can view detailed attack log information in the web application attack report. The attack type is**Deep learning**.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/895635/156679024951289_en-US.png)

