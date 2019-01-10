# DescribeRegions {#doc_api_908123 .reference}

调用DescribeRegions接口获取当前WAF支持的地域信息。

**说明：** 请求该API接口时，无需指定**Region**和**InstanceId**这两个公共请求参数。

## 调试 {#apiExplorer .section}

单击[这里](https://api.aliyun.com/#product=waf-openapi&api=DescribeRegions)在OpenAPI Explorer中进行可视化调试，并生成SDK代码示例。

## 请求参数 {#parameters .section}

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Regions| | |地域列表信息。

 |
|└Display|String|ture|是否在该地域提供WAF服务：

 -   **true**：表示是。
-   **false**：表示否。

 |
|└Region|String|cn|地域ID。

 |
|RequestId|String|276D7566-31C9-4192-9DD1-51B10DAC29D2|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=DescribeRegions
&公共请求参数

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeRegionsResponse>
  <RequestId>56B40D30-4960-4F19-B7D5-2B1F0EE6CB70</RequestId>
  <Regions>
    <Region>
      <Region>cn</Region>
      <Display>true</Display>
    </Region>
    <Region>
      <Region>cn-hongkong</Region>
      <Display>true</Display>
    </Region>
  </Regions>
</DescribeRegionsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"276D7566-31C9-4192-9DD1-51B10DAC29D2",
	"Regions":{
		"Region":[
			{
				"region":"cn",
				"display":"true"
			},
			{
				"region":"cn-hongkong",
				"display":"true"
			}
		]
	}
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/waf-openapi)

