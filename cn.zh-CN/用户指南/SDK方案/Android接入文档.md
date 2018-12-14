# Android接入文档 {#concept_wqs_5hq_p2b .concept}

本文介绍了使用Android App接入WAF SDK的操作方法。

## SDK-Android文件说明 {#section_qsx_lnq_p2b .section}

联系WAF技术支持人员获取对应的SDK包，解压至本地。

在sdk-Android文件夹中，包含以下Android SDK文件：

|文件|功能|
|--|--|
|SecurityGuardSDK-xxx.aar|主框架SDK|
|AVMPSDK-xxx.aar|虚拟机引擎插件|
|SecurityBodySDK-xxx.aar|人机识别插件|
|yw\_1222\_0335\_mwua.jpg|虚拟机引擎配置文件|

## 项目工程配置 {#section_wsx_lnq_p2b .section}

参照以下步骤，来配置项目工程。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15447822467850_zh-CN.png)

1.  在Android Studio中导入SDK中的aar文件。将SDK中所有的aar文件都复制到项目的libs目录下。如果没有libs目录，请手工创建一个。
2.  打开该Module的build.gradle文件，在其中增加以下配置（图示 ③ 和 ④ ）。
    -   将libs目录作为查找依赖的源。

        ```
        repositories{
            flatDir {
                dirs 'libs'
            }
        }
        ```

    -   增加编译依赖。

        **说明：** aar文件版本号可能会有不同，以下载得到的文件为准。

        ```
        dependencies {
            compile fileTree(include: ['*.jar'], dir: 'libs')
            compile ('com.android.support:appcompat-v7:23.0.0')
            compile (name:'AVMPSDK-external-release-xxx', ext:'aar')
            compile (name:'SecurityBodySDK-external-release-xxx', ext:'aar')
            compile (name:'SecurityGuardSDK-external-release-xxx', ext:'aar')
        }
        ```

3.  向drawable文件夹中导入jpg文件。将SDK目录下的yw\_1222\_0335\_mwua.jpg配置文件复制到 Android 应用工程的drawable目录下。

    **说明：** 如果默认没有drawable目录，请手动创建一个。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15447822467851_zh-CN.png)

4.  过滤ABI（删除多余架构SO）。WAF SDK目前仅支持armeabi、armeabi-v7a、arm64-v8a架构的SO。因此，您需要对最终导出的ABI进行过滤。否则，会造成App崩溃。具体操作如下：

    1.  在Android工程lib目录下，删除除armeabi、armeabi-v7a、arm64-v8a文件夹外所有其他CPU架构的文件夹，包括x86、x86\_64、mips、mips64等。最终，只保留armeabi、armeabi-v7a、arm64-v8a目录。
    2.  在工程的build.gradle配置文件中增加过滤规则，被abiFilters指定的架构即会被包含在APK里面。示例代码如下：

        **说明：** 本代码示例中指定了armeabi架构，您可以根据实际情况指定或兼容armeabi-v7a、arm64-v8a架构。

        ```
        defaultConfig {
            applicationId "com.xx.yy"
            minSdkVersion xx
            targetSdkVersion xx
            versionCode xx
            versionName "x.x.x"
            ndk {
                abiFilters "armeabi"
        // abiFilters  "armeabi-v7a"
        // abiFilters  "arm64-v8a"
            }
        }
        ```

        **说明：** 只保留armeabi架构的SO不会影响App的兼容性，并且还能大大减小App的体积。

    下图显示了手机淘宝App的ABI情况。可以看出，手机淘宝App只有armeabi架构的目录。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15447822467852_zh-CN.png)

5.  添加App权限。
    -   如果是Android Studio项目，并且使用aar方式集成，那么则不需要在项目中额外配置权限，因为在aar中已经声明了相关权限。
    -   如果是Eclipse项目，需要在AndroidMenifest.xml文件中添加下列权限配置：

        ```
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" /> 
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        ```

6.  添加ProGuard配置。如果您使用了Proguard进行混淆，则需要添加ProGuard配置。ProGuard配置也根据接入方式的不同，分为Eclipse和AndrodStudio两种情况。

    -   **Android Studio**

        如果在build.gradle中配置了proguardFiles，并且开启了minifyEnabled，则表明使用了proguard-rules.pro这个配置文件进行混淆。如下图所示。

        ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/62889/cn_zh/1514354175536/ProGuard.png)

    -   **Eclipse**

        如果在project.properties中指定了proguard配置，比如在project.properties中有如下的语句：`proguard.config=proguard.cfg`，则表明使用了proguard进行混淆。混淆配置在proguard.cfg文件中：

        ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/62889/cn_zh/1514354275311/proguard.cfg.png)

    **添加keep规则**

    为了保证需要的一些类不被混淆，需要在proguard的配置文件中添加以下规则。

    ```
    -keep class com.taobao.securityjni.**{*;}
    -keep class com.taobao.wireless.security.**{*;}
    -keep class com.ut.secbody.**{*;}
    -keep class com.taobao.dp.**{*;}
    -keep class com.alibaba.wireless.security.**{*;}
    ```


## 代码编写 {#section_xtx_lnq_p2b .section}

1.  导入包。

    ```
    import com.alibaba.wireless.security.jaq.JAQException;
    import com.alibaba.wireless.security.jaq.avmp.IJAQAVMPSignComponent;
    import com.alibaba.wireless.security.open.SecurityGuardManager;
    import com.alibaba.wireless.security.open.avmp.IAVMPGenericComponent;
    ```

2.  初始化。
    -   接口定义：`boolean initialize();`
    -   接口描述：
        -   功能：初始化SDK。
        -   参数：无。
        -   返回值：boolean类型。初始化成功返回true，失败返回false。
    -   示例代码：

        ```
        IJAQAVMPSignComponent jaqVMPComp = SecurityGuardManager.getInstance(getApplicationContext()).getInterface(IJAQAVMPSignComponent.class);
        boolean result = jaqVMPComp.initialize();
        ```

3.  签名请求数据。
    -   接口定义：`byte[] avmpSign(int signType, byte[] input);`
    -   接口描述：
        -   功能：使用avmp技术对input的数据进行签名处理，并且返回签名串。
        -   参数见下表。

            |参数名|类型|是否必需|说明|
            |signType|int|是|签名使用的算法，目前是固定值，填写3。|
            |input|byte\[\]|否|待签名的数据，一般是整个请求体（request body）。**说明：** 如果请求体为空（例如POST请求的body为空、或者GET请求），则填写空对象null或空字符串的Bytes值（例如，"".getBytes\("UTF-8"\)\)。

|

        -   返回值：byte\[\]类型，返回签名串。
        -   示例代码。客户端往服务器端发送数据时，需要调用avmpSign接口对整个body数据进行签名处理，之后得到签名串，这个签名串就是wToken。

            ```
            int VMP_SIGN_WITH_GENERAL_WUA2 = 3;
            String request_body = "i am the request body, encrypted or not!";
            byte[] result = jaqVMPComp.avmpSign(VMP_SIGN_WITH_GENERAL_WUA2, request_body.getBytes("UTF-8"));
            String wToken = new String(result, "UTF-8");
            Log.d("wToken", wToken);
            ```

4.  将wToken放进协议头。在HttpURLConnection类的对象中增加wToken字段的内容。示例代码如下：

    ```
    String request_body = "i am the request body, encrypted or not!";
    URL url = new URL("http://www.xxx.com");
    HttpURLConnection conn = (HttpURLConnection) url.openConnection();
    conn.setRequestMethod("POST");
    // set wToken info to header 
    conn.setRequestProperty("wToken", wToken);
    OutputStream os = conn.getOutputStream();
    // set request body info
    byte[] requestBody = request_body.getBytes("UTF-8");
    os.write(requestBody);
    os.flush();
    os.close();
    ```

5.  发送数据到服务器。将修改好协议头的数据发到App自有服务器，中间会由WAF截获，并解析wToken进行风险识别。

**说明：** 被签名的请求体应该跟客户端实际发送出来的请求体完全一样，完全一样的含义包括请求体中字符串的编码格式、空格、特殊字符以及参数的顺序等等，否则会造成验签失败。

## 错误码 {#section_u5x_lnq_p2b .section}

上述initialize和avmpSign接口有可能会出现异常。如果生成签名串异常或失败，请搜索 Log 中 “SecException” 相关的信息。

常见错误信息及描述见下表。

|错误代码|含义|
|1901|参数不正确，请检查输入的参数。|
|1902|图片文件有问题。一般是获取图片文件时的apk签名和当前程序的apk签名不一致。请使用当前程序的apk重新生成图片。iOS可能是应为BundleID不匹配。|
|1903|图片文件格式有问题。|
|1904|请升级新版本图片。AVMP签名功能仅支持v5图片。|
|1905|没有找到图片文件。请确保图片文件在res\\drawable目录下，AVMP相关的图片为：yw\_1222\_0335\_mwua.jpg。|
|1906|图片中缺少AVMP签名对应的byteCode。请检查使用的图片是否正确。|
|1907|初始化AVMP失败，请重试。|
|1910|非法的avmpInstance实例。可能原因如下：AVMPInstance是否被destroy后，调用InvokeAVMP。图片byteCode版本与SDK不匹配。|
|1911|加密图片的byteCode没有相应导出的函数。|
|1912|AVMP调用失败。请联系我们。|
|1913|AVMPInstance被destroy之后，调用InvokeAVMP出现该错误。|
|1915|AVMP调用内存不足，请重试。|
|1999|未知错误，请重试。|

## 常见问题：指定 shrinkResources 之后，密钥图片被优化掉了 {#section_cvx_lnq_p2b .section}

在Android Studio中，如果指定了shrinkResources为true，那么，在工程编译的时候会把没有在代码中引用的资源文件给优化掉。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15447822467855_zh-CN.png)

上述操作会使SDK中提供的两个jpg文件不能正常工作。如下图所示，打包出来的APK中，yw\_1222\_0335.jpg的配置文件大小为0KB，表明这个图片被优化掉了。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15447822467856_zh-CN.png)

**解决方法**

在工程的res目录下新建raw目录，在raw目录下创建keep.xml文件。在keep.xml中输入如下内容：

```
<?xml version="1.0" encoding="utf-8"?>
<resources xmlns:tools="http://schemas.android.com/tools"
tools:keep="@drawable/yw_1222_0335.jpg,@drawable/yw_1222_0335_mwua.jpg" />
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15447822467857_zh-CN.png)

添加完上述内容，重新编译工程apk即可。

## 集成效果确认 {#section_ivx_lnq_p2b .section}

参照以下步骤确认您的App已正确集成了WAF SDK。

1.  将打包出来的apk文件重命名成zip文件，然后用解压工具将该文件解压。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15447822477858_zh-CN.png)

2.  解压之后，定位到工程的lib目录，确保文件夹下只存在armeabi、armeabi-v7a、arm64-v8a文件夹。如果还有其他架构的文件夹，请参考[项目工程配置 步骤 4](https://help.aliyun.com/document_detail/62889.html?spm=a2c4g.11186623.6.591.FDq2Jl#%E9%A1%B9%E7%9B%AE%E5%B7%A5%E7%A8%8B%E9%85%8D%E7%BD%AE)，移除其他架构的文件夹。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15447822477859_zh-CN.png)

3.  定位到工程的res/drawable目录下，确保yw\_1222\_0335.jpg和yw\_1222\_0335\_mwua.jpg文件在其中，并且文件大小不为0。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15447822477860_zh-CN.png)

4.  通过打印日志，确保调用avmpSign接口之后能生成正确的签名信息。如果没有生成，则查看是否有错误码产生。

