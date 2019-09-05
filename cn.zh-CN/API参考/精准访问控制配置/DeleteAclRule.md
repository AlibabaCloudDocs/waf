# DeleteAclRule {#doc_api_waf-openapi_DeleteAclRule .reference}

调用DeleteAclRule接口删除指定精准访问控制规则。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=DeleteAclRule&type=RPC&version=2018-01-17)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAclRule|要执行的操作。取值：**DeleteAclRule**。

 |
|Domain|String|是|rstest.cdn.com|域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以通过调用[DescribePayInfo](~~86651~~)接口查看您当前WAF实例ID。

 |
|RuleId|Long|是|65899|精准访问控制规则ID。

 |
|Region|String|否|cn|WAF实例所在的地域。取值：

 -   **cn**：表示中国大陆地区（默认）
-   **cn-hongkong**：表示海外地区

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|请求ID。

 |
|Result| | |返回结果。

 |
|Status|Integer|2|请求执行状态：

 -   **0**：表示该请求等待执行。
-   **1**：表示该请求正在执行中。
-   **2**：表示该请求已执行完成。

 |
|WafTaskId|String|aliyun.waf.20180712214032277.qmxI9a|WAF的请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DeleteAclRule
&Domain=www.aliyun.com
&InstanceId=waf_elasticity-cn-0xldbqtm005
&RuleId=65899
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteAclRuleResponse>
      <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
      <Result>
            <Status>2</Status>
            <WafTaskId>aliyun.waf.20180712214032277.qmxI9a</WafTaskId>
      </Result>
</DeleteAclRuleResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Result":{
		"Status":2,
		"WafTaskId":"aliyun.waf.20180712214032277.qmxI9a"
	},
	"RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/waf-openapi)查看更多错误码。

