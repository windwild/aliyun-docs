### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[图像生成](https://help.aliyun.com/zh/model-studio/image-generation/)万相-涂鸦作画

# 万相-涂鸦作画API参考

更新时间：2026-02-11 02:22:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：万相-通用图像编辑2.1](https://help.aliyun.com/zh/model-studio/wanx-image-edit-api-reference)[下一篇：万相-图像局部重绘](https://help.aliyun.com/zh/model-studio/vary-region-api-reference)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型概览

前提条件

HTTP调用

步骤1：创建任务获取任务ID

步骤2：根据任务ID查询结果

DashScope SDK调用

Python SDK调用

Java SDK调用

错误码

常见问题

模型计费及限流

配置域名白名单以访问图片OSS链接

本文介绍万相-涂鸦作画模型的API输入输出参数。

**相关指南**： [涂鸦作画](https://help.aliyun.com/zh/model-studio/sketch-to-image "")

**重要**

本文档仅适用于“中国内地（北京）”地域，且必须使用该地域的 [API Key](https://bailian.console.aliyun.com/?tab=model#/api-key)。

## **模型概览**

**模型效果示意**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2400704371/p883780.png)

**模型简介**

| **模型名称** | **模型简介** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名称** | **模型简介** |
| wanx-sketch-to-image-lite | 万相-涂鸦作画通过手绘图案和文字描述，生成精美的涂鸦绘画作品。 |

**模型说明**

| **模型名称** | **计费单价** | **限流（主账号与RAM子账号共用）** | **免费额度** [（查看）](https://help.aliyun.com/zh/model-studio/new-free-quota "") |
| --- | --- | --- | --- |
| **任务下发接口QPS限制** | **同时处理中任务数量** |
| --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型名称** | **计费单价** | **限流（主账号与RAM子账号共用）** | **免费额度** [（查看）](https://help.aliyun.com/zh/model-studio/new-free-quota "") |
| **任务下发接口QPS限制** | **同时处理中任务数量** |
| wanx-sketch-to-image-lite | 0.06元/张 | 2 | 1 | 500张 |

更多说明请参见 [模型计费及限流](https://help.aliyun.com/zh/model-studio/wanx-sketch-to-image-api-reference#b8457b7223zhp "")。

## **前提条件**

涂鸦作画API支持通过HTTP和DashScope SDK进行调用。

在调用前，您需要 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，再 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

如需通过SDK进行调用，请 [安装DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。目前，该SDK已支持Python和Java。

## HTTP调用

图像模型处理时间较长，为了避免请求超时，HTTP调用仅支持异步获取模型结果。您需要发起两个请求：

1. **创建任务获取任务ID**：首先发起创建任务请求，该请求会返回任务ID（task\_id）。

2. **根据任务ID查询结果**：使用上一步获得的任务ID，查询任务状态及结果。任务成功执行时将返回图像URL，有效期24小时。


**说明**

创建任务后，该任务将被加入到排队队列，等待调度执行。后续需要调用“根据任务ID查询结果接口”获取任务状态及结果。

### **步骤1：创建任务获取任务ID**

`POST https://dashscope.aliyuncs.com/api/v1/services/aigc/image2image/image-synthesis/`

|     |     |
| --- | --- |
| #### 请求参数 | curl<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/image2image/image-synthesis' \<br>--header 'X-DashScope-Async: enable' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--header 'Content-Type: application/json' \<br>--data '{<br>    "model": "wanx-sketch-to-image-lite",<br>    "input": {<br>        "sketch_image_url": "https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6609471071/p743851.jpg",<br>        "prompt": "一棵参天大树"<br>    },<br>    "parameters": {<br>        "size": "768*768",<br>        "n": 2,<br>        "sketch_weight": 3,<br>        "style": "<watercolor>"<br>    }<br>}'<br>``` |
| ##### **请求头（Headers）** |
| **Content-Type**`string` **（必选）**<br>请求内容类型。此参数必须设置为`application/json`。 |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| **X-DashScope-Async**`string` **（必选）**<br>异步处理配置参数。HTTP请求只支持异步， **必须设置为**`enable`。<br>**重要**<br>缺少此请求头将报错：“current user api does not support synchronous calls”。 |
| **X-DashScope-WorkSpace**`string`（可选）<br>阿里云百炼业务空间ID。示例值：llm-xxxx。<br>您可以在此 [获取Workspace ID](https://help.aliyun.com/zh/model-studio/obtain-the-app-id-and-workspace-id#d3eb3cd37b7fu "")。<br>**详细说明**<br>此参数根据阿里云百炼API-Key进行填写。<br>- 若为主账号API-Key，可不填。不填则使用主账号权限，填写则使用对应的业务空间权限。<br>  <br>- 若为RAM子账号API-Key，则必填。RAM子账号一定归属于某个业务空间。<br>  <br>业务空间必须具备访问模型的权限，才能调用API。若无权限，请参考 [授权子业务空间模型调用、训练和部署](https://help.aliyun.com/zh/model-studio/use-workspace#f2e68d7ba7ubk "")。<br>> 关于如何区分阿里云百炼主账号和RAM子账号，请参考 [主账号管理](https://help.aliyun.com/zh/model-studio/business-space-management "")。 |
| ##### **请求体（Request Body）** |
| **model**`string` **（必选）**<br>调用模型。 |
| **input**`object` **（必选）**<br>输入的基本信息，比如提示词、图像URL地址。<br>**属性**<br>**prompt**`string` **（必选）**<br>提示词，用来描述生成图像中期望包含的元素和视觉特点。<br>支持中英文，长度不超过75个字符，超过部分会自动截断。<br>示例值：一棵参天大树。<br>**sketch\_image\_url**`string` **（必选）**<br>输入草图的URL地址。输入草图需要与输出图像的分辨率比例保持一致，否则会导致图片拉伸变形，建议使用白色背景图。<br>URL 需为公网可访问的地址，并支持 HTTP 或 HTTPS 协议。您也可在此 [获取临时公网URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。 <br>图像限制：<br>- 图像格式：JPG、JPEG、PNG、TIFF、WEBP。<br>  <br>- 图像分辨率：不小于256×256像素且不超过2048×2048像素。<br>  <br>- 图像大小：不超过10 MB。<br>  <br>- URL地址中不能包含中文字符。<br>  <br>草图示例：<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9289386271/p850798.png) |
| **parameters**`object`（可选）<br>图像处理参数。<br>**属性**<br>**style**`string`（可选）<br>输出图像的风格，目前支持以下风格取值：<br>- <auto>：默认值，由模型随机输出图像风格。<br>  <br>- <3d cartoon>：3D卡通。<br>  <br>- <anime>：二次元。<br>  <br>- <oil painting>：油画。<br>  <br>- <watercolor>：水彩。<br>  <br>- <sketch>：素描。<br>  <br>- <chinese painting>：中国画。<br>  <br>- <flat illustration>：扁平插画。<br>  <br>**size**`string`（可选）<br>输出图像的分辨率。目前仅支持一种图像分辨率：768\*768，且为默认值。<br>**n**`integer`（可选）<br>生成图片的数量。取值范围为1~4张，默认为4。<br>**sketch\_weight**`integer`（可选）<br>输入草图对输出图像的约束程度。<br>取值范围为0-10，取值间隔为1， 默认值为10。取值越大表示输出图像跟输入草图越相似。<br>**sketch\_extraction**`boolean`（可选）<br>如果上传图片是RGB图片，而非草图（sketch线稿），此参数可控制是否对输入图片进行sketch边缘提取。<br>默认值为False，表示不进行提取。设置为True时，表示进行提取，此时，`sketch_color`字段失效。<br>**sketch\_color**`array`（可选）<br>此字段在`sketch_extraction=false`时生效，所包含数值均被视为画笔色，其余数值均会视为背景色。模型会基于一种或多种画笔色描绘的区域生成新的画作。默认值为\[\]。<br>当sketch\_image\_url线稿中的线条不是黑色，而是包含其他一种或多种颜色时，可以指定一个或多个RGB颜色数值作为画笔色。<br>示例值：\[\[134, 134, 134\], \[0, 0, 0\]\] |

|     |     |
| --- | --- |
| #### **响应参数** | 成功响应<br>异常响应<br>请保存 task\_id，用于查询任务状态与结果。<br>```json<br>{<br>    "output": {<br>        "task_status": "PENDING",<br>        "task_id": "0385dc79-5ff8-4d82-bcb6-xxxxxx"<br>    },<br>    "request_id": "4909100c-7b5a-9f92-bfe5-xxxxxx"<br>}<br>```<br>创建任务失败，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "code": "InvalidApiKey",<br>    "message": "No API-key provided.",<br>    "request_id": "7438d53d-6eb8-4596-8835-xxxxxx"<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>**属性**<br>**task\_id**`string`<br>任务ID。查询有效期24小时。<br>**task\_status**`string`<br>任务状态。<br>**枚举值**<br>- PENDING：任务排队中<br>  <br>- RUNNING：任务处理中<br>  <br>- SUCCEEDED：任务执行成功<br>  <br>- FAILED：任务执行失败<br>  <br>- CANCELED：任务已取消<br>  <br>- UNKNOWN：任务不存在或状态未知 |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |
| **code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |
| **message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |

### 步骤2：根据任务ID查询结果

`GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id}`

|     |     |
| --- | --- |
| #### 请求参数 | 查询任务结果<br>请将`86ecf553-d340-4e21-xxxxxxxxx`替换为真实的task\_id。<br>> 若使用新加坡地域的模型，需将base\_url替换为https://dashscope-intl.aliyuncs.com/api/v1/tasks/86ecf553-d340-4e21-xxxxxxxxx<br>```curl<br>curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/86ecf553-d340-4e21-xxxxxxxxx \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY"<br>``` |
| #### **请求头（Headers）** |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| #### **URL路径参数（Path parameters）** |
| **task\_id**`string` **（必选）**<br>任务ID。 |

|     |     |
| --- | --- |
| #### **响应参数** | 任务执行成功<br>任务执行失败<br>任务部分失败<br>任务数据（如任务状态、图像URL等）仅保留24小时，超时后会被自动清除。请您务必及时保存生成的图像。<br>```json<br>{<br>    "request_id": "85eaba38-0185-99d7-8d16-4d9135238846",<br>    "output": {<br>        "task_id": "86ecf553-d340-4e21-af6e-a0c6a421c010",<br>        "task_status": "SUCCEEDED",<br>        "results": [<br>            {<br>                "url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/123/a1.png"<br>            },<br>            {<br>                "url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/123/b2.png"<br>            }<br>        ],<br>        "task_metrics": {<br>            "TOTAL": 2,<br>            "SUCCEEDED": 2,<br>            "FAILED": 0<br>        }<br>    },<br>    "usage": {<br>        "image_count": 2<br>    }<br>}<br>```<br>若任务执行失败，task\_status将置为 FAILED，并提供错误码和信息。请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "request_id": "e5d70b02-ebd3-98ce-9fe8-759d7d7b107d",<br>    "output": {<br>        "task_id": "86ecf553-d340-4e21-af6e-a0c6a421c010",<br>        "task_status": "FAILED",<br>        "code": "InvalidParameter",<br>        "message": "The size is not match the allowed size ['1024*1024', '720*1280', '1280*720']",<br>        "task_metrics": {<br>            "TOTAL": 4,<br>            "SUCCEEDED": 0,<br>            "FAILED": 4<br>        }<br>    }<br>}<br>```<br>模型可以在一次任务中生成多张图片。只要有一张图片生成成功，任务状态将标记为`SUCCEEDED`，并且返回相应的图像URL。对于生成失败的图片，结果中会返回相应的失败原因。同时在usage统计中，只会对成功的结果计数。请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "request_id": "85eaba38-0185-99d7-8d16-4d9135238846",<br>    "output": {<br>        "task_id": "86ecf553-d340-4e21-af6e-a0c6a421c010",<br>        "task_status": "SUCCEEDED",<br>        "results": [<br>            {<br>                "url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/123/a1.png"<br>            },<br>            {<br>                "code": "InternalError.Timeout",<br>                "message": "An internal timeout error has occured during execution, please try again later or contact service support."<br>            }<br>        ],<br>        "task_metrics": {<br>            "TOTAL": 2,<br>            "SUCCEEDED": 1,<br>            "FAILED": 1<br>        }<br>    },<br>    "usage": {<br>        "image_count": 1<br>    }<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>**属性**<br>**task\_id**`string`<br>任务ID。查询有效期24小时。<br>**task\_status**`string`<br>任务状态。<br>**枚举值**<br>- PENDING：任务排队中<br>  <br>- RUNNING：任务处理中<br>  <br>- SUCCEEDED：任务执行成功<br>  <br>- FAILED：任务执行失败<br>  <br>- CANCELED：任务已取消<br>  <br>- UNKNOWN：任务不存在或状态未知<br>  <br>**task\_metrics**`object`<br>任务结果统计。<br>**属性**<br>**TOTAL**`integer`<br>总的任务数。<br>**SUCCEEDED**`integer`<br>任务状态为成功的任务数。<br>**FAILED**`integer`<br>任务状态为失败的任务数。<br>**results**`array of object`<br>任务结果列表，包括图像URL、部分任务执行失败报错信息等。<br>**数据结构**<br>```json<br>{<br>    "results": [<br>        {<br>            "url": ""<br>        },<br>        {<br>            "code": "",<br>            "message": ""<br>        }<br>    ]<br>}<br>```<br>**code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。<br>**message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |
| **usage**`object`<br>输出信息统计。只对成功的结果计数。<br>**属性**<br>**image\_count**`integer`<br>模型成功生成图片的数量。计费公式：费用 = 图片数量 × 单价。 |  |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |  |

## DashScope SDK调用

请先确认已安装最新版DashScope SDK： [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

DashScope SDK目前已支持Python和Java。

SDK与HTTP接口的参数名基本一致，参数结构根据不同语言的SDK封装而定。参数说明可参考 [HTTP调用](https://help.aliyun.com/zh/model-studio/text-to-image-api-reference#42703589880ts "")。

由于图像模型处理时间较长，底层服务采用异步方式提供。SDK在上层进行了封装，支持同步、异步两种调用方式。

### Python SDK调用

同步调用

异步调用

##### **请求示例**

```python
from http import HTTPStatus
from urllib.parse import urlparse, unquote
from pathlib import PurePosixPath
import requests
from dashscope import ImageSynthesis
import os

prompt = "一棵参天大树"
sketch_image_url = "https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6609471071/p743851.jpg"
model = "wanx-sketch-to-image-lite"
task = "image2image"

print('----sync call, please wait a moment----')
rsp = ImageSynthesis.call(api_key=os.getenv("DASHSCOPE_API_KEY"),
                          model=model,
                          prompt=prompt,
                          n=1,
                          style='<watercolor>',
                          size='768*768',
                          sketch_image_url=sketch_image_url,
                          task=task)
print('response: %s' % rsp)
if rsp.status_code == HTTPStatus.OK:
    print(rsp.output)
    # save file to current directory
    for result in rsp.output.results:
        file_name = PurePosixPath(unquote(urlparse(result.url).path)).parts[-1]
        with open('./%s' % file_name, 'wb+') as f:
            f.write(requests.get(result.url).content)
else:
    print('sync_call Failed, status_code: %s, code: %s, message: %s' %
          (rsp.status_code, rsp.code, rsp.message))
```

##### **响应示例**

```json
{
	"status_code": 200,
	"request_id": "4126d9dd-e037-9f32-8d56-6d29ab3f9a06",
	"code": null,
	"message": "",
	"output": {
		"task_id": "b476bc4e-35c1-4c4e-a4d9-xxxxxxx",
		"task_status": "SUCCEEDED",
		"results": [{\
			"url": "https://dashscope-result-sh.oss-cn-shanghai.aliyuncs.com/xxxx.png"\
		}],
		"submit_time": "2024-11-01 09:50:56.081",
		"scheduled_time": "2024-11-01 09:50:56.104",
		"end_time": "2024-11-01 09:51:22.740",
		"task_metrics": {
			"TOTAL": 1,
			"SUCCEEDED": 1,
			"FAILED": 0
		}
	},
	"usage": {
		"image_count": 1
	}
}
```

##### **请求示例**

```python
from http import HTTPStatus
from urllib.parse import urlparse, unquote
from pathlib import PurePosixPath
import requests
from dashscope import ImageSynthesis
import os

prompt = "一棵参天大树"
sketch_image_url = "https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6609471071/p743851.jpg"
model = "wanx-sketch-to-image-lite"
task = "image2image"

# 异步调用
def async_call():
    print('----create task----')
    task_info = create_async_task()
    print('----wait task done then save image----')
    wait_async_task(task_info)

# 创建异步任务
def create_async_task():
    rsp = ImageSynthesis.async_call(api_key=os.getenv("DASHSCOPE_API_KEY"),
                                    model=model,
                                    prompt=prompt,
                                    n=1,
                                    style='<watercolor>',
                                    size='768*768',
                                    sketch_image_url=sketch_image_url,
                                    task=task)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output)
    else:
        print('create_async_task Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))
    return rsp

# 等待异步任务结束
def wait_async_task(task):
    rsp = ImageSynthesis.wait(task)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output.task_status)
        # save file to current directory
        for result in rsp.output.results:
            file_name = PurePosixPath(unquote(urlparse(result.url).path)).parts[-1]
            with open('./%s' % file_name, 'wb+') as f:
                f.write(requests.get(result.url).content)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    async_call()
```

##### **响应示例**

**1、创建任务的响应示例**

```json
{
	"status_code": 200,
	"request_id": "31b04171-011c-96bd-ac00-f0383b669cc7",
	"code": "",
	"message": "",
	"output": {
		"task_id": "4f90cf14-a34e-4eae-xxxxxxxx",
		"task_status": "PENDING",
		"results": []
	},
	"usage": null
}
```

**2、查询任务结果的响应示例**

```json
{
	"status_code": 200,
	"request_id": "d861d3ba-4b29-9491-abad-266ef4fb2f08",
	"code": null,
	"message": "",
	"output": {
		"task_id": "4f90cf14-a34e-4eae-xxxxxxxx",
		"task_status": "SUCCEEDED",
		"results": [{\
			"url": "https://dashscope-result-hz.oss-cn-hangzhou.aliyuncs.com/xxxx.png"\
		}],
		"submit_time": "2024-10-31 20:40:35.631",
		"scheduled_time": "2024-10-31 20:40:35.684",
		"end_time": "2024-10-31 20:41:02.700",
		"task_metrics": {
			"TOTAL": 1,
			"SUCCEEDED": 1,
			"FAILED": 0
		}
	},
	"usage": {
		"image_count": 1
	}
}
```

### Java SDK调用

同步调用

异步调用

##### 请求示例

```java
// Copyright (c) Alibaba, Inc. and its affiliates.

import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesis;
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesisParam;
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.JsonUtils;

public class Main {

    public void syncCall() {
        String prompt = "一棵参天大树";
        String sketchImageUrl = "https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6609471071/p743851.jpg";
        String model = "wanx-sketch-to-image-lite";
        ImageSynthesisParam param = ImageSynthesisParam.builder()
                .model(model)
                .prompt(prompt)
                .n(1)
                .size("768*768")
                .sketchImageUrl(sketchImageUrl)
                .style("<watercolor>")
                .build();

        String task = "image2image";
        ImageSynthesis imageSynthesis = new ImageSynthesis(task);
        ImageSynthesisResult result = null;
        try {
            System.out.println("---sync call, please wait a moment----");
            result = imageSynthesis.call(param);
        } catch (ApiException | NoApiKeyException e){
            throw new RuntimeException(e.getMessage());
        }
        System.out.println(JsonUtils.toJson(result));
    }

    public static void main(String[] args){
        Main text2Image = new Main();
        text2Image.syncCall();
    }

}
```

##### **响应示例**

```json
{
	"request_id": "150edcda-05d5-9ffe-8803-84626d1db623",
	"output": {
		"task_id": "f2098ff0-146e-404c-bb25-xxxxxxxx",
		"task_status": "SUCCEEDED",
		"results": [{\
			"url": "https://dashscope-result-hz.oss-cn-hangzhou.aliyuncs.com/xxxx.png"\
		}],
		"task_metrics": {
			"TOTAL": 1,
			"SUCCEEDED": 1,
			"FAILED": 0
		}
	},
	"usage": {
		"image_count": 1
	}
}
```

##### **请求示例**

```java
// Copyright (c) Alibaba, Inc. and its affiliates.

import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesis;
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesisParam;
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.JsonUtils;

public class Main {

    public void asyncCall() {
        System.out.println("---create task----");
        String taskId = this.createAsyncTask();
        System.out.println("---wait task done then return image url----");
        this.waitAsyncTask(taskId);
    }

    /**
     * 创建异步任务
     * @return taskId
     */
    public String createAsyncTask() {
        String prompt = "一棵参天大树";
        String sketchImageUrl = "https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6609471071/p743851.jpg";
        String model = "wanx-sketch-to-image-lite";
        ImageSynthesisParam param = ImageSynthesisParam.builder()
                .model(model)
                .prompt(prompt)
                .n(1)
                .size("768*768")
                .sketchImageUrl(sketchImageUrl)
                .style("<watercolor>")
                .build();

        String task = "image2image";
        ImageSynthesis imageSynthesis = new ImageSynthesis(task);
        ImageSynthesisResult result = null;
        try {
            result = imageSynthesis.asyncCall(param);
        } catch (Exception e){
            throw new RuntimeException(e.getMessage());
        }
        String taskId = result.getOutput().getTaskId();
        System.out.println("taskId=" + taskId);
        return taskId;
    }

    /**
     * 等待异步任务结束
     * @param taskId 任务id
     * */
    public void waitAsyncTask(String taskId) {
        ImageSynthesis imageSynthesis = new ImageSynthesis();
        ImageSynthesisResult result = null;
        try {
            // If you have set the DASHSCOPE_API_KEY in the system environment variable, the apiKey can be null.
            result = imageSynthesis.wait(taskId, null);
        } catch (ApiException | NoApiKeyException e){
            throw new RuntimeException(e.getMessage());
        }

        System.out.println(JsonUtils.toJson(result.getOutput()));
        System.out.println(JsonUtils.toJson(result.getUsage()));
    }

    public static void main(String[] args){
        Main text2Image = new Main();
         text2Image.asyncCall();
    }

}
```

##### **响应示例**

**1、步骤1：创建任务获取任务ID的响应示例**

```json
{
	"request_id": "5dbf9dc5-4f4c-9605-85ea-542f97709ba8",
	"output": {
		"task_id": "7277e20e-aa01-4709-xxxxxxxx",
		"task_status": "PENDING"
	}
}
```

**2、步骤2：根据任务ID查询结果的响应示例**

```json
{
	"request_id": "c44213ba-7aa3-91e4-97c1-c527ade82597",
	"output": {
		"task_id": "7277e20e-aa01-4709-xxxxxxxx",
		"task_status": "SUCCEEDED",
		"results": [{\
			"url": "https://dashscope-result-hz.oss-cn-hangzhou.aliyuncs.com/xxxx.png"\
		}],
		"task_metrics": {
			"TOTAL": 1,
			"SUCCEEDED": 1,
			"FAILED": 0
		}
	},
	"usage": {
		"image_count": 1
	}
}
```

## 错误码

如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。

此API还有特定状态码，具体如下所示。

| **HTTP状态码** | **接口错误码（code）** | **接口错误信息（message）** | **含义说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **HTTP状态码** | **接口错误码（code）** | **接口错误信息（message）** | **含义说明** |
| 400 | InvalidURL | The request URL is invalid, please check the request URL is available and the request image format is one of the following types: JPEG, JPG, PNG, BMP, and WEBP. | 输入图片下载失败，请检查网络或者输入格式。 |
| 400 | InvalidFile.Resolution | The image resolution is invalid, please make sure that the aspect ratio is smaller than 2.0, and largest length of image is smaller than 4096. | 上传图片大小不符合要求。 |

## **常见问题**

### 模型计费及限流

**免费额度**

- 额度说明：免费额度是指模型成功生成的输出图片数量。输入图片及模型处理失败的情况不占用免费额度。

- 领取方式：开通阿里云百炼大模型服务后自动发放，有效期90天。

- 使用账号：阿里云主账号与其RAM子账号共享免费额度。

- 更多详情请参见 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "")。


**限时免费**

- 当计费为限时免费时，表示该模型处于公测阶段，免费额度用尽后不可使用。


**计费说明**

- 当计费有明确单价时，如0.2元/秒，表示该模型已商业化，免费额度用尽或过期后需付费使用。

- 计费项：只对模型成功生成的输出图片进行收费，其余情况暂不计费。

- 付费方式：由阿里云主账号统一付费。RAM子账号不能独立计量计费，必须由所属的主账号付费。如果您需要查询账单信息，请前往阿里云控制台 [账单概览](https://billing-cost.console.aliyun.com/finance/month-bill/account)。

- 充值途径：您可以在阿里云控制台 [费用与成本](https://billing-cost.console.aliyun.com/home?spm=a2c4g.11186623.0.0.2d543048F4KRQP) 页面进行充值。

- 模型调用情况：您可以前往阿里云百炼的[模型观测](https://bailian.console.aliyun.com/#/model-telemetry)查看模型调用量及调用次数。

- 更多计费问题请参见 [计费项](https://help.aliyun.com/zh/model-studio/billing-for-model-studio "")。


**限流**

- 限流说明：阿里云主账号与其RAM子账号共享限流限制。


### 配置域名白名单以访问图片OSS链接

模型生成的图像存储于阿里云OSS，每张图像会被分配一个OSS链接，如`https://dashscope-result-xx.oss-cn-xxxx.aliyuncs.com/xxx.png`。OSS链接允许公开访问，您可以使用此链接查看或者下载图片，链接仅在 24 小时内有效。

特别注意的是，如果您的业务对安全性要求较高，无法访问阿里云OSS链接，您需要单独配置外网访问白名单。请将以下域名添加到您的白名单中，以便顺利访问图片链接。

```plaintext
# OSS域名列表
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