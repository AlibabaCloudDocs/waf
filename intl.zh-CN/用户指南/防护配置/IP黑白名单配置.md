# IP黑白名单配置 {#concept_rbj_mbp_p2b .concept}

在WAF中，您可以配置[精准访问控制规则](intl.zh-CN/用户指南/防护配置/精准访问控制.md#)来阻断或放行指定IP的访问请求，即设置IP黑/白名单。IP黑白名单仅针对配置的特定域名生效。

## 操作步骤 {#section_ckj_xlp_p2b .section}

参照以下步骤，配置IP黑名单和IP白名单：

**说明：** 执行以下操作前，请确保已将网站接入WAF进行防护。具体操作请参考[CNAME接入指南](intl.zh-CN/用户指南/使用DNS配置模式接入WAF/业务接入WAF配置.md#)。

1.  登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)。
2.  前往**管理** \> **网站配置**页面，并在页面上方选择WAF所在地区（中国大陆、海外地区）。
3.  选择要操作的域名，单击其操作列下的**防护配置**。
4.  在**精确访问控制**下，开启防护，并单击**前去配置**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15653334197783_zh-CN.jpg)

5.  单击**新增规则**，新增一条防护规则。
    -   白名单配置示例：使用下图配置，放行源IP为1.1.1.1的所有访问。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15653334197784_zh-CN.jpg)

        **说明：** 如果想完全放行这个IP的所有请求，则不要勾选匹配动作下方的继续执行其它防护选项。如果勾选，则来自这个IP的部分请求仍然可能被相应防护的规则拦截。

    -   黑名单配置示例：使用下图配置，阻断源IP为1.1.1.1的所有访问。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15653334197785_zh-CN.jpg)


## 注意事项 {#section_kd4_cmp_p2b .section}

-   防护规则中的IP支持掩码格式（如1.1.1.0/24），且逻辑符支持选择“不属于”。因此，如果您想只允许来自某个网段（如公司网段）的请求访问某个域名时，可参考下图配置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15653334197787_zh-CN.jpg)

-   多条防护规则之间存在匹配优先级，按照规则列表中从上到下的顺序进行匹配，通过单击右上角的**规则排序**可以调整防护规则之间的优先级。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15653334197789_zh-CN.jpg)


