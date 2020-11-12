# Tutorial

Web Application Firewall \(WAF\) protects your website after you add it to WAF. If you do not add your website to WAF, WAF does not protect it.

## Add your website to WAF

After you activate WAF, you can add your website to WAF in **CNAME** mode.

After you add the domain name of your website in the WAF console, you must change the DNS record to redirect the traffic destined for your website to WAF. Then, WAF filters the traffic and forwards normal traffic to the origin server of the domain name. You can add the domain name by manually adding a website or by configuring WAF to automatically add a website.

In CNAME mode, perform the following operations to add a website:

1.  [Add websites](/intl.en-US/Website Access/Website access with CNAME/Add websites.md): This topic describes how to manually add a website or configure WAF to automatically add a website.

    **Note:**

    -   If your website uses HTTPS, you must upload a correct and valid HTTPS certificate in the WAF console so that HTTPS requests can be processed as normal. For more information, see [Upload HTTPS certificates](/intl.en-US/Website Access/Website access with CNAME/Add websites.md).
    -   If the origin server uses a port other than port 80 over HTTP and port 443 over HTTPS, you can customize the port in the WAF console. For more information, see [Supported custom ports](/intl.en-US/Website Access/Supported custom ports.md).
2.  [Allow access from WAF back-to-origin CIDR blocks](/intl.en-US/Website Access/Website access with CNAME/Allow access from WAF back-to-origin CIDR blocks.md): WAF uses specified back-to-origin CIDR blocks to forward normal traffic back to the origin server. To allow inbound traffic from the back-to-origin CIDR blocks, you must configure the security software or access control policies of the origin server when you add a website to WAF.
3.  [Verify domain name settings](/intl.en-US/Website Access/Website access with CNAME/Verify domain name settings.md): This topic describes how to set up a staging environment after a domain name is added and how to verify whether the traffic forwarding settings are in effect. You cannot change the DNS record before the settings take effect. Otherwise, your services are interrupted.
4.  [Change a DNS record](/intl.en-US/Website Access/Website access with CNAME/Change a DNS record.md): This topic describes how to manually change the DNS record to redirect the traffic destined for your website to WAF.

After you add the domain name, WAF filters access requests and forwards normal requests to the origin server of the domain name. WAF provides multiple protection features to protect your website against different types of attacks. Among the features, only **RegEx Protection Engine** and **HTTP Flood Protection** are enabled by default. The RegEx Protection Engine feature protects your website against common web attacks, such as SQL injection, Cross-Site Scripting \(XSS\) attacks, and webshell upload. The HTTP Flood Protection feature protects your website against HTTP flood attacks. You need to manually enable other features and configure protection rules. For more information, see [Overview](/intl.en-US/Website Protection Settings/Overview.md).

## Best practices

-   [Configure protection for an origin server](/intl.en-US/Website Access/Website access with CNAME/Configure protection for an origin server.md): If the origin server is deployed on an ECS instance, you can configure security group policies in the ECS or SLB instance to allow only inbound requests from WAF. This prevents web attackers from bypassing WAF and directly attacking the origin server.
-   [Retrieve actual IP addresses of clients](/intl.en-US/Website Access/Retrieve actual IP addresses of clients.md): After you configure WAF, all requests to your website are forwarded to WAF, and WAF forwards the processed requests to the origin server. You must use X-Forwarded-For to retrieve the actual IP addresses of sources that initiated these requests.

## Connect cloud services to WAF

-   [Deploy WAF and Anti-DDoS Pro together](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and Anti-DDoS Pro together.md): You can deploy Anti-DDoS Pro or Anti-DDoS Premium and WAF in sequence to protect your website against web and DDoS attacks.
-   [t15558.md\#](/intl.en-US/Website Access/Connect cloud services to WAF/Deploy WAF and CDN together.md): You can deploy your CDN service and WAF in sequence to protect your website against web attacks while accelerating your website.

