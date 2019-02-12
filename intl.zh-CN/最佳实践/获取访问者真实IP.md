# 获取访问者真实IP {#concept_l4w_fkc_p2b .concept}

在大部分实际业务场景中，网站访问请求并不是简单地从用户（访问者）的浏览器直达网站的源站服务器，中间可能经过所部署的CDN、高防IP、WAF等代理服务器。例如，网站可能采用这样的部署架构：用户 \> CDN/高防IP/WAF \> 源站服务器。这种情况下，访问请求在经过多层加速或代理转发后，源站服务器该如何获取发起请求的真实客户端IP？

一般情况下，透明的代理服务器在将用户的访问请求转发到下一环节的服务器时，会在HTTP的请求头中添加一条**X-Forwarded-For**记录，用于记录用户的真实IP，其记录格式为`X-Forwarded-For:用户IP`。如果期间经历多个代理服务器，则**X-Forwarded-For**将以该格式记录用户真实IP和所经过的代理服务器IP：`X-Forwarded-For:用户IP, 代理服务器1-IP, 代理服务器2-IP, 代理服务器3-IP, ……`。

因此，常见的Web应用服务器可以**使用X-Forwarded-For的方式获取访问者真实IP**。以下分别针对Nginx、IIS 6、IIS 7、Apache和Tomcat服务器，介绍相应的X-Forwarded-For配置方案。

**说明：** 在开始配置前，务必对现有环境进行备份，包括ECS快照备份和Web应用服务器配置文件备份。

## Nginx配置方案 {#section_msy_zkc_p2b .section}

**1. 确认已安装http\_realip\_module模块**

为实现负载均衡，Nginx使用**http\_realip\_module**模块来获取真实IP。

您可以通过执行`# nginx -V | grep http_realip_module`命令查看是否已安装该模块。如未安装，则需要重新编译Nginx服务并加装该模块。

**说明：** 一般情况下，如果通过一键安装包安装Nginx服务器，默认不安装该模块。

参考以下方法，安装**http\_realip\_module**模块：

```
wget http://nginx.org/download/nginx-1.12.2.tar.gz
tar zxvf nginx-1.12.2.tar.gz
cd nginx-1.12.2
./configure --user=www --group=www --prefix=/alidata/server/nginx --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module
make
make install
kill -USR2 `cat /alidata/server/nginx/logs/nginx.pid`
kill -QUIT `cat /alidata/server/nginx/logs/ nginx.pid.oldbin`
```

**2. 修改Nginx对应server的配置**

打开`default.conf`配置文件，在`location / {}`中添加以下内容：

**说明：** 

其中，`ip_range1，2，...，x` 指WAF的回源IP地址，需要分多条分别添加。

```
set_real_ip_from ip_range1;
set_real_ip_from ip_range2;
...
set_real_ip_from ip_rangex;
real_ip_header    X-Forwarded-For;
```

**3. 修改日志记录格式 log\_format**

log\_format一般在`nginx.conf`配置文件中的http配置部分。在log\_format中，添加x-forwarded-for字段，替换原来remote-address字段，即将log\_format修改为以下内容：

```
log_format  main  '$http_x_forwarded_for - $remote_user [$time_local] "$request" ' '$status $body_bytes_sent "$http_referer" ' '"$http_user_agent" ';
```

完成以上操作后，执行`nginx -s reload`命令重启Nginx服务。配置生效后，Nignx服务器即可通过X-Forwarded-For的方式记录访问者真实IP。

## IIS 6配置方案 {#section_w4f_gkc_p2b .section}

您可以通过安装[F5XForwardedFor.dll](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/F5XForwardedFor2008.zip)插件，从IIS 6服务器记录的访问日志中获取访问者真实IP地址。

1.  根据您服务器的操作系统版本将x86\\Release或者x64\\Release目录中的F5XForwardedFor.dll文件拷贝至指定目录（例如，C:\\ISAPIFilters），同时确保IIS进程对该目录有读取权限。
2.  打开IIS管理器，找到当前开启的网站，在该网站上右键选择**属性**，打开属性页。
3.  在属性页切换至**ISAPI筛选器**，单击**添加**。
4.  在添加窗口下，配置以下参数，并单击**确定**。
    -   **筛选器名称**：F5XForwardedFor
    -   **可执行文件**：F5XForwardedFor.dll的完整路径，例如C:\\ISAPIFilters\\F5XForwardedFor.dll
5.  重启 IIS 服务器，等待配置生效。

## IIS 7配置方案 {#section_apf_gkc_p2b .section}

您可以通过安装[F5XForwardedFor 模块](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/x_forwarded_for.rar)模块，获取访问者真实IP地址。

1.  根据服务器的操作系统版本将x86\\Release或者x64\\Release目录中的F5XFFHttpModule.dll和F5XFFHttpModule.ini文件拷贝到指定目录（例如，C:\\x\_forwarded\_for\\x86或C:\\x\_forwarded\_for\\x64），并确保IIS进程对该目录有读取权限。
2.  在**IIS服务器**选项中，双击打开**模块**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15588/15499518007620_zh-CN.png)

3.  单击**配置本机模块**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15588/15499518007621_zh-CN.png)

4.  在**配置本机模块**对话框中，单击**注册**，分别注册已下载的DLL文件。

    -   注册模块 x\_forwarded\_for\_x86
        -   **名称**：x\_forwarded\_for\_x86
        -   **路径**：C:\\x\_forwarded\_for\\x86\\F5XFFHttpModule.dll
    -   注册模块 x\_forwarded\_for\_x64
        -   **名称**：x\_forwarded\_for\_x64
        -   **路径**：C:\\x\_forwarded\_for\\x64\\F5XFFHttpModule.dll
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15588/15499518007622_zh-CN.png)

5.  注册完成后，勾选新注册的模块（x\_forwarded\_for\_x86 和 x\_forwarded\_for\_x64）并单击**确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15588/15499518007624_zh-CN.png)

6.  在API 和CGI限制中，分别添加已注册的DLL，并将其**限制**改为**允许**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15588/15499518007625_zh-CN.png)

7.  重启IIS服务器，等待配置生效。

## Apache配置方案 {#section_dtm_vnc_p2b .section}

**Windows操作系统**

在Apache 2.4及以上版本的安装包中已自带remoteip\_module模块文件（mod\_remoteip.so），您可以通过该模块获取访问者真实IP地址。

1.  在Apache的extra配置文件夹（conf/extra/）中，新建httpd-remoteip.conf配置文件。

    **说明：** 为减少直接修改httpd.conf配置文件的次数，避免因操作失误而导致的业务异常，通过引入remoteip.conf配置文件的方式加载相关配置。

2.  在httpd-remoteip.conf配置文件中，添加以下访问者真实IP的获取规则。

    ```
    ＃加载mod_remoteip.so模块
    LoadModule remoteip_module modules/mod_remoteip.so
    ＃设置RemoteIPHeader头部
    RemoteIPHeader X-Forwarded-For
    ＃设置回源IP段
    RemoteIPInternalProxy 112.124.159.0/24 118.178.15.0/24 120.27.173.0/24 203.107.20.0/24 203.107.21.0/24 203.107.22.0/24 203.107.23.0/24 47.97.128.0/24 47.97.129.0/24 47.97.130.0/24 47.97.131.0/24
    ```

3.  修改conf/httpd.conf配置文件，插入httpd-remoteip.conf配置文件。

    ```
    Include conf/extra/httpd-remoteip.conf
    ```

4.  在httpd.conf配置文件中，修改日志格式。

    ```
    LogFormat "%a %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
    LogFormat "%a %l %u %t \"%r\" %>s %b" common
    ```

5.  重启Apache服务，使配置生效。

**Linux操作系统**

您可以通过安装Apache的[mod\_rpaf](http://stderr.net/apache/rpaf/)第三方模块，获取访问者真实IP地址。

1.  执行以下命令，安装mod\_rpaf模块。

    ```
    wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
    tar zxvf mod_rpaf-0.6.tar.gz
    cd mod_rpaf-0.6
    /alidata/server/httpd/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
    ```

2.  修改Apache配置文件/alidata/server/httpd/conf/httpd.conf，在文件最后添加以下内容：

    **说明：** 其中，`RPAFproxy_ips ip地址`不是负载均衡提供的公网IP。具体IP可参考Apache的日志，通常会有两个IP地址。

    ```
    LoadModule rpaf_module modules/mod_rpaf-2.0.so
    RPAFenable On
    RPAFsethostname On
    RPAFproxy_ips ip地址
    RPAFheader X-Forwarded-For
    ```

3.  添加完成后，执行以下命令重启Apache服务，使配置生效。

    ```
    /alidata/server/httpd/bin/apachectl restart
    ```


**mod\_rpaf模块配置示例**

```

LoadModule rpaf_module modules/mod_rpaf-2.0.so
RPAFenable On
RPAFsethostname On
RPAFproxy_ips 10.242.230.65 10.242.230.131
RPAFheader X-Forwarded-For
```

## Tomcat配置方案 {#section_tpf_gkc_p2b .section}

通过启用Tomcat的X-Forwarded-For功能，获取访问者真实IP地址。

打开tomcat/conf/server.xml配置文件，将AccessLogValve日志记录功能部分修改为以下内容：

```
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
prefix="localhost_access_log." suffix=".txt"
pattern="%{X-FORWARDED-FOR}i %l %u %t %r %s %b %D %q %{User-Agent}i %T" resolveHosts="false"/>
```

