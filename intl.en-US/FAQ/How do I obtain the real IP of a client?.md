# How do I obtain the real IP of a client? {#concept_ndz_fjq_kgb .concept}

When an HTTP request goes through a layer-7 proxy, the source IP of this packet is modified with the proxy IP, instead of the real IP of the client \(client IP\). Practically, the client IP is often written into the x-forwarded-for field in the HTTP head field, as shown in the following figure.

The Alibaba Cloud WAF works as follows.

Suppose that WAF protects the domain “www.abc.com”. Generally, packets from the client follow the Client browser \> WAF \> Origin server \(Apache/Nginx/IIS and so on\) path. In this architecture, WAF acts as a reverse proxy between the client and the origin server.

However, in a network architecture containing multiple proxies \(for example, CDN and Anti-DDoS Pro\), multiple IP addresses get added to the `x-forwarded-for` field. This is because each proxy adds on the client IP, or the last proxy IP.

Therefore, the `x-forwarded-for` field may appear as `X-Forwarded-For: Client IP, Proxy 1, Proxy 2, Proxy 3, ...` However, the client IP still occupies the first address position in the x-forwarded-for field.

## Procedure {#section_qvf_q1p_mgb .section}

Follow these steps to obtain the real IP address of a client:

1.  Send a request command for the `x-forwarded-for` field content.

    The following are examples of request commands for several common languages.

    -   For ASP

        `Request.ServerVariables("HTTP_X_FORWARDED_FOR")`

    -   For ASP.NET\(C\#\)

        `Request.ServerVariables["HTTP_X_FORWARDED_FOR"]`

    -   For PHP

        `$_SERVER["HTTP_X_FORWARDED_FOR"]`

    -   For JSP

        `request.getHeader(“HTTP_X_FORWARDED_FOR”)`

2.  Separate the output `x-forwarded-for` with commas. The first derived IP address is the client IP.

