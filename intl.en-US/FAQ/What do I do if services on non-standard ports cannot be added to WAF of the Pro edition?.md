# What do I do if services on non-standard ports cannot be added to WAF of the Pro edition?

## Problem description

WAF of the Pro edition protects only website services that use standard HTTP ports 80 or 8080 or HTTPS ports 443 or 8443. If your services use non-standard ports, the services cannot be added to WAF of the Pro edition.

## Solution

-   WAF of the Business edition or higher supports specific non-standard ports. For more information, see [Supported custom ports](/intl.en-US/Website Access/Supported custom ports.md). If your services use ports within the port range that is supported by WAF, upgrade your WAF instance to the Business edition or higher. For more information, see [t15543.md\#section\_h76\_hk9\_g1k](/intl.en-US/Billing and Service Activation/Renewal and upgrade.md).
-   If your services use ports that are not supported by WAF, you can deploy an SLB instance that serves as a proxy. The services are deployed in the following sequence: WAF, SLB, and ECS.

    If you deploy an SLB instance that serves as a proxy, you can configure HTTPS services in WAF. By default, port 443 is used. If you deploy an HTTPS listener on the SLB instance, the frontend port is port 443 and the backend port is the service port.

    **Note:** If you deploy services as described in this section, you must upload HTTPS certificate files to both the WAF and SLB instances. Otherwise, requests cannot be forwarded to origin servers.


