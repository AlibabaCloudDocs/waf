---
keyword: [IP addresses of clients, proxy, X-Forwarded-For, Web Application Firewall, WAF]
---

# Retrieve actual IP addresses of clients

If you deploy proxy servers, such as CDN, Anti-DDoS Premium, Anti-DDoS Pro, or WAF, on your website, the origin server can use the X-Forwarded-For header in back-to-origin requests to retrieve actual IP addresses of clients. This topic describes how to configure web application servers, such as NGINX, IIS 6, IIS 7, Apache, and Tomcat servers, and Kubernetes containers to retrieve the IP addresses of clients.

## Background information

In most scenarios, access requests initiated from the browsers of clients \(visitors\) are not directly sent to the origin server of a website. Instead, the access requests may pass through intermediate proxy servers, such as CDN, Anti-DDoS Premium, Anti-DDoS Pro, or WAF. During the process, these access requests are forwarded through multiple proxies for security and acceleration. This increases the difficulty in retrieving the actual IP addresses of the clients that initiated the requests.

To address the issue, the X-Forwarded-For header is implemented to record the actual IP addresses of the clients. The transparent proxy adds the X-Forwarded-For header to the HTTP request header before forwarding the access requests to the next-hop server. The header is in the `X-Forwarded-For:Client IP address` format. If the access requests pass through multiple intermediate proxy servers, the X-Forwarded-For header records the actual IP addresses of the clients and IP addresses of intermediate proxy servers. The header records multiple IP addresses separated by a comma \(,\), such as `X-Forwarded-For:Client IP address, IP address of Proxy Server 1, IP address of Proxy Server 2, IP address of Proxy Server 3, …`.

Therefore, common web application servers can use the X-Forwarded-For header to retrieve the actual IP addresses of the clients.

The following content demonstrates how to configure the X-Forwarded-For header on the NGINX, IIS 6, IIS 7, Apache, and Tomcat servers, as well as on the Kubernetes containers.

**Note:** Before you start, make sure that you have backed up the existing environment, including ECS instance snapshots and configuration files of the web application servers.

## Configure NGINX servers

The NGINX servers use an http\_realip\_module module to retrieve the actual IP addresses of the clients.

1.  Install the http\_realip\_module module.

    Run the `# nginx -V | grep http_realip_module` command on the NGINX server to check whether the module is installed. If the module is not installed, recompile NGINX and load the module.

    **Note:** This module is not installed when NGINX is installed by using a quick installation package.

    Install the http\_realip\_module module by using the following method:

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

2.  Modify the configuration file of NGINX.

    1.  Open the `default.conf` configuration file.

    2.  Add the following content to `location / {}`:

        ```
        set_real_ip_from <ip_range1>;
        set_real_ip_from <ip_range2>;
        ...
        set_real_ip_from <ip_rangex>;
        real_ip_header X-Forwarded-For;
        ```

        where, `<ip_range1>`, `<ip_range2>`, and `<ip_rangex>` are the back-to-origin IP addresses of WAF. For more information about the back-to-origin CIDR blocks of WAF, see [Allow access from WAF back-to-origin CIDR blocks](/intl.en-US/Website Access/Website access with CNAME/Allow access from WAF back-to-origin CIDR blocks.md).

        Enter one back-to-origin IP address in each line. If the back-to-origin IP addresses of the proxy servers include 10.0.0.1, 10.0.0.2, and 10.0.0.3, use the format similar to:

        ```
        set_real_ip_from 10.0.0.1;
        set_real_ip_from 10.0.0.2;
        set_real_ip_from 10.0.0.3;
        real_ip_header X-Forwarded-For;
        ```

3.  Modify the log format.

    1.  Open the `nginx.conf` configuration file. `log_format` is typically located in the HTTP configuration.

    2.  In `log_format`, replace the `remote-address` field with the `x-forwarded-for` field.

        The modified log\_format is as follows:

        ```
        log_format  main  '$http_x_forwarded_for - $remote_user [$time_local] "$request" ' '$status $body_bytes_sent "$http_referer" ' '"$http_user_agent" ';
        ```

4.  Run the `nginx -s reload` command to restart NGINX.

    The configurations take effect after the restart. The NGINX server records the actual IP addresses of the clients by using the X-Forwarded-For header.


## Configure IIS 6 servers

You must install the `F5XForwardedFor.dll` plug-in to retrieve the actual IP addresses of the clients from the access log recorded by an IIS 6 server.

1.  Depending on your server OS version, copy the `F5XForwardedFor.dll` file from the `x86\Release` or `x64\Release` directory to a custom directory, such as `C:\ISAPIFilters`.

    **Note:** Make sure that the IIS process has read and write permissions on the custom directory.

    If the plug-in is unavailable from the directory, click [F5XForwardedFor.dll](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/F5XForwardedFor2008.zip) to download it.

2.  Open Internet Information Services \(IIS\) Manager, find the website, right-click the website, and select **Properties**.

3.  In the **Default Web Site Properties** dialog box that appears, click the **ISAPI Filters** tab and click **Add**.

4.  In the Add ISAPI Filter dialog box, set the following parameters and click **OK**.

    -   **Filter name**: Enter `F5XForwardedFor`.
    -   **Executable**: Enter the complete path of `F5XForwardedFor.dll`, for example, `C:\ISAPIFilters\F5XForwardedFor.dll`.
5.  Restart the IIS server for the configurations to take effect.


## Configure IIS 7 servers

You can install the F5XForwardedFor module to retrieve the actual IP addresses of the clients from the access log recorded by an IIS 7 server.

1.  Depending on your server OS version, copy the `F5XFFHttpModule.dll` and `F5XFFHttpModule.ini` files from the `x86\Release` or `x64\Release` directory to a custom directory, such as `C:\x_forwarded_for\x86` or `C:\x_forwarded_for\x64`.

    **Note:** Make sure that the IIS process has read and write permissions on the custom directory.

    If the files are unavailable from the directory, click [F5XForwardedFor](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/x_forwarded_for.rar) to download it.

2.  In the **IIS Server** section, double-click **Module**.

3.  Click **Configure Local Module**.

4.  In the **Configure Local Module** dialog box, click **Register** to register the DLL file.

    -   Register the x\_forwarded\_for\_x86 module in a 32-bit system.
        -   **Name**: Enter `x_forwarded_for_x86`.
        -   **Path**: Enter the full path of the `F5XFFHttpModule.dll` module, for example `C:\x_forwarded_for\x86\F5XFFHttpModule.dll`.
    -   Register the x\_forwarded\_for\_x64 module in a 64-bit system.
        -   **Name**: Enter `x_forwarded_for_x64`.
        -   **Path**: Enter the full patch of the `F5XFFHttpModule.dll` module, for example C:\\x\_forwarded\_for\\x64\\F5XFFHttpModule.dll.
5.  In the **Configure Local Module** dialog box, select the newly registered x\_forwarded\_for\_x86 or x\_forwarded\_for\_x64 module and click **OK**.

6.  In the **ISAPI and CGI Restrictions** section, add the registered DLL file and set **Restriction** to **Allow**.

7.  Restart the IIS server and wait for the configurations to take effect.


## Configure Apache servers

Configure Apache servers in Windows.

The installation packages of Apache 2.4 and later provide the remoteip\_module module file \(`mod_remoteip.so`\). You can use this module to retrieve the actual IP addresses of clients.

1.  Create a configuration file named `httpd-remoteip.conf` in the extra configuration folder of Apache \(`conf/extra/`\).

    **Note:** You can load the related configurations by importing the `remoteip.conf` configuration file. This reduces the number of times that you modify the `httpd.conf` file and avoids service exceptions due to misoperations.

2.  Add the following content to the `httpd-remoteip.conf` configuration file:

    ```
    # Load the mod_remoteip.so module.
    LoadModule remoteip_module modules/mod_remoteip.so
    # Set the RemoteIPHeader header.
    RemoteIPHeader X-Forwarded-For
    # Set the back-to-origin IP addresses.
    RemoteIPInternalProxy <ip_range1> <ip_range2> …… <ip_rangex>
    ```

    where, `<ip_range1>`, `<ip_range2>`, and `<ip_rangex>` are the back-to-origin IP addresses of WAF. For more information about the back-to-origin CIDR blocks of WAF, see [Allow access from WAF back-to-origin CIDR blocks](/intl.en-US/Website Access/Website access with CNAME/Allow access from WAF back-to-origin CIDR blocks.md).

    Separate multiple back-to-origin IP addresses with spaces. If the IP addresses of the proxy servers include 10.0.0.1, 10.0.0.2, and 10.0.0.3, use the format similar to:

    ```
    RemoteIPInternalProxy 10.0.0.1 10.0.0.2 10.0.0.3
    ```

3.  Add the following content to the conf/httpd.conf configuration file:

    ```
    Include conf/extra/httpd-remoteip.conf
    ```

    The preceding content inserts the `httpd-remoteip.conf` configuration file into conf/httpd.conf.

4.  Modify the log format in the `httpd.conf` configuration file.

    ```
    LogFormat "%a %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
    LogFormat "%a %l %u %t \"%r\" %>s %b" common
    ```

5.  Restart Apache for the configurations to take effect.


Configure Apache servers in Linux.

Follow the preceding steps to add the remoteip\_module module \(`mod_remoteip.so`\) and configure the log format to retrieve the actual IP addresses of clients. This module is included in Apache 2.4 and later.

If the version of Apache is earlier than 2.4, install mod\_rpaf \(third-party module\) to retrieve the actual IP addresses of clients.

1.  Install the mod\_rpaf module.

    ```
    wget https://github.com/gnif/mod_rpaf/archive/v0.6.0.tar.gz
    tar zxvf mod_rpaf-0.6.tar.gz
    cd mod_rpaf-0.6
    /alidata/server/httpd/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
    ```

2.  Append the following content to the `/alidata/server/httpd/conf/httpd.conf` configuration file of Apache:

    ```
    LoadModule rpaf_module modules/mod_rpaf-2.0.so
    RPAFenable On
    RPAFsethostname On
    RPAFproxy_ips <rpaf IP address>
    RPAFheader X-Forwarded-For
    ```

    where, `<rpaf IP address>` is the IP address of the mod\_rpaf module. You can query the specific IP addresses in the Apache log. Do not use the IP addresses of the proxy servers. Typically, two IP addresses are included, as shown in the following example:

    ```
    LoadModule rpaf_module modules/mod_rpaf-2.0.so
    RPAFenable On
    RPAFsethostname On
    RPAFproxy_ips 10. ***. ***.65 10. ***. ***.131
    RPAFheader X-Forwarded-For
    ```

3.  Restart Apache for the configurations to take effect.

    ```
    /alidata/server/httpd/bin/apachectl restart
    ```


For more information about the Apache modules, see [Apache help document](http://httpd.apache.org/docs/2.4/mod/mod_remoteip.html).

## Configure Tomcat servers

Take the following steps to allow the Tomcat servers to retrieve the actual IP addresses of clients by using the X-Forwarded-For header.

1.  Open the `tomcat/conf/server.xml` configuration file.

2.  Modify the AccessLogValve logging function as follows:

    ```
    <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
    prefix="localhost_access_log." suffix=".txt"
    pattern="%{X-FORWARDED-FOR}i %l %u %t %r %s %b %D %q %{User-Agent}i %T" resolveHosts="false"/>
    ```


## Configure Kubernetes containers

If your ECS instance is deployed on Kubernetes, Kubernetes records the actual IP addresses of clients in the X-Original-Forwarded-For field and the back-to-origin IP addresses of WAF in the X-Forwarded-For field. To obtain the actual IP addresses of clients, you must modify the container configuration file to enable an Ingress controller to add them to the X-Forwarded-For field.

You can modify the container configuration file by performing the following steps:

1.  Run the following command to modify the `kube-system/nginx-configuration` configuration file:

    ```
    kubectl -n kube-system edit cm nginx-configuration
    ```

2.  Add the following content to the configuration file:

    ```
    compute-full-forwarded-for: "true"
    forwarded-for-header: "X-Forwarded-For"
    use-forwarded-headers: "true"
    ```

3.  Save the configuration file.

    The configurations take effect immediately after you save the configuration file. Then, the Ingress controller adds the actual IP addresses of clients to the X-Forwarded-For field.

4.  Change the field you use to obtain the actual IP addresses of clients to the X-Original-Forwarded-For field.


