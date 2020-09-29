# FastJSON远程代码执行0day漏洞（2019-7-23）

2019年7月23日，阿里云云盾应急响应中心监测到FastJSON存在0day漏洞，攻击者可以利用该漏洞绕过黑名单策略进行远程代码执行。

## 漏洞名称

FastJSON远程代码执行0day漏洞

## 漏洞描述

利用该0day漏洞，恶意攻击者可以构造绕过FastJSON黑名单策略补丁的攻击请求，进行远程代码执行攻击。例如，攻击者通过精心构造的请求，绕过FastJSON黑名单策略补丁远程让服务端执行指定命令（以下示例中成功运行计算器程序）。

![攻击成功示例](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8565287951/p53065.png)

## 影响范围

-   FastJSON 1.2.24及以下版本
-   FastJSON 1.2.41至1.2.45版本

## 官方解决方案

升级至FastJSON最新版本，建议升级至1.2.58版本。

**说明：** 强烈建议不在本次影响范围内的低版本FastJSON也进行升级。

**升级方法**

您可以通过更新Maven依赖配置，升级FastJSON至最新版本（1.2.58版本）。

```
<dependency>
 <groupId>com.alibaba</groupId>
 <artifactId>fastjson</artifactId>
 <version>1.2.58</version>
</dependency>
```

## 防护建议

Web应用防火墙的Web攻击防护规则中已默认配置相应规则防护该FastJSON 0day漏洞，启用Web应用防火墙的Web应用攻击防护功能即可。

