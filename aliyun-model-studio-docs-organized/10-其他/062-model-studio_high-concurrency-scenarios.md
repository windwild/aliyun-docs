### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音合成](https://help.aliyun.com/zh/model-studio/speech-synthesis-api-reference/)[实时语音合成（CosyVoice）](https://help.aliyun.com/zh/model-studio/cosyvoice-large-model-for-speech-synthesis/)高并发场景

# CosyVoice高并发场景

更新时间：2026-02-11 02:25:25

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：iOS SDK](https://help.aliyun.com/zh/model-studio/cosyvoice-ios-sdk)[下一篇：CosyVoice声音复刻API](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

Python SDK：对象池优化

实现步骤

资源管理与异常处理

Java SDK：连接池与对象池优化

实现步骤

推荐配置

资源管理与异常处理

调用预热与耗时统计说明

Java SDK常见异常

异常 1、 业务流量平稳，但是服务器 TCP 连接数持续上升

异常 2、任务耗时比正常调用多 60 秒

异常 3、服务启动时任务慢，之后慢慢恢复正常

异常 4、服务端报错 Invalid action('run-task')! Please follow the protocol!

异常 5、业务流量平稳，调用量出现异常尖刺

异常 6、随着并发数提升，所有任务都变慢

CosyVoice 语音合成服务基于 WebSocket 协议，以支持流式实时通信。然而，在高并发场景下，为每个请求独立创建和销毁 WebSocket 连接会产生巨大的网络与系统资源开销，并引入显著的连接延迟。为优化性能并确保稳定性，DashScope SDK 内置了高效的资源复用机制（如连接池与对象池）。本文档将详细介绍如何利用 DashScope Python 和 Java SDK 中的这些特性，在高并发场景下高效调用 CosyVoice 服务。

## **前提条件**

- [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")

- 已安装符合版本要求的DashScope SDK，建议 [安装最新版](https://help.aliyun.com/zh/model-studio/install-sdk "")：

  - Python SDK：版本≥1.25.2

  - Java SDK：版本≥2.16.6

## **Python SDK：对象池优化**

Python SDK 通过 `SpeechSynthesizerObjectPool` 实现对象池优化，用于管理和复用 `SpeechSynthesizer` 对象。

对象池在初始化时会立即创建指定数量的 `SpeechSynthesizer` 实例并预先建立 WebSocket 连接。从池中获取对象时无需等待连接建立，可直接发起请求，有效降低首包延迟。当任务完成并将对象归还到对象池后，其 WebSocket 连接不会关闭，而是保持活跃状态等待下次任务复用。

### **实现步骤**

1. 安装依赖：安装DashScope依赖（`pip install -U dashscope`）

2. 创建并配置对象池

对象池大小需要通过`SpeechSynthesizerObjectPool`进行设置。推荐值：峰值并发数的 1.5 至 2 倍。对象池大小不应超过您账户的 QPS（每秒查询率）限制。

通过以下代码创建全局单例固定大小对象池。对象池在初始化时会立即创建指定数量的 `SpeechSynthesizer` 对象并建立 WebSocket 连接，因此会有一定耗时。















```python
from dashscope.audio.tts_v2 import SpeechSynthesizerObjectPool

synthesizer_object_pool = SpeechSynthesizerObjectPool(max_size=20)
```

3. 从对象池中获取`SpeechSynthesizer`对象

如果当前未归还的对象数量已超过对象池的最大容量，系统会额外创建一个新的`SpeechSynthesizer`对象。

此类新创建的对象需要重新进行初始化并建立 WebSocket 连接，无法利用对象池的既有连接资源，因此不具备复用效果。















```python
speech_synthesizer = connectionPool.borrow_synthesizer(
       model='cosyvoice-v3-flash',
       voice='longanyang',
       seed=12382,
       callback=synthesizer_callback
)
```

4. 进行语音合成

调用`SpeechSynthesizer`对象的call或streaming\_call方法进行语音合成。

5. 归还`SpeechSynthesizer`对象

语音合成任务结束后，归还`SpeechSynthesizer`对象，以便后续任务可以复用该对象。

不要归还未完成任务或任务失败的对象。















```python
connectionPool.return_synthesizer(speech_synthesizer)
```


#### **完整代码**

```python
# !/usr/bin/env python3
# Copyright (C) Alibaba Group. All Rights Reserved.
# MIT License (https://opensource.org/licenses/MIT)

import os
import time
import threading

import dashscope
from dashscope.audio.tts_v2 import *

USE_CONNECTION_POOL = True
text_to_synthesize = [\
    '第一句、欢迎使用阿里巴巴语音合成服务。',\
    '第二句、欢迎使用阿里巴巴语音合成服务。',\
    '第三句、欢迎使用阿里巴巴语音合成服务。',\
]
connectionPool = None
if USE_CONNECTION_POOL:
    print('creating connection pool')
    start_time = time.time() * 1000
    connectionPool = SpeechSynthesizerObjectPool(max_size=3)
    end_time = time.time() * 1000
    print('connection pool created, cost: {} ms'.format(end_time - start_time))

def init_dashscope_api_key():
    '''
    Set your DashScope API-key. More information:
    https://github.com/aliyun/alibabacloud-bailian-speech-demo/blob/master/PREREQUISITES.md
    '''
    # 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    if 'DASHSCOPE_API_KEY' in os.environ:
        dashscope.api_key = os.environ[\
            'DASHSCOPE_API_KEY']  # load API-key from environment variable DASHSCOPE_API_KEY
    else:
        dashscope.api_key = '<your-dashscope-api-key>'  # set API-key manually

def synthesis_text_to_speech_and_play_by_streaming_mode(text, task_id):
    global USE_CONNECTION_POOL, connectionPool
    '''
    Synthesize speech with given text by streaming mode, async call and play the synthesized audio in real-time.
    for more information, please refer to https://help.aliyun.com/document_detail/2712523.html
    '''

    complete_event = threading.Event()

    # Define a callback to handle the result

    class Callback(ResultCallback):
        def on_open(self):
            # when using object pool, on_open will be called after task start
            self.file = open(f'result_{task_id}.mp3', 'wb')
            print(f'[task_{task_id}] start')

        def on_complete(self):
            print(f'[task_{task_id}] speech synthesis task complete successfully.')
            complete_event.set()

        def on_error(self, message: str):
            print(f'[task_{task_id}] speech synthesis task failed, {message}')

        def on_close(self):
            # when using object pool, on_open will be called after task finished
            print(f'[task_{task_id}] finished')

        def on_event(self, message):
            # print(f'recv speech synthsis message {message}')
            pass

        def on_data(self, data: bytes) -> None:
            # send to player
            # save audio to file
            self.file.write(data)

    # Call the speech synthesizer callback
    synthesizer_callback = Callback()

    # Initialize the speech synthesizer
    # you can customize the synthesis parameters, like voice, format, sample_rate or other parameters
    if USE_CONNECTION_POOL:
        speech_synthesizer = connectionPool.borrow_synthesizer(
            model='cosyvoice-v3-flash',
            voice='longanyang',
            seed=12382,
            callback=synthesizer_callback
        )
    else:
        speech_synthesizer = SpeechSynthesizer(model='cosyvoice-v3-flash',
                                               voice='longanyang',
                                               seed=12382,
                                               callback=synthesizer_callback)
    try:
        speech_synthesizer.call(text)
    except Exception as e:
        print(f'[task_{task_id}] speech synthesis task failed, {e}')
        if USE_CONNECTION_POOL:
            # close the synthesizer connection manually if task failed when using connection pool.
            speech_synthesizer.close()
        return

    print('[task_{}] Synthesized text: {}'.format(task_id, text))
    complete_event.wait()
    print('[task_{}][Metric] requestId: {}, first package delay ms: {}'.format(
        task_id,
        speech_synthesizer.get_last_request_id(),
        speech_synthesizer.get_first_package_delay()))
    if USE_CONNECTION_POOL:
        connectionPool.return_synthesizer(speech_synthesizer)

# main function
if __name__ == '__main__':
    # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
    dashscope.base_websocket_api_url='wss://dashscope.aliyuncs.com/api-ws/v1/inference'
    init_dashscope_api_key()
    task_thread_list = []
    for task_id in range(3):
        thread = threading.Thread(
            target=synthesis_text_to_speech_and_play_by_streaming_mode,
            args=(text_to_synthesize[task_id], task_id))
        task_thread_list.append(thread)

    for task_thread in task_thread_list:
        task_thread.start()

    for task_thread in task_thread_list:
        task_thread.join()

    if USE_CONNECTION_POOL:
        connectionPool.shutdown()
```

### **资源管理与异常处理**

- 任务成功：当语音合成任务正常完成时，必须调用 `connectionPool.return_synthesizer(speech_synthesizer)` 将 `SpeechSynthesizer` 对象归还到池中，以便复用。



**重要**





不要归还未完成任务或任务失败的`SpeechSynthesizer`对象。

- 任务失败：当 SDK 内部或业务逻辑抛出异常导致任务中断时，主动关闭底层的 WebSocket 连接：`speech_synthesizer.close()`

- 在所有语音合成任务完成后，要通过如下方式关闭对象池：`connectionPool.shutdown()`。

- 在服务出现TaskFailed报错时，不需要额外处理。


## **Java SDK：连接池与对象池优化**

Java SDK通过内置的连接池和自定义的对象池协同工作，实现最佳性能。

- 连接池：SDK 内部集成的 OkHttp3 连接池，负责管理和复用底层的 WebSocket 连接，减少网络握手开销。此功能默认开启。

- 对象池：基于 `commons-pool2` 实现，用于维护一组已预先建立好连接的 `SpeechSynthesizer` 对象。从池中获取对象可消除连接建立的延迟，显著降低首包延迟。


### **实现步骤**

1. 添加依赖

根据项目构建工具，在依赖配置文件中添加 dashscope-sdk-java 和 commons-pool2。

以Maven和Gradle为例，配置如下：






Maven



Gradle



















1. 打开您的Maven项目的`pom.xml`文件。

2. 在`<dependencies>`标签内添加以下依赖信息。


```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>dashscope-sdk-java</artifactId>
    <!-- 请将 'the-latest-version' 替换为2.16.9及以上版本，可在如下链接查询相关版本号：https://mvnrepository.com/artifact/com.alibaba/dashscope-sdk-java -->
    <version>the-latest-version</version>
</dependency>

<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-pool2</artifactId>
    <!-- 请将 'the-latest-version' 替换为最新版本，可在如下链接查询相关版本号：https://mvnrepository.com/artifact/org.apache.commons/commons-pool2 -->
    <version>the-latest-version</version>
</dependency>
```

3. 保存`pom.xml`文件。

4. 使用Maven命令（如`mvn clean install`或`mvn compile`）来更新项目依赖


1. 打开您的Gradle项目的`build.gradle`文件。

2. 在`dependencies`块内添加以下依赖信息。















      ```groovy
      dependencies {
          // 请将 'the-latest-version' 替换为2.16.6及以上版本，可在如下链接查询相关版本号：https://mvnrepository.com/artifact/com.alibaba/dashscope-sdk-java
          implementation group: 'com.alibaba', name: 'dashscope-sdk-java', version: 'the-latest-version'

          // 请将 'the-latest-version' 替换为最新版本，可在如下链接查询相关版本号：https://mvnrepository.com/artifact/org.apache.commons/commons-pool2
          implementation group: 'org.apache.commons', name: 'commons-pool2', version: 'the-latest-version'
      }
      ```

3. 保存`build.gradle`文件。

4. 在命令行中，切换到您的项目根目录，执行以下Gradle命令来更新项目依赖。















      ```bash
      ./gradlew build --refresh-dependencies
      ```



      或者，如果您使用的是Windows系统，命令应为：















      ```dos
      gradlew build --refresh-dependencies
      ```


2. 配置连接池

通过环境变量配置连接池关键参数：




| **环境变量** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **环境变量** | **描述** |
| DASHSCOPE\_CONNECTION\_POOL\_SIZE | 连接池大小。<br>推荐值：峰值并发数的 2 倍以上。<br>默认值：32。 |
| DASHSCOPE\_MAXIMUM\_ASYNC\_REQUESTS | 最大异步请求数。<br>推荐值：与 `DASHSCOPE_CONNECTION_POOL_SIZE` 保持一致。<br>默认值：32。 |
| DASHSCOPE\_MAXIMUM\_ASYNC\_REQUESTS\_PER\_HOST | 单主机最大异步请求数。<br>推荐值：与 `DASHSCOPE_CONNECTION_POOL_SIZE` 保持一致。<br>默认值：32。 |

3. 配置对象池

通过环境变量配置对象池大小：




| **环境变量** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **环境变量** | **描述** |
| COSYVOICE\_OBJECTPOOL\_SIZE | 对象池大小。<br>推荐值：峰值并发数的 1.5 至 2 倍。<br>默认值：500。 |





**重要**





   - 对象池的大小（`COSYVOICE_OBJECTPOOL_SIZE`）必须小于或等于连接池的大小（`DASHSCOPE_CONNECTION_POOL_SIZE`）。否则，当对象池请求对象时，若连接池已满，会导致调用线程阻塞，等待可用连接。

   - 对象池大小不应超过您账户的 QPS（每秒查询率）限制。


通过如下代码创建对象池：

```java
class CosyvoiceObjectPool {
    // 。。。这里省略其它代码，完整示例请参见完整代码
    public static GenericObjectPool<SpeechSynthesizer> getInstance() {
        lock.lock();
        if (synthesizerPool == null) {
            // 您可以在这里设置对象池的大小。或在环境变量COSYVOICE_OBJECTPOOL_SIZE中设置。
            // 建议设置为服务器最大并发连接数的1.5到2倍。
            int objectPoolSize = getObjectivePoolSize();
            SpeechSynthesizerObjectFactory speechSynthesizerObjectFactory =
                    new SpeechSynthesizerObjectFactory();
            GenericObjectPoolConfig<SpeechSynthesizer> config =
                    new GenericObjectPoolConfig<>();
            config.setMaxTotal(objectPoolSize);
            config.setMaxIdle(objectPoolSize);
            config.setMinIdle(objectPoolSize);
            synthesizerPool =
                    new GenericObjectPool<>(speechSynthesizerObjectFactory, config);
        }
        lock.unlock();
        return synthesizerPool;
    }
}
```

4. 从对象池中获取`SpeechSynthesizer`对象

如果当前未归还的对象数量已超过对象池的最大容量，系统会额外创建一个新的`SpeechSynthesizer`对象。

此类新创建的对象需要重新进行初始化并建立 WebSocket 连接，无法利用对象池的既有连接资源，因此不具备复用效果。















```java
synthesizer = CosyvoiceObjectPool.getInstance().borrowObject();
```

5. 进行语音合成

调用`SpeechSynthesizer`对象的call或streamingCall方法进行语音合成。

6. 归还`SpeechSynthesizer`对象

语音合成任务结束后，归还`SpeechSynthesizer`对象，以便后续任务可以复用该对象。

不要归还未完成任务或任务失败的对象。















```python
CosyvoiceObjectPool.getInstance().returnObject(synthesizer);
```


#### **完整代码**

```java
import com.alibaba.dashscope.audio.tts.SpeechSynthesisResult;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisAudioFormat;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;
import com.alibaba.dashscope.common.ResultCallback;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.Constants;
import lombok.extern.slf4j.Slf4j;
import org.apache.commons.pool2.BasePooledObjectFactory;
import org.apache.commons.pool2.PooledObject;
import org.apache.commons.pool2.impl.DefaultPooledObject;
import org.apache.commons.pool2.impl.GenericObjectPool;
import org.apache.commons.pool2.impl.GenericObjectPoolConfig;

import java.time.LocalDateTime;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Lock;

/**
 * 您需要在项目中引入org.apache.commons.pool2和DashScope相关的包。
 *
 * DashScope SDK 2.16.6及后续版本针对高并发场景进行了优化，
 * DashScope SDK 2.16.6之前的版本不推荐在高并发场景下使用。
 *
 *
 * 在对TTS服务进行高并发调用之前，
 * 请通过以下环境变量配置连接池的相关参数。
 *
 * DASHSCOPE_MAXIMUM_ASYNC_REQUESTS
 * DASHSCOPE_MAXIMUM_ASYNC_REQUESTS_PER_HOST
 * DASHSCOPE_CONNECTION_POOL_SIZE
 *
 */

class SpeechSynthesizerObjectFactory
        extends BasePooledObjectFactory<SpeechSynthesizer> {
    public SpeechSynthesizerObjectFactory() {
        super();
    }
    @Override
    public SpeechSynthesizer create() throws Exception {
        return new SpeechSynthesizer();
    }

    @Override
    public PooledObject<SpeechSynthesizer> wrap(SpeechSynthesizer obj) {
        return new DefaultPooledObject<>(obj);
    }
}

class CosyvoiceObjectPool {
    public static GenericObjectPool<SpeechSynthesizer> synthesizerPool;
    public static String COSYVOICE_OBJECTPOOL_SIZE_ENV = "COSYVOICE_OBJECTPOOL_SIZE";
    public static int DEFAULT_OBJECT_POOL_SIZE = 500;
    private static Lock lock = new java.util.concurrent.locks.ReentrantLock();
    public static int getObjectivePoolSize() {
        try {
            Integer n = Integer.parseInt(System.getenv(COSYVOICE_OBJECTPOOL_SIZE_ENV));
            System.out.println("Using Object Pool Size In Env: "+ n);
            return n;
        } catch (NumberFormatException e) {
            System.out.println("Using Default Object Pool Size: "+ DEFAULT_OBJECT_POOL_SIZE);
            return DEFAULT_OBJECT_POOL_SIZE;
        }
    }
    public static GenericObjectPool<SpeechSynthesizer> getInstance() {
        lock.lock();
        if (synthesizerPool == null) {
            // 您可以在这里设置对象池的大小。或在环境变量COSYVOICE_OBJECTPOOL_SIZE中设置。
            // 建议设置为服务器最大并发连接数的1.5到2倍。
            int objectPoolSize = getObjectivePoolSize();
            SpeechSynthesizerObjectFactory speechSynthesizerObjectFactory =
                    new SpeechSynthesizerObjectFactory();
            GenericObjectPoolConfig<SpeechSynthesizer> config =
                    new GenericObjectPoolConfig<>();
            config.setMaxTotal(objectPoolSize);
            config.setMaxIdle(objectPoolSize);
            config.setMinIdle(objectPoolSize);
            synthesizerPool =
                    new GenericObjectPool<>(speechSynthesizerObjectFactory, config);
        }
        lock.unlock();
        return synthesizerPool;
    }
}

class SynthesizeTaskWithCallback implements Runnable {
    String[] textArray;
    String requestId;
    long timeCost;
    public SynthesizeTaskWithCallback(String[] textArray) {
        this.textArray = textArray;
    }
    @Override
    public void run() {
        SpeechSynthesizer synthesizer = null;
        long startTime = System.currentTimeMillis();
        // if recv onError
        final boolean[] hasError = {false};
        try {
            class ReactCallback extends ResultCallback<SpeechSynthesisResult> {
                ReactCallback() {}

                @Override
                public void onEvent(SpeechSynthesisResult message) {
                    if (message.getAudioFrame() != null) {
                        try {
                            byte[] bytesArray = message.getAudioFrame().array();
                            System.out.println("收到音频，音频文件流length为：" + bytesArray.length);
                        } catch (Exception e) {
                            throw new RuntimeException(e);
                        }
                    }
                }

                @Override
                public void onComplete() {}

                @Override
                public void onError(Exception e) {
                    System.out.println(e.getMessage());
                    e.printStackTrace();
                    hasError[0] = true;
                }
            }

            // 将your-dashscope-api-key替换成您自己的API-KEY
            String dashScopeApiKey = "your-dashscope-api-key";

            SpeechSynthesisParam param =
                    SpeechSynthesisParam.builder()
                            .model("cosyvoice-v3-flash")
                            .voice("longanyang")
                            // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                            // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                            .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                            .format(SpeechSynthesisAudioFormat
                                    .MP3_22050HZ_MONO_256KBPS) // 流式合成使用PCM或者MP3
                            .apiKey(dashScopeApiKey)
                            .build();

            try {
                synthesizer = CosyvoiceObjectPool.getInstance().borrowObject();
                synthesizer.updateParamAndCallback(param, new ReactCallback());
                for (String text : textArray) {
                    synthesizer.streamingCall(text);
                }
                Thread.sleep(20);
                synthesizer.streamingComplete(60000);
                requestId = synthesizer.getLastRequestId();
            } catch (Exception e) {
                System.out.println("Exception e: " + e.toString());
                hasError[0] = true;
            }
        } catch (Exception e) {
            hasError[0] = true;
            throw new RuntimeException(e);
        }
        if (synthesizer != null) {
            try {
                if (hasError[0] == true) {
                    // 如果出现异常，则关闭连接并在对象池中禁用该对象。
                    synthesizer.getDuplexApi().close(1000, "bye");
                    CosyvoiceObjectPool.getInstance().invalidateObject(synthesizer);
                } else {
                    // 如果任务正常结束，则归还对象。
                    CosyvoiceObjectPool.getInstance().returnObject(synthesizer);
                }
            } catch (Exception e) {
                throw new RuntimeException(e);
            }
            long endTime = System.currentTimeMillis();
            timeCost = endTime - startTime;
            System.out.println("[线程 " + Thread.currentThread() + "] 语音合成任务结束。耗时 " + timeCost + " ms, RequestId " + requestId);
        }
    }
}

@Slf4j
public class SynthesizeTextToSpeechWithCallbackConcurrently {
    public static void checkoutEnv(String envName, int defaultSize) {
        if (System.getenv(envName) != null) {
            System.out.println("[ENV CHECK]: " + envName + " "
                    + System.getenv(envName));
        } else {
            System.out.println("[ENV CHECK]: " + envName
                    + " Using Default which is " + defaultSize);
        }
    }

    public static void main(String[] args)
            throws InterruptedException, NoApiKeyException {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";
        // Check for connection pool env
        checkoutEnv("DASHSCOPE_CONNECTION_POOL_SIZE", 32);
        checkoutEnv("DASHSCOPE_MAXIMUM_ASYNC_REQUESTS", 32);
        checkoutEnv("DASHSCOPE_MAXIMUM_ASYNC_REQUESTS_PER_HOST", 32);
        checkoutEnv(CosyvoiceObjectPool.COSYVOICE_OBJECTPOOL_SIZE_ENV, CosyvoiceObjectPool.DEFAULT_OBJECT_POOL_SIZE);

        int runTimes = 3;
        // Create the pool of SpeechSynthesis objects
        ExecutorService executorService = Executors.newFixedThreadPool(runTimes);

        for (int i = 0; i < runTimes; i++) {
            // Record the task submission time
            LocalDateTime submissionTime = LocalDateTime.now();
            executorService.submit(new SynthesizeTaskWithCallback(new String[] {
                    "床前明月光，", "疑似地上霜。", "举头望明月，", "低头思故乡。"}));
        }

        // Shut down the ExecutorService and wait for all tasks to complete
        executorService.shutdown();
        executorService.awaitTermination(1, TimeUnit.MINUTES);
        System.exit(0);
    }
}
```

### **推荐配置**

以下配置基于在指定规格的阿里云服务器上仅运行 CosyVoice 语音合成服务的测试结果。过高的并发数可能导致任务处理延迟。

其中单机并发数指的是同一时刻正在运行的CosyVoice语音合成任务数，也可以理解为工作线程数。

| **机器配置（阿里云）** | **单机最大并发数** | **对象池大小** | **连接池大小** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **机器配置（阿里云）** | **单机最大并发数** | **对象池大小** | **连接池大小** |
| 4核8GiB | 100 | 500 | 2000 |
| 8核16GiB | 150 | 500 | 2000 |
| 16核32GiB | 200 | 500 | 2000 |

### **资源管理与异常处理**

- 任务成功：当语音合成任务正常完成时，必须调用GenericObjectPool的returnObject方法将`SpeechSynthesizer`对象归还到池中，以便复用。

在当前代码中，对应`CosyvoiceObjectPool.getInstance().returnObject(synthesizer)`



**重要**





不要归还未完成任务或任务失败的`SpeechSynthesizer`对象。

- 任务失败：当 SDK 内部或业务逻辑抛出异常导致任务中断时，必须执行以下两个操作：


1. 主动关闭底层的 WebSocket 连接

2. 从对象池中废弃该对象，防止被再次使用


```java
// 在当前代码中对应如下内容
// 关闭连接
synthesizer.getDuplexApi().close(1000, "bye");
// 在对象池中废弃出现异常的synthesizer
CosyvoiceObjectPool.getInstance().invalidateObject(synthesizer);
```

- 在服务出现TaskFailed报错时，不需要额外处理。


### **调用预热与耗时统计说明**

在对 DashScope Java SDK 进行并发调用延迟等性能评估时，建议在正式测试前执行充分的预热操作。预热能够确保测量结果准确反映服务在稳定状态下的真实性能，避免因初始连接耗时导致的数据偏差。

#### **连接复用机制**

DashScope Java SDK 通过全局单例的连接池高效管理和复用 WebSocket 连接，旨在减少频繁建连和断连的开销，提升高并发场景下的处理能力。

该机制的工作特点如下：

- **按需创建**：SDK 不会在服务启动时预创建 WebSocket 连接，而是在首次调用时按需建立。

- **限时复用**：请求完成后，连接将在池中保留最多 60 秒以备复用。

  - 若 60 秒内有新请求，将复用现有连接，避免重复握手开销。

  - 若连接空闲超过 60 秒，将被自动关闭以释放资源。

#### **预热的重要性**

在以下场景中，连接池中可能没有可复用的活跃连接，导致请求需要新建连接：

- 应用刚启动，尚未发起任何调用。

- 服务空闲时间超过 60 秒，池中连接已因超时而关闭。


在这些场景下，首次或初期请求会触发完整的 WebSocket 建连过程（包括 TCP 握手、TLS 加密协商和协议升级），其端到端延迟会显著高于后续复用连接的请求。这部分额外耗时源于网络连接初始化，并非服务本身的处理延迟。因此，若未进行预热，性能测试结果会因包含初始建连时间而产生偏差。

#### **推荐做法**

为获取可靠的性能数据，在正式进行性能压测或延迟统计前，请遵循以下预热步骤：

1. 模拟正式测试的并发级别，提前发起一定数量的调用（例如，持续 1-2 分钟），以充分填充连接池。

2. 确认连接池已建立并维持足够的活跃连接后，再开始正式的性能数据采集。


通过合理的预热，可使 SDK 连接池进入稳定复用状态，从而测量出更具代表性的延迟指标，真实反映服务在线上平稳运行时的性能。

## **Java SDK常见异常**

### **异常 1、 业务流量平稳，但是服务器 TCP 连接数持续上升**

**出错原因：**

**类型一：**

每一个 SDK 对象创建时都会申请一个连接。如果没有使用对象池，每一次任务结束后对象都被析构。此时这一个连接将进入无引用状态，需要等待 61s 秒后服务端报错连接超时才会真正断开，这会导致这个连接在 61 秒内不可复用。

在高并发场景下，新的任务在发现没有可复用连接时会创建新连接，会造成如下后果：

1. 连接数持续上升。

2. 由于连接数过多，服务器资源不足，服务器卡顿。

3. 连接池被打满、新任务由于启动时需要等待可用连接而阻塞。


**类型二：**

对象池配置的MaxIdle小于MaxTotal，导致在对象闲置时，超过MaxIdle的对象被销毁，从而造成连接泄漏。泄漏的连接需要等待61秒超时后断连，同类型一造成连接数持续上升。

**解决方法**：

对于类型一，使用对象池解决。

对于类型二，检查对象池配置参数，设置MaxIdle和MaxTotal相等，关闭对象池自动销毁策略解决。

### 异常 2、任务耗时比正常调用多 60 秒

同“ **异常 1**”，连接池已经达到最大连接限制，新的任务需要等待无引用状态的连接 61 秒触发超时后才可以获得连接。

### 异常 3、服务启动时任务慢，之后慢慢恢复正常

**出错原因**：

在高并发调用时，同一个对象会复用同一个WebSocket连接，因此WebSocket连接只会在服务启动时创建。需要注意的是，任务启动阶段如果立刻开始较高并发调用，同时创建过多的WebSocket连接会导致阻塞。

**解决方法**：

启动服务后逐步提升并发量，或增加预热任务。

### 异常 4、服务端报错 Invalid action('run-task')! Please follow the protocol!

**出错原因**：

这是由于出现了客户端报错后，服务端不知道客户端出错，连接处于任务中状态。此时连接和对象被复用并开启下一个任务，导致流程错误，下一个任务失败。

**解决方法**：

在抛出异常后主动关闭 WebSocket 连接后归还对象池。

### 异常 5、业务流量平稳，调用量出现异常尖刺

**出错原因**：

同时创建过多 WebSocket 连接导致阻塞，但业务流量持续打进来，导致任务短时间积压，并且在阻塞后所有积压任务立刻调用。这会造成调用量尖刺，并且有可能造成瞬时超过账号的并发数限制导致部分任务失败、服务器卡顿等。

这种瞬间创建过多 WebSocket 的情况多发生于：

- 服务启动阶段

- 网络出现异常，大量 WebSocket 连接同时中断重连

- 某一时刻出现大量服务端报错，导致大量 WebSocket 重连。常见报错如并发数超过账号限制（“Requests rate limit exceeded, please try again later.”）。


**解决方法**：

1. 检查网络情况。

2. 排查尖刺前是否出现大量其他服务端报错。

3. 提高账号并发限制。

4. 调小对象池和连接池大小，通过对象池上限限制最大并发数。

5. 提升服务器配置或扩充机器数。


### 异常 6、随着并发数提升，所有任务都变慢

**解决方法**：

1. 检查是否已经达到网络带宽上限。

2. 检查实际并发数是否已经过高。