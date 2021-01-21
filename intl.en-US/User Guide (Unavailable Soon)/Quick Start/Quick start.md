# Quick start

This topic describes how to configure and use Web Application Firewall \(WAF\) after you activate WAF. To use WAF, you must complete the configuration procedure of WAF so that your website can be protected by WAF. You can view the security reports and statistics to learn about the security status of your website.

## Procedure

|Operation|Description|Recommended method|Prerequisites|
|---------|-----------|------------------|-------------|
|[1. Add website configurations automatically]()|Add the website configuration for the website that needs protection in the WAF console.|Add website configurations automatically.|-   The domain name of the website is managed by Alibaba Cloud DNS, and you have created an A record on Alibaba Cloud DNS.
-   \(Mainland China regions\) You have obtained an ICP license for the website.
-   \(HTTPS-based websites\) You have obtained the HTTPS certificate and the private key file of the website, or the HTTPS certificate is managed by Alibaba Cloud SSL Certificates Service. |
|[\(Optional\) 2. Change DNS records]()|Change the DNS record of the website to redirect requests that are sent to the website to WAF for monitoring. **Note:** You must perform this operation when you are required to manually change the DNS record, or you need to manually add a website configuration.

|Change the CNAME record to configure WAF.|-   You have obtained the WAF CNAME address.
-   You have the permissions to change DNS records at your DNS service provider. |
|[3. Specify WAF protection policies]()|Specify and adjust WAF protection policies in the WAF console.|Use the default protection settings.|You have configured WAF for your website and DNS resolution is working properly.|
|[4. View security reports]()|View security reports of your website in the WAF console.|-   View your business and security status on the Overview page.
-   View security details and risk warnings on the Reports page.

|You have configured WAF for your website and DNS resolution is working properly.|

