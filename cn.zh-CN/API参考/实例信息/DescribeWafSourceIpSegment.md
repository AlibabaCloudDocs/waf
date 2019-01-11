# DescribeWafSourceIpSegment {#doc_api_919609 .reference}

调用DescribeWafSourceIpSegment接口获取WAF实例的回源IP网段列表。

## 调试 {#apiExplorer .section}

单击[这里](https://api.aliyun.com/#product=waf-openapi&api=DescribeWafSourceIpSegment)在OpenAPI Explorer中进行可视化调试，并生成SDK代码示例。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|waf\_elasticity-cn-0xldbqtm005|WAF实例ID。

 **说明：** 您可以通过调用[DescribePayInfo](~~86651~~)接口查看您当前WAF实例ID。

 |
|Region|String|否|cn|WAF实例所在的地域。取值：

 -   **cn**：表示中国大陆地区。
-   **cn-hongkong**：表示海外地区。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Ips|String|121.43.18.0/24,120.25.115.0/24,101.200.106.0/24|WAF回源IP网段，网段间以逗号（,）分隔。

 |
|RequestId|String|9087ADDC-9047-4D02-82A7-33021B58083C|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeWafSourceIpSegment
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Region=cn
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeWafSourceIpSegment>
  <RequestId>9087ADDC-9047-4D02-82A7-33021B58083C</RequestId>
  <Ips>121.43.18.0/24,120.25.115.0/24,101.200.106.0/24</Ips>
</DescribeWafSourceIpSegment>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"9087ADDC-9047-4D02-82A7-33021B58083C",
	"Ips":"121.43.18.0/24,120.25.115.0/24,101.200.106.0/24"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

