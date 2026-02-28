### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[录音文件识别闲时版](https://help.aliyun.com/zh/isi/developer-reference/recording-file-recognition-off-peak-edition/)[调用示例](https://help.aliyun.com/zh/isi/developer-reference/sample-code-1/)Java Demo

# Java Demo

更新时间：2025-01-16 05:13:40

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference)[下一篇：C++ Demo](https://help.aliyun.com/zh/isi/developer-reference/c-demo)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

SDK说明

Java依赖

示例说明

鉴权

录音文件识别请求调用接口

录音文件识别结果查询

示例代码

常见问题

如何结合SDK日志分析延迟问题？

Java SDK找不到com.alibaba的JAR包，如何安装Alibaba Cloud SDK for Java？

Java SDK通过传入阿里云账号的AccessKey ID和AccessKey Secret，调用阿里云Java SDK得到client提示错误org.json.JSONArray.iterator()Ljava/util/Iterator如何解决？

本文介绍如何使用阿里云智能语音服务提供的Java SDK，包括SDK的安装方法及SDK代码示例。

## 前提条件

- 使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference#topic-2170103 "")。

- 已开通智能语音交互并获取AccessKey ID和AccessKey Secret，详情请参见 [从这里开始](https://help.aliyun.com/zh/isi/getting-started/start-here "")。


## SDK说明

录音文件识别的Java示例使用了阿里云Java SDK的CommonRequest提交录音文件识别请求和识别结果查询，采用的是RPC风格的POP API调用。阿里云Java SDK CommonRequest的使用方法请参见 [使用CommonRequest进行调用](https://help.aliyun.com/document_detail/61469.html#concept-ivk-p1k-zdb "")。

**重要**

阿里云Java SDK不支持Android开发。

### Java依赖

您只需依赖阿里云Java SDK的核心库与阿里巴巴开源库fastjson。阿里云Java SDK的核心库版本支持3.5.0及以上（如果版本在4.0.0及以上，需要根据错误提示补充对应的第三方依赖）。

```xml
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>3.7.1</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.83</version>
</dependency>
```

## 示例说明

- [下载nls-sample-16k.wav](https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav)。示例中使用的WAV录音文件为PCM编码格式16000 Hz采样率，模型设置为通用模型。

- 调用接口前，需配置环境变量，通过环境变量读取访问凭证。智能语音交互的AccessKey ID、AccessKey Secret和AppKey的环境变量名： **ALIYUN\_AK\_ID**、 **ALIYUN\_AK\_SECRET**、 **NLS\_APP\_KEY**。


### 鉴权

通过传入阿里云账号的AccessKey ID和AccessKey Secret（获取方式请参见 [开通服务](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1#topic-2572187 "")），调用阿里云Java SDK得到client，示例如下：

```java
final String accessKeyId = System.getenv().get("ALIYUN_AK_ID");
final String accessKeySecret = System.getenv().get("ALIYUN_AK_SECRET");
/**
 * 地域ID
 */
final String regionId = "cn-shanghai";
final String endpointName = "cn-shanghai";
final String product = "SpeechFileTranscriberLite";
final String domain = "speechfiletranscriberlite.cn-shanghai.aliyuncs.com";

IAcsClient client;
// 设置endpoint
DefaultProfile.addEndpoint(endpointName, regionId, product, domain);
// 创建DefaultAcsClient实例并初始化
DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
client = new DefaultAcsClient(profile);
```

### 录音文件识别请求调用接口

Java 示例采用轮询的方式，提交录音文件识别请求，获取任务ID，供后续轮询使用。

**说明**

参数设置请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference-2#topic-2572231 "")，只需设置JSON字符串中的参数，其他方法的参数值保持不变。

```java
/**
 * 创建CommonRequest 设置请求参数
 */
CommonRequest postRequest = new CommonRequest();
postRequest.setDomain("speechfiletranscriberlite.cn-shanghai.aliyuncs.com"); // 设置域名，固定值。
postRequest.setVersion("2021-12-21");         // 设置API的版本号，固定值。
postRequest.setAction("SubmitTask");          // 设置action，固定值。
postRequest.setProduct("SpeechFileTranscriberLite");      // 设置产品名称，固定值。
// 设置录音文件识别请求参数，以JSON字符串的格式设置到请求Body中。
JSONObject taskObject = new JSONObject();
taskObject.put("appkey", "您的appkey");    // 项目的Appkey，获取Appkey请前往控制台：https://nls-portal.console.aliyun.com/applist
taskObject.put("file_link", "您的录音文件访问链接");  // 设置录音文件的链接
String task = taskObject.toJSONString();
postRequest.putBodyParameter("Task", task);  // 设置以上JSON字符串为Body参数。
postRequest.setMethod(MethodType.POST);      // 设置为POST方式请求。
// postRequest.setHttpContentType(FormatType.JSON);    //当aliyun-java-sdk-core 版本为4.6.0及以上时，请取消该行注释
/**
 * 提交录音文件识别请求
 */
String taskId = "";   // 获取录音文件识别请求任务的ID，以供识别结果查询使用。
CommonResponse postResponse = client.getCommonResponse(postRequest);
if (postResponse.getHttpStatus() == 200) {
    JSONObject result = JSONObject.parseObject(postResponse.getData());
    String statusText = result.getString("StatusText");
    if ("SUCCESS".equals(statusText)) {
        System.out.println("录音文件识别请求成功响应： " + result.toJSONString());
        taskId = result.getString("TaskId");
    }
    else {
        System.out.println("录音文件识别请求失败： " + result.toJSONString());
        return;
    }
}
else {
    System.err.println("录音文件识别请求失败，Http错误码：" + postResponse.getHttpStatus());
    System.err.println("录音文件识别请求失败响应：" + JSONObject.toJSONString(postResponse));
    return;
}
```

### 录音文件识别结果查询

使用获取的任务ID，查询录音文件识别的结果。

```java
/**
 * 创建CommonRequest，设置任务ID。
 */
CommonRequest getRequest = new CommonRequest();
getRequest.setDomain("speechfiletranscriberlite.cn-shanghai.aliyuncs.com");   // 设置域名，固定值。
getRequest.setVersion("2021-12-21");             // 设置API版本，固定值。
getRequest.setAction("GetTaskResult");           // 设置action，固定值。
getRequest.setProduct("SpeechFileTranscriberLite");          // 设置产品名称，固定值。
getRequest.putQueryParameter("TaskId", taskId);  // 设置任务ID为查询参数。
getRequest.setMethod(MethodType.GET);            // 设置为GET方式的请求。
/**
 * 提交录音文件识别结果查询请求
 * 以轮询的方式进行识别结果的查询，直到服务端返回的状态描述为“SUCCESS”、“SUCCESS_WITH_NO_VALID_FRAGMENT”，或者为错误描述，则结束轮询。
 */
String statusText = "";
while (true) {
    CommonResponse getResponse = client.getCommonResponse(getRequest);
    if (getResponse.getHttpStatus() != 200) {
        System.err.println("识别结果查询请求失败，Http错误码： " + getResponse.getHttpStatus());
        System.err.println("识别结果查询请求失败： " + getResponse.getData());
        break;
    }
    JSONObject result = JSONObject.parseObject(getResponse.getData());
    System.out.println("识别查询结果：" + result.toJSONString());
    statusText = result.getString("StatusText");
    if ("RUNNING".equals(statusText) || "QUEUEING".equals(statusText)) {
        // 继续轮询
        Thread.sleep(3000);
    }
    else {
        break;
    }
}
if ("SUCCESS".equals(statusText) || "SUCCESS_WITH_NO_VALID_FRAGMENT".equals(statusText)) {
    System.out.println("录音文件识别成功！");
}
else {
    System.err.println("录音文件识别失败！");
}
```

## 示例代码

调用接口前，需配置环境变量，通过环境变量读取访问凭证。智能语音交互的AccessKey ID、AccessKey Secret和AppKey的环境变量名： **ALIYUN\_AK\_ID**、 **ALIYUN\_AK\_SECRET**、 **NLS\_APP\_KEY**。

```java
import com.alibaba.fastjson.JSONObject;
import com.aliyuncs.CommonRequest;
import com.aliyuncs.CommonResponse;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.http.MethodType;
import com.aliyuncs.profile.DefaultProfile;
public class FileTransJavaDemo {
    // 地域ID，常量，固定值。
    public static final String REGIONID = "cn-shanghai";
    public static final String ENDPOINTNAME = "cn-shanghai";
    public static final String PRODUCT = "SpeechFileTranscriberLite";
    public static final String DOMAIN = "speechfiletranscriberlite.cn-shanghai.aliyuncs.com";
    public static final String API_VERSION = "2021-12-21";
    public static final String POST_REQUEST_ACTION = "SubmitTask";
    public static final String GET_REQUEST_ACTION = "GetTaskResult";
    // 请求参数
    public static final String KEY_APP_KEY = "appkey";
    public static final String KEY_FILE_LINK = "file_link";
    public static final String KEY_VERSION = "version";
    public static final String KEY_ENABLE_WORDS = "enable_words";
    // 响应参数
    public static final String KEY_TASK = "Task";
    public static final String KEY_TASK_ID = "TaskId";
    public static final String KEY_STATUS_TEXT = "StatusText";
    public static final String KEY_RESULT = "Result";
    // 状态值
    public static final String STATUS_SUCCESS = "SUCCESS";
    private static final String STATUS_RUNNING = "RUNNING";
    private static final String STATUS_QUEUEING = "QUEUEING";
    // 阿里云鉴权client
    IAcsClient client;
    public FileTransJavaDemo(String accessKeyId, String accessKeySecret) {
        // 设置endpoint
        try {
            DefaultProfile.addEndpoint(ENDPOINTNAME, REGIONID, PRODUCT, DOMAIN);
        } catch (ClientException e) {
            e.printStackTrace();
        }
        // 创建DefaultAcsClient实例并初始化
        DefaultProfile profile = DefaultProfile.getProfile(REGIONID, accessKeyId, accessKeySecret);
        this.client = new DefaultAcsClient(profile);
    }
    public String submitFileTransRequest(String appKey, String fileLink) {
        /**
         * 1. 创建CommonRequest，设置请求参数。
         */
        CommonRequest postRequest = new CommonRequest();
        // 设置域名
        postRequest.setDomain(DOMAIN);
        // 设置API的版本号，格式为YYYY-MM-DD。
        postRequest.setVersion(API_VERSION);
        // 设置action
        postRequest.setAction(POST_REQUEST_ACTION);
        // 设置产品名称
        postRequest.setProduct(PRODUCT);
        /**
         * 2. 设置录音文件识别请求参数，以JSON字符串的格式设置到请求Body中。
         */
        JSONObject taskObject = new JSONObject();
        // 设置appkey
        taskObject.put(KEY_APP_KEY, appKey);
        // 设置音频文件访问链接
        taskObject.put(KEY_FILE_LINK, fileLink);
        // 设置是否输出词信息，默认为false。
        taskObject.put(KEY_ENABLE_WORDS, true);
        String task = taskObject.toJSONString();
        System.out.println(task);
        // 设置以上JSON字符串为Body参数。
        postRequest.putBodyParameter(KEY_TASK, task);
        // 设置为POST方式的请求。
        postRequest.setMethod(MethodType.POST);
        // postRequest.setHttpContentType(FormatType.JSON);    //当aliyun-java-sdk-core 版本为4.6.0及以上时，请取消该行注释
        /**
         * 3. 提交录音文件识别请求，获取录音文件识别请求任务的ID，以供识别结果查询使用。
         */
        String taskId = null;
        try {
            CommonResponse postResponse = client.getCommonResponse(postRequest);
            System.err.println("提交录音文件识别请求的响应：" + postResponse.getData());
            if (postResponse.getHttpStatus() == 200) {
                JSONObject result = JSONObject.parseObject(postResponse.getData());
                String statusText = result.getString(KEY_STATUS_TEXT);
                if (STATUS_SUCCESS.equals(statusText)) {
                    taskId = result.getString(KEY_TASK_ID);
                }
            }
        } catch (ClientException e) {
            e.printStackTrace();
        }
        return taskId;
    }
    public String getFileTransResult(String taskId) {
        /**
         * 1. 创建CommonRequest，设置任务ID。
         */
        CommonRequest getRequest = new CommonRequest();
        // 设置域名
        getRequest.setDomain(DOMAIN);
        // 设置API版本
        getRequest.setVersion(API_VERSION);
        // 设置action
        getRequest.setAction(GET_REQUEST_ACTION);
        // 设置产品名称
        getRequest.setProduct(PRODUCT);
        // 设置任务ID为查询参数
        getRequest.putQueryParameter(KEY_TASK_ID, taskId);
        // 设置为GET方式的请求
        getRequest.setMethod(MethodType.GET);
        /**
         * 2. 提交录音文件识别结果查询请求
         * 以轮询的方式进行识别结果的查询，直到服务端返回的状态描述为“SUCCESS”或错误描述，则结束轮询。
         */
        String result = null;
        while (true) {
            try {
                CommonResponse getResponse = client.getCommonResponse(getRequest);
                System.err.println("识别查询结果：" + getResponse.getData());
                if (getResponse.getHttpStatus() != 200) {
                    break;
                }
                JSONObject rootObj = JSONObject.parseObject(getResponse.getData());
                String statusText = rootObj.getString(KEY_STATUS_TEXT);
                if (STATUS_RUNNING.equals(statusText) || STATUS_QUEUEING.equals(statusText)) {
                    // 继续轮询，注意设置轮询时间间隔。
                    Thread.sleep(10000);
                }
                else {
                    // 状态信息为成功，返回识别结果；状态信息为异常，返回空。
                    if (STATUS_SUCCESS.equals(statusText)) {
                        result = rootObj.getString(KEY_RESULT);
                       // 状态信息为成功，但没有识别结果，则可能是由于文件里全是静音、噪音等导致识别为空。
                        if(result == null) {
                            result = "";
                        }
                    }
                    break;
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        return result;
    }
    public static void main(String args[]) throws Exception {
        final String accessKeyId = System.getenv().get("ALIYUN_AK_ID");
        final String accessKeySecret = System.getenv().get("ALIYUN_AK_SECRET");
        final String appKey = System.getenv().get("NLS_APP_KEY");
        String fileLink = "https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav";
        FileTransJavaDemo demo = new FileTransJavaDemo(accessKeyId, accessKeySecret);
        // 第一步：提交录音文件识别请求，获取任务ID用于后续的识别结果轮询。
        String taskId = demo.submitFileTransRequest(appKey, fileLink);
        if (taskId != null) {
            System.out.println("录音文件识别请求成功，task_id: " + taskId);
        }
        else {
            System.out.println("录音文件识别请求失败！");
            return;
        }
        // 第二步：根据任务ID轮询识别结果。
        String result = demo.getFileTransResult(taskId);
        if (result != null) {
            System.out.println("录音文件识别结果查询成功：" + result);
        }
        else {
            System.out.println("录音文件识别结果查询失败！");
        }
    }
}
```

**说明**

如果使用回调方式，请设置如下`enable_callback`、`callback_url`参数：

```java
taskObject.put("enable_callback", true);
taskObject.put("callback_url", "回调地址");
```

回调服务示例：该服务用于回调方式获取识别结果，假设设置回调地址为 **http://ip:port/filetrans/callback/result**。

```java
package com.example.filetrans;

import com.alibaba.fastjson.JSONObject;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

import java.util.regex.Matcher;
import java.util.regex.Pattern;
@RequestMapping("/filetrans/callback")
@RestController
public class FiletransCallBack {
    // 以4开头的状态码是客户端错误。
    private static final Pattern PATTERN_CLIENT_ERR = Pattern.compile("4105[0-9]*");
    // 以5开头的状态码是服务端错误。
    private static final Pattern PATTERN_SERVER_ERR = Pattern.compile("5105[0-9]*");
    // 必须是post方式
    @RequestMapping(value = "result", method = RequestMethod.POST)
    public void GetResult(@RequestBody String body) {
        System.out.println("body: " + body);
        try {
            // 获取JSON格式的文件识别结果。
            String result = body;
            JSONObject jsonResult = JSONObject.parseObject(result);
            // 解析并输出相关结果内容。
            System.out.println("获取文件中转写回调结果:" + result);
            System.out.println("TaskId: " + jsonResult.getString("TaskId"));
            System.out.println("StatusCode: " + jsonResult.getString("StatusCode"));
            System.out.println("StatusText: " + jsonResult.getString("StatusText"));
            Matcher matcherClient = PATTERN_CLIENT_ERR.matcher(jsonResult.getString("StatusCode"));
            Matcher matcherServer = PATTERN_SERVER_ERR.matcher(jsonResult.getString("StatusCode"));
            // 以2开头状态码为正常状态码，回调方式正常状态只返回“21050000”。
            if("21050000".equals(jsonResult.getString("StatusCode"))) {
                System.out.println("RequestTime: " + jsonResult.getString("RequestTime"));
                System.out.println("SolveTime: " + jsonResult.getString("SolveTime"));
                System.out.println("BizDuration: " + jsonResult.getString("BizDuration"));
                System.out.println("Result.Sentences.size: " +
                    jsonResult.getJSONObject("Result").getJSONArray("Sentences").size());
                for (int i = 0; i < jsonResult.getJSONObject("Result").getJSONArray("Sentences").size(); i++) {
                    System.out.println("Result.Sentences[" + i + "].BeginTime: " +
                        jsonResult.getJSONObject("Result").getJSONArray("Sentences").getJSONObject(i).getString("BeginTime"));
                    System.out.println("Result.Sentences[" + i + "].EndTime: " +
                        jsonResult.getJSONObject("Result").getJSONArray("Sentences").getJSONObject(i).getString("EndTime"));
                    System.out.println("Result.Sentences[" + i + "].SilenceDuration: " +
                        jsonResult.getJSONObject("Result").getJSONArray("Sentences").getJSONObject(i).getString("SilenceDuration"));
                    System.out.println("Result.Sentences[" + i + "].Text: " +
                        jsonResult.getJSONObject("Result").getJSONArray("Sentences").getJSONObject(i).getString("Text"));
                    System.out.println("Result.Sentences[" + i + "].ChannelId: " +
                        jsonResult.getJSONObject("Result").getJSONArray("Sentences").getJSONObject(i).getString("ChannelId"));
                    System.out.println("Result.Sentences[" + i + "].SpeechRate: " +
                        jsonResult.getJSONObject("Result").getJSONArray("Sentences").getJSONObject(i).getString("SpeechRate"));
                    System.out.println("Result.Sentences[" + i + "].EmotionValue: " +
                        jsonResult.getJSONObject("Result").getJSONArray("Sentences").getJSONObject(i).getString("EmotionValue"));
                }
            }
            else if(matcherClient.matches()) {
                System.out.println("状态码以4开头表示客户端错误......");
            }
            else if(matcherServer.matches()) {
                System.out.println("状态码以5开头表示服务端错误......");
            }
            else {
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 常见问题

### 如何结合SDK日志分析延迟问题？

以Java SDK日志为例。

- 一句话识别的延迟为一句话说完开始，到收到最终识别结果为止，消耗的时间。

在日志中搜索关键字`StopRecognition`以及`RecognitionCompleted`，分别找到语音发送完毕时的日志，以及一句话识别结束的日志。记录的时间差即为SDK端记录的一句话延时，如下日志延迟为：984-844=140（ms）。















```java
14:24:44.844 DEBUG [           main] [c.a.n.c.transport.netty4.NettyConnection] thread:1,send:{"header":{"namespace":"SpeechRecognizer","name":"StopRecognition","message_id":"bccac69b505f4e2897d12940e5b38953","appkey":"FWpPCaVYDRp6J1rO","task_id":"8c5c28d9a40c4a229a5345c09bc9c968"}}
14:24:44.984 DEBUG [ntLoopGroup-2-1] [  c.a.n.c.p.asr.SpeechRecognizerListener] on message:{"header":{"namespace":"SpeechRecognizer","name":"RecognitionCompleted","status":20000000,"message_id":"2869e93427b9429190206123b7a3d397","task_id":"8c5c28d9a40c4a229a5345c09bc9c968","status_text":"Gateway:SUCCESS:Success."},"payload":{"result":"北京的天气。","duration":2959}}
```

- 语音合成关注首包延迟，即从发送合成请求开始，到收到第一个语音包为止，消耗的时间。

日志中搜索关键字`send`，找到这条日志和紧随其后的一条收到语音包的日志。记录的时间差即为SDK端记录的首包延时。如下日志延时为1035-813=222（ms）。















```java
14:32:13.813 DEBUG [           main] [c.a.n.c.transport.netty4.NettyConnection] thread:1,send:{"payload":{"volume":50,"voice":"Ruoxi","sample_rate":8000,"format":"wav","text":"国家是由领土、人民、文化和政府四个要素组成的，国家也是政治地理学名词。从广义的角度，国家是指拥有共同的语言、文化、血统、领土、政府或者历史等的社会群体。从狭义的角度，国家是一定范围内的人群所形成的共同体形式。"},"context":{"sdk":{"name":"nls-sdk-java","version":"2.1.0"},"network":{"upgrade_cost":160,"connect_cost":212}},"header":{"namespace":"SpeechSynthesizer","name":"StartSynthesis","message_id":"6bf2a84444434c0299974d8242380d6c","appkey":"FWpPCaVYDRp6J1rO","task_id":"affa5c90986e4378907fbf49eddd283a"}}
14:32:14.035  INFO [ntLoopGroup-2-1] [  c.a.n.c.protocol.tts.SpeechSynthesizer] write array:6896
```

- 实时语音识别SDK日志类似一句话识别，可以从日志中计算语音末尾处延迟（关键字：`StopTranscription`和`TranscriptionCompleted`）。

- RESTful形式访问，客户端自带日志中没有体现延迟。需要用户自己编写代码，或者查看服务端日志。


### Java SDK找不到com.alibaba的JAR包，如何安装Alibaba Cloud SDK for Java？

请参见 [V1.0 Java SDK](https://help.aliyun.com/zh/sdk/developer-reference/v1-0-java-sdk/ "") 安装Alibaba Cloud SDK for Java。

### Java SDK通过传入阿里云账号的AccessKey ID和AccessKey Secret，调用阿里云Java SDK得到client提示错误org.json.JSONArray.iterator()Ljava/util/Iterator如何解决？

请确认依赖包是否完整，查找并添加如下两个依赖JAR包。

```xml
<dependency>
<groupId>org.json</groupId>
<artifactId>json</artifactId>
<version>20170516</version>
</dependency>

<dependency>
<groupId>com.google.code.gson</groupId>
<artifactId>gson</artifactId>
<version>2.8.2</version>
</dependency>
```