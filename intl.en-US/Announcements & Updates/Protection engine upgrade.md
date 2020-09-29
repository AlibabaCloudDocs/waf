# Protection engine upgrade

From March 11, 2020, Web Application Firewall \(WAF\) upgraded the protection engine for all users. The new protection engine is reliable and easy to use.

The new protection engine offers the following benefits:

-   Improved protection effects

    Functions are integrated into protection modules, such as web intrusion prevention, data security, bot management, and access control and throttling. The modules provide protection for your business.

    The new protection engine also provides precise throttling and account security capabilities. These capabilities allow you to protect your servers from unauthorized access, HTTP flood attacks, credential stuffing, weak password attacks, and brute-force attacks. After the upgrade, WAF displays a visual report of the security and protection services.

-   Fine-grained throttling can be achieved by using custom protection policies.

    The custom protection policy feature allows you to configure more fields and rules. It also provides you with precise throttling capabilities under complex conditions. This feature enables you to manage unauthorized access requests in various business scenarios.

    -   The custom HTTP flood protection rules in the original engine are integrated into custom protection policies to provide more precise throttling capabilities. For more information, see [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md).
    -   The original HTTP ACL policy feature can be used to allow legitimate traffic. After the upgrade, you can configure website whitelists for each protection module to allow legitimate traffic. For more information, see [Configure the website whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the website whitelist.md).
-   Convenient IP address blacklist configuration

    You can add IP addresses, CIDR blocks, and the regions to which IP addresses belong to blacklists. This way, you can implement quick access control and block traffic.


You can configure the following items for each protection module: website whitelists, scan reports, and priorities of protection rules. For more information, see [Configure RegEx Protection Engine](/intl.en-US/Website Protection Settings/Web security/Configure the RegEx Protection Engine.md).

## Upgrade your protection engine

The protection engine will be upgraded for all users who activated WAF before January 2020. After the engine is upgraded in the backend, you will receive an upgrade notification when you log on to the WAF console. Then, you can click **Try Now** to experience your new protection engine.

![Try now](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5525338951/p96666.png)

