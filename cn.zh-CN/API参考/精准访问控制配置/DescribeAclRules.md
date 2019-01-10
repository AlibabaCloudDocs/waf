# DescribeAclRules {#doc_api_908697 .reference}

调用DescribeAclRules接口获取指定域名的精准访问控制规则列表。

## 调试 {#apiExplorer .section}

单击[这里](https://api.aliyun.com/#product=waf-openapi&api=DescribeAclRules)在OpenAPI Explorer中进行可视化调试，并生成SDK代码示例。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|CurrentPage|Integer|是|1|分页查询请求时返回的页码。例如，查询第一页的返回结果，则填写1。

 |
|Domain|String|是|www.aliyun.com|域名名称。

 |
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以通过调用[DescribePayInfo](~~86651~~)接口查看您当前WAF实例ID。

 |
|PageSize|Integer|是|10|页面显示最大记录数量。

 |
|Region|String|否|cn|WAF实例所在的地域。取值：

 -   **cn**：表示中国大陆地区。
-   **cn-hongkong**：表示海外地区。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D7861F61-5B61-46CE-A47C-6B19160D5EB0|请求ID。

 |
|Result| | |返回结果。

 |
|└AclRules| | |精准访问控制规则列表，其中每条精准访问控制规则都会以AclRule子参数表述。AclRule子参数以JSON格式的字符串表述。

 |
|└Action|Integer|1|规则的匹配动作，取值：

 -   **0**：表示阻断，即命中该规则的匹配条件，则阻断该访问请求。
-   **1**：表示放行，即命中该规则的匹配条件，则放行该访问请求。
-   **2**：表示告警，即命中该规则的匹配条件，将放行该访问请求，但会记录该请求并告警。

 |
|└Conditions| | |规则匹配条件结构体。

 |
|└Contain|String|1|逻辑符：

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

 |
|└Key|String|url|匹配字段，包括IP、URL、Referer、User-Agent、Params、Cookie、Content-Type、X-Forwarded-For、Content-Length、Post-Body、Http-Method、Header。

 **说明：** 说明：不同版本的WAF实例支持的匹配字段不同，您可以在Web应用防火墙管理控制台中查看您的实例当前所支持的匹配字段。

 |
|└Value|String|login|匹配内容。

 |
|└ContinueBlockGeo|Integer|1|是否继续执行地区封禁，取值：

 -   **0**：表示否。
-   **1**：表示是。

 |
|└ContinueCc|Integer|1|是否继续执行CC防护规则检测，取值：

 -   **0**：表示否。
-   **1**：表示是。

 |
|└ContinueDataRiskControl|Integer|1|是否继续执行数据风控防护，取值：

 -   **0**：表示否。
-   **1**：表示是。

 |
|└ContinueSA|Integer|1|是否继续执行智能防护引擎规则检测，取值：

 -   **0**：表示否。
-   **1**：表示是。

 |
|└ContinueSdk|Integer|1|是否继续执行SDK防护，取值：

 -   **0**：表示否
-   **1**：表示是。

 |
|└ContinueWaf|Integer|1|是否继续执行Web攻击防护规则检测，取值：

 -   **0**：表示否。
-   **1**：表示是。

 |
|└Id|Long|1111|ACL规则ID。

 |
|└IsDefault|Integer|1|是否默认规则：

 -   **0**：表示否。
-   **1**：表示是。

 |
|└Name|String|test|规则名称。

 |
|└Order|Integer|1|规则顺序。

 **说明：** 说明：该值越大，规则的优先级越高。

 |
|└Total|Integer|1|规则总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeAclRules
&Domain=www.aliyun.com
&CurrentPage=1
&PageSize=50
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAclRulesResponse>
  <RequestId>D7861F61-5B61-46CE-A47C-6B19160D5EB0</RequestId>
  <Result>
    <AclRules>
      <AclRule>
        <IsDefault>1</IsDefault>
        <Order>0</Order>
        <ContinueBlockGeo>1</ContinueBlockGeo>
        <Action>1</Action>
        <ContinueWaf>1</ContinueWaf>
        <ContinueSdk>0</ContinueSdk>
        <Id>16572</Id>
        <ContinueCc>1</ContinueCc>
        <Conditions>
          <condition>
            <key>URL</key>
            <contain>1</contain>
            <value>asfas</value>
          </condition>
        </Conditions>
        <Name>default</Name>
        <ContinueDataRiskControl>1</ContinueDataRiskControl>
        <ContinueSA>1</ContinueSA>
      </AclRule>
    </AclRules>
    <Total>1</Total>
  </Result>
</DescribeAclRulesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Result":{
		"AclRules":{
			"AclRule":[
				{
					"Name":"default",
					"Conditions":{
						"condition":[
							{
								"contain":1,
								"value":"asfas",
								"key":"URL"
							}
						]
					},
					"ContinueDataRiskControl":1,
					"Action":1,
					"ContinueSdk":0,
					"ContinueWaf":1,
					"IsDefault":1,
					"Order":0,
					"Id":16572,
					"ContinueCc":1,
					"ContinueSA":1,
					"ContinueBlockGeo":1
				}
			]
		},
		"Total":1
	},
	"RequestId":"D7861F61-5B61-46CE-A47C-6B19160D5EB0"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

