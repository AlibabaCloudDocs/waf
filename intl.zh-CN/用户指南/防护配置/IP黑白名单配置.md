# IP黑白名单配置 {#task_1796800 .task}

业务接入Web应用防火墙（WAF）后，您可以配置精确访问控制规则来阻断或放行指定IP的访问请求，即设置IP黑名单、白名单。IP黑白名单仅针对配置的特定域名生效。

已将网站接入WAF进行防护。具体操作请参见[CNAME接入指南](intl.zh-CN/用户指南/使用DNS配置模式接入WAF/业务接入WAF配置.md#)。

1.  登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)。
2.  前往**管理** \> **网站配置**页面，并在页面上方选择WAF所在地区（**中国大陆**、**海外地区**）。
3.  选择要操作的域名，单击其操作列下的**防护配置**。
4.  在**精确访问控制**下，开启防护，并单击**前去配置**。![精确访问控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15663503227783_zh-CN.jpg)


5.  单击**新增规则**，新增一条防护规则。 

    -   白名单配置示例：使用下图配置，放行源IP为1.1.1.1的所有访问。

        ![白名单配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15663503227784_zh-CN.jpg)

        **说明：** 如果想完全放行这个IP的所有请求，则不要勾选匹配动作下方的继续执行其它防护选项。如果勾选，则来自这个IP的部分请求仍然可能被相应防护的规则拦截。

    -   黑名单配置示例：使用下图配置，阻断源IP为1.1.1.1的所有访问。

        ![黑名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15663503227785_zh-CN.jpg)

    **说明：** 

    -   防护规则中的IP支持掩码格式（如1.1.1.0/24），且逻辑符支持选择“不属于”。因此，如果您想只允许来自某个网段（如公司网段）的请求访问某个域名时，可参见下图配置。

        ![只允许公司访问](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15663503237787_zh-CN.jpg)

    -   多条防护规则之间存在匹配优先级，按照规则列表中从上到下的顺序进行匹配，通过单击右上角的**规则排序**可以调整防护规则之间的优先级。

        ![规则排序](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15567/15663503237789_zh-CN.jpg)


