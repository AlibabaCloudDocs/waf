# Features

Web Application Firewall \(WAF\) leverages core protection and big data capabilities to ensure web security and availability. You can use WAF to handle various web application attacks. This topic describes the features that WAF provides.

## Business configuration

You can configure protection policies to protect the HTTP and HTTPS traffic of your website. HTTPS protection is available in WAF Pro or higher editions.

## Web application protection

Protection against common web application attacks

-   WAF protects your services against common Open Web Application Security Project \(OWASP\) attacks. These attacks include SQL injections, XSS attacks, webshell uploads, backdoors, command injections, invalid HTTP requests, common web server vulnerabilities, unauthorized access to core files, path traversals, and scan attacks.
-   WAF supports website stealth to prevent server IP addresses from being exposed. Attack traffic cannot bypass WAF to reach your servers.
-   WAF implements regular and timely updates of patches for zero-day vulnerabilities. WAF synchronizes its protection rules with Taobao. Alibaba Cloud updates the latest patches and distributes the patches to WAF at the earliest opportunity to protect websites.
-   WAF supports user-friendly monitoring mode. You can enable the monitoring mode to monitor new website services. WAF alerts rather than intercepts suspicious attacks that match the protection rules to help measure false positives.

Precise protection

-   WAF parses HTTP data in common formats. The HTTP data includes header, form, multipart, JSON, and XML data.
-   WAF decodes data that is encoded by using the following methods: URL encoding, JavaScript Unicode encoding, HEX encoding, HTML entity encoding, Java serialization, PHP serialization, Base64 encoding, UTF-7 encoding, UTF-8 encoding, and nested encoding.
-   WAF preprocesses data to provide more fine-grained and accurate data sources for detection engines at the upper layer. The preprocessing mechanisms include space compression, comment pruning, and special character processing.
-   WAF detects data in complicated formats. WAF supports specific complexity in detection logic to avoid false positives caused by excessive detection operations. This reduces the false positive rate. WAF also supports adaptive decoding of data encoded in different formats. This avoids bypassing.

Protection against HTTP flood attacks

-   WAF restricts the frequency of access requests from a specific IP address based on different methods, such as CAPTCHA verification and redirection for authentication.
-   To protect against a large number of low-speed request attacks, WAF executes precise protection rules based on statistical data, such as distribution of status code, distribution of requested URLs, abnormal HTTP Referer headers, and User-Agent characteristics.
-   WAF takes full advantage of Alibaba Cloud big data to build analysis models for threat intelligence and trusted access. These models help identify malicious requests.

Precise access control

-   In the WAF console, you can combine different HTTP fields, such as IP, URL, Referer, and User-Agent fields, to configure policies and implement precise access control. You can configure specific policies to provide protection in different scenarios, such as hotlinking protection and website background protection.
-   The combination of different security modules, such as web security and HTTP flood protection, helps build a multi-layer protection architecture. This way, WAF can identify trusted and malicious traffic.

Virtual patches

Before the patches for web application vulnerabilities are released or installed, you can adjust web protection policies to protect your services.

## Attack event management

WAF allows you to manage attack events based on statistical data, such as attack events, attack traffic, and attack scales.

## Reliability

-   Load balancing: WAF can provide services in cluster mode. It uses multiple servers to balance loads and supports different scheduling algorithms.
-   Smooth and elastic scaling: You can add servers to or remove servers from a cluster to adjust the WAF service capability based on your business requirements.
-   Preclusion of single point of failures \(SPOFs\): If a WAF node fails unexpectedly or is taken offline for repair, the WAF service is not affected.

For more information, see the [product page of Web Application Firewall](https://www.alibabacloud.com/zh/product/waf).

