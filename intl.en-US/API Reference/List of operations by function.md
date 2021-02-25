# List of operations by function

The following tables list API operations available for use in Web Application Firewall \(WAF\).

## Instance management

|Operation|Description|
|---------|-----------|
|[DescribeInstanceInfo](/intl.en-US/API Reference/Instance information/DescribeInstanceInfo.md)|Queries the basic information about a WAF instance. The information includes the ID, type, and status of the WAF instance.|
|[DescribeInstanceSpecInfo](/intl.en-US/API Reference/Instance information/DescribeInstanceSpecInfo.md)|Queries the specification information about the WAF instance that you purchase.|
|[DeleteInstance](/intl.en-US/API Reference/Instance information/DeleteInstance.md)|Releases a subscription WAF instance that has expired.|

## Domain name management

|Operation|Description|
|---------|-----------|
|[DescribeDomainNames](/intl.en-US/API Reference/Domain configurations/DescribeDomainNames.md)|Queries the domain names that are added to a WAF instance.|
|[DescribeDomain](/intl.en-US/API Reference/Domain configurations/DescribeDomain.md)|Queries the configurations of the domain names that are added to a WAF instance.|
|[CreateDomain](/intl.en-US/API Reference/Domain configurations/CreateDomain.md)|Adds domain name configurations to the WAF instance.|
|[ModifyDomain](/intl.en-US/API Reference/Domain configurations/ModifyDomain.md)|Modifies the configuration of a specified domain name.|
|[DeleteDomain](/intl.en-US/API Reference/Domain configurations/DeleteDomain.md)|Deletes the configuration of a specified domain name.|
|[DescribeCertificates](/intl.en-US/API Reference/Domain configurations/DescribeCertificates.md)|Queries the existing certificates that are associated with a specified domain name. The certificates are managed by SSL Certificates Service.|
|[DescribeCertMatchStatus](/intl.en-US/API Reference/Domain configurations/DescribeCertMatchStatus.md)|Checks whether the certificate and the private key that you upload for the domain name match each other.|
|[CreateCertificate](/intl.en-US/API Reference/Domain configurations/CreateCertificate.md)|Uploads the certificate file and private key file for a protected domain name.|
|[CreateCertificateByCertificateId](/intl.en-US/API Reference/Domain configurations/CreateCertificateByCertificateId.md)|Uploads the certificate file for a specified domain name based on the certificate ID.|
|[DescribeDomainBasicConfigs](/intl.en-US/API Reference/Domain configurations/DescribeDomainBasicConfigs.md)|Queries the protection status of the domain name that is added to a WAF instance.|
|[DescribeDomainAdvanceConfigs](/intl.en-US/API Reference/Domain configurations/DescribeDomainAdvanceConfigs.md)|Queries the configuration details of the domain name that is added to a WAF instance.|

## Protection configuration

|Operation|Description|
|---------|-----------|
|[ModifyDomainIpv6Status](/intl.en-US/API Reference/Protection configuration/ModifyDomainIpv6Status.md)|Enables or disables the IPv6 traffic protection feature for a domain name.|
|[DescribeProtectionModuleStatus](/intl.en-US/API Reference/Protection configuration/DescribeProtectionModuleStatus.md)|Queries whether the features in the specified WAF protection modules are enabled. The WAF protection modules include web intrusion prevention, data security, advanced protection, bot management, and access control or throttling.|
|[ModifyProtectionModuleStatus](/intl.en-US/API Reference/Protection configuration/ModifyProtectionModuleStatus.md)|Enables or disables the features in the specified WAF protection modules. The WAF protection modules include web intrusion prevention, data security, advanced protection, bot management, and access control or throttling.|
|[DescribeProtectionModuleMode](/intl.en-US/API Reference/Protection configuration/DescribeProtectionModuleMode.md)|Queries the current protection modes of features. The features include the RegEx Protection Engine, Big Data Deep Learning Engine, HTTP flood protection, data risk control, and proactive defense.|
|[ModifyProtectionModuleMode](/intl.en-US/API Reference/Protection configuration/ModifyProtectionModuleMode.md)|Modifies the protection modes of features. The features include the RegEx Protection Engine, Big Data Deep Learning Engine, HTTP flood protection, data risk control, and proactive defense.|
|[DescribeProtectionModuleRules](/intl.en-US/API Reference/Protection configuration/DescribeProtectionModuleRules.md)|Queries the rules that are created for the features in the specified WAF protection modules. The WAF protection modules include web intrusion prevention, data security, bot management, access control or throttling, and whitelist.|
|[CreateProtectionModuleRule](/intl.en-US/API Reference/Protection configuration/CreateProtectionModuleRule.md)|Creates rules for the features in the specified WAF protection modules. The WAF protection modules include web intrusion prevention, data security, bot management, access control or throttling, and whitelist.|
|[ModifyProtectionModuleRule](/intl.en-US/API Reference/Protection configuration/ModifyProtectionModuleRule.md)|Modifies the rules that are created for the features in the specified WAF protection modules. The WAF protection modules include web intrusion prevention, data security, advanced protection, bot management, access control or throttling, and whitelist.|
|[ModifyProtectionRuleStatus](/intl.en-US/API Reference/Protection configuration/ModifyProtectionRuleStatus.md)|Enables or disables the rules that are created for features. The features include website tamper-proofing, allowed crawlers, bot threat intelligence, custom protection policy, and whitelist.|
|[DescribeDomainRuleGroup](/intl.en-US/API Reference/Protection configuration/DescribeDomainRuleGroup.md)|Queries the ID of the protection rule group that is provided by the RegEx Protection Engine for a specified domain name.|
|[SetDomainRuleGroup](/intl.en-US/API Reference/Protection configuration/SetDomainRuleGroup.md)|Configures the protection rule group that is provided by the RegEx Protection Engine for a specified domain name. The system provides three default protection rule groups. You can also select a custom rule group.|
|[ModifyProtectionRuleCacheStatus](/intl.en-US/API Reference/Protection configuration/ModifyProtectionRuleCacheStatus.md)|Updates the cached pages of the domain name that is protected by a specified website tamper-proofing rule.|
|[DeleteProtectionModuleRule](/intl.en-US/API Reference/Protection configuration/DeleteProtectionModuleRule.md)|Deletes the rule that is created for a specified feature.|
|[t2037902.md\#]()|Queries the codes of regions that can be configured in the WAF region blacklist.|

## Log management

|Operation|Description|
|---------|-----------|
|[ModifyLogServiceStatus](/intl.en-US/API Reference/Log management/ModifyLogServiceStatus.md)|Enables or disables the log collection feature for a domain name.|
|[ModifyLogRetrievalStatus](/intl.en-US/API Reference/Log management/ModifyLogRetrievalStatus.md)|Enables or disables the log search feature for a domain name.|
|[t2037909.md\#]()|Queries whether the log collection feature is enabled for the domain names that are added to a WAF instance.|

## System management

|Operation|Description|
|---------|-----------|
|[DescribeWafSourceIpSegment](/intl.en-US/API Reference/System management/DescribeWafSourceIpSegment.md)|Queries the back-to-origin CIDR blocks that are used by the WAF protection cluster.|

