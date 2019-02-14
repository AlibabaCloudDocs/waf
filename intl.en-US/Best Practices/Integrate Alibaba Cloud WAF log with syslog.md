# Integrate Alibaba Cloud WAF log with syslog {#concept_fqm_n13_tgb .concept}

This topic describes how to integrate Alibaba Cloud WAF log with syslog to guarantee all compliance, auditing, and other related logs can be ingested into your Security Operation Center.

## Overview {#section_wt1_rd3_tgb .section}

The following figure illustrates the syslog integration architecture:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981638718_en-US.png)

**Alibaba Cloud Log Service** is a one-stop service for log data. Log Service experiences massive big data scenarios of Alibaba Group. Log Service \(LOG or SLS\) allows you to quickly complete the collection, consumption, shipping, query, and analysis of log data without the need for development, which improves the Operation & Maintenance \(O&M\) efficiency and the operational efficiency, and builds the processing capabilities to handle massive logs in the DT \(data technology\) era. For more information, see [Log Service Production Introduction](../../../../../reseller.en-US/Product Introduction/What is Log Service.md#).

**Python Program** is a program running on ECS to deliver WAF log to a syslog server. The consumer library is an advanced mode of log consumption in Log Service, and provides the consumer group concept to abstract and manage the consumption end. Compared with using SDKs directly to read data, you can only focus on the business logic by using the consumer library, without caring about the implementation details of Log Service, or the load balancing or failover between consumers. For more information, see [Consumer group introduction](../../../../../reseller.en-US/User Guide/Real-time subscription and consumption/Consumption by consumer groups/Consumer group - Usage.md#).

**Syslog Server** is a centralize log message management server to receive multiple syslog sources.

## Prerequisites {#section_q22_n23_tgb .section}

Before you begin, make sure of the following:

-   You have purchased Alibaba Cloud WAF business edition or above to protect your website. For more information, see [Purchase Alibaba Cloud WAF](../../../../../reseller.en-US/Pricing/Subscription/Purchase Web Application Firewall.md#) and [Implement Alibaba Cloud WAF](../../../../../reseller.en-US/User Guide/Access WAF/WAF deployment guide.md#).
-   You have a Linux ECS server with the following recommended hardware spec:
    -   Operating System with Ubuntu
    -   8 vCPUs with 2.0+ GHz
    -   32GB Memory
    -   at least 2GB available disk space \(10GB or more is suggested\)
-   You have a syslog server with UDP port 514 enabled to receive syslog.

## Procedure {#section_gyj_t23_tgb .section}

1.  Enable Alibaba Cloud WAF logging.

    Follow these steps to enable Alibaba Cloud WAF logging in the WAF console:

    1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
    2.  In the left-side navigation pane, select**App Market** \> **App Management**.
    3.  Under **Real-time Log Query and Analysis Service**, click **Upgrade**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981638719_en-US.png)

    4.  On the Update page, enable **Access Log Service** and select **Log Storage Period** and **Log storage Size** accordingly.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981738720_en-US.png)

    5.  After activating Log service, click **Authorization** under **Real-time Log Query and Analysis Service**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981738721_en-US.png)

    6.  On the Cloud Resource Access Authorization page, click **Confirm Authorization Policy**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981738723_en-US.png)

    7.  Under **Real-time Log Query and Analysis Service**, click **Configure**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981738724_en-US.png)

    8.  In the domain name drop-down box, enable the website you want to enable Log service.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981738725_en-US.png)

2.  Set up the Python environment in ECS.

    Follow these steps to install the Log Service Python SDK in ECS:

    1.  Log on to the ECS instance through SSH or the console. For more information, see [Connect to an ECS instance](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 3: Connect to an instance.md#).
    2.  Install Python3, pip and Python SDK of Log Service. For more information on Log Service Python SDK, see [User Guide](https://aliyun-log-python-sdk.readthedocs.io/README.html).

        ```
        apt-get update
        apt-get install -y python3-pip python3-dev
        cd /usr/local/bin
        ln -s /usr/bin/python3 python
        pip3 install --upgrade pip
        pip install aliyun-log-python-sdk
        ```

3.  Configure Python program to send logs to the syslog server.

    Follow these steps to configure Python Program to ship WAF logs to the syslog server:

    1.  Download the latest example of integration code from [GitHub](https://github.com/aliyun/aliyun-log-python-sdk/blob/master/tests/consumer_group_examples/sync_data_to_syslog.py):

        ```
        wget https://raw.githubusercontent.com/aliyun/aliyun-log-python-sdk/master/tests/consumer_group_examples/sync_data_to_syslog.py
        ```

    2.  Replace Log Service and syslog related settings in Python Program, including:

        |Parameter|Meaning|Description|
        |---------|-------|-----------|
        |SLS Project|Log Service project name|Project is Log Service's resource management unit, used to isolate and control resources. You can find the Project Name in the [Alibaba Cloud Log Service console](https://partners-intl.console.aliyun.com/#/sls).![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981738727_en-US.png)

|
        |SLS Endpoint|Log Service Endpoint|Log Service Endpoint is a URL used to access a project and logs within the project, and is associated with the Alibaba Cloud region where the project resides and the project name. You can find the Endpoint URL in [Service endpoint](../../../../../reseller.en-US/API Reference/Service endpoint.md#).|
        |SLS Logstore|Logstore|Logstore is a unit in Log Service for the collection, storage, and query of log data. Each Logstore belongs to a project, and each project can create multiple Logstores. You can find the Logstore Name under your Log Service Project in the [Alibaba Cloud Log Service console](https://partners-intl.console.aliyun.com/#/sls):![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981738728_en-US.png)

|
        |SLS accessKeyId and accessKey|AccessKey|AccessKey is a "secure password" designed for you to access your cloud resources by using APIs \(not the console\). You can use the AccessKey to sign API request content to pass the security authentication in Log Service. For more information, see [AccessKey Introduction](../../../../../reseller.en-US/API Reference/AccessKey.md#). You can find your Accesskey in the User Management console:![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981738729_en-US.png)

|
        |Syslog Host|Syslog Host|Syslog host is same as the IP address/Hostname you access syslog server.|
        |Syslog Port|Syslog Port|Syslog port is a port to receive syslog. UDP uses port 514 and TCP uses port 1468.|
        |Syslog protocol|Syslog protocol|You can specify UDP or TCP to receive syslog, depending on your syslog server setting.|
        |Syslog separator|Syslog separator|Syslog separator is used to separate syslog key-value pairs.|

        The following is the sample setting in Python Program:

        -   Log Services

            ```
            endpoint = os.environ.get('SLS_ENDPOINT', 'http://ap-southeast-1.log.aliyuncs.com')
            accessKeyId = os.environ.get('SLS_AK_ID', 'replace to your accessid')
            accessKey = os.environ.get('SLS_AK_KEY', 'replace to your accesskey')
            project = os.environ.get('SLS_PROJECT', 'waf-project-5486134142760591-ap-southeast-1')
            logstore = os.environ.get('SLS_LOGSTORE', 'waf-logstore')
            consumer_group = os.environ.get('SLS_CG', 'WAF-SLS')
            ```

        -   Syslog

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

    3.  Run Python Program. Suppose the Python program is saved as "sync\_data\_to\_syslog.py". You can launch it as:

        ```
        python sync_data_to_syslog.py
        ```

        The Python program log shows successfully sent log to remote syslog server.

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


You are able to search the WAF log in syslog server now.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123589/155010981738730_en-US.png)

