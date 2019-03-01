# 已配置WAF防护的ECS源站遭受入侵的处理建议 {#concept_zcm_kvl_q2b .concept}

如果您为网站配置WAF防护后，源站服务器ECS仍然被恶意攻击者入侵，请参照下表查看可能原因和对应解决方案。

|序号|可能原因|解决方案|
|--|----|----|
|1|接入WAF之前已被入侵，需要先把服务器清理干净。|参照下文给出的方案清理您的服务器。|
|2|WAF配置好后，没有更改DNS解析，访问流量实际上还是直接去向服务器，没有经过WAF防御。|确保已经修改DNS解析，让网站在WAF防御之下。请参考[业务接入WAF配置](../../../../../intl.zh-CN/用户指南/接入WAF/业务接入WAF配置.md#)。|
|3|使用WAF之前，ECS IP已经暴露，且未配置安全组，黑客直接攻击ECS。|配置安全组，防止直接绕过WAF直接攻击ECS。请参考[源站保护](../../../../../intl.zh-CN/最佳实践/源站保护.md#)。|
|4|ECS服务器上还有其他站点，且该站点未受到WAF防护，导致服务器被“旁注”。|确保该ECS上所有HTTP业务都经过WAF防御。|
|5|非Web攻击方式入侵，比如暴力破解ECS SSH密码等。|确保ECS、数据库全部使用强密码。|

**说明：** 清理主机木马、病毒前，请先[创建快照](../../../../../intl.zh-CN/快照/使用快照/创建快照.md#)进行备份，避免误操作导致数据丢失无法还原。

## 排查病毒木马 {#section_twr_clb_ygb .section}

1.  使用`netstat`查看网络连接，分析是否有可疑发送行为，如有则停止服务器。
2.  使用杀毒软件进行病毒查杀。

Linux中常用的木马清理命令有：

```
chattr -i /usr/bin/.sshd 
rm -f /usr/bin/.sshd 
chattr -i /usr/bin/.swhd 
rm -f /usr/bin/.swhd 
rm -f -r /usr/bin/bsd-port 
cp /usr/bin/dpkgd/ps /bin/ps 
cp /usr/bin/dpkgd/netstat /bin/netstat 
cp /usr/bin/dpkgd/lsof /usr/sbin/lsof 
cp /usr/bin/dpkgd/ss /usr/sbin/ss
rm -r -f /root/.ssh 
rm -r -f /usr/bin/bsd-port
find /proc/ -name exe | xargs ls -l | grep -v task |grep deleted| awk '{print $11}' | awk -F/ '{print $NF}' | xargs killall -9
```

## 排查并修复服务器漏洞 {#section_kw1_flb_ygb .section}

1.  查看服务器账号是否有异常。如有，则停止服务器，并删除异常账号。
2.  查看服务器是否有异地登录情况。如有，则修改登录密码为强密码。强密码由10位以上字符组成，同时包含大小写字母、数字，和特殊符号。
3.  检查Jenkins、Tomcat、PhpMyadmin、WDCP、Weblogic等服务的后台密码，确保启用强密码。对于不使用的服务，建议关闭其8080管理端口。
4.  查看Web应用（如struts、ElasticSearch等）是否存在漏洞。确保网站在WAF防御之下，建议结和使用态势感知来查杀木马、病毒，并安装补丁。
5.  查看是否存在Jenkins管理员无密码远程执行命令漏洞。如有，请设置密码或关闭8080端口管理页面。
6.  查看是否有Redis无密码可远程写入文件漏洞。检查`/root/`下是否有黑客创建的SSH登录密钥文件，如有则将其删除。修改Redis为有密码访问并使用强密码。若不需要公网访问，请使用`bind 127.0.0.1`绑定本地访问。
7.  查看MySQL、SQLServer、FTP、WEB管理后台等其它设置密码的地方，确保启用强密码。

## 使用云盾服务 {#section_kq2_glb_ygb .section}

-   确保该ECS上所有网站都已启用WAF。
-   使用云盾态势感知，扫描主机风险和漏洞，查杀木马并修复漏洞。

## 重新初始化云盘 {#section_yhd_hlb_ygb .section}

假如在排查过病毒木马及服务器漏洞，并启用云盾服务后，问题仍然存在，建议您重新初始化云盘，将作系统盘或数据盘用的云盘恢复到创建时的状态。

具体操作请参考[重新初始化云盘](../../../../../intl.zh-CN/块存储/云盘/重新初始化云盘.md#)。

**说明：** 在重新初始化云盘前，请将系统盘和数据盘的数据完全下载备份到本地保存；初始化以后，对数据进行杀毒后再上传。

重置磁盘后，重新执行排查病毒木马，排查并修复服务器漏洞，使用云盾服务。

