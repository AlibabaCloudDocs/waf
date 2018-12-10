# WAF back-to-origin CIDR blocks update {#concept_hng_pgr_bgb .concept}

To provide better web application protection for you, Alibaba Cloud Web Application Firewall \(WAF\) expands the capacity of the global WAF server rooms to further improve service capabilities. After the expansion of the capacity, WAF's WAF back-to-origin CIDR blocks are expanded.

If your origin servers have IP whitelist or security group settings for access control, to only allow accesses from WAF back-to-origin CIDR blocks, you must add the following new WAF back-to-origin CIDR blocks into the whitelist. Otherwise, traffic forwarded by WAF to the origin servers can be blocked by access control policies, and your website cannot be visited as expected.

**Note:** Besides adding new back-to-origin CIDR blocks, some existing CIDR blocks are also updated this time. Please verify the new CIDR blocks carefully.

**New WAF back-to-origin CIDR blocks for the mainland China instances**

121.43.18.0/24, 120.25.115.0/24, 101.200.106.0/24, 120.55.177.0/24, 120.27.173.0/24, 120.55.107.0/24, 123.57.117.0/24, 120.76.16.0/24, 182.92.253.32/27, 60.205.193.64/27, 60.205.193.96/27, 120.78.44.128/26, 118.178.15.0/24, 39.106.237.192/26, 106.15.101.96/27, 47.101.16.64/27, 47.106.31.0/24, 47.98.74.0/25, 47.97.242.96/27, 112.124.159.0/24, 39.96.130.0/24, 39.96.119.0/24, 47.99.20.0/24, 47.104.53.0/26, 47.108.23.192/26, 47.101.16.64/27

**New WAF back-to-origin CIDR blocks for the International instances**

47.89.1.160/27, 47.89.7.192/26, 47.88.145.96/27, 47.88.250.0/24, 47.52.120.0/24, 47.254.217.32/27, 47.88.74.0/24, 47.89.132.224/27, 47.91.69.64/27, 47.91.54.128/27, 47.74.160.0/24, 47.91.113.64/27, 149.129.211.0/27, 149.129.140.0/27, 47.89.7.224/27, 8.208.2.192/27

You can also log on to the Web Application Firewall management console, and go to the **Management** \> **Website Configuration** page, to check the latest WAF back-to-origin CIDR blocks.

