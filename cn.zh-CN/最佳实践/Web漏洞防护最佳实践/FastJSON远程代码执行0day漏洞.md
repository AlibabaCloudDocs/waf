# FastJSON远程代码执行0day漏洞 {#concept_861968 .concept}

2019年7月23日，阿里云云盾应急响应中心监测到FastJSON存在0day漏洞，攻击者可以利用该漏洞绕过黑名单策略进行远程代码执行。

## 漏洞名称 {#section_qdh_84k_bta .section}

FastJSON远程代码执行0day漏洞

## 漏洞描述 {#section_gbg_mah_0e1 .section}

利用该0day漏洞，恶意攻击者可以构造绕过FastJSON黑名单策略补丁的攻击请求，进行远程代码执行攻击。例如，攻击者通过精心构造的请求，绕过FastJSON黑名单策略补丁远程让服务端执行指定命令（以下示例中成功运行计算器程序）。

![攻击成功示例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1082622/156405208953065_zh-CN.png)

## 影响范围 {#section_mmd_wzu_i8a .section}

-   FastJSON 1.2.24及以下版本
-   FastJSON 1.2.41至1.2.45版本

## 官方解决方案 {#section_t3d_8b9_47b .section}

升级至FastJSON最新版本，建议升级至1.2.58版本。

**说明：** 强烈建议不在本次影响范围内的低版本FastJSON也进行升级。

**升级方法**

您可以通过更新Maven依赖配置，升级FastJSON至最新版本（1.2.58版本）。

``` {#codeblock_19o_iwo_ugm}
<dependency>
 <groupId>com.alibaba</groupId>
 <artifactId>fastjson</artifactId>
 <version>1.2.58</version>
</dependency>
```

## 防护建议 {#section_xmv_5a4_yyb .section}

Web应用防火墙的Web攻击防护规则中已默认配置相应规则防护该FastJSON 0day漏洞，启用Web应用防火墙的Web应用攻击防护功能即可。

## 更多信息 {#section_6h5_m60_j32 .section}

安全管家服务可以为您提供包括安全检测、安全加固、安全监控、安全应急等一系列专业的安全服务项目，帮助您更加及时、有效地应对漏洞及黑客攻击，详情请关注[安全管家服务](https://www.aliyun.com/product/sos)。

