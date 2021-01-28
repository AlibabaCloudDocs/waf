# DescribeLogServiceStatus

调用DescribeLogServiceStatus查询已接入WAF进行防护的域名的日志采集状态（是否开启日志采集）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=DescribeLogServiceStatus&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeLogServiceStatus|要执行的操作。取值：**DescribeLogServiceStatus**。 |
|InstanceId|String|是|waf-cn-zz11sr5\*\*\*\*|WAF实例的ID。

 **说明：** 您可以调用[DescribeInstanceInfo](~~140857~~)查询当前WAF实例的ID。 |
|Region|String|否|cn|WAF实例的地域ID。默认为**cn**，表示中国内地；如果WAF实例的地域是海外地区，请填写**cn-hongkong**。

 **说明：** 您可以调用[DescribeInstanceInfo](~~140857~~)查询当前WAF实例的地域ID。 |
|ResourceGroupId|String|否|rg-acfm2pz25js\*\*\*\*|WAF实例在资源管理服务中所属的资源组ID。默认为空，即属于默认资源组。

 关于资源组的更多信息，请参见[创建资源组](~~94485~~)。 |
|PageNumber|Integer|否|1|列表的页码。默认值为**1**。 |
|PageSize|Integer|否|10|分页查询时每页的行数。默认值为**10**。 |
|DomainNames.N|RepeatList|否|www.aliyun.com|要查询的域名列表。一次最多允许查询10个域名。不填写该参数表示查询所有域名。

 **说明：** 您可以调用[DescribeDomainNames](~~86373~~)查询所有已经接入当前WAF实例进行防护的域名。 |

调用API时，除了本文中该API的请求参数，还需加入阿里云API公共请求参数。公共请求参数的详细介绍，请参见[公共参数](~~162719~~)。

调用API的请求格式，请参见本文**示例**中的请求示例。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DomainStatus|Array of status| |域名的日志采集状态（是否开启了日志采集）。 |
|Domain|String|www.aliyun.com|域名名称。 |
|SlsLogActive|Integer|1|该域名是否开启了日志采集。取值：

 -   **1**：表示已开启。
-   **0**：表示未开启。 |
|RequestId|String|C2E97B3F-1623-4CDF-A7E2-FD9D4CF1027A|本次请求的ID。 |
|TotalCount|Integer|1|返回结果的总数。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeLogServiceStatus
&InstanceId=waf-cn-zz11sr5****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeLogServiceStatusResponse>
	  <RequestId>C2E97B3F-1623-4CDF-A7E2-FD9D4CF1027A</RequestId>
	  <TotalCount>1</TotalCount>
	  <DomainStatus>
		    <Domain>www.aliyun.com</Domain>
		    <SlsLogActive>1</SlsLogActive>
	  </DomainStatus>
</DescribeLogServiceStatusResponse>
```

`JSON`格式

```
{
    "RequestId": "C2E97B3F-1623-4CDF-A7E2-FD9D4CF1027A",
    "TotalCount": 1,
    "DomainStatus": [
        {
            "Domain": "www.aliyun.com",
            "SlsLogActive": 1
        }
    ]
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/waf-openapi)查看更多错误码。

