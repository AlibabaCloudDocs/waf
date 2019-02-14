# 集成Web应用防火墙日志到syslog系统 {#concept_fqm_n13_tgb .concept}

本文介绍了如何将Web应用防火墙（WAF）的日志集成到syslog日志系统中，以实现合规、审计等要求，也方便您在安全操作中心统一管理所有相关日志。

## 概览 {#section_wt1_rd3_tgb .section}

该方案的整体集成架构如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038718_zh-CN.png)

**阿里云日志服务**为日志数据提供一站式服务，被广泛应用于阿里巴巴集团的许多大数据场景中。日志服务在无需开发介入的前提下，帮助您快速完成数据采集、消费、投递、查询和分析，提高运维运营效率，建立DT时代海量数据的处理能力。更多信息，请查看[什么是日志服务](../../../../../intl.zh-CN/产品简介/什么是日志服务.md#)。

**Python Program** 是运行在ECS上的一段日志投递程序，帮助您将WAF日志投递到syslog服务器。消费库（Consumer Library）是对LogHub消费者提供的高级模式，它使用消费组（Consumer Group）统一处理消费端问题。相比于直接使用SDK读取数据，消费库让您只关注业务逻辑，而无需在意日志服务的实施细节或多消费者间的容错问题。更多信息，请查看[消费组消费](../../../../../intl.zh-CN/用户指南/实时消费/消费组消费/消费组消费.md#)。

**Syslog服务器**是一个集中的日志消息管理服务器，它可以从多个syslog源接收数据。

## 前提条件 {#section_q22_n23_tgb .section}

进行配置前，请确保满足以下条件：

-   您已购买企业版或旗舰版Web应用防火墙，并为您的网站配置防护。更多信息，请查看[购买Web应用防火墙](../../../../../intl.zh-CN/产品定价/开通WAF/购买Web应用防火墙.md#)和[业务接入WAF配置](../../../../../intl.zh-CN/用户指南/接入WAF/业务接入WAF配置.md#)。
-   您拥有一个Linux ECS服务器，该服务器满足以下推荐配置：
    -   Ubuntu操作系统
    -   8核处理器，2.0Ghz以上主频率
    -   32GB内存
    -   可用磁盘空间大于2GB（建议在10GB以上）
-   您拥有一个syslog服务器，并开放UDP协议514端口用来接收syslog数据。

## 操作步骤 {#section_gyj_t23_tgb .section}

1.  开启Web应用防火墙日志功能。

    参照以下步骤，在Web应用防火墙控制台开启日志功能：

    1.  登录[云盾Web应用防火墙控制台](https://yundun.console.aliyun.com/?p=waf)。
    2.  在左侧导航栏，选择**市场管理** \> **应用管理**。
    3.  在**日志服务实时查询分析**应用下，单击**升级**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038719_zh-CN.png)

    4.  在变配页面，开通**日志服务**， 并根据实际需求选择**日志存储时长**和**日志存储容量**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038720_zh-CN.png)

    5.  开通日志服务后，在**日志服务实时查询分析**应用下，单击**授权**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038721_zh-CN.png)

    6.  在云资源访问授权页面，单击**同意授权**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038723_zh-CN.png)

    7.  在**日志服务实时查询分析**应用下，单击**配置**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038724_zh-CN.png)

    8.  在下拉框中选择要配置的域名，并打开功能开关。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038725_zh-CN.png)

2.  在ECS中配置Python环境。

    参照以下步骤在ECS实例中安装日志服务的Python SDK：

    1.  通过SSH或控制台登录到ECS。具体操作请参考[连接ECS实例](../../../../../intl.zh-CN/个人版快速入门/步骤 3：连接ECS实例.md#)。
    2.  安装Python3、pip和aliyun-log-python-sdk。关于日志服务Python SDK的介绍，请参考[用户指南](https://aliyun-log-python-sdk.readthedocs.io/README.html)。

        ```
        apt-get update
        apt-get install -y python3-pip python3-dev
        cd /usr/local/bin
        ln -s /usr/bin/python3 python
        pip3 install --upgrade pip
        pip install aliyun-log-python-sdk
        ```

3.  配置Python Program。

    参照以下步骤配置Python Program，投递WAF日志到syslog服务器：

    1.  从[GitHub](https://github.com/aliyun/aliyun-log-python-sdk/blob/master/tests/consumer_group_examples/sync_data_to_syslog.py)下载最新的集成示例代码。

        ```
        wget https://raw.githubusercontent.com/aliyun/aliyun-log-python-sdk/master/tests/consumer_group_examples/sync_data_to_syslog.py
        ```

    2.  替换示例代码Python Program中与日志服务（SLS）、syslog相关的配置参数，具体包括：

        |参数|释义|描述|
        |--|--|--|
        |SLS Project|日志项目名称|日志项目是日志服务的资源管理单元，用来划分和操作资源。您可以在[阿里云日志服务控制台](https://sls.console.aliyun.com/#/)上查看项目名称。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038727_zh-CN.png)

|
        |SLS Endpoint|日志服务入口|日志服务入口是访问一个日志项目及其内部日志数据的URL。它和项目所在的阿里云地域及日志项目名称相关。您可以在[服务入口](../../../../../intl.zh-CN/API 参考/服务入口.md#)中查看服务入口URL。|
        |SLS Logstore|日志库|日志库是日志服务用来采集、存储和查询日志数据的单元。每个日志库归属在一个项目下，每个项目可以拥有多个日志库。您可以在[阿里云日志服务控制台](https://sls.console.aliyun.com/#/)，特定日志服务项目下查看日志库的名称。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038728_zh-CN.png)

|
        |SLS accessKeyId和accessKey|访问密钥|访问密钥是您在使用API（而非控制台）访问云资源时的“密码”。您需要使用AccessKey为API请求内容签名，使其能够通过日志服务的安全认证。具体请参考[访问密钥](../../../../../intl.zh-CN/API 参考/访问秘钥.md#)。您可以在[用户信息管理控制台](https://usercenter.console.aliyun.com/#/manage/ak)查看您的AccessKey信息。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038729_zh-CN.png)

|
        |Syslog Host|Syslog主机|Syslog服务器的IP地址或主机名称。|
        |Syslog Port|Syslog端口|接收syslog的端口。UDP协议使用514，TCP协议使用1468。|
        |Syslog protocol|Syslog协议|指定使用UDP或TCP协议来接收syslog，具体取决于syslog服务器的配置。|
        |Syslog separator|Syslog分隔符|指定用于分隔syslog键值对的分隔符。|

        以下是Python Program的配置示例。

        -   日志服务配置

            ```
            endpoint = os.environ.get('SLS_ENDPOINT', 'http://ap-southeast-1.log.aliyuncs.com')
            accessKeyId = os.environ.get('SLS_AK_ID', '替换成您自己的AccessKey ID')
            accessKey = os.environ.get('SLS_AK_KEY', '替换成您自己的AccessKey')
            project = os.environ.get('SLS_PROJECT', 'waf-project-5486134142760591-ap-southeast-1')
            logstore = os.environ.get('SLS_LOGSTORE', 'waf-logstore')
            consumer_group = os.environ.get('SLS_CG', 'WAF-SLS')
            ```

        -   Syslog配置

            ```
            settings = {
                            "host": "1.2.3.4",
                            "port": 514,       
                            "protocol": "udp", 
                            "sep": ",",       
                            "cert_path": None, 
                            "timeout": 120,    
                            "facility": syslogclient.FAC_USER,  
                            "severity": syslogclient.SEV_INFO,  
                            "hostname": None,  
                            "tag": None        
                        }
            ```

    3.  启用Python Program。假设Python program被保存为"sync\_data\_to\_syslog.py"，您可以使用以下命令启用它：

        ```
        python sync_data_to_syslog.py
        ```

        启用Python Program后，会显示成功投递日志到syslog服务器。

        ```
        *** start to consume data...
        consumer worker "WAF-SLS-1" start 
        heart beat start
        heart beat result: [] get: [0, 1]
        Get data from shard 0, log count: 6
        Complete send data to remote
        Get data from shard 0, log count: 2
        Complete send data to remote
        heart beat result: [0, 1] get: [0, 1]
        ```


完成以上操作后，您可以在syslog服务器中查询WAF日志。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010962038730_zh-CN.png)

