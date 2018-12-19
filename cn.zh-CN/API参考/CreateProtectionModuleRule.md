# CreateProtectionModuleRule {#reference_src_c2r_dgb .reference}

调用CreateProtectionModuleRule接口新增一条网站防篡改规则。

## 描述 {#section_b22_32r_dgb .section}

URL：`/openapi/waf-openapi/2018-01-17/CreateProtectionModuleRule.json`

## 请求参数 {#section_znz_j2r_dgb .section}

|名称|类型|是否必须|描述|
|--|--|----|--|
|Action|String|是|要执行的操作。取值：CreateProtectionModuleRule

|
|Region|String|是|地域ID。取值：-   cn：中国大陆地区。
-   cn-hongkong：海外地区。

|
|InstanceId|String|是|WAF实例ID。|
|Domain|String|是|要操作的域名名称。|
|Defense|String|是|要操作的防护功能。取值：tamperproof

|
|Rule|String|是|要添加的防篡改规则。按照[Rule](#)构造成Json后转换成字符串作为入参。示例：`"{\"name\":\"test\",\"uri\":\"http://xx.aliyun.com/example/\"}"`

|

|名称|类型|是否必须|描述|
|--|--|----|--|
|uri|String|是|要防护的URI。|
|name|String|是|自定义规则名称。|
|status|Integer|否|是否启用规则。取值：-   0：关闭
-   1：启用

**说明：** ：新增防篡改规则时无需填写，更改防篡改规则时必须填写。

|

## 返回参数 {#section_py2_j1w_dgb .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|当前请求的ID。|
|success|boolen|是否成功新增规则。|
|TaskStatus|Integer|当前请求的执行状态：-   0：等待执行。
-   1：正在执行中。
-   2：已执行完成。

|
|WafTaskId|String|WAF的请求ID。|

## 示例 {#section_omh_k1w_dgb .section}

**请求示例**

```
https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=CreateProtectionModuleRule
&Region=cn
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Domain=www.aliyun.com
&Defense=tamperproof
&Rule={\"name\":\"test\",\"uri\":\"http://xx.aliyun.com/example/\"}
```

**返回示例**

```
{
	"code": 200,
	"data": {
        "WafTaskId":"dsfdsfds"
	"TaskStatus": 2
	},
	"requestId": "66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"success": true
}
```

