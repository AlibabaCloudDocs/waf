# ECS实例实现专线NAT网络转发最佳实践

阿里云混合云WAF的控制台访问地址会随机变换，您可以通过在ECS实例上配置iptables的NAT规则，实现在不添加本地网络到云上其他网段地址路由的情况上，线下的IDC或者机房WAF服务器通过NAT转化的方式访问Web应用防火墙控制台。

-   已创建CentOS系统的ECS实例，并且该ECS实例所在地域要与混合云WAF实例地域相同。
-   已创建NAT实例。
-   已准备好一个仅提供给混合云WAF使用的网段，例如101.0.0.0/8网段。

阿里云混合云WAF通过云端统一Restful API方式对外提供混合云下多种流量防护结果的统一管控。您可以通过访问阿里云Web应用防火墙控制台的方式访问混合云WAF实例。但在部分场景下，需要通过CEN专线进行统一配置和规格管理，以保持访问流量的私密性和安全性。这种情况下，您可以通过在云企业网内的ECS实例上配置NAT规则打通网络连接。

![架构图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4437132161/p237962.png)

## 操作步骤

1.  使用root用户登录ECS实例。

2.  查看iptables组件的规则。

    ```
    IPtables–L
    ```

3.  确认IP转发功能是否已打开。

    ```
    sysctl-a|grep'net.ipv4.ip_forward'
    ```

    命令执行后：

    -   如果返回值为1，说明IP转发规则已打开，请直接跳转至步骤5。
    -   如果返回值不为1，说明IP转发规则未打开，请跳转至步骤4修改配置文件/etc/sysctl.conf。
4.  修改配置文件/etc/sysctl.conf。

    1.  添加`net.ipv4.ip_forward=1`。
    2.  运行`sysctl -p`。
5.  部署混合云WAF服务器。

    配置一条101.0.0.0/8网段的路由，下一跳指向云上配置NAT的ECS。

    **说明：** 内部的101网段和WAF域名的100网段，需要根据域名信息一一对应。

6.  配置云上NAT服务器的iptables规则，将请求转发到混合云WAF的管控云端域名地址空间中。

    1.  转换SNAT源地址，将所有请求通过NAT服务器的10网段发送。

        ```
        iptables-tnat-APOSTROUTING-s输入来源网段-jSNAT--to-source输入NAT服务器IP
        ```

    2.  DNAT目的地址转换，将所有请求中的101网段，转换为WAF域名对应的100网段。

        ```
        iptables-tnat-APREROUTING-d输入用户内部101网段IP-jDNAT--to-destination输入对应的WAF域名的100网段IP
        ```

        **说明：** WAF域名的所有IP，均需要配置一条iptables DNAT规则，如果云上WAF的IP有改变，则对应的iptables规则中的IP也需要同步修改。

7.  如果自建了内网DNS解析服务，需要在DNS服务器上配置WAF域名的解析。

8.  测试转发请求是否成功。

    从本地服务器访问Curl <WAF域名\>-v，在云上NAT服务器上抓包查看该请求转发是否成功。


