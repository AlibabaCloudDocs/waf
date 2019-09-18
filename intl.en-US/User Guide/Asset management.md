# Asset management {#task_1375152 .task}

Web Application Firewall \(WAF\) provides the asset management function. WAF can detect the network assets in your Alibaba Cloud account by obtaining the configuration information of Alibaba Cloud services such as SSL Certificates, Alibaba Cloud DNS, and WAF, and the website information in the network traffic. WAF also allows you to quickly add your assets for protection.

Network assets act as the most important carrier of network applications in a security management system and the most fundamental component in a business system. The rapid development of enterprise business has led to the increase of business platforms. Employees may not release resources after they build websites or testing environments. As a result, the business systems may contain a lot of zombie assets that lack management. The security level of a business system depends on the most vulnerable part of the system. The zombie assets use low-version open source systems, components, or Web structures. As a result, vulnerabilities of zombie assets are exposed. Attackers can use weak websites to bypass the network perimeter protection and intrude into the internal network of an enterprise.

WAF provides the asset management function to help you discover network assets in Alibaba Cloud and monitor the asset changes. This ensures protection for all assets and enhances the overall security of your system. The asset management function allows you to locate the assets that are affected by 0-day vulnerabilities and quickly add these assets to WAF for protection. You can use this function as a basis for making security management decisions on your domain assets.

After WAF is authorized, WAF discovers all domain assets in your Alibaba Cloud account based on the website information in the website traffic and the configuration information of your cloud services, such as SSL Certificates, DNS, and WAF. The domain asset information includes the domain, subdomains, server IP address, ports, protocol, and WAF protection status.

## Authorize WAF to access cloud resources {#section_mfp_6nj_f9q .section}

To enable WAF to discover network assets, you must authorize WAF to obtain the website information of the cloud services in your Alibaba Cloud account and manage the domain name resolution records of the Alibaba Cloud DNS service.

1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf), and open the Assets page. The **Authorize WAF to Access Cloud Resources** dialog box is displayed. 

    ![](images/53159_en-US.png)

2.  Click **Authorize**. The authorization page in the RAM console is displayed. 

    ![](images/53161_en-US.png)

3.  Click **Confirm Authorization Policy** to authorize WAF to access cloud resources in your account.

After the authorization is complete, WAF can discover the domain name assets in your account.

## View domain name assets {#section_xjj_saw_kbp .section}

On the Assets page in the WAF console, you can view all the domain name assets that WAF has discovered.

1.  Log on to the [WAF console](https://partners-intl.console.aliyun.com/#/waf), and set the region of the WAF instance to China Mainland or International.
2.  Open the Assets page to view your domain name assets. 

    WAF classifies the domain names by top-level domain name. You can expand the list of a specific top-level domain name to view the information of all related domain names, including the server IP address, port number, access protocol, and protection status.

    **Note:** 

    -   The Assets page displays only domain names that has traffic recently.
    -   If the information of a domain name, such as the server IP address, port number, and protocol, is not displayed, the IP address does not belong to this Alibaba cloud account.
    The protection status indicates whether a domain name is added to WAF for protection.

    -   **Unprotected**: The domain name is not added to WAF for protection.
    -   **Added but Unprotected**: The domain name is added to WAF, but WAF has not detected any traffic bound to this domain.
    -   **Protected**: The domain name is added to WAF, and WAF has detected traffic bound to this domain.
    **Note:** If the protection status of a domain name is **Unprotected**, We recommend that you add it to WAF for protection. For more information, see [Add website configurations automatically](reseller.en-US/User Guide/Use the DNS proxy mode to configure WAF/Website configuration.md#auto-website-configuration).

    You can also enter a keyword in the search box above the domain name list, and click **Search** to search for specified domain name assets.

    ![](images/53204_en-US.png)


