# Quick start

This topic walks you through how to quickly deploy and use Web Application Firewall \(WAF\). WAF protects your website only after you purchase a WAF instance, add your website to WAF, and configure website protection policies. WAF also provides security reports that show attack records and access statistics. This way, you can monitor the security status of your service.

## Step 1: Purchase a WAF instance

1.  Log on to the [Web Application Firewall console](https://yundun.console.aliyun.com/?p=waf).

2.  On the **Welcome to Web Application Firewall \(WAF\)** page, click **Purchase WAF Subscription** to go to the buy page.

    If you have purchased a WAF instance, the **Welcome to Web Application Firewall \(WAF\)** page is not displayed. You can go to the WAF console. For more information, see [Step 2: Add a website to WAF](#section_g5c_r2c_ip7).

    ![Welcome to Web Application Firewall (WAF) - International site](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7601543061/p173419.png)

3.  On the **Web Application Firewall** buy page, select the product edition and specifications, and complete the payment.

    For more information, see [Purchase a WAF instance](/intl.en-US/Billing and Service Activation/Subscription/Purchase a WAF instance.md).

4.  After you purchase a WAF instance, go back to the WAF console.


## Step 2: Add a website to WAF

To add a website to WAF, you must add the domain name of the website to the WAF console and change the DNS record to redirect the traffic destined for the website to WAF for protection.

1.  Add the website.

    1.  On the **Website Access** page, click **Add Domain Name**.

    2.  On the **Add Domain Name** page, select the website that you want to protect and a protocol. Then, click **Manually Add Other Websites**.

        WAF automatically adds the websites under your Alibaba cloud account. If no websites are discovered under your Alibaba Cloud account, the **Add Domain Name** page is not displayed. Follow the next step to add your websites.

    3.  Complete the **Add Domain Name** wizard.

        For more information, see [Manually add website configurations](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).

        **Note:** If you configure a proxy, such as Anti-DDoS Pro, Anti-DDoS Premium, or Content Delivery Network \(CDN\) before WAF, select **Yes** for **Does a layer 7 proxy \(DDoS Protection/CDN, etc.\) exist in front of WAF**. Otherwise, WAF cannot obtain the actual IP addresses of clients.

        ![Enter the website information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7601543061/p66025.png)

    After the website is added to WAF, you can view its CNAME address on the **Website Access** page.

    ![CNAME record](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7801549951/p97144.png)

    **Note:** If your website uses HTTPS, you must upload the SSL certificate for the domain name of the website. This way, WAF can process HTTPS traffic. For more information, see [Upload HTTPS certificates](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).

2.  Change the DNS record of the domain name to map the domain name to the CNAME address assigned by WAF.

    -   If you do not configure a proxy, such as Anti-DDoS Pro, Anti-DDoS Premium, or CDN, before WAF, visit the website of your DNS service provider and change the CNAME record. In the record, use the CNAME address assigned by WAF. If you use Alibaba Cloud DNS, log on to the [Alibaba Cloud DNS](https://dns.console.aliyun.com/#/dns/domainList) console to change the DNS record.

        ![Change a CNAME record ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7801549951/p7590.png)

        For more information, see [Change a DNS record](/intl.en-US/Website Access/Website access with CNAME/Change a DNS record.md).

    -   If you configure a proxy, such as Anti-DDoS Pro, Anti-DDoS Premium, or CDN, before WAF, go to the console of the proxy service and change the back-to-origin address of the proxy to the CNAME address assigned by WAF. This way, WAF receives the requests destined for your website.

        For more information, see [Deploy WAF and Anti-DDoS Pro together](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and Anti-DDoS Pro together.md) and [Deploy WAF and CDN together](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and CDN together.md).


## Step 3: Configure website protection policies

After you add the domain name, WAF filters access requests and forwards normal requests to the origin server of the domain name. WAF provides multiple protection features to protect your website against different types of attacks. Among the features, only **RegEx Protection Engine** and **HTTP Flood Protection** are enabled by default. The RegEx Protection Engine feature protects your website against common web attacks, such as SQL injection, Cross-Site Scripting \(XSS\) attacks, and webshell upload. The HTTP Flood Protection feature protects your website against HTTP flood attacks. You need to manually enable other features and configure protection rules. For more information, see [Overview](/intl.en-US/Website Protection Settings/Overview.md).

## Step 4: View security reports

On the **Security report** page, you can view the attack records and access statistics of the websites that WAF protects. For more information, see [View security reports](/intl.en-US/.md).

![Security reports](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7601543061/p173206.png)

