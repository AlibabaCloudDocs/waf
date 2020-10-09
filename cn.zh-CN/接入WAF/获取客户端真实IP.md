---
keyword: [客户端IP, 流量代理, X-Forwarded-For, Web应用防火墙, WAF]
---

# 获取客户端真实IP

网站部署了流量代理服务（例如Web应用防火墙、DDoS高防、CDN）后，源站服务器可以通过解析回源请求中的X-Forwarded-For记录，获取客户端的真实IP。本文介绍了不同类型的Web应用服务器（包括Nginx、IIS 6、IIS 7、Apache、Tomcat）以及容器K8s如何进行相关设置，以获取客户端的真实IP。

## 背景信息

在大部分实际业务场景中，网站访问请求并不是简单地从客户端（访问者）的浏览器直接到达网站的源站服务器，而是在客户端和服务器之前经过了根据业务需要部署的Web应用防火墙、DDoS高防、CDN等代理服务器。这种情况下，访问请求在到达源站服务器之前可能经过了多层安全代理转发或加速代理转发，源站服务器该如何获取发起请求的真实客户端IP？

透明的代理服务器在将客户端的访问请求转发到下一环节的服务器时，会在HTTP的请求头中添加一条X-Forwarded-For记录，用于记录客户端的IP，格式为`X-Forwarded-For:客户端IP`。如果客户端和服务器之前有多个代理服务器，则X-Forwarded-For记录使用以下格式记录客户端IP和依次经过的代理服务器IP：`X-Forwarded-For:客户端IP, 代理服务器1的IP, 代理服务器2的IP, 代理服务器3的IP, ……`。

因此，常见的Web应用服务器可以通过解析X-Forwarded-For记录获取客户端真实IP。

下文分别针对Nginx、IIS 6、IIS 7、Apache和Tomcat服务器以及容器K8s，介绍相应的X-Forwarded-For配置方案。

**说明：** 开始配置之前，请务必对现有环境进行备份，包括ECS快照备份和Web应用服务器配置文件备份。

## Nginx配置方案

Nginx服务器使用http\_realip\_module模块获取客户端IP地址。

1.  安装http\_realip\_module模块。

    在Nginx服务器上执行`# nginx -V | grep http_realip_module`命令，查看是否已安装http\_realip\_module模块。如果没有安装，请重新编译Nginx服务并加装该模块。

    **说明：** 一般情况下，通过一键安装包安装的Nginx服务器默认不安装http\_realip\_module模块。

    参考以下方法，安装http\_realip\_module模块。

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

2.  修改Nginx服务配置文件。

    1.  打开`default.conf`配置文件。

    2.  在`location / {}`中添加以下内容：

        ```
        set_real_ip_from <ip_range1>;
        set_real_ip_from <ip_range2>;
        ...
        set_real_ip_from <ip_rangex>;
        real_ip_header X-Forwarded-For;
        ```

        其中，`<ip_range1>`、`<ip_range2>`、`<ip_rangex>`需要设置为代理服务器（即Web应用防火墙）的回源IP段。关于Web应用防火墙的回源IP段，请参见[放行WAF回源IP段](/cn.zh-CN/接入WAF/CNAME接入/放行WAF回源IP段.md)。

        多个回源IP段必须分行添加。假设代理服务器的回源IP段包含10.0.0.1、10.0.0.2、10.0.0.3，则使用以下格式：

        ```
        set_real_ip_from 10.0.0.1;
        set_real_ip_from 10.0.0.2;
        set_real_ip_from 10.0.0.3;
        real_ip_header X-Forwarded-For;
        ```

3.  修改log\_format日志记录格式。

    1.  打开`nginx.conf`配置文件，定位到http配置部分的`log_format`。

    2.  在`log_format`中添加`x-forwarded-for`字段，替换默认的`remote-address`字段。

        修改后的log\_format内容如下：

        ```
        log_format  main  '$http_x_forwarded_for - $remote_user [$time_local] "$request" ' '$status $body_bytes_sent "$http_referer" ' '"$http_user_agent" ';
        ```

4.  执行`nginx -s reload`命令，重启Nginx服务。

    重启Nignx服务器后，上述配置才会生效，Nignx服务器将可以通过X-Forwarded-For记录获取客户端真实IP。


## IIS 6配置方案

IIS 6服务器必须安装`F5XForwardedFor.dll`插件，才可以从服务器记录的访问日志中获取客户端IP地址。

1.  根据服务器操作系统版本，将`x86\Release`或`x64\Release`目录下的`F5XForwardedFor.dll`文件拷贝到某个自定义目录（例如`C:\ISAPIFilters`）。

    **说明：** 请确保IIS进程对自定义目录拥有读取权限。

    如果`x86\Release`或`x64\Release`目录下没有`F5XForwardedFor.dll`插件，您可以手动下载[F5XForwardedFor.dll](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/F5XForwardedFor2008.zip)。

2.  打开IIS管理器，定位到当前开启的网站，在网站上右键单击**属性**。

3.  在**属性**页切换到**ISAPI筛选器**，单击**添加**。

4.  在添加对话框，完成以下参数设置，并单击**确定**。

    -   **筛选器名称**：输入`F5XForwardedFor`。
    -   **可执行文件**：填写`F5XForwardedFor.dll`的完整路径，例如`C:\ISAPIFilters\F5XForwardedFor.dll`。
5.  重启IIS服务器，等待配置生效。


## IIS 7配置方案

IIS 7服务器必须安装F5XForwardedFor模块，才可以从服务器记录的访问日志中获取客户端IP地址。

1.  根据服务器操作系统版本，将`x86\Release`或`x64\Release`目录下的`F5XFFHttpModule.dll`和`F5XFFHttpModule.ini`文件拷贝到某个自定义目录（例如`C:\x_forwarded_for\x86`或`C:\x_forwarded_for\x64`）。

    **说明：** 请确保IIS进程对自定义目录拥有读取权限。

    如果`x86\Release`或`x64\Release`目录下没有`F5XFFHttpModule.dll`和`F5XFFHttpModule.ini`，您可以手动下载[F5XForwardedFor模块](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/x_forwarded_for.rar)。

2.  在**IIS**选项中，双击打开**模块**。

    ![打开模块配置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9011549951/p7620.png)

3.  单击**配置本机模块**。

    ![配置本机模块](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0111549951/p7621.png)

4.  在**配置本机模块**对话框，单击**注册**，服务器操作系统版本注册相关的DLL文件。

    -   32为操作系统注册x\_forwarded\_for\_x86模块

        -   **名称**：输入`x_forwarded_for_x86`。
        -   **路径**：填写`F5XFFHttpModule.dll`的完整路径，例如`C:\x_forwarded_for\x86\F5XFFHttpModule.dll`。
        ![注册模块](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0111549951/p7622.png)

    -   64为操作系统注册x\_forwarded\_for\_x64模块

        -   **名称**：输入`x_forwarded_for_x64`。
        -   **路径**：填写`F5XFFHttpModule.dll`的完整路径，例如C:\\x\_forwarded\_for\\x64\\F5XFFHttpModule.dll。
        ![注册本机模块](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0111549951/p101433.png)

5.  在**配置本机模块**对话框，选中新注册的模块（x\_forwarded\_for\_x86、x\_forwarded\_for\_x64）并单击**确定**。

    ![启用模块](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0111549951/p7624.png)

6.  在**ISAPI 和CGI限制**页面，添加已注册的DLL，并将**限制**设置为**允许**。

    ![启用功能](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0111549951/p7625.png)

7.  重启IIS服务器，等待配置生效。


## Apache配置方案

Windows操作系统

Apache 2.4及以上版本的安装包中自带remoteip\_module模块文件（`mod_remoteip.so`），Apache服务器使用该模块获取客户端IP地址。

1.  进入Apache服务器的extra配置文件夹（`conf/extra/`），新建`httpd-remoteip.conf`配置文件。

    **说明：** 通过引入`remoteip.conf`配置文件的方式加载相关配置，减少直接修改`httpd.conf`配置文件的次数，避免因操作失误导致业务异常。

2.  编辑`httpd-remoteip.conf`配置文件，在文件中添加以下内容：

    ```
    ＃ 加载mod_remoteip.so模块
    LoadModule remoteip_module modules/mod_remoteip.so
    ＃ 设置RemoteIPHeader头部
    RemoteIPHeader X-Forwarded-For
    ＃ 设置回源IP段
    RemoteIPInternalProxy <ip_range1> <ip_range2> …… <ip_rangex>
    ```

    其中，`<ip_range1>`、`<ip_range2>`、`<ip_rangex>`需要设置为代理服务器（即Web应用防火墙）的回源IP段。关于Web应用防火墙的回源IP段，请参见[放行WAF回源IP段](/cn.zh-CN/接入WAF/CNAME接入/放行WAF回源IP段.md)。

    多个回源IP段之前使用空格分隔。假设代理服务器的回源IP段包含10.0.0.1、10.0.0.2、10.0.0.3，则使用以下格式：

    ```
    RemoteIPInternalProxy 10.0.0.1 10.0.0.2 10.0.0.3
    ```

3.  编辑conf/httpd.conf配置文件，在文件中添加以下内容：

    ```
    Include conf/extra/httpd-remoteip.conf
    ```

    以上命令表示在conf/httpd.conf中插入`httpd-remoteip.conf`配置文件。

4.  在`httpd.conf`配置文件中修改日志格式。

    ```
    LogFormat "%a %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
    LogFormat "%a %l %u %t \"%r\" %>s %b" common
    ```

5.  重启Apache服务，使配置生效。


Linux操作系统

您可以参考上述Windows操作系统服务器的配置方式，添加Apache 2.4及以上版本自带的remoteip\_module模块（`mod_remoteip.so`）并配置日志格式，获取客户端IP地址。

如果Linux服务器使用的Apache版本低于2.4，请参照以下步骤，通过设置Apache的第三方模块（mod\_rpaf），获取客户端IP地址。

1.  安装mod\_rpaf模块。

    ```
    wget https://github.com/gnif/mod_rpaf/archive/v0.6.0.tar.gz
    tar zxvf mod_rpaf-0.6.tar.gz
    cd mod_rpaf-0.6
    /alidata/server/httpd/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
    ```

2.  编辑Apache配置文件`/alidata/server/httpd/conf/httpd.conf`，在文件最后添加以下内容：

    ```
    LoadModule rpaf_module modules/mod_rpaf-2.0.so
    RPAFenable On
    RPAFsethostname On
    RPAFproxy_ips <rpaf ip地址>
    RPAFheader X-Forwarded-For
    ```

    其中，`<rpaf ip地址>`不是代理服务器的公网IP地址，具体IP请通过Apache日志查询。通常包含两个IP地址，示例如下：

    ```
    LoadModule rpaf_module modules/mod_rpaf-2.0.so
    RPAFenable On
    RPAFsethostname On
    RPAFproxy_ips 10.***.***.65 10.***.***.131
    RPAFheader X-Forwarded-For
    ```

3.  重启Apache服务，使配置生效。

    ```
    /alidata/server/httpd/bin/apachectl restart
    ```


更多Apache相关模块的信息，请参见[Apache帮助文档](http://httpd.apache.org/docs/2.4/mod/mod_remoteip.html)。

## Tomcat配置方案

Tomcat服务器通过启用X-Forwarded-For功能，获取客户端IP地址。

1.  打开`tomcat/conf/server.xml`配置文件。

2.  将AccessLogValve日志记录功能部分修改为以下内容：

    ```
    <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
    prefix="localhost_access_log." suffix=".txt"
    pattern="%{X-FORWARDED-FOR}i %l %u %t %r %s %b %D %q %{User-Agent}i %T" resolveHosts="false"/>
    ```


## 容器K8s配置方案

如果您的ECS服务器部署在K8s上，K8s会将真实的客户端IP记录在X-Original-Forwarded-For字段中，并将WAF回源地址记录在X-Forwarded-For字段中。您需要修改容器的配置文件，使Ingress将真实的IP添加到X-Forwarded-For字段中，以便您正常获取真实的客户端IP地址。

您可以参考以下步骤，对容器配置文件进行修改。

1.  执行以下命令修改配置文件`kube-system/nginx-configuration`。

    ```
    kubectl -n kube-system edit cm nginx-configuration
    ```

2.  在配置文件中添加以下内容：

    ```
    compute-full-forwarded-for: "true"
    forwarded-for-header: "X-Forwarded-For"
    use-forwarded-headers: "true"
    ```

3.  保存配置文件。

    保存后配置即刻生效，Ingress会将真实的客户端IP添加到X-Forwarded-For字段中。

4.  将业务程序获取客户端真实IP的字段修改为X-Original-Forwarded-For。


