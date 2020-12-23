# Common SQL statements

This topic describes the SQL statements that are supported by Log Service for WAF. You can execute these statements to query and analyze specific metrics.

Log Service for WAF provides the following metrics:

**Note:** You can click a metric to view the SQL statements that are supported by the metric. For more information about the metrics, see [Common monitoring metrics](/intl.en-US/Monitoring and Alarm/Best practices for configuring alerts in Log Service/Common monitoring metrics.md).

-   [request\_time\_msec](#section_m5d_he9_cgo)
-   [upstream\_response\_time](#section_2vh_it1_ize)
-   [ssl\_handshake\_time](#section_mbp_z1y_72m)
-   [status:200](#section_dt8_01e_w6c)
-   [status:302 or 200 and block\_action:tmd](#section_any_url_ysu)
-   [status:200 and block\_action:‘antifraud’](#section_r5z_3to_dic)
-   [status:404](#section_gjp_u80_2vw)
-   [status:405 and aliwaf\_action='block'](#section_w14_4jd_b3s)
-   [status:405 and aliwaf\_action='acl'](#section_yrj_fwq_jgo)
-   [status:444](#section_2am_6el_u3b)
-   [status:499](#section_do4_wvf_7ar)
-   [status:500](#section_j5p_1zl_ei9)
-   [status:502](#section_dlx_z8u_idq)
-   [status:503](#section_svs_n1x_7hw)
-   [status:504](#section_j6k_1mv_dnp)

## request\_time\_msec

The period between the time when the client sends a request and the time when the client receives the response.

```
* |SELECT user_id,host,round(round(request_time_cnt*1.0000/countall,4)*100,2)
as percent FROM  (select user_id,host,count_if(request_time_msec>500)
AS request_time_cnt ,COUNT(*)  as countall from log group by user_id,host)
group by user_id,host,percent
```

## upstream\_response\_time

The period between the time when WAF forwards a request to the origin server and the time when WAF receives the response from the origin server.

```
* |SELECT
user_id,host,round(round(upstream_response_time_cnt*1.0000/countall,4)*100,2)
as percent FROM  (select
user_id,host,count_if(upstream_response_time>500) AS
upstream_response_time_cnt ,COUNT(*)  as countall from log group by
user_id,host) group by user_id,host,percent
```

## ssl\_handshake\_time

The time required for an SSL handshake between the client and WAF if requests are sent over HTTPS.

```
* |SELECT
user_id,host,round(round(ssl_handshake_time_cnt*1.0000/countall,4)*100,2) as
percent FROM  (select user_id,host,count_if(ssl_handshake_time>10) AS
ssl_handshake_time_cnt ,COUNT(*)  as countall from log group by
user_id,host) group by user_id,host,percent
```

## status:200

The server has processed the request and returned the requested data.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as Rate_502,round(round(status_503*1.0000/countall,4)*100,2)
as Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as
status_200,count_if(status=302) as status_302,count_if(status=404) as
status_404,count_if(status=405) as status_405,count_if(status=444) as
status_444,count_if(status=499) as status_499,count_if(status=500) as status_500,count_if(status=502)
as status_502,count_if(status=503) as status_503,count_if(status=504) as
status_504,COUNT(*)  as countall from log group by user_id,host))
where  countall>120 order by Rate_200 DESC  limit 5
```

## status:302 or 200 and block\_action:tmd

The status code indicates whether CAPTCHA is triggered. Status code 302 indicates that CAPTCHA is triggered. Status code 200 indicates that CAPTCHA is not triggered and HTTP flood protection rules that you customize are triggered.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as Rate_444,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as
Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as Rate_503,round(round(status_504*1.0000/countall,4)*100,2)
as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200 and 

block_action:tmd

) as status_200,count_if(status=302 and 

block_action:tmd

) as
status_302,count_if(status=404) as status_404,count_if(status=405) as
status_405,count_if(status=444) as status_444,count_if(status=499) as
status_499,count_if(status=500) as status_500,count_if(status=502) as
status_502,count_if(status=503) as status_503,count_if(status=504) as
status_504,COUNT(*)  as countall from log group by user_id,host))
where  countall>120 order by Rate_200 DESC  limit 5
```

## status:200 and block\_action:‘antifraud’

A request is blocked based on data risk control rules.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302, round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as
Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as
Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200 and block_action:‘antifraud’) as
status_200,count_if(status=302) as status_302,count_if(status=404) as
status_404,count_if(status=405) as status_405,count_if(status=444) as
status_444,count_if(status=499) as status_499,count_if(status=500) as
status_500,count_if(status=502) as status_502,count_if(status=503) as
status_503,count_if(status=504) as status_504,COUNT(*)  as countall from
log group by user_id,host)) where  countall>120 order by Rate_200
DESC  limit 5
```

## status:404

The server cannot find the requested resources.

```
*|select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_500 as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503
as "Percentage of status code 503",Rate_504 as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_405,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as
Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as
Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as
Rate_504,status_200,status_302,status_404,status_405,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as
status_200,count_if(status=302) as status_302,count_if(status=404) as
status_404,count_if(status=405) as status_405,count_if(status=499) as
status_499,count_if(status=500) as status_500,count_if(status=502) as
status_502,count_if(status=503) as status_503,count_if(status=504) as
status_504,COUNT(*)  as countall from log group by user_id,host))
where  countall>120 order by Rate_404 DESC  limit 5
```

## status:405 and aliwaf\_action='block'

A request is blocked based on WAF protection rules.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as "aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as
Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as
Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as
status_200,count_if(status=302) as status_302,count_if(status=404) as
status_404,count_if(status=405 and aliwaf_action='block' ) as
status_405,count_if(status=444) as status_444,count_if(status=499) as
status_499,count_if(status=500) as status_500,count_if(status=502) as
status_502,count_if(status=503) as status_503,count_if(status=504) as status_504,COUNT(*) 
as countall from log group by user_id,host)) where  countall>120 order
by Rate_405 DESC  limit 5
```

## status:405 and aliwaf\_action='acl'

A request is blocked based on custom protection policies.

```
user_id: 1111111111111 |select user_id,host as "Domain",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as Rate_500,round(round(status_502*1.0000/countall,4)*100,2)
as Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as
Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as
status_200,count_if(status=302) as status_302,count_if(status=404) as
status_404,count_if(status=405 and aliwaf_action='acl') as
status_405,count_if(status=444) as status_444,count_if(status=499) as
status_499,count_if(status=500) as status_500,count_if(status=502) as
status_502,count_if(status=503) as status_503,count_if(status=504) as
status_504,COUNT(*)  as countall from log group by user_id,host)) where 
countall>120 order by Rate_405 DESC  limit 5
```

## status:444

A request is blocked based on custom HTTP flood protection rules.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as
Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as Rate_503,round(round(status_504*1.0000/countall,4)*100,2)
as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as status_200,count_if(status=302)
as status_302,count_if(status=404) as status_404,count_if(status=405) as
status_405,count_if(status=444) as status_444,count_if(status=499) as
status_499,count_if(status=500) as status_500,count_if(status=502) as
status_502,count_if(status=503) as status_503,count_if(status=504) as
status_504,COUNT(*)  as countall from log group by user_id,host))
where  countall>120 order by Rate_444 DESC  limit 5
```

## status:499

After a client sends a request, the server does not return data. After the connection times out, the client closes the connection, and the server returns this status code.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as
Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as
Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as
status_200,count_if(status=302) as status_302,count_if(status=404) as
status_404,count_if(status=405) as status_405,count_if(status=444) as
status_444,count_if(status=499) as status_499,count_if(status=500) as
status_500,count_if(status=502) as status_502,count_if(status=503) as
status_503,count_if(status=504) as status_504,COUNT(*)  as countall from
log group by user_id,host)) where  countall>120 order by Rate_499
DESC  limit 5
```

## status:500

An internal error occurs, and the request cannot be processed.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as
Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as
Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as
status_200,count_if(status=302) as status_302,count_if(status=404) as
status_404,count_if(status=405) as status_405,count_if(status=444) as
status_444,count_if(status=499) as status_499,count_if(status=500) as
status_500,count_if(status=502) as status_502,count_if(status=503) as
status_503,count_if(status=504) as status_504,COUNT(*)  as countall from
log group by user_id,host)) where  countall>120 order by Rate_500
DESC  limit 5
```

## status:502

The WAF instance is used as a gateway or a proxy and receives invalid responses from the origin server. The origin server does not respond due to the low quality of the back-to-origin network or the fact that back-to-origin requests are blocked based on access control policies that are configured for the origin server.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as Rate_502,round(round(status_503*1.0000/countall,4)*100,2)
as Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as
status_200,count_if(status=302) as status_302,count_if(status=404) as
status_404,count_if(status=405) as status_405,count_if(status=444) as
status_444,count_if(status=499) as status_499,count_if(status=500) as status_500,count_if(status=502)
as status_502,count_if(status=503) as status_503,count_if(status=504) as
status_504,COUNT(*)  as countall from log group by user_id,host))
where  countall>120 order by Rate_502 DESC  limit 5
```

## status:503

The service is unavailable due to overload or maintenance needs.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as
Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as
Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as
status_200,count_if(status=302) as status_302,count_if(status=404) as status_404,count_if(status=405)
as status_405,count_if(status=444) as status_444,count_if(status=499) as
status_499,count_if(status=500) as status_500,count_if(status=502) as
status_502,count_if(status=503) as status_503,count_if(status=504) as status_504,COUNT(*) 
as countall from log group by user_id,host)) where  countall>120 order
by Rate_503 DESC  limit 5
```

## status:504

The WAF instance is used as a gateway or proxy, but cannot receive requests from the origin server in time. The 504 Gateway Timeout error occurred.

```
* |select user_id,host as "Domain name",Rate_200 as
"Percentage of status code 200",Rate_302 as "Percentage of status code 302",Rate_404 as "Percentage of status code 404",Rate_405
as "Percentage of status code 405",Rate_444 as "Percentage of status code 444",Rate_499 as "Percentage of status code 499",Rate_500
as "Percentage of status code 500",Rate_502 as "Percentage of status code 502",Rate_503 as "Percentage of status code 503",Rate_504
as "Percentage of status code 504",countall/60 as
"aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from(SELECT user_id,host,round(round(status_200*1.0000/countall,4)*100,2) as
Rate_200,round(round(status_302*1.0000/countall,4)*100,2) as Rate_302,
round(round

(status_404*1.0000/countall,4)*100,2) as
Rate_404,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_405,round(round

(status_405*1.0000/countall,4)*100,2) as
Rate_444,round(round

(status_405*1.0000/countall,4)*100,2)
as Rate_499,round(round(status_500*1.0000/countall,4)*100,2) as
Rate_500,round(round(status_502*1.0000/countall,4)*100,2) as
Rate_502,round(round(status_503*1.0000/countall,4)*100,2) as
Rate_503,round(round(status_504*1.0000/countall,4)*100,2) as
Rate_504,status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
from (select user_id,host,count_if(status=200) as
status_200,count_if(status=302) as status_302,count_if(status=404) as
status_404,count_if(status=405) as status_405,count_if(status=444) as
status_444,count_if(status=499) as status_499,count_if(status=500) as
status_500,count_if(status=502) as status_502,count_if(status=503) as
status_503,count_if(status=504) as status_504,COUNT(*)  as countall from
log group by user_id,host)) where  countall>120 order by Rate_504 DESC 
limit 5
```

