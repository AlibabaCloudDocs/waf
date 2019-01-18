# How to fix WAF blackholes? {#concept_yr3_bcl_q2b .concept}

## What is a blackhole {#section_d1r_bcl_q2b .section}

When Web Application Firewall \(WAF\) suffers heavy-traffic DDoS attack that is beyond the free-protection capability of Anti-DDoS Basic, WAF is thrown into a blackhole.

After a WAF IP address is thrown into the blackhole, all traffic that flows through WAF \(normal access or attack\) is blocked, which means that **during the blackhole period, you cannot access any domain names protected by the WAF instance**.

**Note:** If a site is thrown into a blackhole, it can only be recovered after the blackhole period is over. The default blackhole period lasts for 150 minutes. The WAF blackhole threshold is the same as the default threshold of the region where the ECS is located.

## How to avoid a blackhole {#section_f1r_bcl_q2b .section}

By default, each WAF instance allocates an exclusive IP address to you. Once this WAF IP address is thrown into the black hole, none of the domain names protected by this WAF instance can be accessed during the black hole period. **To avoid this, you can purchase an additional [Exclusive IP](../../../../../reseller.en-US/Pricing/Subscription/Exclusive WAF IP.md#) address for an important domain name. In this case, this important domain name is not affected by other domain names under DDoS attacks.**

## WAF black hole FAQ {#section_g1r_bcl_q2b .section}

**My WAF is thrown into a blackhole. Can you recover it immediately?**

The blackhole is a service that Alibaba Cloud purchases from the operator who imposes strict restrictions on the time and frequency to trigger a blackhole. Therefore, you cannot manually deactivate the blackhole state, rather you have to patiently wait for the system to automatically free the server.

In fact, even if the blackhole is deactivated immediately, it gets triggered again if the WAF is still under heavy-traffic DDoS attack.

**How do I know the specific domain name that is under attack when the WAF is configured with multiple domain names?**

Generally, the hacker resolves a WAF protected domain name to obtain the WAF instance’s IP address, and then starts the DDoS attack against this IP address. Heavy-traffic DDoS attacks are targeting at a WAF IP address. We cannot figure out the domain name that is under attack, based on the traffic.

However, you can use the domain name split method to find out the domain name that is under attack. For example, you can resolve some of the domain names to WAF, and the rest to some other places \(ECS origin, CDN, or SLB\). If the WAF is no longer in the blackhole, it means that the hacker’s target lies in the domain names that are resolved to other places. However, this operation is relatively complex and may expose the origin and other assets, which may lead to a greater security issue. Unless necessary, do not use this method to find the domain name that is under attack.

**Can you help change the WAF IP address so that my WAF is not thrown into the blackhole?**

Changing the WAF IP address does not resolve the problem. A hacker can obtain your new IP address by pinging your domain name and can start another DDoS attack. So, changing your IP address will not be of much help.

**Is there any difference between a DDoS attack and an HTTP flood attack? Why cannot WAF defend against DDoS attacks?**

Heavy-traffic DDoS attacks are layer 4 attacks against IP addresses; while HTTP flood attacks are layer 7 attacks \(for example, HTTP GET/POST Flood\).

WAF can defend against HTTP flood attacks. However, in the case of heavy-traffic DDoS attacks, it requires sufficient bandwidth resources to take over all traffic to perform the traffic cleaning. Therefore, you can only count on protection from Anti-DDoS Pro.

