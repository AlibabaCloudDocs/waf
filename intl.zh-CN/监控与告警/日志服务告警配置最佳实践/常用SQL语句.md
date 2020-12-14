# 常用SQL语句

本文介绍了使用Web应用防火墙日志服务查询和分析具体监控指标时用到的SQL查询语句。

使用Web应用防火墙日志服务发起查询和分析时常用的监控指标包括：

**说明：** 您可以单击关注的指标，查看对应的SQL语句。关于监控指标的更多信息，请参见[常用监控指标](/intl.zh-CN/监控与告警/日志服务告警配置最佳实践/常用监控指标.md)。

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

指标释义：客户端请求到返回结果的请求耗时。

```
* |SELECT user_id,host,round(round(request_time_cnt*1.0000/countall,4)*100,2)
as percent FROM  (select user_id,host,count_if(request_time_msec>500)
AS request_time_cnt ,COUNT(*)  as countall from log group by user_id,host)
group by user_id,host,percent
```

## upstream\_response\_time

指标释义：请求回源时，源站返回数据的响应时间。

```
* |SELECT
user_id,host,round(round(upstream_response_time_cnt*1.0000/countall,4)*100,2)
as percent FROM  (select
user_id,host,count_if(upstream_response_time>500) AS
upstream_response_time_cnt ,COUNT(*)  as countall from log group by
user_id,host) group by user_id,host,percent
```

## ssl\_handshake\_time

指标释义：HTTPS协议请求时，客户端与WAF的SSL握手时间。

```
* |SELECT
user_id,host,round(round(ssl_handshake_time_cnt*1.0000/countall,4)*100,2) as
percent FROM  (select user_id,host,count_if(ssl_handshake_time>10) AS
ssl_handshake_time_cnt ,COUNT(*)  as countall from log group by
user_id,host) group by user_id,host,percent
```

## status:200

指标释义：服务器已成功处理请求，返回了请求的数据。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

指标释义：人机校验JS请求状态码（302表示默认策略，200表示手动策略）。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

指标释义：请求被数据风控规则拦截。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

指标释义：服务器找不到请求的资源。

```
*|select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_500 as "500比例",Rate_502 as "502比例",Rate_503
as "503比例",Rate_504 as "504比例",countall/60 as
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

指标释义：请求被Web应用防护规则拦截。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as "aveQPS",status_200,status_302,status_404,status_405,status_444,status_499,status_500,status_502,status_503,status_504,countall
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

指标释义：请求被精准访问控制规则拦截。

```
user_id: 1111111111111 |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

指标释义：请求被WAF CC自定义规则拦截。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

指标释义：客户端请求，服务端未返回数据，超时后，客户端主动断链，服务端返回给客户端该状态码。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

指标释义：（Internal Server Error） 服务器内部错误，无法完成请求。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

指标释义：（Bad Gateway）错误网关， 服务器作为网关或代理，从上游服务器收到无效响应。一般由于回源网络质量变差、回源链路有访问控制拦截回源请求导致源站无响应。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

指标释义：（Service Unavailable）服务不可用，由于超载或停机维护，服务器目前无法使用。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

指标释义：（Gateway Timeout） 网关超时，服务器作为网关或代理，但是没有及时从上游服务器收到请求。

```
* |select user_id,host as "域名",Rate_200 as
"200比例",Rate_302 as "302比例",Rate_404 as "404比例",Rate_405
as "405比例",Rate_444 as "444比例",Rate_499 as "499比例",Rate_500
as "500比例",Rate_502 as "502比例",Rate_503 as "503比例",Rate_504
as "504比例",countall/60 as
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

