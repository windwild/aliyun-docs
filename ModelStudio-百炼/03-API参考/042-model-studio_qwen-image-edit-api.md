### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[图像生成](https://help.aliyun.com/zh/model-studio/image-generation/)千问-图像编辑

# 千问-图像编辑API参考

更新时间：2026-02-08 21:12:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型概览

前提条件

HTTP调用

DashScope SDK调用

Python SDK调用

Java SDK调用

图像访问权限配置

错误码

计费与限流

常见问题

千问-图像编辑模型支持多图输入和多图输出，可精确修改图内文字、增删或移动物体、改变主体动作、迁移图片风格及增强画面细节。

|     |
| --- |
| **快速入口：** [使用指南](https://help.aliyun.com/zh/model-studio/qwen-image-edit-guide "") **\|** [技术博客](https://qwen.ai/blog?id=1675c295dc29dd31073e5b3f72876e9d684e41c6&from=research.research-list) \| [在线体验](https://bailian.console.aliyun.com/?tab=model#/efm/model_experience_center/vision?currentTab=imageGenerate&modelId=qwen-image-edit) |

## **模型概览**

多图图像修改展示器

![输入图1](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/thtclx/input1.png)

![输入图2](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/iclsnx/input2.png)

![输入图3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/gborgw/input3.png)

![原图](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/thtclx/input1.png)

![修改后的图](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/kgfnqe/image100.png)

图1中的女孩穿着图2中的黑色裙子按图3的姿势坐下

| **模型名称** | **模型简介** | **输出图像规格** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **模型简介** | **输出图像规格** |
| qwen-image-edit-max<br>> 当前与qwen-image-edit-max-2026-01-16能力相同 | 支持单图编辑和多图融合。<br>- 可输出 **1-6** 张图片。<br>  <br>- 支持自定义分辨率。<br>  <br>- 支持 [提示词智能改写](https://help.aliyun.com/zh/model-studio/qwen-image-edit-api#e2aeaf0d93cy9 "") **。** | **格式**：PNG<br>**分辨率**：<br>- **可指定**：通过 `parameters.size` 参数指定输出图像的`宽*高`（单位：像素）。<br>  <br>- **默认（不指定时）**：总像素数接近 `1024*1024`，宽高比与输入图（多图输入时为最后一张）相近。 |
| qwen-image-edit-max-2026-01-16 |
| qwen-image-edit-plus<br>> 当前与qwen-image-edit-plus-2025-10-30能力相同 |
| qwen-image-edit-plus-2025-12-15 |
| qwen-image-edit-plus-2025-10-30 |
| qwen-image-edit | 支持单图编辑和多图融合。<br>- 仅支持输出 1 张图片。<br>  <br>- 不支持自定义分辨率。 | **格式**：PNG<br>**分辨率**： **不可指定**。生成规则同上方的 **默认** 规则。 |

**说明**

调用前，请查阅各地域支持的[模型列表](https://help.aliyun.com/zh/model-studio/models#bfe15d8aa2lxh "")。

## **前提条件**

在调用前，您需要 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，再 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

如需通过SDK进行调用，请 [安装DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。目前，该SDK已支持Python和Java。

**重要**

北京和新加坡地域拥有独立的 **API Key** 与 **请求地址**，不可混用，跨地域调用将导致鉴权失败或服务报错。

## HTTP调用

**北京地域**：`POST https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation`

**新加坡地域**：`POST https://dashscope-intl.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation`

|     |     |
| --- | --- |
| #### 请求参数 | 单图编辑<br>多图融合<br>此处以使用`qwen-image-edit-max`模型输出2张图片为例。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation' \<br>--header 'Content-Type: application/json' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--data '{<br>    "model": "qwen-image-edit-max",<br>    "input": {<br>        "messages": [<br>            {<br>                "role": "user",<br>                "content": [<br>                    {<br>                        "image": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/fpakfo/image36.webp"<br>                    },<br>                    {<br>                        "text": "生成一张符合深度图的图像，遵循以下描述：一辆红色的破旧的自行车停在一条泥泞的小路上，背景是茂密的原始森林"<br>                    }<br>                ]<br>            }<br>        ]<br>    },<br>    "parameters": {<br>        "n": 2,<br>        "negative_prompt": " ",<br>        "prompt_extend": true,<br>        "watermark": false,<br>        "size": "1536*1024"<br>    }<br>}'<br>```<br>此处以使用`qwen-image-edit-max`模型输出2张图片为例。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation' \<br>--header 'Content-Type: application/json' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--data '{<br>    "model": "qwen-image-edit-max",<br>    "input": {<br>        "messages": [<br>            {<br>                "role": "user",<br>                "content": [<br>                    {<br>                        "image": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/thtclx/input1.png"<br>                    },<br>                    {<br>                        "image": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/iclsnx/input2.png"<br>                    },<br>                    {<br>                        "image": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/gborgw/input3.png"<br>                    },<br>                    {<br>                        "text": "图1中的女生穿着图2中的黑色裙子按图3的姿势坐下"<br>                    }<br>                ]<br>            }<br>        ]<br>    },<br>    "parameters": {<br>        "n": 2,<br>        "negative_prompt": " ",<br>        "prompt_extend": true,<br>        "watermark": false,<br>        "size": "1024*1536"<br>    }<br>}'<br>``` |
| ##### 请求头（Headers） |
| **Content-Type**`string` **（必选）**<br>请求内容类型。此参数必须设置为`application/json`。 |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| ##### 请求体（Request Body） |
| **model**`string` **（必选）**<br>模型名称，示例值qwen-image-edit-max。 |
| **input**`object` **（必选）**<br>输入参数对象，包含以下字段：<br>**属性**<br>**messages**`array` **（必选）**<br>请求内容数组。 **当前仅支持单轮对话**，因此数组内 **有且只有一个对象**，该对象包含`role`和`content`两个属性。<br>**属性**<br>**role**`string` **（必选）**<br>消息发送者角色，必须设置为`user`。<br>**content**`array` **（必选）**<br>消息内容，包含1-3张图像，格式为 `{"image": "..."}`；以及单个编辑指令，格式为 `{"text": "..."}`。<br>**属性**<br>**image**`string` **（必选）**<br>输入图像的 URL 或 Base64 编码数据。支持传入1-3张图像。<br>多图输入时，按照数组顺序定义图像顺序，输出图像的比例以最后一张为准。<br>**图像要求：**<br>- 图像格式：JPG、JPEG、PNG、BMP、TIFF、WEBP和GIF。<br>  <br>  <br>> 输出图像为PNG格式，对于GIF动图，仅处理其第一帧。<br>  <br>- 图像分辨率：为获得最佳效果，建议图像的宽和高均在384像素至3072像素之间。分辨率过低可能导致生成效果模糊，过高则会增加处理时长。<br>  <br>- 图像大小：不超过10MB。<br>  <br>**支持的输入格式**<br>1. 公网URL：<br>   <br>   - 支持 HTTP 和 HTTPS 协议。<br>     <br>   - 示例值：`https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/fpakfo/image36.webp`。<br>2. 临时URL：<br>   <br>   - 支持OSS协议，必须通过 [上传文件获取临时 URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。<br>     <br>   - 示例值：`oss://dashscope-instant/xxx/2024-07-18/xxx/cat.png`。<br>3. 传入 Base64 编码图像后的字符串<br>   <br>   - 示例值：`data:image/jpeg;base64,GDU7MtCZz...`（示例已截断，仅做演示）<br>     <br>   - Base64 编码规范请参见[通过Base64编码传入图片](https://help.aliyun.com/zh/model-studio/qwen-image-edit-api#907c84c1a6wrm "")。<br>**text**`string` **（必选）**<br>正向提示词，用于描述期望生成的图像内容、风格和构图。<br>支持中英文，长度不超过800个字符，每个汉字、字母、数字或符号计为一个字符，超过部分会自动截断。<br>示例值：图1中的女生穿着图2中的黑色裙子按图3的姿势坐下，保持其服装、发型和表情不变，动作自然流畅。<br>**注意**：仅支持传入一个text，不传或传入多个将报错。 |
| **parameters**`object` （可选）<br>控制图像生成的附加参数。<br>**属性**<br>**n**`integer` （可选）<br>输出图像的数量，默认值为1。<br>对于qwen-image-edit-max、qwen-image-edit-plus系列模型，可选择输出1-6张图片。<br>对于`qwen-image-edit`，仅支持输出1张图片。<br>**negative\_prompt**`string` （可选）<br>反向提示词，用来描述不希望在画面中看到的内容，可以对画面进行限制。<br>支持中英文，长度上限500个字符，每个汉字、字母、数字或符号计为一个字符，超过部分会自动截断。<br>示例值：低分辨率、错误、最差质量、低质量、残缺、多余的手指、比例不良等。<br>**size**`string` （可选）<br>设置输出图像的分辨率，格式为`宽*高`，例如`"1024*1536"`。宽和高的取值范围均为\[512, 2048\]像素。<br>常见比例推荐分辨率<br>- 1:1: 1024\*1024、1536\*1536<br>  <br>- 2:3: 768\*1152、1024\*1536<br>  <br>- 3:2: 1152\*768、1536\*1024<br>  <br>- 3:4: 960\*1280、1080\*1440<br>  <br>- 4:3: 1280\*960、1440\*1080<br>  <br>- 9:16: 720\*1280、1080\*1920<br>  <br>- 16:9: 1280\*720、1920\*1080<br>  <br>- 21:9: 1344\*576、2048\*872<br>  <br>**输出图像尺寸的规则**<br>- 指定 `size` 参数，系统会以 `size`指定的宽高为目标，将实际输出图像的宽高调整为最接近的16的倍数。例如，设置`1033*1032`，输出图像尺寸为`1040*1024`。<br>  <br>- 若不设置，输出图像将保持与输入图像（多图输入时为最后一张）相似的宽高比，总像素数接近`1024*1024`。<br>  <br>**支持模型**：qwen-image-edit-max、qwen-image-edit-plus系列模型。<br>**prompt\_extend**`bool` （可选） <br>是否开启提示词智能改写，默认值为 `true`。开启后，模型会优化正向提示词（`text`），对描述较简单的提示词效果提升明显。<br>**支持模型**：qwen-image-edit-max、qwen-image-edit-plus系列模型。<br>**watermark**`bool` （可选） <br>是否在图像右下角添加 "Qwen-Image" 水印。默认值为 `false`。水印样式如下：<br>![1](<Base64-Image-Removed>)<br>**seed**`integer` （可选）<br>随机数种子，取值范围`[0,2147483647]`。<br>使用相同的`seed`参数值可使生成内容保持相对稳定。若不提供，算法将自动使用随机数种子。<br>**注意**：模型生成过程具有概率性，即使使用相同的`seed`，也不能保证每次生成结果完全一致。 |

|     |     |
| --- | --- |
| #### 响应参数 | 任务执行成功<br>任务执行异常<br>任务数据（如任务状态、图像URL等）仅保留24小时，超时后会被自动清除。请您务必及时保存生成的图像。<br>```json<br>{<br>    "output": {<br>        "choices": [<br>            {<br>                "finish_reason": "stop",<br>                "message": {<br>                    "role": "assistant",<br>                    "content": [<br>                        {<br>                            "image": "https://dashscope-result-sz.oss-cn-shenzhen.aliyuncs.com/xxx.png?Expires=xxx"<br>                        },<br>                        {<br>                            "image": "https://dashscope-result-sz.oss-cn-shenzhen.aliyuncs.com/xxx.png?Expires=xxx"<br>                        }<br>                    ]<br>                }<br>            }<br>        ]<br>    },<br>    "usage": {<br>        "width": 1536,<br>        "image_count": 2,<br>        "height": 1024<br>    },<br>    "request_id": "bf37ca26-0abe-98e4-8065-xxxxxx"<br>}<br>```<br>如果因为某种原因导致任务执行失败，将返回相关信息，可以通过code和message字段明确指示错误原因。请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "request_id": "31f808fd-8eef-9004-xxxxx",<br>    "code": "InvalidApiKey",<br>    "message": "Invalid API-key provided."<br>}<br>``` |
| **output**`object`<br>包含模型生成结果。<br>**属性**<br>**choices**`array`<br>结果选项列表。<br>**属性**<br>**finish\_reason**`string`<br>任务停止原因，自然停止时为`stop`。<br>**message**`object`<br>模型返回的消息。<br>**属性**<br>**role**`string`<br>消息的角色，固定为`assistant`。<br>**content**`array`<br>消息内容，包含生成的图像信息。<br>**属性**<br>**image**`string`<br>生成图像的 URL，格式为PNG。 **链接有效期为24小时**，请及时下载并保存图像。 |
| **usage**`object`<br>本次调用的资源使用情况，仅调用成功时返回。<br>**属性**<br>**image\_count**`integer`<br>生成图像的张数。<br>**width**`integer`<br>生成图像的宽度（像素）。<br>**height**`integer`<br>生成图像的高度（像素）。 |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |
| **code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |
| **message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |

## DashScope SDK调用

SDK 的参数命名与 [HTTP接口](https://help.aliyun.com/zh/model-studio/qwen-image-edit-api#42703589880ts "") 基本一致，参数结构根据语言特性进行封装，完整参数列表请参见 [千问 API 参考](https://help.aliyun.com/zh/model-studio/qwen-api-reference/ "")。

### Python SDK调用

**说明**

- 推荐安装最新版DashScope Python SDK，否则可能运行报错： [安装或升级SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

- 不支持异步接口。


#### **请求示例**

通过公网URL传入图片

通过Base64编码传入图片

通过URL下载图像

```python
import json
import os
from dashscope import MultiModalConversation
import dashscope

# 以下为中国（北京）地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 模型支持输入1-3张图片
messages = [\
    {\
        "role": "user",\
        "content": [\
            {"image": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/thtclx/input1.png"},\
            {"image": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/iclsnx/input2.png"},\
            {"image": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/gborgw/input3.png"},\
            {"text": "图1中的女生穿着图2中的黑色裙子按图3的姿势坐下"}\
        ]\
    }\
]

# 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 若没有配置环境变量，请用百炼 API Key 将下行替换为：api_key="sk-xxx"
api_key = os.getenv("DASHSCOPE_API_KEY")

# qwen-image-edit-max、qwen-image-edit-plus系列支持输出1-6张图片，此处以2张为例
response = MultiModalConversation.call(
    api_key=api_key,
    model="qwen-image-edit-max",
    messages=messages,
    stream=False,
    n=2,
    watermark=False,
    negative_prompt=" ",
    prompt_extend=True,
    size="1024*1536",
)

if response.status_code == 200:
    # 如需查看完整响应，请取消下行注释
    # print(json.dumps(response, ensure_ascii=False))
    for i, content in enumerate(response.output.choices[0].message.content):
        print(f"输出图像{i+1}的URL:{content['image']}")
else:
    print(f"HTTP返回码：{response.status_code}")
    print(f"错误码：{response.code}")
    print(f"错误信息：{response.message}")
    print("请参考文档：https://help.aliyun.com/zh/model-studio/error-code")
```

```python
import json
import os
from dashscope import MultiModalConversation
import base64
import mimetypes
import dashscope

# 以下为中国（北京）地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# ---用于 Base64 编码 ---
# 格式为 data:{mime_type};base64,{base64_data}
def encode_file(file_path):
    mime_type, _ = mimetypes.guess_type(file_path)
    if not mime_type or not mime_type.startswith("image/"):
        raise ValueError("不支持或无法识别的图像格式")

    try:
        with open(file_path, "rb") as image_file:
            encoded_string = base64.b64encode(
                image_file.read()).decode('utf-8')
        return f"data:{mime_type};base64,{encoded_string}"
    except IOError as e:
        raise IOError(f"读取文件时出错: {file_path}, 错误: {str(e)}")

# 获取图像的 Base64 编码
# 调用编码函数，请将 "/path/to/your/image.png" 替换为您的本地图片文件路径，否则无法运行
image = encode_file("/path/to/your/image.png")

messages = [\
    {\
        "role": "user",\
        "content": [\
            {"image": image},\
            {"text": "生成一张符合深度图的图像，遵循以下描述：一辆红色的破旧的自行车停在一条泥泞的小路上，背景是茂密的原始森林"}\
        ]\
    }\
]

# 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 若没有配置环境变量，请用百炼 API Key 将下行替换为：api_key="sk-xxx"
api_key = os.getenv("DASHSCOPE_API_KEY")

# qwen-image-edit-max、qwen-image-edit-plus系列支持输出1-6张图片，此处以2张为例
response = MultiModalConversation.call(
    api_key=api_key,
    model="qwen-image-edit-max",
    messages=messages,
    stream=False,
    n=2,
    watermark=False,
    negative_prompt=" ",
    prompt_extend=True,
    size="1536*1024",
)

if response.status_code == 200:
    # 如需查看完整响应，请取消下行注释
    # print(json.dumps(response, ensure_ascii=False))
    for i, content in enumerate(response.output.choices[0].message.content):
        print(f"输出图像{i+1}的URL:{content['image']}")
else:
    print(f"HTTP返回码：{response.status_code}")
    print(f"错误码：{response.code}")
    print(f"错误信息：{response.message}")
    print("请参考文档：https://help.aliyun.com/zh/model-studio/error-code")
```

```python
# 需要安装requests以下载图像: pip install requests
import requests

def download_image(image_url, save_path='output.png'):
    try:
        response = requests.get(image_url, stream=True, timeout=300)  # 设置超时
        response.raise_for_status()  # 如果HTTP状态码不是200，则引发异常
        with open(save_path, 'wb') as f:
            for chunk in response.iter_content(chunk_size=8192):
                f.write(chunk)
        print(f"图像已成功下载到: {save_path}")

    except requests.exceptions.RequestException as e:
        print(f"图像下载失败: {e}")

image_url = "https://dashscope-result-sz.oss-cn-shenzhen.aliyuncs.com/xxx.png?Expires=xxx"
download_image(image_url, save_path='output.png')
```

#### **响应示例**

图像链接的有效期为24小时，请及时下载图像。

> `input_tokens`、`output_tokens`和`characters`为兼容字段，当前固定为0。

```json
{
    "status_code": 200,
    "request_id": "fa41f9f9-3cb6-434d-a95d-4ae6b9xxxxxx",
    "code": "",
    "message": "",
    "output": {
        "text": null,
        "finish_reason": null,
        "choices": [\
            {\
                "finish_reason": "stop",\
                "message": {\
                    "role": "assistant",\
                    "content": [\
                        {\
                            "image": "https://dashscope-result-hz.oss-cn-hangzhou.aliyuncs.com/xxx.png?Expires=xxx"\
                        },\
                        {\
                            "image": "https://dashscope-result-hz.oss-cn-hangzhou.aliyuncs.com/xxx.png?Expires=xxx"\
                        }\
                    ]\
                }\
            }\
        ],
        "audio": null
    },
    "usage": {
        "input_tokens": 0,
        "output_tokens": 0,
        "characters": 0,
        "height": 1536,
        "image_count": 2,
        "width": 1024
    }
}
```

### Java SDK调用

**说明**

推荐安装最新版DashScope Java SDK，否则可能运行报错： [安装或升级SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

#### **请求示例**

通过公网URL传入图片

通过Base64编码传入图片

通过URL下载图像

```java
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversation;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationParam;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationResult;
import com.alibaba.dashscope.common.MultiModalMessage;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.exception.UploadFileException;
import com.alibaba.dashscope.utils.Constants;
import com.alibaba.dashscope.utils.JsonUtils;

import java.io.IOException;
import java.util.*;

public class QwenImageEdit {

    static {
        // 以下为中国（北京）地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    // 若没有配置环境变量，请用百炼 API Key 将下行替换为：apiKey="sk-xxx"
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    public static void call() throws ApiException, NoApiKeyException, UploadFileException, IOException {

        MultiModalConversation conv = new MultiModalConversation();

        // 模型支持输入1-3张图片
        MultiModalMessage userMessage = MultiModalMessage.builder().role(Role.USER.getValue())
                .content(Arrays.asList(
                        Collections.singletonMap("image", "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/thtclx/input1.png"),
                        Collections.singletonMap("image", "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/iclsnx/input2.png"),
                        Collections.singletonMap("image", "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/gborgw/input3.png"),
                        Collections.singletonMap("text", "图1中的女生穿着图2中的黑色裙子按图3的姿势坐下")
                )).build();
        // qwen-image-edit-max、qwen-image-edit-plus系列支持输出1-6张图片，此处以2张为例
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("watermark", false);
        parameters.put("negative_prompt", " ");
        parameters.put("n", 2);
        parameters.put("prompt_extend", true);
        parameters.put("size", "1024*1536");

        MultiModalConversationParam param = MultiModalConversationParam.builder()
                .apiKey(apiKey)
                .model("qwen-image-edit-max")
                .messages(Collections.singletonList(userMessage))
                .parameters(parameters)
                .build();

        MultiModalConversationResult result = conv.call(param);
        // 如需查看完整响应，请取消下行注释
        // System.out.println(JsonUtils.toJson(result));
        List<Map<String, Object>> contentList = result.getOutput().getChoices().get(0).getMessage().getContent();
        int imageIndex = 1;
        for (Map<String, Object> content : contentList) {
            if (content.containsKey("image")) {
                System.out.println("输出图像" + imageIndex + "的URL：" + content.get("image"));
                imageIndex++;
            }
        }
    }

    public static void main(String[] args) {
        try {
            call();
        } catch (ApiException | NoApiKeyException | UploadFileException | IOException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

```java
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversation;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationParam;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationResult;
import com.alibaba.dashscope.common.MultiModalMessage;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.exception.UploadFileException;
import com.alibaba.dashscope.utils.Constants;
import com.alibaba.dashscope.utils.JsonUtils;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.*;

public class QwenImageEdit {

    static {
        // 以下为中国（北京）地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    // 若没有配置环境变量，请用百炼 API Key 将下行替换为：apiKey="sk-xxx"
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    public static void call() throws ApiException, NoApiKeyException, UploadFileException, IOException {

        // 请将 "/path/to/your/image.png" 替换为您的本地图片文件路径，否则无法运行
        String image = encodeFile("/path/to/your/image.png");

        MultiModalConversation conv = new MultiModalConversation();

        MultiModalMessage userMessage = MultiModalMessage.builder().role(Role.USER.getValue())
                .content(Arrays.asList(
                        Collections.singletonMap("image", image),
                        Collections.singletonMap("text", "生成一张符合深度图的图像，遵循以下描述：一辆红色的破旧的自行车停在一条泥泞的小路上，背景是茂密的原始森林")
                )).build();
        // qwen-image-edit-max、qwen-image-edit-plus系列支持输出1-6张图片，此处以2张为例
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("watermark", false);
        parameters.put("negative_prompt", " ");
        parameters.put("n", 2);
        parameters.put("prompt_extend", true);
        parameters.put("size", "1536*1024");

        MultiModalConversationParam param = MultiModalConversationParam.builder()
                .apiKey(apiKey)
                .model("qwen-image-edit-max")
                .messages(Collections.singletonList(userMessage))
                .parameters(parameters)
                .build();

        MultiModalConversationResult result = conv.call(param);
        // 如需查看完整响应，请取消下行注释
        // System.out.println(JsonUtils.toJson(result));
        List<Map<String, Object>> contentList = result.getOutput().getChoices().get(0).getMessage().getContent();
        int imageIndex = 1;
        for (Map<String, Object> content : contentList) {
            if (content.containsKey("image")) {
                System.out.println("输出图像" + imageIndex + "的URL：" + content.get("image"));
                imageIndex++;
            }
        }
    }

    /**
     * 将文件编码为Base64字符串
     * @param filePath 文件路径
     * @return Base64字符串，格式为 data:{mime_type};base64,{base64_data}
     */
    public static String encodeFile(String filePath) {
        Path path = Paths.get(filePath);
        if (!Files.exists(path)) {
            throw new IllegalArgumentException("文件不存在: " + filePath);
        }
        // 检测MIME类型
        String mimeType = null;
        try {
            mimeType = Files.probeContentType(path);
        } catch (IOException e) {
            throw new IllegalArgumentException("无法检测文件类型: " + filePath);
        }
        if (mimeType == null || !mimeType.startsWith("image/")) {
            throw new IllegalArgumentException("不支持或无法识别的图像格式");
        }
        // 读取文件内容并编码
        byte[] fileBytes = null;
        try{
            fileBytes = Files.readAllBytes(path);
        } catch (IOException e) {
            throw new IllegalArgumentException("无法读取文件内容: " + filePath);
        }

        String encodedString = Base64.getEncoder().encodeToString(fileBytes);
        return "data:" + mimeType + ";base64," + encodedString;
    }

    public static void main(String[] args) {
        try {
            call();
        } catch (ApiException | NoApiKeyException | UploadFileException | IOException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

```java
import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class ImageDownloader {
    public static void downloadImage(String imageUrl, String savePath) {
        try {
            URL url = new URL(imageUrl);
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setConnectTimeout(5000);
            connection.setReadTimeout(300000);
            connection.setRequestMethod("GET");
            InputStream inputStream = connection.getInputStream();
            FileOutputStream outputStream = new FileOutputStream(savePath);
            byte[] buffer = new byte[8192];
            int bytesRead;
            while ((bytesRead = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, bytesRead);
            }
            inputStream.close();
            outputStream.close();

            System.out.println("图像已成功下载到: " + savePath);
        } catch (Exception e) {
            System.err.println("图像下载失败: " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        String imageUrl = "http://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/xxx?Expires=xxx";
        String savePath = "output.png";
        downloadImage(imageUrl, savePath);
    }
}
```

#### **响应示例**

图像链接的有效期为24小时，请及时下载图像。

```json
{
    "requestId": "46281da9-9e02-941c-ac78-be88b8xxxxxx",
    "usage": {
        "image_count": 2,
        "width": 1024,
        "height": 1536
    },
    "output": {
        "choices": [\
            {\
                "finish_reason": "stop",\
                "message": {\
                    "role": "assistant",\
                    "content": [\
                        {\
                            "image": "https://dashscope-result-sz.oss-cn-shenzhen.aliyuncs.com/xxx.png?Expires=xxx"\
                        },\
                        {\
                            "image": "https://dashscope-result-sz.oss-cn-shenzhen.aliyuncs.com/xxx.png?Expires=xxx"\
                        }\
                    ]\
                }\
            }\
        ]
    }
}
```

## **图像访问权限配置**

模型生成的图像存储于阿里云OSS，每张图像会被分配一个OSS链接，如`https://dashscope-result-xx.oss-cn-xxxx.aliyuncs.com/xxx.png`。OSS链接允许公开访问，可以使用此链接查看或者下载图片，链接仅在 24 小时内有效。

如果您的业务对安全性要求较高，无法访问阿里云OSS链接，则需要单独配置外网访问白名单。请将以下域名添加到您的白名单中，以便顺利访问图片链接。

```plaintext
dashscope-result-bj.oss-cn-beijing.aliyuncs.com
dashscope-result-hz.oss-cn-hangzhou.aliyuncs.com
dashscope-result-sh.oss-cn-shanghai.aliyuncs.com
dashscope-result-wlcb.oss-cn-wulanchabu.aliyuncs.com
dashscope-result-zjk.oss-cn-zhangjiakou.aliyuncs.com
dashscope-result-sz.oss-cn-shenzhen.aliyuncs.com
dashscope-result-hy.oss-cn-heyuan.aliyuncs.com
dashscope-result-cd.oss-cn-chengdu.aliyuncs.com
dashscope-result-gz.oss-cn-guangzhou.aliyuncs.com
dashscope-result-wlcb-acdr-1.oss-cn-wulanchabu-acdr-1.aliyuncs.com
```

## **错误码**

如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。

## **计费与限流**

- 模型免费额度和计费单价请参见[模型列表](https://help.aliyun.com/zh/model-studio/models#bfe15d8aa2lxh "")。

- 模型限流请参见[通义千问（Qwen-Image）](https://help.aliyun.com/zh/model-studio/rate-limit#f812e7c63axvx "")。

- 计费说明：按成功生成的 **图像张数** 计费。模型调用失败或处理错误不产生任何费用，也不消耗 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "")。


## **常见问题**

#### **Q：千问图像编辑模型支持哪些语言？**

A：目前正式支持 **简体中文和英文**；其他语言可自行尝试，但效果存在不确定性。

#### **Q：如何查看模型调用量？**

A：模型的调用信息存在小时级延迟，在模型调用完一小时后，请在模型观测（ [北京](https://bailian.console.aliyun.com/#/model-telemetry) 或 [新加坡](https://modelstudio.console.aliyun.com/#/model-telemetry)）页面，查看调用量、调用次数、成功率等指标。详情请参见 [账单查询与成本管理](https://help.aliyun.com/zh/model-studio/bill-query-and-cost-management "")。