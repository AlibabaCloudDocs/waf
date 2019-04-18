# CreateAclRule {#doc_api_waf-openapi_CreateAclRule .reference}

调用CreateAclRule接口为指定域名添加精准访问控制规则。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=waf-openapi&api=CreateAclRule)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAclRule|要执行的操作。取值：**CreateAclRule**。

 |
|Domain|String|是|rstest.cdn.com|域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以通过调用[DescribePayInfo](~~86651~~)接口查看您当前WAF实例ID。

 |
|Rules|String|是|Rules:'\{"conditions":\[\{"key":"URL","contain":1,"value":"asfas"\}\],"continueComponent":\{"post\_action\_cc":1,"post\_action\_waf":1,"post\_action\_sa":1,"post\_action\_block\_geo":"0","post\_action\_data\_risk\_control":"1"\},"action":"1","name":"lei123"\}'|精准访问控制规则详细信息，采用JSON格式的字符串表述，具体结构见下表。

 -   **Id**：Long类型，可选，规则ID。
-   **Name**：String类型，必选，规则名称。
-   **Action**：Integer类型，必选，规则的匹配动作，取值：
    -   **0**：表示阻断，即命中该规则的匹配条件，则阻断该访问请求。
    -   **1**：表示放行，即命中该规则的匹配条件，则放行该访问请求。
    -   **2**：表示告警，即命中该规则的匹配条件，将放行该访问请求，但会记录该请求并告警。
-   **ContinueComponent**：String类型，可选，是否继续执行其它WAF防护策略，采用JSON格式的字符串表述，具体结构见下表。
    -   **post\_action\_cc**，Integer类型，可选，是否继续执行CC防护规则检测，取值：
        -   **0**：表示否。
        -   **1**：表示是。
    -   **post\_action\_waf**，Integer类型，可选，是否继续执行Web攻击防护规则检测，取值：
        -   **0**：表示否。
        -   **1**：表示是。
    -   **post\_action\_sa**，Integer类型，可选，是否继续执行智能防护引擎规则检测，取值：
        -   **0**：表示否。
        -   **1**：表示是。
    -   **post\_action\_block\_geo**，Integer类型，可选，是否继续执行地区封禁，取值：
        -   **0**：表示否。
        -   **1**：表示是。
    -   **post\_action\_data\_risk\_control**，Integer类型，可选，是否继续执行数据风控防护，取值：
        -   **0**：表示否。
        -   **1**：表示是。
    -   **post\_action\_sdk**，Integer类型，可选，是否继续执行SDK防护，取值：
        -   **0**：表示否。
        -   **1**：表示是。
-   **Conditions**，Array类型，可选，规则匹配条件，数组中具体定义见下表。
    -   **Key**，String类型，必选，匹配字段，取值包括IP、URL、Referer、User-Agent、Params、Cookie、Content-Type、X-Forwarded-For、Content-Length、Post-Body、Http-Method、Header。不同版本的WAF实例支持的匹配字段不同，您可以在Web应用防火墙管理控制台中查看您的实例当前所支持的匹配字段。
    -   **Contain**，Integer类型，必选，逻辑符，取值：
        -   **0**：表示不包含。
        -   **1**：表示包含。
        -   **2**：表示不存在。
        -   **10**：表示不等于。
        -   **11**：表示等于。
        -   **20**：表示长度小于。
        -   **21**：表示长度等于。
        -   **22**：表示长度大于。
        -   **30**：表示值小于。
        -   **31**：表示值等于。
        -   **32**：表示值大于。
    -   **Value**，String类型，必选，匹配内容。

 |
|Region|String|否|cn|WAF实例所在的地域。取值：

 -   **cn**：表示中国大陆地区（默认）
-   **cn-hongkong**：表示海外地区

 |

匹配字段和逻辑符的映射关系

|匹配字段

|逻辑符

|
|------|-----|
|IP

|属于、不属于

|
|Referer

|包含、不包含、等于、不等于、长度小于、长度等于、长度大于

|
|User-Agent

|包含、不包含、等于、不等于、长度小于、长度等于、长度大于

|
|Param

|包含、不包含、等于、不等于、长度小于、长度等于、长度大于

|
|Cookie

|包含、不包含、等于、不等于、长度小于、长度等于、长度大于、不存在

|
|Content-Type

|包含、不包含、等于、不等于、长度小于、长度等于、长度大于

|
|X-Forwarded-For

|包含、不包含、等于、不等于、长度小于、长度等于、长度大于、不存在

|
|Content-Length

|值小于、值等于、值大于

|
|Post-Body

|包含、不包含、等于、不等于

|
|Http-Method

|等于、不等于

|
|Header

|包含、不包含、等于、不等于、长度小于、长度等于、长度大于、不存在

|

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|该请求的ID。

 |
|Result| | |返回结果。

 |
|└Status|Integer|2|请求执行状态：

 -   **0**：表示该请求等待执行。
-   **1**：表示该请求正在执行中。
-   **2**：表示该请求已执行完成。

 |
|└WafTaskId|String|aliyun.waf.20180712214032277.qmxI9a|WAF的请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=CreateAclRule
&Domain=www.aliyun.com
&ServiceOn=1
&Rules={...}
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateAclRuleResponse>
  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
  <Result>
    <Status>2</Status>
    <WafTaskId>aliyun.waf.20180712214032277.qmxI9a</WafTaskId>
  </Result>
</CreateAclRuleResponse>

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

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

