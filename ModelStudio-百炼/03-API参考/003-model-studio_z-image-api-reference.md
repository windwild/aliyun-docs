### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[图像生成](https://help.aliyun.com/zh/model-studio/image-generation/)文生图Z-Image

# Z-Image API参考

更新时间：2026-02-11 02:21:56

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：千问-图像翻译](https://help.aliyun.com/zh/model-studio/qwen-mt-image-api)[下一篇：万相-文生图V2](https://help.aliyun.com/zh/model-studio/text-to-image-v2-api-reference)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

效果展示

模型概览

前提条件

HTTP同步调用

使用限制

计费与限流

错误码

常见问题

Z-Image 是一款轻量级文生图模型，可快速生成图像，支持中英文字渲染，并灵活适配多种分辨率与宽高比例。

**快速入口**：在线体验（ [北京](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/model_experience_center/vision?currentTab=imageGenerate&modelId=z-image-turbo) \| [新加坡](https://modelstudio.console.aliyun.com/ap-southeast-1?tab=dashboard#/efm/model_experience_center/vision?currentTab=imageGenerate&modelId=z-image-turbo)） \| [技术博客](https://tongyi-mai.github.io/Z-Image-blog/)

## **效果展示**

| **输入提示词** | **输出图像** |
| --- | --- |

|     |     |
| --- | --- |
| **输入提示词** | **输出图像** |
| film grain, analog film texture, soft film lighting, Kodak Portra 400 style, cinematic grainy texture, photorealistic details, subtle noise, (film grain:1.2)。采用近景特写镜头拍摄的东亚年轻女性，呈现户外雪地场景。她体型纤瘦，呈站立姿势，身体微微向右侧倾斜，头部抬起看向画面上方，姿态自然放松。她的面部是典型东亚长相，肤色白皙，脸颊带有自然的红润感，五官清秀：眼睛是深棕色，眼型偏圆，眼神略带惊讶地望向上方，眼白部分可见；眉毛是深黑色，形状自然弯长；鼻子小巧挺直，嘴唇涂有红色口红，唇瓣微张，表情带着轻微的惊讶或好奇。她的头发是深黑色长直发，发丝被风吹得略显凌乱，部分垂在脸颊两侧，头顶佩戴一顶深灰色的头盔，头盔边缘露出少量发丝。服装是蓝白拼接的厚重外套，外套材质看起来是毛绒与布料结合，显得温暖厚实，适合雪地环境。背景是被白雪覆盖的户外场景，远处可见模糊的树木轮廓，天空是明亮的浅蓝色，带有少量白云，光线是强烈的自然日光，照亮人物面部与头发，形成清晰的光影，色调以蓝、白、黑为主，整体风格清新自然。画面顶部有黑色提示框，内有“ **Press esc to exit full screen**”的白色文字。镜头的近景视角放大了人物的表情与细节，营造出户外雪地的真实氛围。 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6915736671/p1036890.png) |

## 模型概览

| **模型名称** | **模型简介** | **输出图像规格** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **模型简介** | **输出图像规格** |
| z-image-turbo | 轻量模型，快速生图 | 图像分辨率：总像素在\[512\*512, 2048\*2048\]之间，推荐分辨率请参见 [size参数设置](https://help.aliyun.com/zh/model-studio/z-image-api-reference#46b942a420o4e "")<br>图像格式：png<br>图像张数：固定1张 |

**说明**

调用前，请查阅各地域支持的 [模型列表](https://help.aliyun.com/zh/model-studio/models#b77c038c56b7y "")。

## **前提条件**

您需要 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

## **HTTP同步调用**

**北京地域**：`POST https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation`

**新加坡地域**：`POST https://dashscope-intl.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation`

|     |     |
| --- | --- |
| #### 请求参数 | 文生图<br>以下示例直接返回图片，响应速度较快。<br>若想开启“智能思考”能力，请设置`prompt_extend=true` 。开启后，系统将在返回图片的同时，返回优化后的提示词及其推理过程，但会增加响应时间。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation' \<br>--header 'Content-Type: application/json' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--data '{<br>    "model": "z-image-turbo",<br>    "input": {<br>        "messages": [<br>            {<br>                "role": "user",<br>                "content": [<br>                    {<br>                        "text": "film grain, analog film texture, soft film lighting, Kodak Portra 400 style, cinematic grainy texture, photorealistic details, subtle noise, (film grain:1.2)。采用近景特写镜头拍摄的东亚年轻女性，呈现户外雪地场景。她体型纤瘦，呈站立姿势，身体微微向右侧倾斜，头部抬起看向画面上方，姿态自然放松。她的面部是典型东亚长相，肤色白皙，脸颊带有自然的红润感，五官清秀：眼睛是深棕色，眼型偏圆，眼神略带惊讶地望向上方，眼白部分可见；眉毛是深黑色，形状自然弯长；鼻子小巧挺直，嘴唇涂有红色口红，唇瓣微张，表情带着轻微的惊讶或好奇。她的头发是深黑色长直发，发丝被风吹得略显凌乱，部分垂在脸颊两侧，头顶佩戴一顶深灰色的头盔，头盔边缘露出少量发丝。服装是蓝白拼接的厚重外套，外套材质看起来是毛绒与布料结合，显得温暖厚实，适合雪地环境。背景是被白雪覆盖的户外场景，远处可见模糊的树木轮廓，天空是明亮的浅蓝色，带有少量白云，光线是强烈的自然日光，照亮人物面部与头发，形成清晰的光影，色调以蓝、白、黑为主，整体风格清新自然。画面顶部有黑色提示框，内有“Press esc to exit full screen”的白色文字。镜头的近景视角放大了人物的表情与细节，营造出户外雪地的真实氛围。"<br>                    }<br>                ]<br>            }<br>        ]<br>    },<br>    "parameters": {<br>        "prompt_extend": false,<br>        "size": "1120*1440"<br>    }<br>}'<br>``` |
| ##### 请求头（Headers） |
| **Content-Type**`string` **（必选）**<br>请求内容类型。此参数必须设置为`application/json`。 |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| ##### 请求体（Request Body） |
| **model**`string` **（必选）**<br>模型名称。必须为：z-image-turbo。 |
| **input**`object` **（必选）**<br>输入的基本信息。<br>**属性**<br>**messages**`array` **（必选）**<br>请求内容数组。当前 **仅支持单轮对话**，即传入一组role、content参数，不支持多轮对话。<br>**属性**<br>**role**`string` **（必选）**<br>消息的角色。此参数必须设置为`user`。<br>**content**`array` **（必选）**<br>消息内容数组。必须包含且仅包含 **1 个 text 对象**。<br>**属性**<br>**text**`string` **（必选）**<br>正向提示词用于描述期望生成的图像内容、风格和构图。<br>支持中英文，长度不超过800个字符，每个汉字、字母、数字或符号计为一个字符，超过部分会自动截断。<br>示例值：一只坐着的橘黄色的猫，表情愉悦，活泼可爱，逼真准确。<br>**注意**：仅支持传入一个text，不传或传入多个将报错。 |
| **parameters**`object` （可选）<br>图像处理参数。<br>**属性**<br>**size**`string` （可选）<br>输出图像的分辨率，格式为`宽*高`。<br>- 默认值：`1024*1536`。<br>  <br>- 总像素范围限制：总像素在 \[512\*512, 2048\*2048\]之间。<br>  <br>- 推荐分辨率范围：总像素在 \[1024\*1024, 1536\*1536\]之间，出图效果更佳。<br>  <br>示例值：1024\*1536。<br>**总像素为1024\*1024的推荐分辨率：**<br>- 1:1: 1024\*1024<br>  <br>- 2:3: 832\*1248 <br>  <br>- 3:2: 1248\*832<br>  <br>- 3:4: 864\*1152<br>  <br>- 4:3: 1152\*864<br>  <br>- 7:9: 896\*1152 <br>  <br>- 9:7: 1152\*896<br>  <br>- 9:16: 720\*1280<br>  <br>- 9:21: 576\*1344<br>  <br>- 16:9: 1280\*720<br>  <br>- 21:9：1344\*576<br>  <br>**总像素为1280\*1280的推荐分辨率：**<br>- 1:1: 1280\*1280<br>  <br>- 2:3: 1024\*1536<br>  <br>- 3:2: 1536\*1024<br>  <br>- 3:4: 1104\*1472<br>  <br>- 4:3: 1472\*1104<br>  <br>- 7:9: 1120\*1440<br>  <br>- 9:7: 1440\*1120 <br>  <br>- 9:16: 864\*1536<br>  <br>- 9:21: 720\*1680<br>  <br>- 16:9: 1536\*864<br>  <br>- 21:9: 1680\*720<br>  <br>**总像素为1536\*1536的推荐分辨率：**<br>- 1:1：1536\*1536<br>  <br>- 2:3: 1248\*1872<br>  <br>- 3:2: 1872\*1248<br>  <br>- 3:4: 1296\*1728 <br>  <br>- 4:3: 1728\*1296<br>  <br>- 7:9: 1344\*1728<br>  <br>- 9:7: 1728\*1344 <br>  <br>- 9:16: 1152\*2048<br>  <br>- 9:21: 864\*2016<br>  <br>- 16:9: 2048\*1152<br>  <br>- 21:9: 2016\*864<br>  <br>**prompt\_extend**`bool` （可选） <br>**重要**<br>prompt\_extend直接影响费用。设为 `true` 时价格高于 `false`，具体见参见[模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#6713612f55h4l "")。<br>是否启用智能提示词（text）改写。开启后，将使用大模型优化提示词，并输出思考过程。<br>- false：默认值，关闭智能改写。输出图像和原始文本提示词。<br>  <br>- true：开启智能改写。输出图像、优化后的文本提示词、思考过程。<br>  <br>**seed**`integer` （可选）<br>随机数种子，取值范围`[0,2147483647]`。<br>使用相同的`seed`参数值可使生成内容保持相对稳定。若不提供，算法将自动使用随机数种子。<br>**注意**：模型生成过程具有概率性，即使使用相同的`seed`，也不能保证每次生成结果完全一致。 |

|     |     |
| --- | --- |
| #### 响应参数 | 任务执行成功<br>任务执行异常<br>任务数据（如任务状态、图像URL等）仅保留24小时，超时后会被自动清除。请您务必及时保存生成的图像。<br>```json<br>{<br>    "output": {<br>        "choices": [<br>            {<br>                "finish_reason": "stop",<br>                "message": {<br>                    "content": [<br>                        {<br>                            "image": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/xxx.png?Expires=xxx"<br>                        },<br>                        {<br>                            "text": "film grain, analog film texture, soft film lighting, Kodak Portra 400 style, cinematic grainy texture, photorealistic details, subtle noise, (film grain:1.2)。采用近景特写镜头拍摄的东亚年轻女性，呈现户外雪地场景。她体型纤瘦，呈站立姿势，身体微微向右侧倾斜，头部抬起看向画面上方，姿态自然放松。她的面部是典型东亚长相，肤色白皙，脸颊带有自然的红润感，五官清秀：眼睛是深棕色，眼型偏圆，眼神略带惊讶地望向上方，眼白部分可见；眉毛是深黑色，形状自然弯长；鼻子小巧挺直，嘴唇涂有红色口红，唇瓣微张，表情带着轻微的惊讶或好奇。她的头发是深黑色长直发，发丝被风吹得略显凌乱，部分垂在脸颊两侧，头顶佩戴一顶深灰色的头盔，头盔边缘露出少量发丝。服装是蓝白拼接的厚重外套，外套材质看起来是毛绒与布料结合，显得温暖厚实，适合雪地环境。背景是被白雪覆盖的户外场景，远处可见模糊的树木轮廓，天空是明亮的浅蓝色，带有少量白云，光线是强烈的自然日光，照亮人物面部与头发，形成清晰的光影，色调以蓝、白、黑为主，整体风格清新自然。画面顶部有黑色提示框，内有“Press esc to exit full screen”的白色文字。镜头的近景视角放大了人物的表情与细节，营造出户外雪地的真实氛围。"<br>                        }<br>                    ],<br>                    "reasoning_content": "",<br>                    "role": "assistant"<br>                }<br>            }<br>        ]<br>    },<br>    "usage": {<br>        "height": 1440,<br>        "image_count": 1,<br>        "input_tokens": 0,<br>        "output_tokens": 0,<br>        "total_tokens": 0,<br>        "width": 1120<br>    },<br>    "request_id": "8a0809b4-a796-47f4-a095-394b02b62xxx"<br>}<br>```<br>如果因为某种原因导致任务执行失败，将返回相关信息，可以通过code和message字段明确指示错误原因。请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "request_id": "a4d78a5f-655f-9639-8437-xxxxxx",<br>    "code": "InvalidParameter",<br>    "message": "num_images_per_prompt must be 1"<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>**属性**<br>**choices**`array`<br>模型生成的输出内容。此数组仅包含1个元素。<br>**属性**<br>**finish\_reason**`string`<br>任务停止原因，正常完成时为 `stop`。<br>**message**`object`<br>模型返回的消息。<br>**属性**<br>**role**`string`<br>消息的角色，固定为`assistant`。<br>**content**`array`<br>**属性**<br>**image**`string`<br>生成图像的 URL，图像格式为PNG。 **链接有效期为24小时**，请及时下载并保存图像。<br>**text**`string`<br>- 当prompt\_extend=false时，为输入的提示词。<br>  <br>- 当prompt\_extend=true时，为改写后的提示词。<br>  <br>**reasoning\_content**`string`<br>模型的思考过程，仅在prompt\_extend=true时返回思考文本。 |
| **usage**`object`<br>输出信息统计。只对成功的结果计数。<br>**属性**<br>**width**`integer`<br>生成图像的宽度（像素）。<br>**height**`integer`<br>生成图像的高度（像素）。<br>**image\_count**`integer`<br>生成图像的数量，固定为1。<br>**input\_tokens**`integer`<br>输入token数量，prompt\_extend=false时固定为0。<br>**output\_tokens**`integer`<br>输出token数量，prompt\_extend=false时固定为0。<br>**output\_tokens\_details**`object`<br>输出 token 详情，仅当prompt\_extend=true时返回。<br>**属性**<br>**reasoning\_tokens**`integer`<br>推理思考使用的 token 数量。<br>**total\_tokens**`integer`<br>总token数量，prompt\_extend=false时固定为0。 |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |
| **code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |  |
| **message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |  |

## **使用限制**

- 图像`url`均只保留 24 小时，请及时下载。

- **内容审核**：输入的 `prompt` 和输出的图像均会经过内容安全审核，包含违规内容的请求将报错“IPInfringementSuspect”或“DataInspectionFailed”，具体参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。

- **网络访问配置**：图像链接存储于阿里云 OSS，如果业务系统因安全策略无法访问外部OSS链接，请将以下 OSS 域名加入网络访问白名单。















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


## **计费与限流**

- 模型免费额度和计费单价请参见[模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#6713612f55h4l "")。

- 模型限流请参见[Z-Image](https://help.aliyun.com/zh/model-studio/rate-limit#e17ad85fd8wwl "")。

- 根据是否开启智能按成功生成的 **图像张数** 计费。模型调用失败或处理错误不产生任何费用，也不消耗 [免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "")。


## **错误码**

如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。

## **常见问题**

**Q: 如何查看模型调用量？**

A: 模型调用完一小时后，请在[**模型监控**（北京）](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/model-telemetry) 或 [**模型监控**（新加坡）](https://modelstudio.console.aliyun.com/ap-southeast-1?tab=dashboard#/model-telemetry) 页面，查看模型的调用次数、成功率等指标。详情请参见 [账单查询与成本管理](https://help.aliyun.com/zh/model-studio/bill-query-and-cost-management "")。