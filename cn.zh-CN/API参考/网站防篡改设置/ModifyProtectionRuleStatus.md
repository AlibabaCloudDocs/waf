# ModifyProtectionRuleStatus {#reference_wtp_d2r_dgb .reference}

调用ModifyProtectionRuleStatus接口启用或关闭指定的网站防篡改规则。

## 请求参数 {#section_gk1_x1w_dgb .section}

|名称|类型|是否必须|描述|
|--|--|----|--|
|Action|String|是|要执行的操作。取值：ModifyProtectionRuleStatus

|
|Region|String|是|地域ID。取值：-   cn：中国大陆地区。
-   cn-hongkong：海外地区。

|
|InstanceId|String|是|WAF实例ID。|
|Domain|String|是|要操作的域名名称。|
|Defense|String|是|要操作的防护功能。取值：tamperproof

|
|Id|Long|是|要操作的规则ID。调用[DescribeProtectionModuleRules](cn.zh-CN/API参考/网站防篡改设置/DescribeProtectionModuleRules.md#)接口可以查询到所有规则ID。|
|RuleStatus|Integer|是|是否启用规则。取值：-   0：关闭
-   1：启用

|
|LockVersion|Long|是|并发锁版本。|

## 返回参数 {#section_ezz_x1w_dgb .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|当前请求的ID。|
|success|boolen|是否成功修改规则状态。|
|TaskStatus|Integer|当前请求的执行状态：-   0：等待执行。
-   1：正在执行中。
-   2：已执行完成。

|

## 示例 {#section_qhs_y1w_dgb .section}

**请求示例**

```
https://wafopenapi.cn-hangzhou.aliyuncs.com/?Action=ModifyProtectionRuleStatus
&Region=cn
&InstanceId=waf_elasticity-cn-0xldbqtm005
&Domain=www.aliyun.com
&Defense=tamperproof
&Id=111
&RuleStatus=1
&LockVersion=0
```

**返回示例**

```
{
	"code": 200,
	"data": {
		"TaskStatus": 2
	},
	"requestId": "66A98669-CC6E-4F3E-80A6-3014697B11AE",
	"success": true
}
```

