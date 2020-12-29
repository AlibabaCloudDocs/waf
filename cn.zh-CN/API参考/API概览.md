# API概览

本文汇总了Web应用防火墙（WAF）服务所有可调用的API。

## 实例信息

|API|描述|
|---|--|
|[DescribeInstanceInfo](/cn.zh-CN/API参考/实例信息/DescribeInstanceInfo.md)|查询已购买的WAF实例的基本信息，例如实例ID、实例的类型和状态等。|
|[DescribeInstanceSpecInfo](/cn.zh-CN/API参考/实例信息/DescribeInstanceSpecInfo.md)|查询已购买的WAF实例的规格信息。|
|[DeleteInstance](/cn.zh-CN/API参考/实例信息/DeleteInstance.md)|释放已开通的按量付费WAF实例或者已到期的包年包月WAF实例。|

## 域名配置

|API|描述|
|---|--|
|[DescribeDomainNames](/cn.zh-CN/API参考/域名配置/DescribeDomainNames.md)|查询WAF实例中已添加的域名名称列表。|
|[DescribeDomain](/cn.zh-CN/API参考/域名配置/DescribeDomain.md)|查询WAF实例中已添加的域名配置信息。|
|[CreateDomain](/cn.zh-CN/API参考/域名配置/CreateDomain.md)|添加域名配置信息，将您的域名接入WAF实例进行防护。|
|[ModifyDomain](/cn.zh-CN/API参考/域名配置/ModifyDomain.md)|修改指定的域名配置信息。|
|[DeleteDomain](/cn.zh-CN/API参考/域名配置/DeleteDomain.md)|删除指定的域名配置信息。|
|[DescribeCertificates](/cn.zh-CN/API参考/域名配置/DescribeCertificates.md)|查询指定域名关联的已有证书，即已在SSL证书服务中进行管理的证书。|
|[DescribeCertMatchStatus](/cn.zh-CN/API参考/域名配置/DescribeCertMatchStatus.md)|查询域名配置中上传的证书和私钥信息是否匹配。|
|[CreateCertificate](/cn.zh-CN/API参考/域名配置/CreateCertificate.md)|为已添加的域名配置上传证书及私钥信息。|
|[CreateCertificateByCertificateId](/cn.zh-CN/API参考/域名配置/CreateCertificateByCertificateId.md)|根据证书ID为指定的域名配置上传证书。|
|[DescribeDomainBasicConfigs](/cn.zh-CN/API参考/域名配置/DescribeDomainBasicConfigs.md)|查询已添加的域名配置的防护设置状态。|
|[DescribeDomainAdvanceConfigs](/cn.zh-CN/API参考/域名配置/DescribeDomainAdvanceConfigs.md)|查询已添加的域名配置的详细信息。|

## 防护配置

|API|描述|
|---|--|
|[ModifyDomainIpv6Status](/cn.zh-CN/API参考/防护配置/ModifyDomainIpv6Status.md)|为域名配置开启或关闭IPv6安全防护功能。|
|[DescribeProtectionModuleStatus](/cn.zh-CN/API参考/防护配置/DescribeProtectionModuleStatus.md)|查询指定的WAF防护功能模块（包括Web入侵防护、数据安全、高级防护、Bot管理、访问控制或限流等模块）的开关状态。|
|[ModifyProtectionModuleStatus](/cn.zh-CN/API参考/防护配置/ModifyProtectionModuleStatus.md)|为域名配置开启或关闭WAF防护功能模块（包括Web入侵防护、数据安全、高级防护、Bot管理、访问控制或限流等模块）。|
|[DescribeProtectionModuleMode](/cn.zh-CN/API参考/防护配置/DescribeProtectionModuleMode.md)|查询域名配置中各WAF防护功能模块（包括正则防护引擎、大数据深度学习引擎、CC安全防护、数据风控、主动防御等模块）当前采用的防护模式。|
|[ModifyProtectionModuleMode](/cn.zh-CN/API参考/防护配置/ModifyProtectionModuleMode.md)|修改指定的WAF防护功能模块（包括正则防护引擎、大数据深度学习引擎、CC安全防护、数据风控、主动防御等模块）的防护模式。|
|[DescribeProtectionModuleRules](/cn.zh-CN/API参考/防护配置/DescribeProtectionModuleRules.md)|查询指定的WAF防护功能模块（包括Web入侵防护、数据安全、Bot管理、访问控制或限流、网站白名单等模块）的规则配置记录。|
|[CreateProtectionModuleRule](/cn.zh-CN/API参考/防护配置/CreateProtectionModuleRule.md)|在指定的WAF防护功能模块（包括Web入侵防护、数据安全、Bot管理、访问控制或限流、网站白名单等模块）中创建规则配置。|
|[ModifyProtectionModuleRule](/cn.zh-CN/API参考/防护配置/ModifyProtectionModuleRule.md)|修改指定的WAF防护功能模块（包括Web入侵防护、数据安全、高级防护、Bot管理、访问控制或限流、白名单等模块）的配置规则。|
|[ModifyProtectionRuleStatus](/cn.zh-CN/API参考/防护配置/ModifyProtectionRuleStatus.md)|为域名配置开启或关闭WAF防护功能模块（包括网站防篡改、合法爬虫、爬虫威胁情报、自定义防护策略、网站白名单等模块）中已创建的规则。|
|[DescribeDomainRuleGroup](/cn.zh-CN/API参考/防护配置/DescribeDomainRuleGroup.md)|查询域名配置当前使用的正则防护引擎的防护规则组ID。|
|[SetDomainRuleGroup](/cn.zh-CN/API参考/防护配置/SetDomainRuleGroup.md)|为域名配置选择正则防护引擎使用的防护规则组（除系统默认的三种防护规则组外，也可以选择自定义规则组）。|
|[ModifyProtectionRuleCacheStatus](/cn.zh-CN/API参考/防护配置/ModifyProtectionRuleCacheStatus.md)|更新指定的网站防篡改规则所防护页面的缓存。|
|[DeleteProtectionModuleRule](/cn.zh-CN/API参考/防护配置/DeleteProtectionModuleRule.md)|删除指定的防护模块下已创建的规则配置。|

## 日志管理

|API|描述|
|---|--|
|[ModifyLogServiceStatus](/cn.zh-CN/API参考/日志管理/ModifyLogServiceStatus.md)|为域名配置开启或关闭日志采集功能。|
|[ModifyLogRetrievalStatus](/cn.zh-CN/API参考/日志管理/ModifyLogRetrievalStatus.md)|为域名配置开启或关闭日志检索功能。|

## 系统管理

|API|描述|
|---|--|
|[DescribeWafSourceIpSegment]()|查询WAF防护集群使用的回源IP网段。|

