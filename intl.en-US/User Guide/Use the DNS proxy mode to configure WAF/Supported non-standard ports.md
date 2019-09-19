# Supported non-standard ports {#concept_ild_n1l_l2b .concept}

Alibaba Cloud WAF returns web traffic to the following ports of origin server by default: port 80 and 8080 for HTTP connection and port 443 and 8443 for HTTPS connection. You can specify other ports with the Business or Enterprise subscription plan. This topic explains the maximum number of ports you can specify and the custom ports you can use.

## Maximum number of ports {#section_x4f_41l_l2b .section}

For each Alibaba Cloud WAF subscription, the maximum number of different ports you can specify in all website configurations is as follows:

-   Business plan: You can specify **a maximum of 10 different ports**, including port 80, 8080, 443, and 8443.
-   Enterprise plan: You can specify **a maximum of 50 different ports**, including port 80, 8080, 443, and 8443.

## Supported ports {#section_z4f_41l_l2b .section}

Alibaba Cloud WAF only inspects web traffic that requests the supported ports. When a client requests an unsupported port \(for example, 4444\), the request will be discarded.

**Note:** You can go to the console to view the specific supported ports.

-   For the Business or Enterprise subscription plan of Alibaba Cloud WAF, the following **HTTP** ports are supported:

    80, 81, 82, 83, 84, 86, 87, 88, 89, 97, 800, 808, 1000, 1090, 3333, 3501, 3601, 5000, 5222, 6001, 6666, 7000, 7001, 7002, 7003, 7004, 7005, 7006, 7009, 7010, 7011, 7012, 7013, 7014, 7015, 7016, 7018, 7019, 7020, 7021, 7022, 7023, 7024, 7025, 7026, 7070, 7081, 7082, 7083, 7088, 7097, 7510, 7777, 7800, 8000, 8001, 8002, 8003, 8008, 8009, 8020, 8021, 8022, 8025, 8026, 8077, 8078, 8080, 8081, 8082, 8083, 8084, 8085, 8086, 8087, 8088, 8089, 8090, 8091, 8106, 8181, 8334, 8336, 8686, 8800, 8888, 8889, 8999, 9000, 9001, 9002, 9003, 9021, 9023, 9027, 9037, 9080, 9081, 9082, 9180, 9200, 9201, 9205, 9207, 9208, 9209, 9210, 9211, 9212, 9213, 9898, 9908, 9916, 9918, 9919, 9928, 9929, 9939, 9999, 10000, 10001, 10080, 12601, 28080, 33702, 48800

    **Note:** Port 48800 is only supported by WAF instance in the Mainland China region.

-   For the Business or Enterprise subscription plan of Alibaba Cloud WAF, the following **HTTPS** ports are supported:

    443, 4443, 5443, 6443, 7443, 8443, 8553, 8663, 9443, 9553, 9663, 18980

    **Note:** Port 18980 is only supported by WAF instance in the Mainland China region.


