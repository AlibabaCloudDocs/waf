# API概览 {#doc_16458 .concept}

Web应用防火墙提供以下相关API接口。

## 实例信息 {#section_icy_k2x_btq .section}

|API|描述|
|---|--|
|[DescribeRegions](cn.zh-CN/API参考/实例信息/DescribeRegions.md)|调用DescribeRegions接口获取当前WAF支持的地域信息。|
|[DescribePayInfo](cn.zh-CN/API参考/实例信息/DescribePayInfo.md)|调用DescribePayInfo接口获取指定地域的WAF实例当前信息。|
|[DescribeWafSourceIpSegment](cn.zh-CN/API参考/实例信息/DescribeWafSourceIpSegment.md)|调用DescribeWafSourceIpSegment接口获取WAF实例的回源IP网段列表。|

## 域名配置 {#section_xue_twe_jbs .section}

|API|描述|
|---|--|
|[DescribeDomainNames](cn.zh-CN/API参考/域名配置/DescribeDomainNames.md)|调用DescribeDomainNames接口获取指定WAF实例中已添加的域名名称列表。|
|[DescribeDomainConfig](cn.zh-CN/API参考/域名配置/DescribeDomainConfig.md)|调用DescribeDomainConfig接口获取指定域名的转发配置信息。|
|[DescribeDomainConfigStatus](cn.zh-CN/API参考/域名配置/DescribeDomainConfigStatus.md)|调用DescribeDomainConfigStatus接口查询指定域名的转发配置是否生效。|
|[CreateDomainConfig](cn.zh-CN/API参考/域名配置/CreateDomainConfig.md)|调用CreateDomainConfig接口添加域名配置信息。|
|[ModifyDomainConfig](cn.zh-CN/API参考/域名配置/ModifyDomainConfig.md)|调用ModifyDomainConfig接口修改指定域名配置信息。|
|[DeleteDomainConfig](cn.zh-CN/API参考/域名配置/DeleteDomainConfig.md)|调用DeleteDomainConfig接口删除指定域名配置信息。|
|[CreateCertAndKey](cn.zh-CN/API参考/域名配置/CreateCertAndKey.md)|调用CreateCertAndKey接口为已添加的域名配置记录上传证书及私钥信息。|

## Web攻击防护配置 {#section_tt5_1sk_bfw .section}

|API|描述|
|---|--|
|[ModifyWafSwitch](cn.zh-CN/API参考/Web攻击防护配置/ModifyWafSwitch.md)|调用ModifyWafSwitch接口打开或关闭Web攻击防护功能开关。|

## 精准访问控制配置 {#section_sc2_fdd_j4l .section}

|API|描述|
|---|--|
|[DescribeAclRules](cn.zh-CN/API参考/精准访问控制配置/DescribeAclRules.md)|调用DescribeAclRules接口获取指定域名的精准访问控制规则列表。|
|[CreateAclRule](cn.zh-CN/API参考/精准访问控制配置/CreateAclRule.md)|调用CreateAclRule接口为指定域名添加精准访问控制规则。|
|[ModifyAclRule](cn.zh-CN/API参考/精准访问控制配置/ModifyAclRule.md)|调用ModifyAclRule接口修改指定精准访问控制规则。|
|[DeleteAclRule](cn.zh-CN/API参考/精准访问控制配置/DeleteAclRule.md)|调用DeleteAclRule接口删除指定精准访问控制规则。|

## 网站防篡改设置 {#section_4rh_wzx_1xr .section}

|API|描述|
|---|--|
|[CreateProtectionModuleRule](cn.zh-CN/API参考/网站防篡改设置/CreateProtectionModuleRule.md)|调用CreateProtectionModuleRule接口新增一条防护规则。|
|[DescribeProtectionModuleRules](cn.zh-CN/API参考/网站防篡改设置/DescribeProtectionModuleRules.md)|调用DescribeProtectionModuleRules接口查询防护规则信息。|
|[ModifyProtectionRuleCacheStatus](cn.zh-CN/API参考/网站防篡改设置/ModifyProtectionRuleCacheStatus.md)|调用ModifyProtectionRuleCacheStatus接口更新指定网站防篡改规则所防护的页面的缓存。|
|[ModifyProtectionRuleStatus](cn.zh-CN/API参考/网站防篡改设置/ModifyProtectionRuleStatus.md)|调用ModifyProtectionRuleStatus接口启用或关闭指定的网站防篡改规则。|

## 异步任务信息 {#section_yno_l8u_jps .section}

|API|描述|
|---|--|
|[DescribeAsyncTaskStatus](cn.zh-CN/API参考/异步任务信息/DescribeAsyncTaskStatus.md)|调用DescribeAsyncTaskStatus接口查询WAF任务执行状态。|

