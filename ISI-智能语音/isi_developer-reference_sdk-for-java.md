### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[一句话识别](https://help.aliyun.com/zh/isi/developer-reference/short-sentence-recognition/)Java SDK

# Java SDK

更新时间：2025-01-16 05:10:15

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：错误码](https://help.aliyun.com/zh/isi/developer-reference/error-codes-1)[下一篇：Python SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-python)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

下载安装

关键接口

代码示例

常见问题

使用Java SDK，SpeechRecognizer recognizer如何调用stop（）实现通知服务端语音数据发送完毕？

Java版SDK可以直接提供上传音频文件的方式进行识别吗？

一句话识别、实时语音识别SDK中，send接口参数含义及使用方式？

如何结合SDK日志分析延迟问题？

Java SDK找不到com.alibaba的JAR包，如何安装Alibaba Cloud SDK for Java？

Java SDK通过传入阿里云账号的AccessKey ID和AccessKey Secret，调用阿里云Java SDK得到client提示错误org.json.JSONArray.iterator()Ljava/util/Iterator如何解决？

本文介绍如何使用智能语音交互一句话识别的Java SDK，包括SDK的安装方法及SDK代码示例等。

## 注意事项

- 在使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference-1#topic-2572207 "")。

- 从2.1.0版本开始，原有 **nls-sdk-short-asr** 更名为 **nls-sdk-recognizer**，升级时需确认已删除 **nls-sdk-short-asr**，并按编译提示添加相应的回调方法。


## 下载安装

1. 从Maven服务器 [下载最新版本SDK](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20220909/qgai/nls-sdk-java-demo-2022-09-09.zip)。















```java
<dependency>
       <groupId>com.alibaba.nls</groupId>
       <artifactId>nls-sdk-recognizer</artifactId>
       <version>2.2.1</version>
</dependency>
```



解压ZIP文件，在pom目录运行`mvn package`，会在target目录生成可执行JAR：nls-example-recognizer-2.0.0-jar-with-dependencies.jar，将JAR包拷贝至目标服务器，用于快速验证及服务压测。

2. 服务验证。

运行如下代码，并按提示提供相应参数。运行后在命令执行目录生成logs/nls.log。















```java
java -cp nls-example-recognizer-2.0.0-jar-with-dependencies.jar com.alibaba.nls.client.SpeechRecognizerDemo
```

3. 服务压测。

运行如下代码，并按提示提供相应参数。其中阿里云服务URL参数为：` wss://nls-gateway-cn-shanghai.aliyuncs.com/ws/v1`，语音文件为16k采样率PCM格式文件，并发数根据您的购买情况进行选择。















```java
java -jar nls-example-recognizer-2.0.0-jar-with-dependencies.jar
```





**重要**





自行压测超过2路并发会产生费用。


## 关键接口

- NlsClient：语音处理客户端，利用该客户端可以进行一句话识别、实时语音识别和语音合成的语音处理任务。该客户端为线程安全，建议全局仅创建一个实例。

- SpeechRecognizer：一句话识别处理类，通过该接口设置请求参数，发送请求及声音数据。非线程安全。

- SpeechRecognizerListener：识别结果监听类，监听识别结果。非线程安全。


更多介绍，请参见 [Java API接口说明](https://g.alicdn.com/idst-fe/nls-sdk-doc-api/2.0.6/GateWay_Java_2.0.2/index.html)。

**重要**

SDK调用注意事项：

- NlsClient使用了Netty框架，NlsClient对象的创建会消耗一定时间和资源，一经创建可以重复使用。建议调用程序将NlsClient的创建和关闭与程序本身的生命周期结合。

- SpeechRecognizer对象不可重复使用，一个识别任务对应一个SpeechRecognizer对象。例如，N个音频文件要进行N次识别任务，需要创建N个SpeechRecognizer对象。

- SpeechRecognizerListener对象和SpeechRecognizer对象是一一对应的，不能将一个SpeechRecognizerListener对象设置到多个SpeechRecognizer对象中，否则不能将各识别任务区分开。

- Java SDK依赖Netty网络库，如果您的应用依赖Netty，其版本需更新至4.1.17.Final及以上。


## 代码示例

**说明**

- [下载nls-sample-16k.wav](https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav)。

示例中使用的音频文件为16000 Hz采样率，请在管控台中将AppKey对应项目的模型设置为 **通用** 模型，以获取准确的识别效果。如果使用其他音频，请设置为支持该音频场景的模型，关于模型设置，请参见 [管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects#topic-2572199 "")。

- 示例中使用SDK内置的默认一句话识别服务的外网访问服务URL，如果您使用阿里云上海ECS，且需要使用内网访问服务URL，则在创建NlsClient对象时，设置内网访问的URL：















```java
client = new NlsClient("ws://nls-gateway-cn-shanghai-internal.aliyuncs.com/ws/v1", accessToken);
```

- 调用接口前，需配置环境变量，通过环境变量读取访问凭证。智能语音交互的AccessKey ID、AccessKey Secret和AppKey的环境变量名： **ALIYUN\_AK\_ID**、 **ALIYUN\_AK\_SECRET**、 **NLS\_APP\_KEY**。


```java
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import com.alibaba.nls.client.protocol.InputFormatEnum;
import com.alibaba.nls.client.protocol.NlsClient;
import com.alibaba.nls.client.protocol.SampleRateEnum;
import com.alibaba.nls.client.protocol.asr.SpeechRecognizer;
import com.alibaba.nls.client.protocol.asr.SpeechRecognizerListener;
import com.alibaba.nls.client.protocol.asr.SpeechRecognizerResponse;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
/**
 * 此示例演示了：
 *      ASR一句话识别API调用。
 *      动态获取Token。获取Token具体操作，请参见：https://help.aliyun.com/document_detail/450514.html
 *      通过本地文件模拟实时流发送。
 *      识别耗时计算。
 */
public class SpeechRecognizerDemo {
    private static final Logger logger = LoggerFactory.getLogger(SpeechRecognizerDemo.class);
    private String appKey;
    NlsClient client;
    public SpeechRecognizerDemo(String appKey, String id, String secret, String url) {
        this.appKey = appKey;
        //应用全局创建一个NlsClient实例，默认服务地址为阿里云线上服务地址。
        //获取Token，实际使用时注意在accessToken.getExpireTime()过期前再次获取。
        AccessToken accessToken = new AccessToken(id, secret);
        try {
            accessToken.apply();
            System.out.println("get token: " + accessToken.getToken() + ", expire time: " + accessToken.getExpireTime());
            if(url.isEmpty()) {
                client = new NlsClient(accessToken.getToken());
            }else {
                client = new NlsClient(url, accessToken.getToken());
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    private static SpeechRecognizerListener getRecognizerListener(int myOrder, String userParam) {
        SpeechRecognizerListener listener = new SpeechRecognizerListener() {
            //识别出中间结果。仅当setEnableIntermediateResult为true时，才会返回该消息。
            @Override
            public void onRecognitionResultChanged(SpeechRecognizerResponse response) {
                //getName是获取事件名称，getStatus是获取状态码，getRecognizedText是语音识别文本。
                System.out.println("name: " + response.getName() + ", status: " + response.getStatus() + ", result: " + response.getRecognizedText());
            }
            //识别完毕
            @Override
            public void onRecognitionCompleted(SpeechRecognizerResponse response) {
                //getName是获取事件名称，getStatus是获取状态码，getRecognizedText是语音识别文本。
                System.out.println("name: " + response.getName() + ", status: " + response.getStatus() + ", result: " + response.getRecognizedText());
            }
            @Override
            public void onStarted(SpeechRecognizerResponse response) {
                System.out.println("myOrder: " + myOrder + "; myParam: " + userParam + "; task_id: " + response.getTaskId());
            }
            @Override
            public void onFail(SpeechRecognizerResponse response) {
                //task_id是调用方和服务端通信的唯一标识，当遇到问题时，需要提供此task_id。
                System.out.println("task_id: " + response.getTaskId() + ", status: " + response.getStatus() + ", status_text: " + response.getStatusText());
            }
        };
        return listener;
    }
    //根据二进制数据大小计算对应的同等语音长度
    //sampleRate仅支持8000或16000。
    public static int getSleepDelta(int dataSize, int sampleRate) {
        // 仅支持16位采样。
        int sampleBytes = 16;
        // 仅支持单通道。
        int soundChannel = 1;
        return (dataSize * 10 * 8000) / (160 * sampleRate);
    }
    public void process(String filepath, int sampleRate) {
        SpeechRecognizer recognizer = null;
        try {
            //传递用户自定义参数
            String myParam = "user-param";
            int myOrder = 1234;
            SpeechRecognizerListener listener = getRecognizerListener(myOrder, myParam);
            recognizer = new SpeechRecognizer(client, listener);
            recognizer.setAppKey(appKey);
            //设置音频编码格式。如果是OPUS文件，请设置为InputFormatEnum.OPUS。
            recognizer.setFormat(InputFormatEnum.PCM);
            //设置音频采样率
            if(sampleRate == 16000) {
                recognizer.setSampleRate(SampleRateEnum.SAMPLE_RATE_16K);
            } else if(sampleRate == 8000) {
                recognizer.setSampleRate(SampleRateEnum.SAMPLE_RATE_8K);
            }
            //设置是否返回中间识别结果
            recognizer.setEnableIntermediateResult(true);
            //设置是否打开语音检测（即vad）
   recognizer.addCustomedParam("enable_voice_detection",true);
            //此方法将以上参数设置序列化为JSON发送给服务端，并等待服务端确认。
            long now = System.currentTimeMillis();
            recognizer.start();
            logger.info("ASR start latency : " + (System.currentTimeMillis() - now) + " ms");
            File file = new File(filepath);
            FileInputStream fis = new FileInputStream(file);
            byte[] b = new byte[3200];
            int len;
            while ((len = fis.read(b)) > 0) {
                logger.info("send data pack length: " + len);
                recognizer.send(b, len);
                //本案例用读取本地文件的形式模拟实时获取语音流，因为读取速度较快，这里需要设置sleep时长。
                // 如果实时获取语音则无需设置sleep时长，如果是8k采样率语音第二个参数设置为8000。
                int deltaSleep = getSleepDelta(len, sampleRate);
                Thread.sleep(deltaSleep);
            }
            //通知服务端语音数据发送完毕，等待服务端处理完成。
            now = System.currentTimeMillis();
            //计算实际延迟，调用stop返回之后一般即是识别结果返回时间。
            logger.info("ASR wait for complete");
            recognizer.stop();
            logger.info("ASR stop latency : " + (System.currentTimeMillis() - now) + " ms");
            fis.close();
        } catch (Exception e) {
            System.err.println(e.getMessage());
        } finally {
            //关闭连接
            if (null != recognizer) {
                recognizer.close();
            }
        }
    }
    public void shutdown() {
        client.shutdown();
    }
    public static void main(String[] args) throws Exception {
        String appKey = System.getenv().get("NLS_APP_KEY");
        String id = System.getenv().get("ALIYUN_AK_ID");
        String secret = System.getenv().get("ALIYUN_AK_SECRET");
        String url = System.getenv().getOrDefault("NLS_GATEWAY_URL", "wss://nls-gateway-cn-shanghai.aliyuncs.com/ws/v1");
        SpeechRecognizerDemo demo = new SpeechRecognizerDemo(appKey, id, secret, url);
        //本案例使用本地文件模拟发送实时流数据。
        demo.process("./nls-sample-16k.wav", 16000);
        //demo.process("./nls-sample.opus", 16000);
        demo.shutdown();
    }
}
```

## 常见问题

### 使用Java SDK，SpeechRecognizer recognizer如何调用stop（）实现通知服务端语音数据发送完毕？

1. 正常情况下自动取调用，不需要单独调用stop()。如果10秒之内没有语音数据发给服务侧, 会报错41010120。如果一直实时发送语音数据给服务端，识别在服务侧是一直进行的，您可以通过设置`enable_intermediate_result=true`参数实时获取识别结果。

2. 如果您判断一句话结束，也可以主动调用stop（）停止发送数据，获取最终识别结果。


### Java版SDK可以直接提供上传音频文件的方式进行识别吗？

如下图所示，SDK示例通过调用RESTfulAPI接口，实现上传音频文件进行识别，详情请参见 [一句话识别Java SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-java#topic-1917910 "")。![Java版SDK直接提供上传音频文件的方式进行识别](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3868780661/p478806.png)

### 一句话识别、实时语音识别SDK中，send接口参数含义及使用方式？

以Java为例。java SDK中，一句话识别和实时语音识别分别提供了三个重载的`send()`接口。如下：

```java
public void send(InputStream ins);
public void send(InputStream ins, int batchSize, int sleepInterval);
public void send(byte[] data);
```

三个接口使用时要保证持续、实时地向服务端发送语音数据。

demo是用语音文件模拟实时语音流的速度发送语音，通常一次发送间隔时间为100 ms或200 ms（sleepInterval）的语音数据，数据量（batchSize）和采样率有关：发送间隔过大，会导致延迟较大，容易断连；发送间隔过小，会消耗服务端和网络资源。可以适当实验调整到合适数值。

第2个接口中`ins`为模拟语音流，需要控制发送速率。ins中的数据每间隔100 ms，发送3200字节（16000采样率）。调用示例：

```java
public void send(ins, 3200, 100); // 16 kHz语音
```

第3个接口中`data`为一次性发送的数据，控制循环调用的间隔，调用示例：

```java
recognizer.send(data); // 100 ms 语音数据
try {
 Thread.sleep(100);
} catch (InterruptedException e) {
 e.printStackTrace();
}
```

### 如何结合SDK日志分析延迟问题？

以Java SDK日志为例。

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


### Java SDK找不到com.alibaba的JAR包，如何安装Alibaba Cloud SDK for Java？

请参见 [V1.0 Java SDK](https://help.aliyun.com/zh/sdk/developer-reference/v1-0-java-sdk/ "") 安装Alibaba Cloud SDK for Java。

### Java SDK通过传入阿里云账号的AccessKey ID和AccessKey Secret，调用阿里云Java SDK得到client提示错误org.json.JSONArray.iterator()Ljava/util/Iterator如何解决？

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