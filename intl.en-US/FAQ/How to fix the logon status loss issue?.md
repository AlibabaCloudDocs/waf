# How to fix the logon status loss issue? {#concept_pfc_ygl_q2b .concept}

## Symptoms {#section_ap3_ygl_q2b .section}

Some sites may encounter loss of logon status or other exceptions related to the logon status when using WAF. Root causes of these exceptions include the following:

-   The domain name has multiple origins \(ECS\), but does not synchronize the sessions, especially in architectures where an SLB is attached after WAF.
-   Failure to obtain the real IP address from X-forwarded-for for validation.

## Resolution {#section_egb_zgl_q2b .section}

-   Configure session synchronization for the server.
-   If the WAF is connected to an SLB, you can use the layer-7 HTTP method to forward the traffic, and enable the cookie-based session persistence.
-   Obtain the real IP address from x-forwarded-for.

    For more information, see [Obtain the visitor’s real IP address](https://www.alibabacloud.com/help/doc-detail/42205.htm).


