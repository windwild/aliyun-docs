### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用广场](https://help.aliyun.com/zh/model-studio/application-gallery/)[官方应用-多模态交互开发套件](https://help.aliyun.com/zh/model-studio/multimodal-products/)[SDK安装](https://help.aliyun.com/zh/model-studio/multimodal-sdk/)[移动端Android SDK](https://help.aliyun.com/zh/model-studio/multimodal-sdk-android/)使用 License 模式接入Android SDK

# 使用 License 模式接入Android SDK

更新时间：2026-02-11 02:09:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：移动端Android SDK](https://help.aliyun.com/zh/model-studio/multimodal-sdk-android/)[下一篇：移动端iOS SDK](https://help.aliyun.com/zh/model-studio/multimodal-sdk-ios/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

1\. 模式说明

1.1. 半托管模式

1.2. 全托管模式

2\. 使用前注意需了解事项

3\. 接口说明

3.1. SDK初始化 initialize

3.2. 半托管模式

3.3. 全托管模式

3.4. 获取License标识签名

3.5. 设备重置 deviceReset

4\. 集成依赖库

5\. 涉及多模态SDK接入修改

本文档指导开发者通过License模式集成Android SDK，实现设备管控和鉴权。多模态SDK需支持License计费模式，支持半托管和全托管两种接入模式。

## **1\. 模式说明**

使用 License 计费模式访问多模态交互开发套件需要集成 License SDK，请参考本文第 4 节集成 SDK。

### 1.1. 半托管模式

适用场景：客户自有云服务，能对自己的设备进行管理和鉴权，客户云服务和设备端有双向通信通道；

- 服务端开发：

  - 参考 [云端接口开发说明](https://help.aliyun.com/zh/model-studio/mmi-rtos-sdk#557a524795xam "") 完成云端接口对接，设备计量管理服务提供设备注册和获取Token两个接口
- 设备端开发：

  - 接入方通过本SDK的genRegisterReq接口获取设备注册签名。

  - 拿到设备注册签名后调用接入方自有云端服务进行设备注册，接入方云端需集成POP SDK。

  - 设备注册返回后调用本SDK的writeDeviceInfo接口写入设备信息。

  - 调用本SDK的genGetTokenReq接口获取访问令牌信息的数据签名。

  - 调用本SDK的getToken获取解签后业务交互令牌信息，之后可使用令牌信息进行业务交互。

### 1.2. 全托管模式

适用场景：客户没有云服务，无法对设备进行管理，由阿里云进行设备管理和鉴权

- 服务端开发：

  - 无
- 设备端开发

  - 调用本SDK的deviceRegister接口执行设备注册。

  - 调用本SDK的getToken接口获取业务交互令牌，之后可使用令牌信息进行业务交互。

## 2\. 使用前注意需了解事项

- 使用License模式前在百炼控制台创建了应用，并购买了License。

- SDK中封装了设备唯一标识生成逻辑并持久化数据到设备，避免同1设备重复注册，通过DeviceUUIDUtil.getAndroid(context)调用，请务必使用SDK中获取deviceName接口逻辑或者接入方自行保证deviceName唯一性。


## 3\. 接口说明

### 3.1. SDK初始化 initialize

半托管和全托管模式均需先执行初始化接口

**入参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| appId | String | 是 | 应用标识，在百炼控制台创建应用之后会生成该ID |
| appSecret | String | 是 | 应用密钥，在百炼控制台创建应用之后会生成该密钥 |
| deviceName | String | 是 | 设备名称：（使用设备WIFI MAC或唯一序列号） |
| callBack | InitCallBack | 是 | SDK初始化回调，参考InitCallBack对象 |

**InitCallBack对象**

| **返回值** | **方法名** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **返回值** | **方法名** | **说明** |
| void | success() | 初始化成功 |
| void | fail(ResultError error) | 初始化失败 |

**ResultError对象**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| code | int | 否 | 返回错误码 |
| message | String | 否 | 返回错误码说明 |

**出参：**

无

**调用示例**

```java
DeviceAuthClient.getInstance().initialize(new InitParams(APP_ID, APP_SECRET, mDeviceName), new InitCallBack() {
   @Override
   public void success() {
       Log.d(TAG, "initialize success");
   }
   @Override
   public void fail(ResultError resultError) {
       Log.e(TAG, "initialize fail: " + resultError.getMessage());
   }
});
```

### 3.2. 半托管模式

#### 3.2.1. 设备注册相关接口

##### 3.2.1.1. 生成设备注册信息 genRegisterReq

**入参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| appId | String | 是 | 应用标识，在百炼控制台创建应用之后会生成该ID |
| deviceName | String | 是 | 设备名称：（使用设备WIFI MAC或唯一序列号） |
| payMode | String | 是 | 计费方式：PAYG（后付费）、LICENSE（license计费） |
| reqNonce | String | 是 | 请求随机串，长度26位 |
| requestTime | String | 是 | 请求时间 |

**出参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| success | boolean | 是 | 请求处理是否成功 |
| code | int | 否 | 请求失败code |
| message | String | 否 | 请求失败描述 |
| data | String | 否 | 设备注册调用POP接口所需的签名参数 |

**调用示例：**

```java
DeviceRegisterInfo deviceRegisterInfo = new DeviceRegisterInfo();
deviceRegisterInfo.setAppId(APP_ID);
deviceRegisterInfo.setDeviceName(mDeviceName);
deviceRegisterInfo.setPayMode(PAY_MODE);
deviceRegisterInfo.setReqNonce(RandomUtil.generateRandomHexString(26));
deviceRegisterInfo.setRequestTime(String.valueOf(System.currentTimeMillis()));
Result<String> result = DeviceAuthClient.getInstance().genRegisterReq(deviceRegisterInfo);
if (result.isSuccess()) {
    Log.d(TAG, "genRegisterReq: " + result.getData());
}
```

##### 3.2.1.2. 写入设备注册信息 writeDeviceInfo

调用云端设备注册的pop接口得到的响应，需要再次传回设备端SDK，进行信息写入

**入参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| appId | String | 是 | 应用标识，在百炼控制台创建应用之后会生成该ID |
| deviceName | String | 是 | 设备名称：（使用设备WIFI MAC或唯一序列号） |
| reqNonce | String | 是 | 请求发起随机串，长度26位 |
| rspNonce | String | 是 | 返回数据的随机串，长度26位 |
| responseTime | String | 是 | 返回数据的时间戳 |
| signature | String | 是 | 设备三元组的签名-云端POP接口返回的signature |

**出参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| success | boolean | 是 | 请求处理是否成功 |
| code | int | 否 | 请求失败code |
| message | String | 否 | 请求失败描述 |
| data | String | 否 | 设备注册调用POP接口所需的签名参数 |

**调用示例：**

```java
DeviceRegisterRsp params = new DeviceRegisterRsp();
params.setAppId(APP_ID);
params.setDeviceName(mDeviceName);
params.setReqNonce("71c81300654ac7363d8c0166bd");
params.setRspNonce("0a7fd7628e4db7146bc2da09e3");
params.setResponseTime("1754630944192");
params.setSignature("mTZMp+gQF7lIY4zLXDx/90C3ZTn7hHVQ4XFc57fGBeMGOpMQy9/bOQL4cWx9f2SPXqgrLR5KExekyrZc4i4WuDQ/fjUktolQXLmBYODEK1QmqpcLhY78U+SHbgPtjkwuAK4Wci1V1f3LJNSsqlUFTqPV/u5DFAPwrkult6wGsTr5EaYDhm+e9N/mGUYOTEm6DHMZlFpUxjCb9VODKYgZOcaKnF+sp07XRziKT/8Rshhx");
Result<String> result = DeviceAuthClient.getInstance().writeDeviceInfo(params);
if (result.isSuccess()) {
    Log.d(TAG, "writeDeviceInfo success");
} else {
    Log.e(TAG, "writeDeviceInfo error: " + result.getMessage());
}
```

#### 3.2.2. 获取业务交互令牌相关接口

##### 3.2.2.1. 生成获取访问令牌信息 genGetTokenReq

**入参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| nonce | String | 是 | 请求随机串，长度26位 |
| appId | String | 是 | 应用标识，在百炼控制台创建应用之后会生成该ID |
| deviceName | String | 是 | 设备名称：（使用设备WIFI MAC或唯一序列号） |
| payMode | String | 是 | 计费方式：PAYG（后付费）、LICENSE（license计费） |
| tokenType | String | 是 | 请求令牌的类型（当前仅支持MMI类型）<br>MMI：多模态交互令牌 |
| requestTime | String | 是 | 请求时间戳,单位ms |

**出参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| success | boolean | 是 | 请求处理是否成功 |
| code | int | 否 | 请求失败code |
| message | String | 否 | 请求失败描述 |
| data | String | 否 | 设备注册调用POP接口所需的签名参数 |

```java
{
    "success": true,
    "data": "84uoRCyy6AG/SH7LrHjJW0D7lsBp/H4RReS7gJY5L0oC517xJWAmwtmghLjYkW/Qj4ZvK6vrM7QC5yxtMl3TQLHdAGSsqQLb0bP6zKOiDzoNFwqs61+GMQ7guTPjbE9Fqaf7"
}
```

**调用示例：**

```codeblock
GenGetTokenParams params = new GenGetTokenParams();
params.setNonce(RandomUtil.generateRandomHexString(26));
params.setAppId(APP_ID);
params.setDeviceName(mDeviceName);
params.setPayMode(PAY_MODE);
params.setTokenType("MMI");
params.setRequestTime(String.valueOf(System.currentTimeMillis()));
Result<String> result = DeviceAuthClient.getInstance().genGetTokenReq(params);
if (result.isSuccess()) {
    Log.d(TAG, "getTokenSign: " + result.getData());
}
```

##### 3.2.2.2. 解签POP接口返回的token数据 getToken

**入参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| appId | String | 是 | 应用标识，在百炼控制台创建应用之后会生成该ID |
| deviceName | String | 是 | 设备名称：（使用设备WIFI MAC或唯一序列号） |
| reqNonce | String | 是 | 请求随机串，长度26位 |
| rspNonce | String | 是 | 返回数据的随机串，长度26位 |
| responseTime | String | 是 | 返回数据的时间戳 |
| signature | String | 是 | 获取token返回数据的签名数据 |

**出参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| success | boolean | 是 | 请求处理是否成功 |
| code | int | 否 | 请求失败code |
| message | String | 否 | 请求失败描述 |
| data | String | 否 | 返回解签后的数据 |

**调用示例：**

```java
AnalyzeTokenSignRsp tokenSignRsp = new AnalyzeTokenSignRsp();
tokenSignRsp.setAppId(APP_ID);
tokenSignRsp.setDeviceName(mDeviceName);
tokenSignRsp.setReqNonce("7e7c8ab3f1fca9bccba25b8065");
tokenSignRsp.setRspNonce("f59dea8a8c35495ca355702aba");
tokenSignRsp.setResponseTime("1754638402957");
tokenSignRsp.setSignature("dW7+vOFoxf6XOQMDd5tt1Q87I7uxcfj9t12Qv9a+1cfUBfF3oEKLetHo7UD611m6SSRVJB6iyPmk6XHvfx3REvfheP92rxxxnDNfI74WR54uIWTX2eJHiZJvblvR3/C/a5+vo2Vzq0m6XhJoXrXuo6TkJstQRPBa1YRqQ8Y8TnDjxUL9G5QDWSYmCzTCr9Zr6oF6I2ZWw8HSCWzqkI0lMV6/Aj5lU0CalCt2qlGGfTSCpY9gh92pFtsKsBvEWX4zWO4ox6eWCv+CmK9DcEMfLJgTNRIuJh7IMwqweF4QzOcYqQxtvZ0gGEPOpQJoA3TQ/2v3GMmzaoVv0KiSQ/02kgW4oiYvyLOz+CLfbXwXGfAT+iJwFgYsfATWYaph31UKVdW7KTYtcmAP");
Result<String> result = DeviceAuthClient.getInstance().getToken(tokenSignRsp);
if (result.isSuccess()) {
    Log.d(TAG, "analyzeTokenSign: " + result.getData());
}
```

### 3.3. 全托管模式

#### 3.3.1. 检查设备是否注册 deviceIsRegistered

**入参：**

**无**

**出参：**

设备是否注册

**调用示例：**

```codeblock
boolean deviceIsRegistered = DeviceAuthClient.getInstance().deviceIsRegistered();
```

#### 3.3.2. 设备注册 deviceRegister

**入参：**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| params | Object | 是 | 设备注册入参对象，参考DeviceRegisterParams对象 |
| callBack | DeviceRegisterCallBack | 是 | 设备注册回调 |

**DeviceRegisterParams对象**

| **字段** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **必填** | **说明** |
| nonce | String | 是 | 请求随机串，长度26位 |
| appId | String | 是 | 应用标识，在百炼控制台创建应用之后会生成该ID |
| deviceName | String | 是 | 设备名称：（使用设备WIFI MAC或唯一序列号） |
| requestTime | String | 是 | 请求时间 |
| payMode | String | 是 | 计费方式：PAYG（后付费）、LICENSE（license计费） |

**出参：**

无

**调用示例：**

```codeblock
DeviceRegisterParams params = new DeviceRegisterParams();
ams.setNonce(RandomUtil.generateRandomHexString(26));
ams.setAppId(APP_ID);
ams.setDeviceName(mDeviceName);
ams.setRequestTime(String.valueOf(System.currentTimeMillis()));
ams.setPayMode(PAY_MODE);
iceAuthClient.getInstance().deviceRegister(params, new DeviceRegisterCallBack() {
 @Override
 public void success() {
     Log.d(TAG, "deviceRegister success");
 }
 @Override
 public void fail(ResultError error) {
     Log.e(TAG, error.getMessage());
 }
});
```

#### 3.3.3. 获取业务交互令牌 getToken

**入参：**

| **字段** | **类型** | **默认值** | **必填** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **字段** | **类型** | **默认值** | **必填** | **说明** |
| params | Object | - | 是 | 设备认证所需参数对象，参考GenGetTokenParams对象 |
| callBack | GetTokenCallBack | - | 是 | 获取token回调，参考GetTokenCallBack<br>对象 |

**GenGetTokenParams对象**

| **字段** | **类型** | **默认值** | **必填** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **字段** | **类型** | **默认值** | **必填** | **说明** |
| nonce | String | - | 是 | 16字节随机数（26字符) |
| appId | String | - | 是 | 应用标识，在百炼控制台创建应用之后会生成该ID |
| apiKey | String | - | 是 | 应用密钥，在百炼控制台密钥管理创建 |
| deviceName | String | - | 是 | 设备唯一标识 |
| requestTime | String | - | 是 | 请求时间戳（ms） |
| payMode | String | - | 是 | 计费方式：PAYG（后付费）、LICENSE（license计费） |
| tokenType | String | - | 是 | 请求令牌的类型（当前仅支持MMI类型）<br>MMI：多模态交互令牌 |

**出参：**

无

**调用示例：**

```java
GenGetTokenParams params = new GenGetTokenParams();
params.setNonce(RandomUtil.generateRandomHexString(26));
params.setAppId(APP_ID);
params.setDeviceName(mDeviceName);
params.setRequestTime(String.valueOf(System.currentTimeMillis()));
params.setPayMode(PAY_MODE);
params.setTokenType("MMI");
DeviceAuthClient.getInstance().getToken(params, new GetTokenCallBack() {
    @Override
    public void success(String tokenInfo) {
        Log.d(TAG, "getToken success: " + tokenInfo);
    }
    @Override
    public void fail(ResultError error) {
        Log.e(TAG, error.getMessage());
    }
});
```

### 3.4. 获取License标识签名

**入参：**

| **字段** | **类型** | **默认值** | **必填** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **字段** | **类型** | **默认值** | **必填** | **说明** |
| params | Object | - | 是 | 设备认证所需参数对象，参考LicenseSignatureParams对象 |

**LicenseSignatureParams对象**

| **字段** | **类型** | **默认值** | **必填** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **字段** | **类型** | **默认值** | **必填** | **说明** |
| appId | String | - | 是 | 应用标识，在百炼控制台创建应用之后会生成该ID |
| deviceName | String | - | 是 | 设备唯一标识 |
| taskId | String | - | 是 | 本次连接唯一标识，用于在工程链路上跟踪任务执行。由客户端生成，格式建议为36位uuid字符串，格式示例："f894c16f-f20e-4c1d-837e-89e0fbc63a43" |

**出参：**

| **字段** | **类型** | **默认值** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **默认值** | **说明** |
| timestamp | String | - | 当前时间戳ms |
| license\_info | String | - | license\_info签名信息 |
| device\_info | String | - | device\_info签名信息 |

**调用示例：**

```codeblock
/// 获取license标识签名
String taskId = UUID.randomUUID().toString().replace("-", "");
LicenseSignatureParams params = new LicenseSignatureParams(authParams.getAppid(), deviceName, taskId);
JSONObject licenseInfoSignature = DeviceAuthClient.getInstance().getLicenseSignature(params);
// 返回包含timestamp和license_info、device_info的JSON字符串
```

### 3.5. 设备重置 deviceReset

tips: 在百炼控制台重置设备后，需要调用SDK deviceReset接口重置设备，可以进行重新注册。

**入参：**

无

**出参：**

Boolean 是否重置成功

**调用示例：**

```java
boolean result = DeviceAuthClient.getInstance().deviceReset();
 if (!result) {
     showToast("设备重置失败");
 } else {
     showToast("设备重置成功，可以重新注册");
 }
```

## 4\. 集成依赖库

使用最新版本 Android SDK，引用其中的multimodal\_dialog\_tongyimetathings-1.0.1.aar

## 5\. 涉及多模态SDK接入修改

1. 在启动会话前完成tongyimetathings SDK的初始化和检测设备是否注册，未注册执行设备注册，具体参考接入示例工程。

2. 初始化该SDK，设备注册完成后获取多模态会话token，参考上述2.1，2.3接口，将getToken接口返回的dashToken数据设置为apiKey，具体参考示例工程。


```java
multimodalParams.setApiKey(jsonObject.getString("dashToken"));
```

3. 创建会话时传入license计费标识,参考接入示例：


```java
private MultiModalRequestParam buildRequestParams() {

MultiModalRequestParam.UpStream.ReplaceWord replaceWord = new MultiModalRequestParam.UpStream.ReplaceWord();
replaceWord.setTarget("一加一");
replaceWord.setSource("1加1");
replaceWord.setMatchMode("partial");
String deviceName = com.aliyun.bailian.billingsignature.utils.DeviceUtil.getAndroidId(this);
taskId = UUID.randomUUID().toString().replace("-", "");
//构建License计费标识
LicenseSignatureParams params = new LicenseSignatureParams(authParams.getAppid(), deviceName, taskId);
JSONObject licenseInfoSignature = DeviceAuthClient.getInstance().getLicenseSignature(params);
Map<String, Object> map = new HashMap<>();
map.put("signature", licenseInfoSignature);
return MultiModalRequestParam.builder()
        .clientInfo(MultiModalRequestParam.ClientInfo.builder()
                .device(MultiModalRequestParam.ClientInfo.Device.builder()
                        .uuid(deviceName).build()) // 请配置为您的设备UUID
                .userId("123")  //userid 需要每个用户唯一，建议使用设备UUID。 对话历史会使用 userId关联
                .passThroughParams(map) //传入License计费标识
                .build())
        .upStream(MultiModalRequestParam.UpStream.builder()
                .mode(authParams.getDialogMode().getValue())
                .type("AudioAndVideo")
                .asrPostProcessing(Collections.singletonList(replaceWord))
                .build())
        .downStream(MultiModalRequestParam.DownStream.builder()
                .voice(mVoiceType) //tts 音色对应的模型需要和管控台配置的模型一致。longxiaochun_v2对应了cosyvoice_v2
                .sampleRate(48000)
                .intermediateText(textStreamFeedback ? "dialog" : "transcript")
                .build())
        .build();
}

```