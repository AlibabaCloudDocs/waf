# Android integration manual {#concept_wqs_5hq_p2b .concept}

This document describes the process of connecting to the WAF SDK using the Android app.

## Download the SDK package {#section_qsx_lnq_p2b .section}

Download and unzip the WAF SDK package. In the sdk-Android folder, you can see the following files:

**Note:** The aar file version numbers may be different.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15452066657849_en-US.png)

The description of these files is as follows \(xxx is the version number\):

|File|Description|
|----|-----------|
|SecurityGuardSDK-xxx.aar|Main framework SDK|
|AVMPSDK-xxx.aar|Virtual machine plugin|
|SecurityBodySDK-xxx.aar|Man/machine identification plugin|
|yw\_1222\_0335.jpg|Mainframe configuration file|
|yw\_1222\_0335\_mwua.jpg|Virtual machine engine configuration file|

## Procedure {#section_wsx_lnq_p2b .section}

Follow these steps to configure the project:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15452066667850_en-US.png)

1.  Import the aar files of the SDK to Android Studio. Copy all aar files from the SDK to the project’s libs directory. If the libs directory does not exist, create one.
2.  Open this Module’s build.gradle file, and add the following configuration to it \(as shown in ③ and ④\).
    -   Use the libs directory as the source for searching dependencies.

        ```
        repositories{
            flatDir {
                dirs 'libs'
            }
        }
        ```

    -   Add compilation dependencies.

        **Note:** The aar file version numbers here may be different with those of the files downloaded by you.

        ```
        dependencies {
            compile fileTree(include: ['*.jar'], dir: 'libs')
            compile ('com.android.support:appcompat-v7:23.0.0')
            compile (name:'AVMPSDK-external-release-xxx', ext:'aar')
            compile (name:'SecurityBodySDK-external-release-xxx', ext:'aar')
            compile (name:'SecurityGuardSDK-external-release-xxx', ext:'aar')
        }
        ```

3.  Import the jpg file into the drawable folder. Move the yw\_1222\_0335\_mwua.jpg and yw\_1222\_0335.jpg files from the SDK directory to the Android application project’s drawable directory.

    **Note:** If the drawable directory does not exist by default, create one.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15452066667851_en-US.png)

4.  Filter out ABI to remove redundant SO architectures. Currently, WAF SDK only provides SO in the armeabi architecture. Therefore, you must filter the exported ABIs. Otherwise, it may cause an App crash. The procedure is as follows:
    1.  Go to the Android project’s lib directory, and delete all CPU architecture folders apart from the armeabi folder, which include armeabi-v7a, x86, x86\_64, arm64-v8a, mips, and mips64. Make sure you keep only the armeabi, armeabi-v7a, and arm64-v8a folders.
    2.  Add a filter rule in the project’s build.gradle configuration file. Architectures specified by abiFilters are included in the APK. The sample code is as follows:

        **Note:** The armeabi architecture is specified in the following sample. You can also specify the armeabi-v7a or arm64-v8a architecture.

        ```
        defaultConfig {
            applicationId "com.xx.yy"
            minSdkVersion xx
            targetSdkVersion xx
            versionCode xx
            versionName "x.x.x"
            ndk {
                abiFilters "armeabi"
        // abiFilters "armeabi-v7a"
        // abiFilters "arm64-v8a"
            }
        }
        ```

        **Note:** Keeping only the SO in the armeabi architecture can remarkably reduce the App size without affecting the App’s compatibility.

5.  Add App permission.
    -   For an Android Studio project that uses the aar method integration, additional permission configuration is not necessary, because the relevant permissions are already specified in the aar files.
    -   For an Eclipse project, you must add the following permission configuration to the AndroidMenifest.xml file:

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

6.  Add ProGuard configuration. If you have used Proguard for obfuscation, then you must add the ProGuard configuration. Based on different access methods, the ProGuard configuration is divided into two types, which are Eclipse and AndrodStudio respectively.

    -   **Android Studio**

        If proguardFiles is configured in build.gradle and minifyEnabled is enabled, it means that the proguard-rules.pro configuration file is used for obfuscation, as shown in the following figure.

        ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/62889/cn_zh/1514354175536/ProGuard.png)

    -   **Eclipse**

        If the proguard configuration is specified in project.properties \(for example, the project.properties contains the following statement `proguard.config=proguard.cfg`\), it means that proguard is used for obfuscation. Obfuscation configuration in the proguard.cfg file is shown in the following figure.

        ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/62889/cn_zh/1514354275311/proguard.cfg.png)

    **Add keep rules**

    To make sure that certain classes are not obfuscated, you must add the following rules in the proguard configuration file.

    ```
    -keep class com.taobao.securityjni.**{*;}
    -keep class com.taobao.wireless.security.**{*;}
    -keep class com.ut.secbody.**{*;}
    -keep class com.taobao.dp.**{*;}
    -keep class com.alibaba.wireless.security. **{*;}
    ```


## Coding process {#section_xtx_lnq_p2b .section}

1.  Import SDK

    ```
    import com.alibaba.wireless.security.jaq.JAQException;
    import com.alibaba.wireless.security.jaq.avmp.IJAQAVMPSignComponent;
    import com.alibaba.wireless.security.open.SecurityGuardManager;
    import com.alibaba.wireless.security.open.avmp.IAVMPGenericComponent;
    ```

2.  Initialize SDK.
    -   Interface definition: `boolean initialize();`
    -   Interface description:
        -   Function: Initialize SDK.
        -   Parameter: N/A.
        -   Return value: Boolean type. Return value: Boolean type. True if the initialization is successful, and False if the initialization fails.
    -   Sample code:

        ```
        IJAQAVMPSignComponent jaqVMPComp = SecurityGuardManager.getInstance(getApplicationContext()).getInterface(IJAQAVMPSignComponent.class);
        boolean result = jaqVMPComp.initialize();
        ```

3.  Sign the request data
    -   Interface definition: `byte[] avmpSign(int signType, byte[] input);`
    -   Interface description:
        -   Function: Use the avmp technology to sign the input data, and return the signature string.
        -   Parameters:

            |Parameter Name|Type|Required|Description|
            |signType|int|Yes|Algorithm used by the signature. Currently, it is a fixed value. Enter 3.|
            |input|byte\[\]|No |Data to be signed, which is generally the entire request body. If the request body is empty, then enter null for this parameter.|

        -   Return value: byte\[\] type. The signature string is returned.
        -   Sample code: When the client sends data to the server, it must call the avmpSign interface to sign the entire body data and obtain the signature string \(the wToken\).

            ```
            int VMP_SIGN_WITH_GENERAL_WUA2 = 3;
            String request_body = "i am the request body, encrypted or not!" ;
            byte[] result = jaqVMPComp.avmpSign(VMP_SIGN_WITH_GENERAL_WUA2, request_body.getBytes("UTF-8"));
            String wToken = new String(result, "UTF-8");
            Log.d("wToken", wToken);
            ```

4.  Put the wToken in the protocol header Add the wToken field’s content to the HttpURLConnection class object. The sample code is as follows:

    ```
    String request_body = "i am the request body, encrypted or not!" ;
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

5.  Send data to the server. Send the data with the modified protocol header to the App’s self-owned server. WAF captures the data and parses the wToken for risk identification.

**Note:** The signed request body must be exactly the same as the request body sent from client.

## Error code {#section_u5x_lnq_p2b .section}

The preceding initialize and avmpSign interfaces may encounter exceptions. If you encounter an exception or error when generating the signature string, search “SecException” for related information in the log.

Common errors are listed as follows:

|Error Code|Meaning|
|1901|Incorrect parameter. Enter the correct parameter.|
|1902|Image file error. It generally indicates that the apk signature used to retrieve the image file is inconsistent with the current application’s apk signature. Use the current application’s apk to generate the image file. In iOS, it may be caused by inconsistent BundleIDs.|
|1903|Incorrect image format.|
|1904|Upgrade to new version images. AVMP signature function only supports v5 images.|
|1905|Unable to find the image file. Make sure that the image file is in the res\\drawable directory. The AVMP image is yw\_1222\_0335\_mwua.jpg.|
|1906|byteCode corresponding to the AVMP signature is missing in the image. Check if the image used is correct.|
|1907|Failed to initialize AVMP. Try again later.|
|1910|Invalid avmpInstance instance. Probable causes are: InvokeAVMP is called after AVMPInstance is destroyed. The image’s byteCode version does not match with that of the SDK.|
|1911|The encrypted image’s byteCode does not have the corresponding export function.|
|1912|AVMP calling fails. Submit a ticket for further assistance.|
|1913|This error occurs when calling InvokeAVMP after AVMPInstance is destroyed.|
|1915|AVMP calling out of memory. Try again later.|
|1999|Unknown error. Try again later.|

## FAQ: Secret key image is optimized away due to specifying shrinkResources. {#section_cvx_lnq_p2b .section}

In Android Studio, if you specify shrinkResources to be True, then resource files that are not referenced in the code are optimized away during project compilation.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15580/15452066667855_en-US.png)

As a result, the two jpg files provided in the SDK cannot work normally. In the following figure, the file size of yw\_1222\_0335.jpg is 0 KB, which means the image is optimized away.

![](images/7856_en-US.png)

**Resolution**

Create a raw folder under the project’s res directory, and then create a keep.xml file in the raw folder. Enter the following content to the keep.xml file:

```
<? xml version="1.0" encoding="utf-8"? >
<resources xmlns:tools="http://schemas.android.com/tools"
tools:keep="@drawable/yw_1222_0335.jpg,@drawable/yw_1222_0335_mwua.jpg" />
```

After that, re-compile the project apk.

## Test and validation {#section_ivx_lnq_p2b .section}

Follow these steps to check if your App is correctly integrated with WAF SDK:

1.  Change the suffix of the compressed apk file to zip, and decompress this zip file.
2.  Locate the project’s lib directory, and make sure that it contains only the armeabi folder. If you find folders for other architectures, delete them. For more information, see [Procedure step 4](https://help.aliyun.com/document_detail/62889.html?spm=a2c4g.11186623.6.591.FDq2Jl#%E9%A1%B9%E7%9B%AE%E5%B7%A5%E7%A8%8B%E9%85%8D%E7%BD%AE).
3.  Locate the project’s res/drawable directory, and make sure that the yw\_1222\_0335.jpg and yw\_1222\_0335\_mwua.jpg files are there, and the file sizes are not 0.
4.  Print the log, and make sure that the correct signature information is generated after the avmpSign interface is called. If the signature information cannot be generated, check the log for error codes.

