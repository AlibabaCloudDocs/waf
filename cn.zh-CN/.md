# 【防护说明】FireEye攻击事件红队攻击工具泄露

## 事件说明

FireEye公司于2020年12月08日公开了近期遭受黑客攻击后泄露的红方攻击工具相关细节，其中包含一份工具对应的CVE列表（[单击此处查看FireEye官方说明](https://www.fireeye.com/blog/threat-research/2020/12/unauthorized-access-of-fireeye-red-team-tools.html)）。阿里云Web应用防火墙已能针对被泄露的工具和相关漏洞提供默认的检测与防护能力。

## WAF防护漏洞列表

阿里云安全研究团队对这份CVE列表中的漏洞进行了分析，证明阿里云WAF已默认支持Web相关的漏洞防护。CVE列表详细内容如下：

|CVE编号|漏洞名称|
|-----|----|
|CVE-2019-11510|Pulse Secure任意文件读取漏洞|
|CVE-2018-13379|Fortinet FortiOS路径遍历漏洞|
|CVE-2018-15961|Adobe ColdFusion远程代码执行漏洞|
|CVE-2019-0604|SharePoint远程代码执行漏洞|
|CVE-2019-11580|Atlassian Crowd远程代码执行漏洞|
|CVE-2019-19781|Citrix ADC远程代码执行|
|CVE-2020-10189|Zoho ManageEngine反序列化远程代码执行漏洞|
|CVE-2019-3398|Confluence路径穿越漏洞|
|CVE-2020-0688|微软EXCHANGE服务的远程代码执行漏洞|
|CVE-2019-8394|ManageEngine ServiceDesk Plus任意文件上传漏洞|

阿里云安全团队会持续关注此次事件，并在新的利用更新后第一时间进行漏洞的分析与规则的更新。

