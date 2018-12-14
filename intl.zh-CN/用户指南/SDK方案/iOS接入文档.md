# iOS接入文档 {#concept_ts5_thq_p2b .concept}

本文介绍了使用iOS App接入WAF SDK的操作方法。

## SDK-iOS文件说明 {#section_h1q_yjq_p2b .section}

联系WAF技术支持人员获取对应的SDK包，解压至本地。

在sdk-iOS文件夹下，包含以下iOS SDK文件：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15579/15447822317832_zh-CN.png)

各文件说明如下：

|文件|功能|
|--|--|
|SGMain.framework|主框架SDK|
|SecurityGuardSDK.framework|基础安全插件|
|SGSecurityBody.framework|人机识别插件|
|SGAVMP.framework|虚拟机插件|
|yw\_1222\_0335\_mwua.jpg|配置文件|

## 项目工程配置 {#section_l1q_yjq_p2b .section}

参照以下步骤，来配置项目工程。

1.  添加Framework。将WAF SDK中提供的4个.framework文件添加到工程的依赖库中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15579/15447822317833_zh-CN.png)

2.  设置链接选项。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15579/15447822327834_zh-CN.png)

3.  添加系统依赖库。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15579/15447822327835_zh-CN.png)

4.  引入配置文件。将SDK中的yw\_1222\_0335\_mwua.jpg 配置文件加到mainbunle下。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15579/15447822327836_zh-CN.png)

    在应用集成多个target的情况下，请确认yw\_1222\_0335\_mwua.jpg配置文件加入到正确的Target Membership中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15579/15447822327837_zh-CN.png)


## 代码编写 {#section_uhy_gkq_p2b .section}

**1. 初始化SDK**

**接口定义**

```
+ (BOOL) initialize;
```

**接口描述**

-   功能：初始化SDK。
-   参数：无。
-   返回值：BOOL类型。初始化成功返回YES，失败返回NO。

**调用方式**

```
[JAQAVMPSignature initialize];
```

**示例代码**

```
static BOOL avmpInit = NO;
- (BOOL) initAVMP{
    @synchronized(self) {  // just initialize once
        if(avmpInit == YES){
            return YES;
        }
        avmpInit = [JAQAVMPSignature initialize];
        return avmpInit;
    }
}
```

**2. 签名请求数据**

**接口定义**

```
+ (NSData*) avmpSign: (NSInteger) signType input: (NSData*) input;
```

**接口描述**

使用avmp技术对input的数据进行签名处理，并且返回签名串。

**说明：** 被签名的请求体应该跟客户端实际发送出来的请求体完全一样，完全一样的含义包括请求体中字符串的编码格式、空格、特殊字符以及参数的顺序等等，否则会造成验签失败。

接口参数见下表。

|参数名|类型|是否必需|说明|
|signType|NSInteger|是|签名使用的算法，目前是固定值，输入3。|
|input|NSData\*|否|待签名的数据，一般是整个请求体（request body）。**说明：** 如果请求体为空（例如POST请求的body为空、或者GET请求），则填写空对象null或空字符串的Bytes值（例如，"".getBytes\("UTF-8"\)\)。

|

返回值：NSData\*类型，返回签名串。

**调用方式**

```
[JAQAVMPSignature avmpSign: 3 input: request_body];
```

**示例代码**

客户端向服务器端发送数据时，需要调用avmpSign接口对整个body数据进行签名处理，之后会得到签名串。该签名串就是wToken。

```
# define VMP_SIGN_WITH_GENERAL_WUA2 (3)

- (NSString*) avmpSign{
    
    @synchronized(self) {
        NSString* request_body = @"i am the request body, encrypted or not!";  
        
        if(![self initAVMP]){
            [self toast:@"Error: init failed"];
			            return nil;
        }
        
        NSString* wToken = nil;
        NSData* data = [request_body dataUsingEncoding:NSUTF8StringEncoding];
        NSData* sign = [JAQAVMPSignature avmpSign: VMP_SIGN_WITH_GENERAL_WUA2 input:data];
        if(sign == nil || sign.length <= 0){
            return nil;
        }else{
            wToken = [[NSString alloc] initWithData:sign encoding: NSUTF8StringEncoding];
            return wToken;
        }
    }
}
```

**说明：** 如果请求体为空，也需要调用 avmpSign 接口生成 wToken，第二个参数直接传空即可。示例代码如下。

```
NSData* sign = [JAQAVMPSignature avmpSign: VMP_SIGN_WITH_GENERAL_WUA2 input:nil];
```

**3. 将wToken放进协议头**

示例代码如下：

```
#define VMP_SIGN_WITH_GENERAL_WUA2 (3)

-(void)setHeader
{
    NSString* request_body = @"i am the request body, encrypted or not!";  
    NSData* body_data = [request_body dataUsingEncoding:NSUTF8StringEncoding];

NSString* wToken = nil;
NSData* sign = [JAQAVMPSignature avmpSign: VMP_SIGN_WITH_GENERAL_WUA2 input:body_data];
    wToken = [[NSString alloc] initWithData:sign encoding: NSUTF8StringEncoding];
    NSString *strUrl = [NSString stringWithFormat:@"http://www.xxx.com/login"];
    NSURL *url = [NSURL URLWithString:strUrl];
    NSMutableURLRequest *request = 
        [[NSMutableURLRequest alloc]initWithURL:url cachePolicy:NSURLRequestReloadIgnoringCacheData timeoutInterval:20];

    [request setHTTPMethod:@"POST"];

    // set request body info
    [request setHTTPBody:body_data];

    // set wToken info to header
    [request setValue:wToken forHTTPHeaderField:@"wToken"];

    NSURLConnection *mConn = [[NSURLConnection alloc]initWithRequest:request delegate:self startImmediately:true];
    [mConn start];
    // ...
}
```

**4. 发送数据到服务器**

将修改好协议头的数据发送到WAF，并解析wToken进行风险识别，拦截恶意请求后，再把合法请求回源。

## 错误码 {#section_ybq_yjq_p2b .section}

上述initialize和avmpSign接口有可能会出现异常。如果生成签名串异常或失败，请在console中搜索“SG Error”。

常见错误信息及描述见下表。

|错误代码|含义|
|1901|参数不正确，请检查输入的参数。|
|1902|图片文件有问题。一般是获取图片文件时的apk签名和当前程序apk 签名不一致。请使用当前程序的apk重新生成图片。iOS可能是因为BundleID不匹配。|
|1903|图片文件格式有问题。|
|1904|请升级新版本图片。AVMP签名功能仅支持v5图片。|
|1905|没有找到图片文件。请确保图片文件yw\_1222\_0335\_mwua.jpg在工程中。|
|1906|图片中缺少AVMP签名对应的byteCode。请检查使用的图片是否正确。|
|1907|初始化AVMP失败，请重试。|
|1910|非法的avmpInstance实例。可能原因有：-   AVMPInstance被destroy后，调用InvokeAVMP。
-   图片byteCode版本与SDK不匹配。

|
|1911|加密图片的byteCode没有相应导出的函数。|
|1912|AVMP调用失败。请联系我们。|
|1913|AVMPInstance被destroy之后，调用InvokeAVMP出现该错误。|
|1915|AVMP调用内存不足，请重试。|
|1999|未知错误，请重试。|

