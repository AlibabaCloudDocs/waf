# API概览 {#concept_qyw_x1d_cz .concept}

本文档汇总了Web应用防火墙所有可调用的API，具体接口信息请参阅相关文档。关于更多API资源，请访问[API Explorer](https://api.aliyun.com/)。

## 实例信息 {#section_mzf_q1d_p2b .section}

|API|描述|
|:--|:-|
|DescribeRegions|获取当前WAF支持的地域信息。|
|DescribePayInfo|获取指定地域的WAF实例当前信息。|

## 域名配置 {#section_dc5_gfw_pdb .section}

|API|描述|
|:--|:-|
|DescribeDomainNames|获取指定WAF实例中的域名名称列表。|
|DescribeDomainConfig|获取指定域名的转发配置信息。|
|DescribeDomainConfigStatus|查询指定域名配置是否已生效。|
|CreateDomainConfig|添加域名配置信息。|
|ModifyDomainConfig|修改域名配置信息。|
|DeleteDomainConfig|删除域名配置信息。|
|CreateCertAndKey|为指定域名上传证书及私钥信息。|

## Web攻击防护 {#section_vpc_kff_cz .section}

|API|描述|
|:--|:-|
|ModifyWafSwitch|打开或关闭Web攻击防护功能开关。|

## 精准访问控制 {#section_evr_pcy_5db .section}

|API|描述|
|:--|:-|
|CreateAclRule|创建精准访问控制规则。|
|DeleteAclRule|删除指定精准访问控制规则。|
|ModifyAclRule|修改指定精准访问控制规则。|
|DescribeAclRules|获取精准访问控制规则列表。|

## 网站防篡改设置 {#section_cxx_t4n_2gb .section}

|API|描述|
|:--|:-|
|CreateProtectionModuleRule|添加网站防篡改规则。|
|DescribeProtectionModuleRules|获取网站防篡改规则列表。|
|ModifyProtectionRuleCacheStatus|更新网站防篡改规则所防护的页面缓存。|
|ModifyProtectionRuleStatus|启用或禁用指定网站防篡改规则。|

## 异步任务信息 {#section_hvl_sxj_p2b .section}

|API|描述|
|:--|:-|
|DescribeAsyncTaskStatus|查看WAF任务执行状态。|

