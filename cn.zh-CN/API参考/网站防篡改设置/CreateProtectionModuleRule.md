# CreateProtectionModuleRule {#doc_api_waf-openapi_CreateProtectionModuleRule .reference}

调用CreateProtectionModuleRule接口新增一条防护规则。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=waf-openapi&api=CreateProtectionModuleRule&type=RPC&version=2018-01-17)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateProtectionModuleRule|要执行的操作。取值：**CreateProtectionModuleRule**。

 |
|Defense|String|是|tamperproof|要操作的防护功能。取值：

 -   **tamperproof**：新增网站防篡改规则
-   **antifraud**：新增数据风控规则
-   **antifraud\_js**：新增数据风控JS规则

 |
|Domain|String|是|www.aliyun.com|要操作的域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以调用[DescribePayInfo](~~86651~~)接口查看当前WAF实例ID。

 |
|Rule|String|是|\{\\"name\\":\\"test\\",\\"uri\\":\\"http://xx.aliyun.com/example/\\"\}|要添加的规则内容。按照Rule构造成Json后转换成字符串作为入参，根据要添加的规则类型不同，需要传入的参数不同。具体结构说明如下。

 -   添加网站防篡改规则（**Defense**为**tamperproof**）时，传入以下参数：
    -   **uri**，String类型，必选，要防护的URI。
    -   **name**，String类型，必选，自定义规则名称。
    -   **status**，Integer类型，可选，是否启用规则。取值：

**说明：** 新增防篡改规则时无需填写，更改防篡改规则时必须填写。

        -   **0**：关闭
        -   **1**：启用
-   添加数据风控规则（**Defense**为**antifraud**或**antifraud\_js**）时，传入以下参数：
    -   **uri**，String类型，必选，要防护的URI。

 |
|Region|String|否|cn|地域ID。取值：

 -   **cn**：中国大陆地区（默认）
-   **cn-hongkong**：海外地区

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|66A98669-CC6E-4F3E-80A6-3014697B11AE|当前请求的ID。

 |
|TaskStatus|Integer|2|当前请求的执行状态：

 -   **0**：等待执行。
-   **1**：正在执行中。
-   **2**：已执行完成。

 |
|WafTaskId|Integer|123|WAF的请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=CreateProtectionModuleRule
&Region=cn
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Domain=www.aliyun.com
&Defense=tamperproof
&Rule={\"name\":\"test\",\"uri\":\"http://xx.aliyun.com/example/\"}
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateProtectionModuleRuleResponse>
     <code>200</code>
     <data>
          <TaskStatus>2</TaskStatus>
          <WafTaskId>dsfdsfds</WafTaskId>
     </data>
     <requestId>66A98669-CC6E-4F3E-80A6-3014697B11AE</requestId>
</CreateProtectionModuleRuleResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"data":{
		"TaskStatus":2,
		"WafTaskId":"dsfdsfds"
	},
	"code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/waf-openapi)查看更多错误码。

