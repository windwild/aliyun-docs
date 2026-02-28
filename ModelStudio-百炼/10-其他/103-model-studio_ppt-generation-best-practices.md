### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用广场](https://help.aliyun.com/zh/model-studio/application-gallery/)[官方应用-全妙解决方案类产品](https://help.aliyun.com/zh/model-studio/quanmiao-solution-products/)[开发文档](https://help.aliyun.com/zh/model-studio/ai-quan-miao-development-document/)[最佳实践](https://help.aliyun.com/zh/model-studio/miaobi-and-miaoce-best-practices/)PPT生成最佳实践

# PPT生成最佳实践

更新时间：2026-01-30 03:17:56

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：视频混剪](https://help.aliyun.com/zh/model-studio/best-practices-for-video-mixing-and-cutting)[下一篇：服务关联角色](https://help.aliyun.com/zh/model-studio/quanmiao-slr)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

操作步骤

第一步：流式生成PPT大纲内容

第二步：初始化用来创建PPT的会话

第三步：初始化前端SDK

第四步：绑定作品信息

其他

获取PPT组件配置

编辑PPT作品

界面销毁PPT插件

本文提供 **PPT生成** 链路API的最佳实践，帮助您快速入门并开发您自己的业务应用。

## 前提条件

- 点击 [PPT生成下单地址](https://common-buy.aliyun.com/?spm=a2c4g.11186623.0.0.24c66c00ZsOBpm&commodityCode=sfm_pptgeneration_public_cn) 开通服务；

- [获取Workspace ID](https://help.aliyun.com/zh/model-studio/obtain-the-app-id-and-workspace-id#732535cfc959h "")；

- [获取 AccessKey 与 AgentKey](https://help.aliyun.com/zh/model-studio/get-accesskey-appid-and-agentkey "")；

- 引入妙笔SDK [注意获取最新SDK版本](https://api.aliyun.com/api-tools/sdk/AiMiaoBi?version=2023-08-01&language=java-async-tea&tab=primer-doc)。


Java

Python

JavaScript

Java

```java
<dependency>
  <groupId>com.aliyun</groupId>
  <artifactId>alibabacloud-aimiaobi20230801</artifactId>
  <version>1.0.84</version>
</dependency>
```

Python

```python
alibabacloud-tea-openapi-sse==1.0.2
```

JavaScript

```javascript
"@alicloud/openapi-core": "^1.0.2",
"@alicloud/tea-typescript": "^1.7.1",
"@alicloud/openapi-client": "^0.4.12",
```

获取前端SDK：

```json
https://quanmiao-public.oss-cn-beijing.aliyuncs.com/quanmiao-sdk/v1.0.0/index.js
```

## **操作步骤**

### **第一步：流式生成PPT大纲内容**

Java

Python

JavaScript

Java

```java
public static AsyncClient getClient() {
    if (client == null) {
        synchronized (ClientHelper.class) {
            if (client == null) {
                StaticCredentialProvider provider = StaticCredentialProvider.create(
                    Credential.builder()
                            .accessKeyId("access-key-id")
                            .accessKeySecret("access-key-secret")
                            .build()
            );
            client = AsyncClient.builder()
                    .region("cn-beijing")
                    .credentialsProvider(provider)
                    .serviceConfiguration(Configuration.create().setSignatureVersion(SignatureVersion.V3))
                    .overrideConfiguration(
                            ClientOverrideConfiguration.create()
                                    .setProtocol("HTTPS")
                                    .setEndpointOverride("aimiaobi.cn-beijing.aliyuncs.com")
                    )
                    .build();
            }
        }
    }
    return client;
}

AsyncClient client = getClient();
RunPptOutlineGenerationRequest runRequest = RunPptOutlineGenerationRequest.builder()
      .workspaceId(workspaceId)
      .prompt("生成一个关于消防主题的ppt")
      .build();

ResponseIterator<RunPptOutlineGenerationResponseBody> iterator = client.runPptOutlineGenerationWithResponseIterable(runRequest).iterator();
while (iterator.hasNext()) {
    RunPptOutlineGenerationResponseBody event = iterator.next();
    System.out.println(new Date() + " === " + JSON.toJSONString(event));
}
```

Python

```python
# 前置要求：
# 1、python版本：3.7+；
# 2、安装依赖：pip3 install alibabacloud-tea-openapi-sse==1.0.2
import os

from alibabacloud_tea_openapi_sse.client import Client as OpenApiClient
from alibabacloud_tea_openapi_sse import models as open_api_models
from alibabacloud_tea_util_sse import models as util_models
import asyncio
import json

biz_param = ('{"WorkspaceId":"llm-xxxxxx","Prompt":"生成一个关于消防主题的ppt"}')

class AiMiaoBi:
    def __init__(self) -> None:
        # 工程代码泄露可能会导致 AccessKey 泄露，并威胁账号下所有资源的安全性。以下代码示例仅供参考。
        # 建议使用更安全的 STS 方式，更多鉴权访问方式请参见：https://help.aliyun.com/document_detail/378659.html。
        self.access_key_id = os.environ['accessKeyId']
        self.access_key_secret = os.environ['accessKeySecret']
        # 以上字段请改成实际的值。
        self.endpoint = 'aimiaobi.cn-beijing.aliyuncs.com'
        self._client = None
        self._api_info = self._create_api_info()
        self._runtime = util_models.RuntimeOptions(read_timeout=1000 * 100)
        self._client = self._create_client(self.access_key_id, self.access_key_secret, self.endpoint)

    def _create_client(
            self,
            access_key_id: str,
            access_key_secret: str,
            endpoint: str,
    ) -> OpenApiClient:
        config = open_api_models.Config(
            access_key_id=access_key_id,
            access_key_secret=access_key_secret,
            endpoint=endpoint
        )
        return OpenApiClient(config)

    def _create_api_info(self) -> open_api_models.Params:
        """
        API 相关
        @param path: params
        @return: OpenApi.Params
        """
        params = open_api_models.Params(
            # 接口名称
            action='RunPptOutlineGeneration',
            # 接口版本
            version='2023-08-01',
            # 接口协议
            protocol='HTTPS',
            # 接口 HTTP 方法
            method='POST',
            auth_type='AK',
            style='RPC',
            # 接口 PATH,
            pathname='/quanmiao/aimiaosou/runPptOutlineGeneration',
            # 接口请求体内容格式,
            req_body_type='json',
            # 接口响应体内容格式,
            body_type='sse'
        )
        return params

    async def do_sse_query(self):
        if biz_param == '':
            param = {}
        else:
            param: dict = json.loads(biz_param)

        request = open_api_models.OpenApiRequest(
            body=param
        )
        sse_receiver = self._client.call_sse_api_async(params=self._api_info, request=request, runtime=self._runtime)
        return sse_receiver

# 接口调用
async def run():
    aiMiaoBi = AiMiaoBi()
    async for res in await aiMiaoBi.do_sse_query():
        try:
            data = json.loads(res.get('event').data)
            print(data)
        except json.JSONDecodeError:
            print('------json.JSONDecodeError--------')
            print(res.get('headers'))
            print(res.get('event').data)
            print('------json.JSONDecodeError-end--------')
            continue
    print('------end--------')

if __name__ == '__main__':
    asyncio.run(run())
```

JavaScript

```javascript
'use strict';
var __asyncValues = (this && this.__asyncValues) || function (o) {
    if (!Symbol.asyncIterator) throw new TypeError("Symbol.asyncIterator is not defined.");
    var m = o[Symbol.asyncIterator], i;
    return m ? m.call(o) : (o = typeof __values === "function" ? __values(o) : o[Symbol.iterator](), i = {}, verb("next"), verb("throw"), verb("return"), i[Symbol.asyncIterator] = function () { return this; }, i);
    function verb(n) { i[n] = o[n] && function (v) { return new Promise(function (resolve, reject) { v = o[n](v), settle(resolve, reject, v.done, v.value); }); }; }
    function settle(resolve, reject, d, v) { Promise.resolve(v).then(function(v) { resolve({ value: v, done: d }); }, reject); }
};

const OpenApi = require('@alicloud/openapi-core');
const Dara = require('@darabonba/typescript');
class Client {
    /**
     * 使用AK&SK初始化账号Client
     * @return Client
     * @throws Exception
     */
    static createClient() {
        let config = new OpenApi.$OpenApiUtil.Config({
            accessKeyId: 'xxxx',
            accessKeySecret: 'xxxx',
        });
        config.endpoint = `aimiaobi.cn-beijing.aliyuncs.com`;
        return new OpenApi.default(config);
    }
    /**
     * API 相关
     * @param path params
     * @return OpenApi.Params
     */
    static createApiInfo() {
        let params = new OpenApi.$OpenApiUtil.Params({
            // 接口名称
            action: 'RunPptOutlineGeneration',
            // 接口版本
            version: '2023-08-01',
            // 接口协议
            protocol: 'HTTPS',
            // 接口 HTTP 方法
            method: 'POST',
            authType: 'AK',
            style: 'V3',
            // 接口 PATH
            pathname: `/quanmiao/miaosou/runPptOutlineGeneration`,
            // 接口请求体内容格式
            reqBodyType: 'json',
            // 接口响应体内容格式
            bodyType: 'sse',
        });
        return params;
    }

    static async main(args) {
        var _a, e_1, _b, _c;
        let client = Client.createClient();
        let params = Client.createApiInfo();
        let body = { };
        body['WorkspaceId'] = 'llm-xxxxx';
        body['Prompt'] = '生成一个关于消防主题的ppt';
        let request = new OpenApi.$OpenApiUtil.OpenApiRequest({
            body: body,
        });
        try {
            let response = await client.callSSEApi(params, request, new Dara.RuntimeOptions({"readTimeout": 60000, "connectTimeout": 60000}));
            //console.log(response);
            try {
                for (var _d = true, response_1 = __asyncValues(response), response_1_1; response_1_1 = await response_1.next(), _a = response_1_1.done, !_a; _d = true) {
                    _c = response_1_1.value;
                    _d = false;
                    const value = _c;
                    console.log('-'.repeat(30));
                    console.log(value.event);
                }
            }
            catch (e_1_1) { e_1 = { error: e_1_1 }; }
            finally {
                try {
                    if (!_d && !_a && (_b = response_1.return)) await _b.call(response_1);
                }
                finally { if (e_1) throw e_1.error; }
            }
        }
        catch (error) {
            console.log(error);
        }
    }
}
exports.Client = Client;
Client.main(process.argv.slice(2));
```

### **第二步：初始化用来创建PPT的会话**

**重要说明**：这个接口涉及到扣费，请注意费用

这个接口包含两部分：

1. 下发用于初始化“PPT生成”的前端组件的code

2. 进行计费


通过 [InitiatePptCreation - 初始化用来创建PPT的会话](https://help.aliyun.com/zh/model-studio/api-aimiaobi-2023-08-01-initiatepptcreation "") 接口初始化创建PPT的会话，如下为示例代码：

```java
taskId = "xxxx";

AsyncClient client = ClientHelper.getClient();
InitiatePptCreationRequest request = InitiatePptCreationRequest.builder()
      .workspaceId(workspaceId)
      .taskId(taskId)
      .outline("# 中国传统文化艺术的魅力")
      .build();
CompletableFuture<InitiatePptCreationResponse> future = client.initiatePptCreation(request);
try {
    InitiatePptCreationResponse response = future.get();
    System.out.println("result: " + JSON.toJSONString(response));
} catch (InterruptedException e) {
    throw new RuntimeException(e);
} catch (ExecutionException e) {
    throw new RuntimeException(e);
}
```

### **第三步：初始化前端SDK**

1. 全局加载quanmiao-sdk:


```java
const SDK_URL = "https://quanmiao-public.oss-cn-beijing.aliyuncs.com/quanmiao-sdk/v1.0.0/index.js";
const script = document.createElement('script');
script.src = SDK_URL;
script.async = true;
document.body.appendChild(script);
```

2. 创建PPT：


```java
// 确保SDK已经加载完
await windows.Quanmiao.createPPT({
    appkey: 'your appkey', // 必填，从InitiatePptCreation接口获取
    code: 'your code', // 必填，从InitiatePptCreation接口获取
    container: '你的渲染容器', // 必填
    content: '你的PPT大纲', // 必填
    speaker: 'PPT主讲人', // 非必填，不传则默认为 'XXX'
    onMessage(type, data) {
      if (type === 'CHARGING') {
        // 这里可以拿到创建任务id：data?.taskId，
        // 通过任务id绑定作品信息之后可以获取作品列表(包含作品id信息)
      }
      if (type === 'SET_PPT_MAKING_STATUS') {
        if (data?.status === '1') {
          // 正在生成中
        }
        if (data?.status === '0') {
          // 生成完成
        }
      }
    },
  });
} catch (e) {
  console.log('调用PPT SDK err=>', e);
  message.error(e?.msg || e?.message || '操作异常');
}
```

### **第四步：绑定作品信息**

```java
taskId = "6831f55d-fa3b-4592-b3fd-bdf47ca2ab96";

AsyncClient client = ClientHelper.getClient();
BindPptArtifactRequest request = BindPptArtifactRequest.builder()
      .workspaceId(workspaceId)
      .taskId(taskId)
      .artifactId(12345)
      .build();
CompletableFuture<BindPptArtifactResponse> future = client.bindPptArtifact(request);
try {
    BindPptArtifactResponse response = future.get();
    System.out.println("result: " + JSON.toJSONString(response));
} catch (InterruptedException e) {
    throw new RuntimeException(e);
} catch (ExecutionException e) {
    throw new RuntimeException(e);
}
```

## **其他**

### **获取PPT组件配置**

GetPptConfig

```java
AsyncClient client = ClientHelper.getClient();
GetPptConfigRequest request = GetPptConfigRequest.builder()
      .workspaceId(workspaceId)
      .build();
CompletableFuture<GetPptConfigResponse> future = client.getPptConfig(request);
try {
    GetPptConfigResponse response = future.get();
    System.out.println("result: " + JSON.toJSONString(response));
} catch (InterruptedException e) {
    throw new RuntimeException(e);
} catch (ExecutionException e) {
    throw new RuntimeException(e);
}
```

### **编辑PPT作品**

先调接口获取PPT组件配置，然后初始化前端SDK

```java
// 确保SDK已经加载完
await windows.Quanmiao.editPPT({
  appkey: 'your appkey', // 必填，从InitiatePptCreation接口获取
  code: 'your code', // 必填，从InitiatePptCreation接口获取
  container: '你的渲染容器', // 必填
  id: 88888, // 作品id，必填
});
```

### **界面销毁PPT插件**

```java
windows.Quanmiao.deleteIframe();
```