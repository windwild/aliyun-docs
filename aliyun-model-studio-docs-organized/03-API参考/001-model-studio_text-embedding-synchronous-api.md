### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[通用文本向量](https://help.aliyun.com/zh/model-studio/general-text-embedding/)同步接口API详情

# 同步接口API详情

更新时间：2026-02-11 02:31:00

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：音视频翻译-通义千问](https://help.aliyun.com/zh/model-studio/qwen3-livetranslate-flash-api)[下一篇：批处理接口API详情](https://help.aliyun.com/zh/model-studio/text-embedding-batch-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型概览

前提条件

OpenAI兼容

请求体

响应对象

DashScope

请求体

响应对象

错误码


通用文本向量模型可将文本数据转换为数值向量，用于语义搜索、推荐、聚类、分类等下游任务。

## **模型概览**

| **模型名称** | **向量维度** | **最大行数** | **单行最大** [Token](https://help.aliyun.com/zh/model-studio/billing-for-model-studio#f300d75bd5rb2 "") **数** | **单价（每千输入Token）** | **支持语种** | **免费额度** [（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型名称** | **向量维度** | **最大行数** | **单行最大** [Token](https://help.aliyun.com/zh/model-studio/billing-for-model-studio#f300d75bd5rb2 "") **数** | **单价（每千输入Token）** | **支持语种** | **免费额度** [（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| text-embedding-v4<br>> 属于 [Qwen3-Embedding](https://qwenlm.github.io/zh/blog/qwen3-embedding/) 系列 | 2,048、1,536、1,024（默认）、768、512、256、128、64 | 10 | 8,192 | 0.0005元<br>[Batch调用](https://help.aliyun.com/zh/model-studio/batch-interfaces-compatible-with-openai/ "")：0.00025元 | 中文、英语、西班牙语、法语、葡萄牙语、印尼语、日语、韩语、德语、俄罗斯语等100+主流语种及多种编程语言 | 各100万Token<br>有效期：百炼开通后90天内 |
| text-embedding-v3 | 1,024（默认）、768、512、256、128或64 | 中文、英语、西班牙语、法语、葡萄牙语、印尼语、日语、韩语、德语、俄罗斯语等50+主流语种 |
| text-embedding-v2 | 1,536 | 25 | 2,048 | 0.0007元<br>[Batch调用](https://help.aliyun.com/zh/model-studio/batch-interfaces-compatible-with-openai/ "")：0.00035元 | 中文、英语、西班牙语、法语、葡萄牙语、印尼语、日语、韩语、德语、俄罗斯语 | 各50万Token<br>有效期：百炼开通后90天内 |
| text-embedding-v1 | 中文、英语、西班牙语、法语、葡萄牙语、印尼语 |

关于模型限流，请参考 [限流](https://help.aliyun.com/zh/model-studio/rate-limit#953ddcd76495l "")。

## **前提条件**

若熟悉OpenAI生态，可使用兼容API快速迁移；DashScope API则提供更丰富的独有特性。请根据您的需求选择。

您需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。如果通过SDK调用，还需要 [安装DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

## **OpenAI兼容**

公共云

金融云

**使用SDK调用时需配置的base\_url：** `https://dashscope.aliyuncs.com/compatible-mode/v1`

**使用HTTP方式调用时需配置的endpoint：** `POST https://dashscope.aliyuncs.com/compatible-mode/v1/embeddings`

**使用SDK调用时需配置的base\_url：** `https://dashscope-finance.aliyuncs.com/compatible-mode/v1`

**使用HTTP方式调用时需配置的endpoint：** `POST https://dashscope-finance.aliyuncs.com/compatible-mode/v1/embeddings`

|     |     |
| --- | --- |
| ### **请求体** | 输入字符串<br>输入字符串列表<br>输入文件<br>Python<br>Java<br>curl<br>```python<br>import os<br>from openai import OpenAI<br>client = OpenAI(<br>    api_key=os.getenv("DASHSCOPE_API_KEY"),  # 如果您没有配置环境变量，请在此处用您的API Key进行替换<br>    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1"  # 百炼服务的base_url<br>)<br>completion = client.embeddings.create(<br>    model="text-embedding-v4",<br>    input='衣服的质量杠杠的，很漂亮，不枉我等了这么久啊，喜欢，以后还来这里买',<br>    dimensions=1024, # 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>    encoding_format="float"<br>)<br>print(completion.model_dump_json())<br>```<br>```java<br>import com.openai.client.OpenAIClient;<br>import com.openai.client.okhttp.OpenAIOkHttpClient;<br>import com.openai.models.embeddings.CreateEmbeddingResponse;<br>import com.openai.models.embeddings.EmbeddingCreateParams;<br>public class Main {<br>    public static void main(String[] args) {<br>        // 创建客户端，使用环境变量中的API密钥<br>        OpenAIClient client = OpenAIOkHttpClient.builder()<br>                .apiKey(System.getenv("DASHSCOPE_API_KEY"))<br>                .baseUrl("https://dashscope.aliyuncs.com/compatible-mode/v1")<br>                .build();<br>        // 创建向量化请求参数<br>        EmbeddingCreateParams params = EmbeddingCreateParams.builder()<br>                .model("text-embedding-v4")<br>                .input(EmbeddingCreateParams.Input.ofString("衣服的质量杠杠的，很漂亮，不枉我等了这么久啊，喜欢，以后还来这里买"))<br>                // 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>                .dimensions(1024)<br>                .build();<br>        try {<br>            // 发送请求并获取响应<br>            CreateEmbeddingResponse response = client.embeddings().create(params);<br>            System.out.println(response);<br>        } catch (Exception e) {<br>            System.err.println("请求出错，请查看错误码对照网页：");<br>            System.err.println("https://help.aliyun.com/zh/model-studio/faq-about-alibaba-cloud-model-studio?spm=a2c4g.11186623.help-menu-2400256.d_0_17_0.18733a66lTrcHv#1c38f58abfcml");<br>            System.err.println("错误详情：" + e.getMessage());<br>            e.printStackTrace();<br>        }<br>    }<br>}<br>```<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/compatible-mode/v1/embeddings' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--header 'Content-Type: application/json' \<br>--data '{<br>    "model": "text-embedding-v4",<br>    "input": "风急天高猿啸哀，渚清沙白鸟飞回，无边落木萧萧下，不尽长江滚滚来",  <br>    "dimensions": 1024,  <br>    "encoding_format": "float"<br>}'<br>```<br>Python<br>Java<br>curl<br>```python<br>import os<br>from openai import OpenAI<br>client = OpenAI(<br>    api_key=os.getenv("DASHSCOPE_API_KEY"),  # 如果您没有配置环境变量，请在此处用您的API Key进行替换<br>    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1"  # 百炼服务的base_url<br>)<br>completion = client.embeddings.create(<br>    model="text-embedding-v4",<br>    input=['风急天高猿啸哀', '渚清沙白鸟飞回', '无边落木萧萧下', '不尽长江滚滚来'],<br>    dimensions=1024,# 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>    encoding_format="float"<br>)<br>print(completion.model_dump_json())<br>```<br>```java<br>import com.openai.client.OpenAIClient;<br>import com.openai.client.okhttp.OpenAIOkHttpClient;<br>import com.openai.models.embeddings.CreateEmbeddingResponse;<br>import com.openai.models.embeddings.EmbeddingCreateParams;<br>import java.util.Arrays;<br>import java.util.List;<br>import java.util.ArrayList;<br>public class Main {<br>    public static void main(String[] args) {<br>        // 创建客户端，使用环境变量中的API密钥<br>        OpenAIClient client = OpenAIOkHttpClient.builder()<br>                .apiKey(System.getenv("DASHSCOPE_API_KEY"))<br>                .baseUrl("https://dashscope.aliyuncs.com/compatible-mode/v1")<br>                .build();<br>        // 创建输入字符串列表<br>        List<String> inputList = Arrays.asList(<br>            "风急天高猿啸哀",<br>            "渚清沙白鸟飞回",<br>            "无边落木萧萧下",<br>            "不尽长江滚滚来"<br>        );<br>        // 存储所有响应的列表<br>        List<CreateEmbeddingResponse> responses = new ArrayList<>();<br>        // 循环处理每个字符串<br>        for (String text : inputList) {<br>            try {<br>                // 创建向量化请求参数<br>                EmbeddingCreateParams params = EmbeddingCreateParams.builder()<br>                        .model("text-embedding-v4")<br>                        .input(EmbeddingCreateParams.Input.ofString(text))<br>                        // 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>                        .dimensions(1024)<br>                        .build();<br>                // 发送请求并获取响应<br>                CreateEmbeddingResponse response = client.embeddings().create(params);<br>                responses.add(response);<br>                System.out.println("处理文本: " + text);<br>                System.out.println("向量化结果: " + response);<br>                System.out.println("------------------------");<br>            } catch (Exception e) {<br>                System.err.println("处理文本时出错: " + text);<br>                System.err.println("错误详情：" + e.getMessage());<br>                e.printStackTrace();<br>            }<br>        }<br>        // 打印总结信息<br>        System.out.println("\n总共处理了 " + responses.size() + " 个文本");<br>    }<br>} <br>```<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/compatible-mode/v1/embeddings' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--header 'Content-Type: application/json' \<br>--data '{<br>    "model": "text-embedding-v4",<br>    "input": [<br>        "风急天高猿啸哀",<br>        "渚清沙白鸟飞回", <br>        "无边落木萧萧下", <br>        "不尽长江滚滚来"<br>        ],<br>    "dimensions": 1024,<br>    "encoding_format": "float"<br>}'<br>```<br>Python<br>Java<br>curl<br>```python<br>import os<br>from openai import OpenAI<br>client = OpenAI(<br>    api_key=os.getenv("DASHSCOPE_API_KEY"),  # 如果您没有配置环境变量，请在此处用您的API Key进行替换<br>    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1"  # 百炼服务的base_url<br>)<br># 确保将 'texts_to_embedding.txt' 替换为您自己的文件名或路径<br>with open('texts_to_embedding.txt', 'r', encoding='utf-8') as f:<br>    completion = client.embeddings.create(<br>        model="text-embedding-v4",<br>        input=f,<br>        dimensions=1024,# 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>        encoding_format="float"<br>    )<br>print(completion.model_dump_json())<br>```<br>```java<br>import com.openai.client.OpenAIClient;<br>import com.openai.client.okhttp.OpenAIOkHttpClient;<br>import com.openai.models.embeddings.CreateEmbeddingResponse;<br>import com.openai.models.embeddings.EmbeddingCreateParams;<br>import java.io.BufferedReader;<br>import java.io.FileReader;<br>import java.io.IOException;<br>import java.nio.file.Paths;<br>public class Main {<br>    public static void main(String[] args) {<br>        // 创建客户端，使用环境变量中的API密钥<br>        OpenAIClient client = OpenAIOkHttpClient.builder()<br>                .apiKey(System.getenv("DASHSCOPE_API_KEY"))<br>                .baseUrl("https://dashscope.aliyuncs.com/compatible-mode/v1")<br>                .build();<br>        // 确保将 'texts_to_embedding.txt' 替换为您自己的文件名或绝对路径<br>        String filePath = "/src/main/java/org/example/text_to_embedding.txt";<br>        try {<br>            // 读取文件内容<br>            StringBuilder fileContent = new StringBuilder();<br>            try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {<br>                String line;<br>                while ((line = reader.readLine()) != null) {<br>                    fileContent.append(line).append("\n");<br>                }<br>            }<br>            // 创建向量化请求参数<br>            EmbeddingCreateParams params = EmbeddingCreateParams.builder()<br>                    .model("text-embedding-v4")<br>                    .input(EmbeddingCreateParams.Input.ofString(fileContent.toString()))<br>                    // 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>                    .dimensions(1024)<br>                    .build();<br>            // 发送请求并获取响应<br>            CreateEmbeddingResponse response = client.embeddings().create(params);<br>            System.out.println(response);<br>        } catch (IOException e) {<br>            System.err.println("读取文件时出错：" + e.getMessage());<br>            e.printStackTrace();<br>        } catch (Exception e) {<br>            System.err.println("请求出错，请查看错误码对照网页：");<br>            System.err.println("https://help.aliyun.com/zh/model-studio/faq-about-alibaba-cloud-model-studio?spm=a2c4g.11186623.help-menu-2400256.d_0_17_0.18733a66lTrcHv#1c38f58abfcml");<br>            System.err.println("错误详情：" + e.getMessage());<br>            e.printStackTrace();<br>        }<br>    }<br>} <br>```<br>> 确保将 'texts\_to\_embedding.txt' 替换为您自己的文件名或路径<br>```curl<br>FILE_CONTENT=$(cat texts_to_embedding.txt | jq -Rs .)<br>curl --location 'https://dashscope.aliyuncs.com/compatible-mode/v1/embeddings' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--header 'Content-Type: application/json' \<br>--data '{<br>    "model": "text-embedding-v4",<br>    "input": ['"$FILE_CONTENT"'],<br>    "dimensions": 1024,<br>    "encoding_format": "float"<br>}'<br>``` |
| **model**`string` **必选**<br>调用的模型名称，参考 [模型概览](https://help.aliyun.com/zh/model-studio/text-embedding-synchronous-api#6b8938034edvk "") 表格中的模型名称进行选择。 |
| **input**`array<string> 或 string 或 file` **必选**<br>输入待处理的文本。可以是字符串（string）、字符串列表（array）或文件（file）。不同模型版本支持的文本长度和批量大小不同，具体如下：<br>- **text-embedding-v3 / v4 模型：**<br>  - **输入为字符串**：最长支持 **8,192** Token。<br>    <br>  - **输入为字符串列表或文件**：最多支持 **10** 条（行），每条（行）最长支持 **8,192** Token。<br>- **text-embedding-v1 / v2 模型：**<br>  - **输入为字符串**：最长支持 **2,048** Token。<br>    <br>  - **输入为字符串列表或文件**：最多支持 **25** 条（行），每条（行）最长支持 **2,048** Token。 |
| **dimensions**`integer` **可选**<br>指定的向量维度，必须为以下值之一：2048（仅适用于`text-embedding-v4`）、1536（仅适用于`text-embedding-v4`）1024、768、512、256、128 或 64，默认值为1024。 |
| **encoding\_format**`string` **可选**<br>用于控制返回的Embedding格式，当前仅支持`float`格式。 |

|     |     |
| --- | --- |
| ### **响应对象** | 成功响应<br>异常响应<br>```json<br>{<br>  "data": [<br>    {<br>      "embedding": [<br>        -0.0695386752486229, 0.030681096017360687, ...<br>      ],<br>      "index": 0,<br>      "object": "embedding"<br>    },<br>    ...<br>    {<br>      "embedding": [<br>        -0.06348952651023865, 0.060446035116910934, ...<br>      ],<br>      "index": 5,<br>      "object": "embedding"<br>    }<br>  ],<br>  "model": "text-embedding-v4",<br>  "object": "list",<br>  "usage": {<br>    "prompt_tokens": 184,<br>    "total_tokens": 184<br>  },<br>  "id": "73591b79-d194-9bca-8bb5-xxxxxxxxxxxx"<br>}<br>```<br>```json<br>{<br>    "error": {<br>        "message": "Incorrect API key provided. ",<br>        "type": "invalid_request_error",<br>        "param": null,<br>        "code": "invalid_api_key"<br>    }<br>}<br>``` |
| **data**`array`<br>任务输出信息。<br>**属性**<br>**embedding**`list`<br>本次调用返回object对象的value，类型是元素为float数据的数组，包含具体Embedding向量。<br>**index**`integer`<br>本结构中的算法结果对应的输入文字在输入数组中的索引值。<br>**object** _string_<br>本次调用返回的object对象类型，默认为embedding。 |
| **model**`string`<br>本次调用的模型名。 |
| **object** _string_<br>本次调用返回的data类型，默认为list。 |
| **usage**`object`<br>**属性**<br>**prompt\_tokens** _integer_<br>用户输入文本转换成Token后的长度。<br>**total\_tokens** _integer_<br>本次请求输入内容的 Token 数目，算法的计量是根据用户输入字符串被模型Tokenizer解析之后对应的Token数目来进行。 |
| **id** _string_<br>请求唯一标识。可用于请求明细溯源和问题排查。 |

## DashScope

公共云

金融云

**使用SDK调用时需配置的base\_url：** https://dashscope.aliyuncs.com/api/v1

**使用HTTP方式调用时需配置的endpoint：** POST https://dashscope.aliyuncs.com/api/v1/services/embeddings/text-embedding/text-embedding

**使用HTTP方式调用时需配置的endpoint：**`POST https://dashscope-finance.aliyuncs.com/api/v1/services/embeddings/text-embedding/text-embedding`

**通过SDK调用时需配置的base\_url：**`https://dashscope-finance.aliyuncs.com/api/v1`

**Python**：在导入模块之后，添加以下代码：

```python
dashscope.base_http_api_url = 'https://dashscope-finance.aliyuncs.com/api/v1'
```

**Java** ：将`TextEmbedding textEmbedding = new TextEmbedding();`修改为

```java
TextEmbedding textEmbedding = new TextEmbedding("https://dashscope-finance.aliyuncs.com/api/v1");
```

|     |     |
| --- | --- |
| ### **请求体** | 输入字符串<br>输入字符串列表<br>输入文件<br>Python<br>Java<br>curl<br>```python<br>import dashscope<br>from http import HTTPStatus<br>resp = dashscope.TextEmbedding.call(<br>    model="text-embedding-v4",<br>    input='衣服的质量杠杠的，很漂亮，不枉我等了这么久啊，喜欢，以后还来这里买',<br>    dimension=1024,  # 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>    output_type="dense&sparse"<br>)<br>print(resp) if resp.status_code == HTTPStatus.OK else print(resp)<br>```<br>```java<br>import java.util.Arrays;<br>import com.alibaba.dashscope.embeddings.TextEmbedding;<br>import com.alibaba.dashscope.embeddings.TextEmbeddingParam;<br>import com.alibaba.dashscope.embeddings.TextEmbeddingResult;<br>import com.alibaba.dashscope.exception.ApiException;<br>import com.alibaba.dashscope.exception.NoApiKeyException;<br>/**<br> * 千问文本向量模型调用示例<br> */<br>public final class Main {<br>    public static void main(String[] args) {<br>        try {<br>            // 构建请求参数<br>            TextEmbeddingParam param = TextEmbeddingParam<br>                    .builder()<br>                    .model("text-embedding-v4")  // 使用text-embedding-v4模型<br>                    .texts(Arrays.asList("衣服的质量杠杠的，很漂亮，不枉我等了这么久啊，喜欢，以后还来这里买"))  // 输入文本<br>                    .parameter("dimension", 1024)  // 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>                    .build();<br>            // 创建模型实例并调用<br>            TextEmbedding textEmbedding = new TextEmbedding();<br>            TextEmbeddingResult result = textEmbedding.call(param);<br>            <br>            // 输出结果<br>            System.out.println(result);<br>            <br>        } catch (ApiException | NoApiKeyException e) {<br>            System.out.println("调用失败：" + e.getMessage());<br>        }<br>    }<br>}<br>```<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/embeddings/text-embedding/text-embedding' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--header 'Content-Type: application/json' \<br>--data '{<br>    "model": "text-embedding-v4",<br>    "input": {<br>        "texts": [<br>        "风急天高猿啸哀，渚清沙白鸟飞回，无边落木萧萧下，不尽长江滚滚来"<br>        ]<br>    },<br>    "parameters": {<br>    	"dimension": 1024,<br>    	"output_type": "dense"<br>    }<br>}'<br>```<br>Python<br>Java<br>curl<br>```python<br>import dashscope<br>from http import HTTPStatus<br>DASHSCOPE_MAX_BATCH_SIZE = 10<br>inputs = ['风急天高猿啸哀', '渚清沙白鸟飞回', '无边落木萧萧下', '不尽长江滚滚来']<br>result = None<br>batch_counter = 0<br>for i in range(0, len(inputs), DASHSCOPE_MAX_BATCH_SIZE):<br>    batch = inputs[i:i + DASHSCOPE_MAX_BATCH_SIZE]<br>    resp = dashscope.TextEmbedding.call(<br>        model="text-embedding-v4",<br>        input=batch,<br>        dimension=1024  # 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>    )<br>    if resp.status_code == HTTPStatus.OK:<br>        if result is None:<br>            result = resp<br>        else:<br>            for emb in resp.output['embeddings']:<br>                emb['text_index'] += batch_counter<br>                result.output['embeddings'].append(emb)<br>            result.usage['total_tokens'] += resp.usage['total_tokens']<br>    else:<br>        print(resp)<br>    batch_counter += len(batch)<br>print(result)<br>```<br>```java<br>import java.util.Arrays;<br>import java.util.List;<br>import com.alibaba.dashscope.embeddings.TextEmbedding;<br>import com.alibaba.dashscope.embeddings.TextEmbeddingParam;<br>import com.alibaba.dashscope.embeddings.TextEmbeddingResult;<br>import com.alibaba.dashscope.exception.ApiException;<br>import com.alibaba.dashscope.exception.NoApiKeyException;<br>import com.alibaba.dashscope.embeddings.TextEmbeddingResultItem;<br>public final class Main {<br>    private static final int DASHSCOPE_MAX_BATCH_SIZE = 10;<br>    public static void main(String[] args) {<br>        List<String> inputs = Arrays.asList(<br>                "风急天高猿啸哀",<br>                "渚清沙白鸟飞回",<br>                "无边落木萧萧下",<br>                "不尽长江滚滚来"<br>        );<br>        TextEmbeddingResult result = null;<br>        int batchCounter = 0;<br>        for (int i = 0; i < inputs.size(); i += DASHSCOPE_MAX_BATCH_SIZE) {<br>            List<String> batch = inputs.subList(i, Math.min(i + DASHSCOPE_MAX_BATCH_SIZE, inputs.size()));<br>            TextEmbeddingParam param = TextEmbeddingParam.builder()<br>                    .model("text-embedding-v4")<br>                    .texts(batch)<br>                    .parameter("dimension", 1024)  // 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>                    .build();<br>            TextEmbedding textEmbedding = new TextEmbedding();<br>            try {<br>                TextEmbeddingResult resp = textEmbedding.call(param);<br>                if (resp != null) {<br>                    if (result == null) {<br>                        result = resp;<br>                    } else {<br>                        for (var emb : resp.getOutput().getEmbeddings()) {<br>                            emb.setTextIndex(emb.getTextIndex() + batchCounter);<br>                            result.getOutput().getEmbeddings().add(emb);<br>                        }<br>                        result.getUsage().setTotalTokens(result.getUsage().getTotalTokens() + resp.getUsage().getTotalTokens());<br>                    }<br>                } else {<br>                    System.out.println(resp);<br>                }<br>            } catch (ApiException | NoApiKeyException e) {<br>                e.printStackTrace();<br>            }<br>            batchCounter += batch.size();<br>        }<br>        System.out.println(result);<br>    }<br>}<br>```<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/embeddings/text-embedding/text-embedding' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--header 'Content-Type: application/json' \<br>--data '{<br>    "model": "text-embedding-v4",<br>    "input": {<br>        "texts": [<br>          "风急天高猿啸哀",<br>          "渚清沙白鸟飞回", <br>          "无边落木萧萧下", <br>          "不尽长江滚滚来"<br>        ]<br>    },<br>    "parameters": {<br>    	  "dimension": 1024,<br>    	  "output_type": "dense"<br>    }<br>}'<br>```<br>Python<br>Java<br>curl<br>```python<br>from http import HTTPStatus<br>from dashscope import TextEmbedding<br>with open('texts_to_embedding.txt', 'r', encoding='utf-8') as f:<br>    resp = TextEmbedding.call(<br>        model="text-embedding-v4",<br>        input=f,<br>        dimension=1024 # 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>    )<br>    if resp.status_code == HTTPStatus.OK:<br>        print(resp)<br>    else:<br>        print(resp)<br>```<br>```java<br>import java.io.BufferedReader;<br>import java.io.FileReader;<br>import java.io.IOException;<br>import com.alibaba.dashscope.embeddings.TextEmbedding;<br>import com.alibaba.dashscope.embeddings.TextEmbeddingParam;<br>import com.alibaba.dashscope.embeddings.TextEmbeddingResult;<br>import com.alibaba.dashscope.exception.ApiException;<br>import com.alibaba.dashscope.exception.NoApiKeyException;<br>public final class Main {<br>    public static void main(String[] args) {<br>        try (BufferedReader reader = new BufferedReader(new FileReader("<文件所来自的内容根的路径>"))) {<br>            StringBuilder content = new StringBuilder();<br>            String line;<br>            while ((line = reader.readLine()) != null) {<br>                content.append(line).append("\n");<br>            }<br>            TextEmbeddingParam param = TextEmbeddingParam.builder()<br>                    .model("text-embedding-v4")<br>                    .text(content.toString())<br>                    .parameter("dimension", 1024)  // 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）<br>                    .build();<br>            TextEmbedding textEmbedding = new TextEmbedding();<br>            TextEmbeddingResult result = textEmbedding.call(param);<br>            if (result != null) {<br>                System.out.println(result);<br>            } else {<br>                System.out.println("Failed to get embedding: " + result);<br>            }<br>        } catch (IOException | ApiException | NoApiKeyException e) {<br>            e.printStackTrace();<br>        }<br>    }<br>}<br>```<br>> 确保将 'texts\_to\_embedding.txt' 替换为您自己的文件名或路径<br>```curl<br>FILE_CONTENT=$(cat texts_to_embedding.txt | jq -Rs .)<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/embeddings/text-embedding/text-embedding' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--header 'Content-Type: application/json' \<br>--data '{<br>    "model": "text-embedding-v4",<br>    "input": {<br>        "texts": ['"$FILE_CONTENT"']<br>    },<br>    "parameters": {<br>        "dimension": 1024,<br>        "output_type": "dense"<br>    }<br>}'<br>``` |
| **model**`string` **必选**<br>调用的模型，参考 [模型概览](https://help.aliyun.com/zh/model-studio/text-embedding-synchronous-api#6b8938034edvk "") 表格中的模型名称进行选择。 |
| **input**`string` _或_`array<string>` **必选**<br>输入待处理的文本。可以是字符串（string）、字符串列表（array）或文件（file）。不同模型版本支持的文本长度和批量大小不同，具体如下：<br>- **text-embedding-v3 / v4 模型：**<br>  - **输入为字符串**：最长支持 **8,192** Token。<br>    <br>  - **输入为字符串列表或文件**：最多支持 **10** 条（行），每条（行）最长支持 **8,192** Token。<br>- **text-embedding-v1 / v2 模型：**<br>  - **输入为字符串**：最长支持 **2,048** Token。<br>    <br>  - **输入为字符串列表或文件**：最多支持 **25** 条（行），每条（行）最长支持 **2,048** Token。 |
| **text\_type**`string` **可选**<br>> 通过 HTTP 调用时，请将 **text\_type** 放入parameters对象中。<br>文本转换为向量后可以应用于检索、聚类、分类等下游任务，对检索这类非对称任务为了达到更好的检索效果建议区分查询文本（query）和底库文本（document）类型，入库、聚类、分类等对称任务可以不用特殊指定，采用系统默认值`document`即可。 |
| **dimension**`integer` **可选**<br>> 通过 HTTP 调用时，请将 **dimension** 放入parameters对象中。<br>指定的向量维度，必须为以下值之一：2048（仅适用于`text-embedding-v4`）、1536（仅适用于`text-embedding-v4`）1024、768、512、256、128 或 64，默认值为1024。 |
| **output\_type**`string` **可选**<br>> 通过 HTTP 调用时，请将 **output\_type** 放入parameters对象中。<br>用户指定输出离散向量表示只适用于`text-embedding-v3`与`text-embedding-v4`模型，取值在dense、sparse、dense&sparse之间，默认取dense，只输出连续向量。 |
| **instruct**`string` **可选**<br>添加自定义任务说明，可用于指导模型理解查询意图。建议使用英文撰写，通常可带来约 1%–5% 的效果提升。 |

|     |     |
| --- | --- |
| ### **响应对象** | 成功响应<br>异常响应<br>```json<br>{   "status_code": 200, <br>    "request_id": "1ba94ac8-e058-99bc-9cc1-7fdb37940a46", <br>    "code": "", <br>    "message": "",<br>    "output":{<br>        "embeddings": [<br>          {  <br>             "sparse_embedding":[<br>               {"index":7149,"value":0.829,"token":"风"},<br>               .....<br>               {"index":111290,"value":0.9004,"token":"哀"}],<br>             "embedding": [-0.006929283495992422,-0.005336422007530928, ...],<br>             "text_index": 0<br>          }, <br>          {<br>             "sparse_embedding":[<br>               {"index":246351,"value":1.0483,"token":"渚"},<br>               .....<br>               {"index":2490,"value":0.8579,"token":"回"}],<br>             "embedding": [-0.006929283495992422,-0.005336422007530928, ...],<br>             "text_index": 1<br>          },<br>          {<br>             "sparse_embedding":[<br>               {"index":3759,"value":0.7065,"token":"无"},<br>               .....<br>               {"index":1130,"value":0.815,"token":"下"}],<br>             "embedding": [-0.006929283495992422,-0.005336422007530928, ...],<br>             "text_index": 2<br>          },<br>          {<br>             "sparse_embedding":[<br>               {"index":562,"value":0.6752,"token":"不"},<br>               .....<br>               {"index":1589,"value":0.7097,"token":"来"}],<br>             "embedding": [-0.001945948973298072,-0.005336422007530928, ...],<br>             "text_index": 3<br>          }<br>        ]<br>    },<br>    "usage":{<br>        "total_tokens":27<br>    }<br>}<br>```<br>```json<br>{<br>    "code":"InvalidApiKey",<br>    "message":"Invalid API-key provided.",<br>    "request_id":"xxxxxxxx"<br>}<br>``` |
| **status\_code**`string`<br>状态码，表示请求的执行结果（如 200 表示成功）。 |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |
| **code**`string`<br>请求失败，表示错误码，成功时返回参数中该参数为空。 |
| **message**`string`<br>请求失败，表示失败详细信息，成功时返回参数中该参数为空。 |
| **output**`object`<br>任务输出信息。<br>**属性**<br>**embeddings**`array`<br>本次请求的算法输出内容，是一个由结构组成的数组，每一个数组中包含一个对应的输入 text 的算法输出内容。<br>**属性**<br>**sparse\_embedding**`array`<br>对应字符串的算法输出离散向量表示 （sparse embedding仅适用于`text-embedding-v3`与`text-embedding-v4`）。<br>**属性**<br>**index**`integer`<br>词汇或字符在词汇表中的位置索引。<br>**value**`float`<br>表示该 `Token` 的权重或重要性分数，值越高，表示该 `Token` 在当前文本上下文中的重要性或相关性越大。<br>**token**`string`<br>实际的文本单元或词汇表中的词。<br>**embedding**`array`<br>对应字符串的算法输出连续向量表示 （dense embedding)。<br>**text\_index**`integer`<br>本结构中的算法结果对应的输入文字在输入数组中的索引值。 |
| **usage**`object`<br>**属性**<br>**total\_tokens** _integer_<br>本次请求输入内容的 token 数目，算法的计量是根据用户输入字符串被模型tokenizer解析之后对应的token 数目来进行。 |

## 错误码

如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。