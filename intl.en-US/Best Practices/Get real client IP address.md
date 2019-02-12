# Get real client IP address {#concept_l4w_fkc_p2b .concept}

In many cases, a visitor’s browser is not directly connected to the server for website access because CDN, WAF, or Anti-DDoS Pro is deployed in between. For example, the following is a common architecture: Client \> CDN/WAF/Anti-DDoS Pro \> Origin server. Here, how can a server get the real IP address of the client whose initial request passes through multiple layers of acceleration?

When forwarding a user’s request to the server next in the chain, a proxy server that is open and transparent adds an **X-Forwarded-For** record to the HTTP header. This record is used to record the user’s real IP address and takes the format of `X-Forwarded-For: user IP`. If multiple proxy servers are involved in the request process, **X-Forwarded-For** record displays in the following format: `X-Forwarded-For: user's IP address, Proxy 1-IP address, Proxy 2-IP address, Proxy 3-IP address...`.

Therefore, a common application server can **use the X-Forwarded-For record to get a visitor’s real IP address**. The following content describes the corresponding X-Forwarded-For configuration methods for the Nginx, IIS 6, IIS 7, Apache, and Tomcat servers.

**Note:** Back up your current environment such as the ECS snapshot and web server configuration file before performing the following configuration.

## Nginx {#section_msy_zkc_p2b .section}

**1. Install http\_realip\_module.**

As load balancing, Nginx uses **http\_realip\_module** to get the real IP address.

You can run the `# nginx -V | grep http_realip_module` command to verify whether or not, this module is installed. If not, recompile Nginx and load this module.

**Note:** Nginx installed by the default procedure does not have this module installed.

Use the following code to install the **http\_realip\_module** module.

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

**2. Add the WAF IP addresses to the Nginx configuration.**

Open `default.conf` and add the following content to `location / {}`:

```
set_real_ip_from ip_range1;
set_real_ip_from ip_range2;
...
set_real_ip_from ip_rangex;
real_ip_header    X-Forwarded-For;
```

**Note:** `ip_range1,2,...,x` indicates the back-to-source IP addresses of WAF, and multiple entries must be added respectively.

**3. Modify log\_format.**

log\_format usually exists under the HTTP configuration in `nginx.conf`. Add the x-forwarded-for field in log\_format to replace the original remote-address. After the modification, log\_format is as follows.

```
log_format  main  '$http_x_forwarded_for - $remote_user [$time_local] "$request" ' '$status $body_bytes_sent "$http_referer" ' '"$http_user_agent" ';
```

After the preceding operations are completed, run `nginx -s reload` to restart Nginx and validate the configuration. When the configuration is effective, the Nignx server records the client IP address in the X-Forwarded-For field.

## IIS 6 {#section_w4f_gkc_p2b .section}

You can get the visitor’s real IP address from the IIS 6 log, provided that the [F5XForwardedFor.dll](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/F5XForwardedFor2008.zip) plug-in has been installed.

1.  Copy F5XForwardedFor.dll from the x86\\Release or x64\\Release directory \(according to the OS version of the server\) to a specified directory assumed as C:\\ISAPIFilters, and make sure that the IIS process has the read permission for this directory.
2.  Open the IIS manager, find the currently visited website, right-click the website and select **Property** to open the Property page.
3.  Switch to the **ISAPI Filter** tab page on the Property page and click **Add**.
4.  Set the following parameters in the Add window, and then click **OK**.
    -   **Filter name**: F5XForwardedFor
    -   **Executable file**: enter the complete path of F5XForwardedFor.dll. In this example, C:\\ISAPIFilters\\F5XForwardedFor.dll.
5.  Restart the IIS server and wait for the configuration to be effective.

## IIS 7 {#section_apf_gkc_p2b .section}

You can get the visitor’s real IP address through the [F5XForwardedFor](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/x_forwarded_for.rar) module.

1.  Copy F5XFFHttpModule.dll and F5XFFHttpModule.ini from the x86\\Release or x64\\Release directory \(according to the OS version of the server\) to a specified directory assumed as C:\\x\_forwarded\_for\\x86 and C:\\x\_forwarded\_for\\x64, and make sure that the IIS process has the read permission for this directory.
2.  In **IIS Manager**, double-click to open **Module**.
3.  Click **Configure Local Module**.
4.  Click **Register** in the **Configure Local Module** dialog box, and register the downloaded DLL file.
    -   Register the x\_forwarded\_for\_x86 module
        -   **Name**: x\_forwarded\_for\_x86
        -   **Path**: C:\\x\_forwarded\_for\\x86\\F5XFFHttpModule.dll
    -   Register the x\_forwarded\_for\_x64 module
        -   **Name**: x\_forwarded\_for\_x64
        -   **Path**: C:\\x\_forwarded\_for\\x64\\F5XFFHttpModule.dll
5.  After registration, select the newly registered modules \(x\_forwarded\_for\_x86 and x\_forwarded\_for\_x64\), and click **OK** to enable them.
6.  Add the registered DLL in API and CGI restrictions respectively, and change the settings from **Restricted** to **Allowed**.
7.  Restart the IIS server and wait for the configuration to be effective.

## Apache {#section_dtm_vnc_p2b .section}

Follow these steps to obtain the visitor’s real IP address in Apache.

1.  Run the following code to install the third-party module [mod\_rpaf](http://stderr.net/apache/rpaf/) for Apache.

    ```
    wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
    tar zxvf mod_rpaf-0.6.tar.gz
    cd mod_rpaf-0.6
    /alidata/server/httpd/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
    ```

2.  Modify the Apache configuration file `/alidata/server/httpd/conf/httpd.conf` and add the following information at the end.

    ```
    LoadModule rpaf_module modules/mod_rpaf-2.0.so
    RPAFenable On
    RPAFsethostname On
    RPAFproxy_ips IP address
    RPAFheader X-Forwarded-For
    ```

    Where `RPAFproxy_ips ip address` is not the public IP address provided by Server Load Balancer. You can obtain the specific IP address from the Apache log. Usually two IP addresses are included.

3.  Run the following command to restart Apache once you add the IP address.

    ```
    /alidata/server/httpd/bin/apachectl restart
    ```


## Tomcat {#section_tpf_gkc_p2b .section}

You can enable the X-Forwarded-For feature of the Tomcat server as follows.

Open tomcat/conf/server.xml and modify the AccessLogValve log record function to the following content:

```
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
prefix="localhost_access_log." suffix=".txt"
pattern="%{X-FORWARDED-FOR}i %l %u %t %r %s %b %D %q %{User-Agent}i %T" resolveHosts="false"/>
```

