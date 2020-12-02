# WAF log charts and alert configuration examples

This topic provides 13 examples of alert configurations based on log query and analysis in WAF. You can use the SQL statement templates in this topic to configure charts on a WAF log dashboard. In addition, you can configure alerts based on the suggested alert parameters.

## Instructions

To configure alerts based on the examples, you must create a WAF log dashboard. For more information, see [Step 1: Create a WAF log analysis dashboard](/intl.en-US/Monitoring and Alarm/Best practices for configuring alerts in Log Service/Step 1: Create a WAF log analysis dashboard.md).

-   For more information about how to configure charts on a dashboard, see [Step 2: Configure log charts](/intl.en-US/Monitoring and Alarm/Best practices for configuring alerts in Log Service/Step 2: Configure log charts.md).
-   For more information about how to configure alerts on a dashboard, see [Step 3: Configure log alerts](/intl.en-US/Monitoring and Alarm/Best practices for configuring alerts in Log Service/Step 3: Configure log alerts.md).

This topic provides the following 13 alert configuration examples.

|No.|Alert|
|---|-----|
|1|[Abnormal percentage of 4xx status codes](#section_mr0_lkw_uux)|
|2|[Abnormal percentage of 5xx status codes](#section_k77_okl_z1l)|
|3|[Abnormal QPS](#section_jiq_k86_w13)|
|4|[Abrupt increase in QPS](#section_s3x_w1i_dxw)|
|5|[Abrupt decrease in QPS](#section_uxw_vu4_bvy)|
|6|[Requests blocked by HTTP ACL policies in the last five minutes](#section_zc8_xp7_i71)|
|7|[Requests blocked by WAF in the last five minutes](#section_mns_h8q_9zm)|
|8|[Requests blocked by HTTP flood protection in the last five minutes](#section_3yl_2ps_6x5)|
|9|[Requests blocked by scan protection in the last five minutes](#section_x5a_p9n_w8a)|
|10|[Attacks from a single IP address](#section_uym_g3q_gsb)|
|11|[Number of domain names attacked by a single IP address](#section_0pm_y2i_qw2)|
|12|[Average latency in the last five minutes](#section_6to_ax6_e3s)|
|13|[Abrupt decrease in QPS from a single user](#section_rao_757_nah)|

## Abnormal percentage of 4xx status codes

**Chart name**: percentage of 4xx status codes \(blocked requests excluded\)

SQL statement template

```
user_id:11111111110000 and not
real_client_ip:1.1.1.1|select user_id,host as "Domain name",Rate_2XX as
"2xx codes percentage ",Rate_3XX as "3xx codes percentage",Rate_4XX as "4xx codes percentage ",Rate_5XX
as "5xx codes percentage",countall as
"aveQPS",status_2XX,status_3XX,status_4XX,status_5XX,countall
from(select user_id,host,round(round(status_2XX*1.0000/countall,4)*100,2) as
Rate_2XX,round(round(status_3XX*1.0000/countall,4)*100,2) as Rate_3XX,
round(round

(status_4XX*1.0000/countall,4)*100,2) as
Rate_4XX,round(round(status_5XX*1.0000/countall,4)*100,2) as Rate_5XX,status_2XX,status_3XX,status_4XX,status_5XX,countall
from(select user_id, 

host,count_if(status>=200 and status<300) as
status_2XX,count_if(status>=300 and status<400) as
status_3XX,count_if(status>=400 and status<500 and status<>444 and
status<>405 ) as status_4XX,count_if(status>=500 and 

status<600) as
status_5XX,COUNT(*) as countall group by host,user_id)) where  countall>120 order by Rate_4XX DESC  limit 5
```

Suggested parameter settings for the alert:

The chart contains the following parameters: `aveQPS`, `2xx codes percentage`, `3xx codes percentage`, `4xx codes percentage`, and `5xx codes percentage`. aveQPS indicates the QPS of the domain name. To show status code changes caused by system workloads instead of external reasons, 444 and 405 codes triggered by HTTP flood attacks and web attacks blocked by WAF are not included as `4xx codes percentage`. You can select one or more of these parameters to configure alerts. For example, `aveQPS>10 && 2xx codes percentage<60` indicates that the QPS of the specified domain name is higher than 10 and the percentage of 2xx status codes is less than 60% during the specified period. The suggested parameters are as follows:

-   **Search Period**: 5 minutes
-   **Frequency**: 5 minutes
-   **Trigger Condition**: `$0.countall>3000&& $0.4xx codes percentage>80`
-   **Notification Trigger Threshold**: 2
-   **Notification Interval**: 10 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0]. Domain name}
    - Service: WAF
    - Total number of requests in the last five minutes:${Results[0].RawResults[0].countall}
    - 2xx codes percentage:${Results[0].RawResults[0].2xx codes percentage%
    - 3xx codes percentage:${Results[0].RawResults[0].3xx codes percentage} %
    - 4xx codes percentage:${Results[0].RawResults[0].4xx codes percentage} %
    - 5xx codes percentage:${Results[0].RawResults[0].5xx codes percentage} %
    ```


## Abnormal percentage of 5xx status codes

**Chart name**: percentage of 5xx status codes

SQL statement template

```
user_id:11111111110000 and not
real_client_ip:1.1.1.1|select user_id,host as "Domain name",Rate_2XX as
"2xx codes percentage",Rate_3XX as "3xx codes percentage",Rate_4XX as "4xx codes percentage",Rate_5XX
as "5xx codes percentage",countall as "Requests in the specified relative time period",status_2XX,status_3XX,status_4XX,status_5XX,countall
from(select user_id,host,round(round(status_2XX*1.0000/countall,4)*100,2) as
Rate_2XX,round(round(status_3XX*1.0000/countall,4)*100,2) as Rate_3XX,
round(round

(status_4XX*1.0000/countall,4)*100,2) as
Rate_4XX,round(round(status_5XX*1.0000/countall,4)*100,2) as
Rate_5XX,status_2XX,status_3XX,status_4XX,status_5XX,countall from(select
user_id, 

host,count_if(status>=200 and status<300) as
status_2XX,count_if(status>=300 and status<400) as
status_3XX,count_if(status>=400 and status<500) as
status_4XX,count_if(status>=500 and 

status<600) as
status_5XX,COUNT(*) as countall group by host,user_id)) where  countall>120 order by Rate_5XX DESC  limit 5
```

Suggested parameter settings for the alert:

-   **Search Period**: 5 minutes
-   **Frequency**: 5 minutes
-   **Trigger Condition**: `$0.countall>3000&& $0.5xx codes percentage>80`
-   **Notification Trigger Threshold**: 2
-   **Notification Interval**: 10 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0]. Domain name}
    - Service: WAF
    - Total number of requests in the last five minutes:${Results[0].RawResults[0].countall}
    - 2xx codes percentage:${Results[0].RawResults[0].2xx codes percentage%
    - 3xx codes percentage:${Results[0].RawResults[0].3xx codes percentage} %
    - 4xx codes percentage:${Results[0].RawResults[0].4xx codes percentage} %
    - 5xx codes percentage:${Results[0].RawResults[0].5xx codes percentage} %
    ```


## Abnormal QPS

**Chart name**: top 5 domain names with the highest query rates

SQL statement template

```
user_id: 11111111110000 and not
real_client_ip:1.1.1.1|select
user_id,host,Rate_2XX,Rate_3XX,Rate_4XX,Rate_5XX,countall/60 as
"aveQPS",status_2XX,status_3XX,status_4XX,status_5XX,countall
from(select user_id,host,round(round(status_2XX*1.0000/countall,4)*100,2) as Rate_2XX,round(round(status_3XX*1.0000/countall,4)*100,2)
as Rate_3XX, round(round

(status_4XX*1.0000/countall,4)*100,2) as
Rate_4XX,round(round(status_5XX*1.0000/countall,4)*100,2) as
Rate_5XX,status_2XX,status_3XX,status_4XX,status_5XX,countall from(select
user_id, 

host,count_if(status>=200 and status<300) as
status_2XX,count_if(status>=300 and status<400) as
status_3XX,count_if(status>=400 and status<500 and status<>444 and
status<>405 ) as status_4XX,count_if(status>=500 and 

status<600) as
status_5XX,COUNT(*) as countall group by host,user_id)) where  countall>120 order by aveQPS DESC  limit 5
```

Suggested parameter settings for the alert:

-   **Search Period**: 1 minute
-   **Frequency**: 1 minute
-   **Trigger Condition**: `$0.aveQPS>=50`
-   **Notification Trigger Threshold**: 1
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0].host}
    - Service: WAF
    - Average QPS in the past 1 minute:${Results[0].RawResults[0].aveQPS}
    - Status code 2xx percentage:${Results[0].RawResults[0].Rate_2XX}%
    - Status code 3xx percentage:${Results[0].RawResults[0].Rate_3XX}%
    - Status code 4xx percentage :${Results[0].RawResults[0].Rate_4XX}%
    - Status code 5xx percentage:${Results[0].RawResults[0].Rate_5XX}%
    ```


## Abrupt increase in QPS

**Chart name**: abrupt increase in QPS

SQL statement template

```
user_id: 11111111110000 |select
t1.user_id,t1.now1mQPS,t1.past1mQPS,in_ratio,t1.host,t2.Rate_2XX,Rate_3XX,Rate_4XX,Rate_5XX,aveQPS
from (

 (

 SELECT
user_id,round(c[1]/60,0) as now1mQPS,round(c[2]/60,0) as past1mQPS,
round(round(c[1]/60,0)/round(c[2]/60,0)*100-100,0) as in_ratio ,host from 

       (SELECT
compare(t, 60) as c,host, user_id from 

           (SELECT
COUNT(*) as t,host,user_id from log GROUP by host, user_id )  GROUP by host, user_id) where c[3] >1.1
and (c[1]>180 or c[2]>180

        )

  )t1 

           join 

  (select
user_id,host,Rate_2XX,Rate_3XX,Rate_4XX,Rate_5XX,countall/60 as
"aveQPS",status_2XX,status_3XX,status_4XX,status_5XX,countall from

 

     (select
user_id,host,round(round(status_2XX*1.0000/countall,4)*100,2) as
Rate_2XX,round(round(status_3XX*1.0000/countall,4)*100,2) as Rate_3XX,
round(round(status_4XX*1.0000/countall,4)*100,2) as
Rate_4XX,round(round(status_5XX*1.0000/countall,4)*100,2) as
Rate_5XX,status_2XX,status_3XX,status_4XX,status_5XX,countall from

        (select
user_id, host,count_if(status>=200 and status<300) as
status_2XX,count_if(status>=300 and status<400) as
status_3XX,count_if(status>=400 and status<500 and status<>444 and
status<>405 ) as status_4XX,count_if(status>=500 and status<600) as
status_5XX,COUNT(*) as countall from log group by host,user_id)

     ) where  countall>1

   )t2 

     on t1.host=t2.host) order by in_ratio DESC
limit 5
```

Suggested parameter configuration for the alert:

-   **Search Period**: 1 minute
-   **Frequency**: 1 minute
-   **Trigger Condition**: `$0.now1mqps>50&& $0.in_ratio>300`
-   **Notification Trigger Threshold**: 1
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0].host}
    - Service: WAF
    - Average QPS in the past 1 minute:${Results[0].RawResults[0].now1mqps}
    - Abrupt increase ratio of QPS:${Results[0].RawResults[0].in_ratio}%
    - Status code 2xx percentage:${Results[0].RawResults[0].rate_2xx}%
    - Status code 3xx percentage:${Results[0].RawResults[0].Rate_3XX}%
    - Status code 4xx percentage :${Results[0].RawResults[0].Rate_4XX}%
    - Status code 5xx percentage:${Results[0].RawResults[0].Rate_5XX}%
    ```


## Abrupt decrease in QPS

**Chart name**: abrupt decrease in QPS

SQL statement template

```
user_id: 11111111110000 |select
t1.user_id,t1.now1mQPS,t1.past1mQPS,de_ratio,t1.host,t2.Rate_2XX,Rate_3XX,Rate_4XX,Rate_5XX,aveQPS
from (

 (

 SELECT
user_id,round(c[1]/60,0) as now1mQPS,round(c[2]/60,0) as past1mQPS,
round(100-round(c[1]/60,0)/round(c[2]/60,0)*100,2) as de_ratio,host from 

(SELECT compare(t, 60) as c,host, user_id from 

    (SELECT
COUNT(*) as t,host,user_id from log GROUP by host, user_id )  GROUP by host, user_id ) where c[3] <0.9
and (c[1]>180 or c[2]>180

        )

  )t1 

           join 

  (select
user_id,host,Rate_2XX,Rate_3XX,Rate_4XX,Rate_5XX,countall/60 as
"aveQPS",status_2XX,status_3XX,status_4XX,status_5XX,countall from

     (select
user_id,host,round(round(status_2XX*1.0000/countall,4)*100,2) as
Rate_2XX,round(round(status_3XX*1.0000/countall,4)*100,2) as 

Rate_3XX,
round(round(status_4XX*1.0000/countall,4)*100,2) as
Rate_4XX,round(round(status_5XX*1.0000/countall,4)*100,2) as 

Rate_5XX,status_2XX,status_3XX,status_4XX,status_5XX,countall
from

        (select
user_id, host,count_if(status>=200 and status<300) as
status_2XX,count_if(status>=300 and status<400) as status_3XX,count_if

(status>=400 and status<500 and status<>444
and status<>405 ) as status_4XX,count_if(status>=500 and
status<600) as status_5XX,COUNT(*) as countall from log group by host,user_id)

     ) where  countall>1

)t2 on
t1.host=t2.host) order by de_ratio DESC limit 5
```

Suggested parameter settings for the alert:

The chart contains the following parameters: `now1mpqs`, `past1mqps`, `de_ratio` , and `host`. You can select these parameters to configure alerts. now1mpqs indicates the average QPS of the current minute. past1mqps indicates the average QPS of the last minute. de\_ratio indicates the decrease ratio of QPS.

-   **Search Period**: 1 minute
-   **Frequency**: 1 minute
-   **Trigger Condition**: `$0.now1mqps>10&& $0.de_ratio>50`
-   **Notification Trigger Threshold**: 2
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0].host}
    - Service: WAF (International)
    - Average QPS in the past 1 minute:${Results[0].RawResults[0].now1mqps}
    - Abrupt decrease ratio of QPS:${Results[0].RawResults[0].de_ratio}%
    - Status code 2xx percentage:${Results[0].RawResults[0].rate_2xx}%
    - Status code 3xx percentage:${Results[0].RawResults[0].Rate_3XX}%
    - Status code 4xx percentage :${Results[0].RawResults[0].Rate_4XX}%
    - Status code 5xx percentage:${Results[0].RawResults[0].Rate_5XX}%
    ```


## Requests blocked by HTTP ACL policies in the last five minutes

**Chart name**: requests blocked by HTTP ACL policies

SQL statement template

```
user_id:
11111111110000 |select user_id,host,count_if(block_action='antiscan') as "Requests blocked by scan protection",count_if(block_action='acl')
as "Requests blocked by HTTP ACL policies ",count_if(aliwaf_action='block')
as "Requests blocked by WAF",count_if(cc_action='close') as
"Requests blocked by HTTP flood protection",count_if(block_action='acl' or
aliwaf_action='block' or cc_action='close' or block_action='antiscan') as
totalblock  group by host,user_id having
("Requests blocked by HTTP ACL policies" >=0 and "Requests blocked by WAF" >=0 and "Requests blocked by HTTP flood protection">=0
and totalblock>10) order by "Requests blocked by HTTP ACL policies"  DESC limit 5
```

Suggested parameter settings for the alert:

-   **Search Period**: 5 minutes
-   **Frequency**: 5 minutes
-   **Trigger Condition**:`$0.totalblock>=500&&($0.Requests blocked by HTTP ACL policies>=500)`
-   **Notification Trigger Threshold**: 1
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0].host}
    - Service: WAF
    - Total requests blocked in the last 5 minutes:${Results[0].RawResults[0].totalblock}
    - Requests blocked by HTTP ACL policies:${Results[0].RawResults[0].Requests blocked by HTTP ACL policies}
    - Requests blocked by WAF:${Results[0].RawResults[0].Requests blocked by WAF}
    - Requests blocked by HTTP flood protection:${Results[0].RawResults[0].Requests blocked by HTTP flood protection}
    - Requests blocked by scan protection:${Results[0].RawResults[0]. Requests blocked by scan protection}
    ```


## Requests blocked by WAF in the last five minutes

**Chart name**: requests blocked by WAF

SQL statement template

```
user_id:11111111110000
|select user_id,host,count_if(block_action='antiscan') as "Requests blocked by scan protection",count_if(block_action='acl')
as "Requests blocked by HTTP ACL policies",count_if(aliwaf_action='block')
as "Requests blocked by WAF",count_if(cc_action='close') as
"Requests blocked by HTTP flood protection",count_if(block_action='acl' or
aliwaf_action='block' or cc_action='close' or block_action='antiscan') as
totalblock  group by host,user_id having
("Requests blocked by HTTP ACL policies" >=0 and "Requests blocked by WAF" >=0 and "Requests blocked by HTTP flood protection">=0
and totalblock>10) order by "Requests blocked by WAF"  DESC limit 5
```

Suggested parameter settings for the alert:

-   **Search Period**: 5 minutes
-   **Frequency**: 5 minutes
-   **Trigger Condition**: `$0.totalblock>=500&&($0.Requests blocked by WAF>=500)`
-   **Notification Trigger Threshold**: 1
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0].host}
    - Service: WAF
    - Total requests blocked in the last 5 minutes:${Results[0].RawResults[0].totalblock}
    - Requests blocked by HTTP ACL policies:${Results[0].RawResults[0].Requests blocked by HTTP ACL policies}
    - Requests blocked by WAF:${Results[0].RawResults[0].Requests blocked by WAF}
    - Requests blocked by HTTP flood protection:${Results[0].RawResults[0].Requests blocked by HTTP flood protection}
    - Requests blocked by scan protection:${Results[0].RawResults[0]. Requests blocked by scan protection}
    ```


## Requests blocked by HTTP flood protection in the last five minutes

**Chart name**: requests blocked by HTTP flood protection

SQL statement template

```
user_id:
11111111110000 |select user_id,host,count_if(block_action='antiscan') as "Requests blocked by scan protection",count_if(block_action='acl')
as "Requests blocked by HTTP ACL policies",count_if(aliwaf_action='block')
as "Requests blocked by WAF",count_if(cc_action='close') as
"Requests blocked by HTTP flood protection",count_if(block_action='acl' or
aliwaf_action='block' or cc_action='close' or block_action='antiscan') as
totalblock  group by host,user_id having
("Requests blocked by HTTP ACL policies" >=0 and "Requests blocked by WAF" >=0 and "Requests blocked by HTTP flood protection">=0
and totalblock>10) order by "Requests blocked by HTTP flood protection"  DESC limit 5
```

Suggested parameter settings for the alert:

-   **Search Period**: 5 minutes
-   **Frequency**: 5 minutes
-   **Trigger Condition**: `$0.totalblock>=500&&($0.Requests blocked by HTTP flood protection>=500)`
-   **Notification Trigger Threshold**: 1
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0].host}
    - Service: WAF
    - Total requests blocked in the last 5 minutes:${Results[0].RawResults[0].totalblock}
    - Requests blocked by HTTP ACL policies:${Results[0].RawResults[0].Requests blocked by HTTP ACL policies}
    - Requests blocked by WAF:${Results[0].RawResults[0].Requests blocked by WAF}
    - Requests blocked by HTTP flood protection:${Results[0].RawResults[0].Requests blocked by HTTP flood protection}
    - Requests blocked by scan protection:${Results[0].RawResults[0]. Requests blocked by scan protection}
    ```


## Requests blocked by scan protection in the last five minutes

**Chart name**: requests blocked by scan protection

SQL statement template

```
user_id:
11111111110000 |select user_id,host,count_if(block_action='antiscan') as "Requests blocked by scan protection",count_if(block_action='acl')
as "Requests blocked by HTTP ACL policies",count_if(aliwaf_action='block')
as "Requests blocked by WAF",count_if(cc_action='close') as
"Requests blocked by HTTP flood protection",count_if(block_action='acl' or
aliwaf_action='block' or cc_action='close' or block_action='antiscan') as
totalblock  group by host,user_id having
("Requests blocked by HTTP ACL policies" >=0 and "Requests blocked by WAF" >=0 and "Requests blocked by HTTP flood protection">=0
and totalblock>10) order by "Requests blocked by scan protection"  DESC limit 5
```

Suggested parameter settings for the alert:

-   **Search Period**: 5 minutes
-   **Frequency**: 5 minutes
-   **Trigger Condition**: `$0.totalblock>=500&&($0. Requests blocked by scan protection>=500)`
-   **Notification Trigger Threshold**: 1
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0].host}
    - Service: WAF (International)
    - Total requests blocked in the last 5 minutes:${Results[0].RawResults[0].totalblock}
    - Requests blocked by HTTP ACL policies:${Results[0].RawResults[0].Requests blocked by HTTP ACL policies}
    - Requests blocked by WAF:${Results[0].RawResults[0].Requests blocked by WAF}
    - Requests blocked by HTTP flood protection:${Results[0].RawResults[0].Requests blocked by HTTP flood protection}
    - Requests blocked by scan protection:${Results[0].RawResults[0]. Requests blocked by scan protection}
    ```


## Attacks from a single IP address

**Chart name**: attacks from a single IP address

SQL statement template

```
user_id:
11111111110000 |select user_id,real_client_ip,concat('Requests blocked by HTTP ACL policies:',cast(aclblock as
varchar(10)),'  ','Requests blocked by WAF:',cast(wafblock as varchar(10)),' 
','Requests blocked by HTTP flood protection:',cast(aclblock as varchar(10))) as
blockNum,totalblock,allRequest from (select user_id,real_client_ip,count_if(block_action='acl')
as aclblock,count_if(aliwaf_action='block') as
wafblock,count_if(cc_action='close') as ccblock,count_if(block_action='acl' or
aliwaf_action='block' or cc_action='close') as totalblock,COUNT(*) as
allRequest from log group by user_id,real_client_ip having totalblock>1
order by totalblock DESC  limit 5)
```

Suggested parameter settings for the alert:

The chart contains the following parameters: `real_client_ip`, `blockNum`, `totalblock`, and `allRequest`. You can select the parameters to configure alerts. blockNum includes `Requests blocked by HTTP ACL policies`, `Requests blocked by WAF`, and `Requests blocked by HTTP flood protection`. totalblock indicates the total number of blocked requests. allRequest indicates the total number of requests.

-   **Search Period**: 5 minutes
-   **Frequency**: 5 minutes
-   **Trigger Condition**: `$0.totalblock >=500`
-   **Notification Trigger Threshold**: 1
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Service: WAF
    - Top 3 attack source IP addresses in the last 5 minutes:
    - ${Results[0].RawResults[0].real_client_ip}  (${Results[0].RawResults[0].blockNum})
    - ${Results[0].RawResults[1].real_client_ip}  (${Results[0].RawResults[1].blockNum})
    -${Results[0].RawResults[2].real_client_ip}  (${Results[0].RawResults[2].blockNum})
    ```


## Number of domain names attacked by a single IP address

**Chart name**: number of domain names attacked by a single IP address

SQL statement template

```
user_id:
11111111110000  and not
upstream_status:504 and not upstream_addr:- and request_time_msec < 5000 and
upstream_status:200 and not ua_browser:bot |SELECT user_id,host,upstream_time,request_time,ssl_handshake,requestnum
from (select user_id,host,round(avg(upstream_response_time),2)*1000 as
upstream_time,round(avg(request_time_msec),2) as
request_time,round(avg(ssl_handshake_time)*1000,2) as ssl_handshake,COUNT(*) as
requestnum from log group by host,user_id) where requestnum>30 order by
request_time DESC limit 5
```

Suggested parameter settings for the alert:

The chart contains the following parameters: `real_client_ip` \(attacker IP address\), `totalblock` \(total number of blocked requests\), and `domainnum` \(number of domains attacked by this IP address\). You can select one or more of these parameters to configure alerts. For example, `totalblock>500&& domainnum>5` indicates that the total number of attacks launched by an IP address reaches 500 and the number of attacked domain names exceeds 5.

-   **Search Period**: 5 minutes
-   **Frequency**: 1 minute
-   **Trigger Condition**: `$0.domainnum>=10`
-   **Notification Trigger Threshold**: 1
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Service: WAF
    - Attacker IP:${Results[0].RawResults[0].real_client_ip}
    - Number of attacked domain names:${Results[0].RawResults[0].domainnum}
    - Total requests blocked in the last 5 minutes:${Results[0].RawResults[0].totalblock}
    - Please handle the alert in a timely manner.
    ```


## Average latency in the last five minutes

**Chart name**: average latency in the last five minutes

SQL statement template

```
user_id:
11111111110000 and and not upstream_status:504 and not upstream_addr:- and
request_time_msec < 5000 and upstream_status:200 and not ua_browser:bot|SELECT
user_id,host,upstream_time,request_time,ssl_handshake,requestnum from (select user_id,host,round(avg(upstream_response_time),2)*1000
as upstream_time,round(avg(request_time_msec),2) as
request_time,round(avg(ssl_handshake_time)*1000,2) as ssl_handshake,COUNT(*) as
requestnum from log group by host,user_id) where requestnum>30 order by
request_time DESC limit 5
```

Suggested parameter settings for the alert:

-   **Search Period**: 5 minutes
-   **Frequency**: 5 minutes
-   **Trigger Condition**: `$0.request_time>1000&& $0.requestnum>30`
-   **Notification Trigger Threshold**: 2
-   **Notification Interval**: 10 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [Uid]:${Results[0].RawResults[0].user_id}
    - Domain name:${Results[0].RawResults[0].host}
    - Service: WAF (International)
    - [Trigger condition]:${condition}
    - Top 3 domain names with the longest latency in the last 5 minutes (unit: millisecond)
    - Host1:${Results[0].RawResults[0].host} Delay_time:${Results[0].RawResults[0].upstream_time} 
    - Host2:${Results[0].RawResults[1].host} Delay_time:${Results[0].RawResults[1].upstream_time} 
    - Host3:${Results[0].RawResults[2].host} Delay_time:${Results[0].RawResults[2].upstream_time}
    ```


## Abrupt decrease in QPS from a single user

**Chart name**: abrupt decrease in QPS from a single user

SQL statement template

```
user_id: 11111111110000 |select
t1.user_id,t1.now1mQPS,t1.past1mQPS,de_ratio,t2.Rate_2XX,Rate_3XX,Rate_4XX,Rate_5XX,aveQPS
from (

 (

 SELECT
user_id,round(c[1]/60,0) as now1mQPS,round(c[2]/60,0) as past1mQPS,
round(100-round(c[1]/60,0)/round(c[2]/60,0)*100,2) as de_ratio from 

(SELECT compare(t, 60) as c, user_id from 

    (SELECT
COUNT(*) as t,user_id from log GROUP by user_id )  GROUP by user_id ) where c[3] <0.9 and
(c[1]>180 or c[2]>180

        )

  )t1 

           join 

  (select
user_id,Rate_2XX,Rate_3XX,Rate_4XX,Rate_5XX,countall/60 as
"aveQPS",status_2XX,status_3XX,status_4XX,status_5XX,countall from

 

     (select
user_id,round(round(status_2XX*1.0000/countall,4)*100,2) as
Rate_2XX,round(round(status_3XX*1.0000/countall,4)*100,2) as 

 

Rate_3XX,
round(round(status_4XX*1.0000/countall,4)*100,2) as
Rate_4XX,round(round(status_5XX*1.0000/countall,4)*100,2) as 

 

Rate_5XX,status_2XX,status_3XX,status_4XX,status_5XX,countall
from

        (select
user_id,count_if(status>=200 and status<300) as
status_2XX,count_if(status>=300 and status<400) as status_3XX,count_if

 

(status>=400 and status<500 and status<>444
and status<>405 ) as status_4XX,count_if(status>=500 and
status<600) as status_5XX,COUNT(*) as countall from log group by user_id)

     ) where  countall>0

)t2 on
t1.user_id=t2.user_id) order by de_ratio DESC limit 5
```

Suggested parameter settings for the alert:

-   **Search Period**: 1 minute
-   **Frequency**: 1 minute
-   **Trigger Condition**: `$0.de_ratio>50&& $0.now1mqps>20`
-   **Notification Trigger Threshold**: 1
-   **Notification Interval**: 5 minutes
-   **Content**

    ```
    - [Time]:${FireTime}
    - [UID]:${Results[0].RawResults[0].user_id}
    - Service: WAF
    - Average QPS in the past 1 minute:${Results[0].RawResults[0].now1mqps}
    - [Trigger condition (abrupt decrease ratio of QPS & QPS)]:${condition}
    - Abrupt decrease ratio of QPS:${Results[0].RawResults[0].de_ratio}%
    - Status code 2xx percentage:${Results[0].RawResults[0].rate_2xx}%
    - Status code 3xx percentage:${Results[0].RawResults[0].Rate_3XX}%
    - Status code 4xx percentage :${Results[0].RawResults[0].Rate_4XX}%
    - Status code 5xx percentage:${Results[0].RawResults[0].Rate_5XX}%
    ```


