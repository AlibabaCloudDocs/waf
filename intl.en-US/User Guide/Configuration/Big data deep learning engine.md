# Big data deep learning engine {#task_1796669 .task}

Through supervised learning, the big data deep learning engine of web application firewall relies on the neural network system built by Alibaba Cloud powerful algorithm team, Alibaba Cloud conducts classification training for hundreds of millions of attack data each day, and finally detects and intercepts unknown risk requests online in real time through the model. This makes up for other defense engines to detect unknown 0day vulnerabilities.

Make sure that you have added the target domain in WAF for protection. For more information, see [Implement Alibaba Cloud WAF](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Configure DNS settings.md#).

With the development of the Internet, web attack methods are constantly evolving. Traditional single-means protection methods cannot meet the security needs of complex Internet services. Only collaborative protection by multiple detection engines can achieve the best protection effect.

Based on continuous learning and modeling of normal business models, the big data deep learning engine identifies and warns of abnormal and risky behaviors in real time, providing users with the fastest and most comprehensive protection capabilities.

**Note:** The big data deep learning engine mainly targets web attack requests without obvious features, rather than HTTP flood attacks. If you have high web attack protection requirements, we recommend that you enable the big data deep learning engine.

The main features of the big data deep learning engine are as follows:

-   Semantics: New intelligent protection engine merges the similar behavior characteristics of similar attacks and aggregates the attack behaviors and characteristics of a single attack class into an attack feature. By grouping the multiple behavioral characteristics of attacks into specific permutations and combinations to represent individual attack classes, this function creates a semantic structure for attack behavior.
-   Exception and attack set: Leveraging Alibaba Cloud Security’s massive volume of operations data, this function models normal web applications, so that abnormalities can be detected. It extracts exception and attack models from a large volume of web application attacks to form an exception and attack set.

1.  Log on to the [Web Application Firewall console](https://partners-intl.console.aliyun.com/#/waf).
2.  Go to the **Management** \> **Website Configuration** page and select the region of your WAF instance \(**Mainland China** or **International**\).
3.  Locate to the domain name to be configured and click **Policies**.
4.  In the **Big Data Deep Learning Engine** area, turn on the feature and select the protection mode. 

    -   **Report**: Only alert you of the detected attack.
    -   **Block**: Block the detected attack directly.
    **Note:** If you do not require the big data deep learning engine feature, you can turn off it on this page.

    ![Big data deep learning engine](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15562/15667987827758_en-US.jpg)


