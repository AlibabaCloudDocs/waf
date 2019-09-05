# DescribeAsyncTaskStatus {#doc_api_waf-openapi_DescribeAsyncTaskStatus .reference}

调用DescribeAsyncTaskStatus接口查询WAF任务执行状态。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=DescribeAsyncTaskStatus&type=RPC&version=2018-01-17)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAsyncTaskStatus|要执行的操作。取值：**DescribeAsyncTaskStatus**。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以通过调用[DescribePayInfo](~~86651~~)接口查看您当前WAF实例ID。

 |
|WafRequestId|String|是|aliyun.waf.20180719140433783.SvaZeY|WAF任务ID。

 |
|Region|String|否|cn|WAF实例所在的地域。取值：

 -   **cn**：表示中国大陆地区（默认）
-   **cn-hongkong**：表示海外地区

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|12EF3845-CCEB-4B84-AE60-2B49B2FF1EE5|请求ID。

 |
|Result| | |返回结果

 |
|AsyncTaskStatus|String|2|异步任务执行状态：

 -   **0**：表示该请求等待执行。
-   **1**：表示该请求正在执行中。
-   **2**：表示该请求已执行完成。

 |
|Data|String|xx|异步任务需要返回的业务数据。

 |
|ErrCode|String|400|错误代码。

 **说明：** 该参数仅在请求执行发生错误时返回。

 |
|ErrMsg|String|xx|错误信息描述。

 **说明：** 该参数仅在请求执行发生错误时返回。

 |
|Progress|Integer|90|异步任务执行进度（百分比）。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeAsyncTaskStatus
&InstanceId=waf_elasticity-cn-0xldbqtm005
&WafRequestId=aliyun.waf.20180719140433783.SvaZeY
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAsyncTaskStatusResponse>
      <RequestId>12EF3845-CCEB-4B84-AE60-2B49B2FF1EE5</RequestId>
      <Result>
            <DomainConfig>
                  <Progress>100</Progress>
                  <AsyncTaskStatus>2</AsyncTaskStatus>
            </DomainConfig>
      </Result>
</DescribeAsyncTaskStatusResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Result":{
		"DomainConfig":{
			"AsyncTaskStatus":2,
			"Progress":100
		}
	},
	"RequestId":"12EF3845-CCEB-4B84-AE60-2B49B2FF1EE5"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/waf-openapi)查看更多错误码。

