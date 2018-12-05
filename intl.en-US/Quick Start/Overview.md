# Overview {#concept_n21_zx1_p2b .concept}

After activating Alibaba Cloud WAF, you must create a website configuration and update the DNS settings to deploy WAF for your website. With WAF enabled, you can configure WAF protection policies at anytime to handle complicated web attacks, or use the default settings to protect against common web attacks and HTTP flood attacks. Alibaba Cloud WAF provides you with an all-round protection visualization to help you understand your web businesses’ security events and risks.

You can get started with Alibaba Cloud WAF by performing the following tasks.

|Task|Description|Recommended method|Prerequisites|
|----|-----------|------------------|-------------|
|[1. Automatically add a website configuration](intl.en-US/Quick Start/Step1: Automatically add a website configuration.md#)|Create a website configuration in the Alibaba Cloud WAF console to associate your website with the WAF instance.|Automatically create a website configuration.| -   The domain name to be protected is hosted at Alibaba Cloud DNS. Besides, its DNS settings must include at least one valid A record.
-   \(For Mainland China region\) The website is granted an ICP license by the Ministry of Industry and Information Technology \(MIIT\).
-   \(For HTTPS-enabled websites\) You have access to a valid SSL certificate and private key of the website, or you have uploaded the certificate to Alibaba Cloud SSL Certificate Service.

 |
|[\(Optional\) 2. Update the DNS settings](intl.en-US/Quick Start/Step 2: Update the DNS settings.md#)|Modify the domain name’s DNS settings \(CNAME record\) at its DNS host to redirect web traffic to Alibaba Cloud WAF for inspection.**Note:** Required when you are prompted to do so in Step 1: Automatically add a website configuration or you manually add the website configuration.

|Enable a CNAME record for the domain name by using the WAF CNAME address as the value.| -   Obtain the WAF CNAME address.
-   You have permissions to update the domain’s DNS settings in the DNS host’s system.

 |
|[3. Configure WAF protection policies](intl.en-US/Quick Start/Step 3: Configure WAF protection polices.md#)|Enable/Disable different WAF protection functions and manage their related rules in the Alibaba Cloud WAF console.|Use the default protection settings.|Alibaba Cloud WAF is successfully deployed for the website and the DNS resolution status of the website configuration is normal.|
|[4. View security reports](intl.en-US/Quick Start/Step 4: View security reports.md#)|View security reports of your website in the Alibaba Cloud WAF console.| -   Use the Overview page to view security summary statistics for your business.
-   Use the Reports page to view detailed attack protection records and risk warnings.

 |Alibaba Cloud WAF is successfully deployed for the website and the DNS resolution status of the website configuration is normal.|

