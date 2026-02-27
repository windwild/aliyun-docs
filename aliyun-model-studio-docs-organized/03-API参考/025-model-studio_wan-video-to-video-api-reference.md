### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[视频生成](https://help.aliyun.com/zh/model-studio/video-generation-api/)万相-参考生视频

# 万相-参考生视频API参考

更新时间：2026-02-11 03:16:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：万相-图生视频-基于首尾帧](https://help.aliyun.com/zh/model-studio/image-to-video-by-first-and-last-frame-api-reference)[下一篇：万相-文生视频](https://help.aliyun.com/zh/model-studio/text-to-video-api-reference)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

适用范围

HTTP调用

步骤1：创建任务获取任务ID

步骤2：根据任务ID查询结果

使用限制

错误码

万相-参考生视频模型支持 **多模态输入**（文本/图像/视频），可将人或物体作为主角，生成单角色表演或多角色互动视频。模型还支持智能分镜，生成多镜头视频。

**相关文档**： [使用指南](https://help.aliyun.com/zh/model-studio/video-to-video-guide "")

## 适用范围

为确保调用成功，请务必保证模型、Endpoint URL 和 API Key 均属于 **同一地域**。跨地域调用将会失败。

- [**选择模型**](https://help.aliyun.com/zh/model-studio/video-to-video-guide#06f39eafa2dwt "")：确认模型所属的地域。

- **选择 URL**：选择对应的地域 Endpoint URL，支持HTTP URL。

- **配置 API Key**：选择地域并 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，再 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。


**说明**

本文的示例代码适用于 **北京地域**。

## HTTP调用

由于参考生视频任务耗时较长（通常为1-5分钟），API采用异步调用。整个流程包含 **“创建任务 -\> 轮询获取”** 两个核心步骤，具体如下：

### 步骤1：创建任务获取任务ID

北京

新加坡

弗吉尼亚

`POST https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis`

`POST https://dashscope-intl.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis`

`POST https://dashscope-us.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis`

**说明**

- 创建成功后，使用接口返回的 `task_id` 查询结果，task\_id 有效期为 24 小时。 **请勿重复创建任务**，轮询获取即可。

- 新手指引请参见 [Postman](https://help.aliyun.com/zh/model-studio/first-call-to-image-and-video-api "")。


|     |     |
| --- | --- |
| #### 请求参数 | 多角色互动（参考图像和视频）<br>多角色互动（参考视频）<br>单角色扮演<br>生成无声视频<br>通过`reference_urls`传入图像和视频URL。同时设置`shot_type`为`multi`，生成多镜头视频。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.6-r2v-flash",<br>    "input": {<br>        "prompt": "Character2 坐在靠窗的椅子上，手持 character3，在 character4 旁演奏一首舒缓的美国乡村民谣。Character1 对Character2开口说道：“听起来不错”",<br>        "reference_urls": [<br>            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260129/hfugmr/wan-r2v-role1.mp4",<br>            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260129/qigswt/wan-r2v-role2.mp4",<br>            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260129/qpzxps/wan-r2v-object4.png",<br>            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260129/wfjikw/wan-r2v-backgroud5.png"<br>        ]<br>    },<br>    "parameters": {<br>        "size": "1280*720",<br>        "duration": 10,<br>        "audio": true,<br>        "shot_type": "multi",<br>        "watermark": true<br>    }<br>}'<br>```<br>通过`reference_urls`传入多个视频URL。同时设置`shot_type`为`multi`，生成多镜头视频。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.6-r2v",<br>    "input": {<br>        "prompt": "character1对character2说: “I’ll rely on you tomorrow morning!” character2 回答: “You can count on me!”",<br>        "reference_urls": [<br>            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20251217/dlrrly/%E5%B0%8F%E5%A5%B3%E5%AD%A91%E8%8B%B1%E6%96%872.mp4",<br>            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20251217/fkxknn/%E9%93%83%E9%93%83.mp4"<br>        ]<br>    },<br>    "parameters": {<br>        "size": "1280*720",<br>        "duration": 10,<br>        "shot_type": "multi"<br>    }<br>}'<br>```<br>通过`reference_urls`传入单个视频URL。同时设置`shot_type`为`multi`，生成多镜头视频。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.6-r2v",<br>    "input": {<br>        "prompt": "character1一边喝奶茶，一边随着音乐即兴跳舞。",<br>        "reference_urls":["https://cdn.wanx.aliyuncs.com/static/demo-wan26/vace.mp4"]<br>    },<br>    "parameters": {<br>        "size": "1280*720",<br>        "duration": 5,<br>        "shot_type":"multi"<br>    }<br>}'<br>```<br>仅支持`wan2.6-r2v-flash`生成无声视频。<br>当生成无声视频时， **必须显式设置**`parameters.audio = false`。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.6-r2v-flash",<br>    "input": {<br>        "prompt": "character1一边喝奶茶，一边随着音乐即兴跳舞。",<br>        "reference_urls":["https://cdn.wanx.aliyuncs.com/static/demo-wan26/vace.mp4"]<br>    },<br>    "parameters": {<br>        "size": "1280*720",<br>        "duration": 5,<br>        "audio": false,<br>        "shot_type":"multi"<br>    }<br>}'<br>``` |
| ##### 请求头（Headers） |
| **Content-Type**`string` **（必选）**<br>请求内容类型。此参数必须设置为`application/json`。 |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| **X-DashScope-Async**`string` **（必选）**<br>异步处理配置参数。HTTP请求只支持异步， **必须设置为**`enable`。<br>**重要**<br>缺少此请求头将报错：“current user api does not support synchronous calls”。 |
| ##### 请求体（Request Body） |
| **model**`string` **（必选）**<br>模型名称。模型列表与价格详见 [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#5c3d28ad8a4x8 "")。<br>示例值：wan2.6-r2v-flash。 |
| **input**`object` **（必选）**<br>输入的基本信息，如提示词等。<br>**属性**<br>**prompt**`string` **（必选）**<br>文本提示词。用来描述生成视频中期望包含的元素和视觉特点。<br>支持中英文，每个汉字、字母、标点占一个字符，超过部分会自动截断。<br>- wan2.6-r2v-flash：长度不超过1500个字符。<br>  <br>- wan2.6-r2v：长度不超过1500个字符。<br>  <br>角色引用说明：通过“ **character1、character2**”这类标识引用参考角色，每个参考（视频或图像）仅包含单一角色。模型仅通过此方式识别参考中的角色。<br>示例值：character1在沙发上开心地看电影。<br>提示词的使用技巧请参见 [文生视频/图生视频Prompt指南](https://help.aliyun.com/zh/model-studio/text-to-video-prompt "")。<br>**negative\_prompt**`string` （可选）<br>反向提示词，用来描述不希望在视频画面中出现的内容，可以对视频画面进行限制。<br>支持中英文，长度不超过500个字符，超过部分会自动截断。<br>示例值：低分辨率、错误、最差质量、低质量、残缺、多余的手指、比例不良等。<br>**reference\_urls**`array[string]` **（必选）**<br>**重要**<br>reference\_urls直接影响费用，计费规则请参见 [计费与限流](https://help.aliyun.com/zh/model-studio/video-to-video-guide#6f5774ce5fqie "")。<br>上传的参考文件 URL 数组，支持传入视频和图像。用于提取角色形象与音色（如有），以生成符合参考特征的视频。<br>- 每个 URL 可指向 **一张图像** 或 **一段视频**：<br>  <br>  - 图像数量：0～5。<br>    <br>  - 视频数量：0～3。<br>    <br>  - 总数限制：图像 \+ 视频 ≤ 5。<br>- 传入多个参考文件时，按照数组顺序定义角色的顺序。即第 1 个 URL 对应 character1，第 2 个对应 character2，以此类推。<br>  <br>- 每个参考文件仅包含一个主体角色。例如 character1 为小女孩，character2 为闹钟。<br>  <br>支持输入的格式：<br>1. 公网URL:<br>   <br>   - 支持 HTTP 或 HTTPS 协议。<br>     <br>   - 示例值：https://cdn.translate.alibaba.com/xxx.png。<br>2. 临时URL：<br>   <br>   - 支持OSS协议，必须通过 [上传文件获取临时 URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。<br>     <br>   - 示例值：oss://dashscope-instant/xxx/xxx.png。<br>参考视频要求：<br>- 格式：MP4、MOV。<br>  <br>- 时长：1s～30s。<br>  <br>- 视频大小：不超过100MB。<br>  <br>参考图像要求：<br>- 格式：JPEG、JPG、PNG（不支持透明通道）、BMP、WEBP。<br>  <br>- 分辨率：宽高均需在 \[240, 5000\]像素之间。<br>  <br>- 图像大小：不超过10MB。<br>  <br>示例值：\["https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/xxx.mp4", "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/xxx.jpg"\]。<br>**已废弃字段**<br>**reference\_video\_urls**`array[string]`<br>**重要**<br>推荐使用`reference_urls`替代`reference_video_urls`。<br>上传的参考视频文件 URL 数组。用于提取角色形象与音色（如有），以生成符合参考特征的视频。<br>- 最多支持 **3 个视频**。<br>  <br>- 传入多个视频时，按照数组顺序定义视频角色的顺序。即第 1 个 URL 对应 character1，第 2 个对应 character2，以此类推。<br>  <br>- 每个参考视频仅包含一个角色（如 character1 为小女孩，character2 为闹钟）。<br>  <br>- URL支持 HTTP 或 HTTPS 协议。本地文件可通过 [上传文件获取临时URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。 <br>  <br>单个视频要求：<br>- 格式：MP4、MOV。<br>  <br>- 时长：2～30s。<br>  <br>- 文件大小：视频不超过100MB。<br>  <br>示例值：\["https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/xxx.mp4"\]。 |
| **parameters**`object` （可选）<br>图像处理参数。如设置视频分辨率、开启prompt智能改写、添加水印等。<br>**属性**<br>**size**`string` （可选）<br>**重要**<br>- size直接影响费用，费用 = 单价（基于分辨率）× 时长（秒）。同一模型：1080P > 720P ，请在调用前确认 [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#5c3d28ad8a4x8 "")。<br>  <br>- size必须设置为具体数值（如 `1280*720`），而不是 1:1或720P。<br>  <br>指定生成的视频分辨率，格式为`宽*高`。该参数的默认值和可用枚举值依赖于 model 参数，规则如下：<br>- wan2.6-r2v-flash：默认值为 `1920*1080`（1080P）。可选分辨率：720P、1080P对应的所有分辨率。<br>  <br>- wan2.6-r2v：默认值为 `1920*1080`（1080P）。可选分辨率：720P、1080P对应的所有分辨率。<br>  <br>720P档位：可选的视频分辨率及其对应的视频宽高比为：<br>- `1280*720`：16:9。<br>  <br>- `720*1280`：9:16。<br>  <br>- `960*960`：1:1。<br>  <br>- `1088*832`：4:3。<br>  <br>- `832*1088`：3:4。<br>  <br>1080P档位：可选的视频分辨率及其对应的视频宽高比为：<br>- `1920*1080`： 16:9。<br>  <br>- `1080*1920`： 9:16。<br>  <br>- `1440*1440`： 1:1。<br>  <br>- `1632*1248`： 4:3。<br>  <br>- `1248*1632`： 3:4。<br>  <br>**duration**`integer` （可选）<br>**重要**<br>duration直接影响费用。费用 = 单价（基于分辨率）× 时长（秒），请在调用前确认 [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#5c3d28ad8a4x8 "")。<br>生成视频的时长，单位为秒。<br>- wan2.6-r2v-flash：取值为\[2, 10\]之间的整数。默认值为5。<br>  <br>- wan2.6-r2v：取值为\[2, 10\]之间的整数。默认值为5。<br>  <br>示例值：5。<br>**shot\_type**`string` （可选）<br>指定生成视频的镜头类型，即视频是由一个连续镜头还是多个切换镜头组成。<br>参数优先级：`shot_type > prompt`。例如，若 shot\_type设置为"single"，即使 prompt 中包含“生成多镜头视频”，模型仍会输出单镜头视频。<br>可选值：<br>- single：默认值，输出单镜头视频<br>  <br>- multi：输出多镜头视频。<br>  <br>示例值：single。<br>**说明**<br>当希望严格控制视频的叙事结构（如产品展示用单镜头、故事短片用多镜头），可通过此参数指定。<br>**audio**`boolean` （可选）<br>**重要**<br>audio直接影响费用，有声视频与无声视频价格不同，请在调用前确认 [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#5c3d28ad8a4x8 "")。<br>**支持模型：wan2.6-r2v-flash。**<br>是否生成有声视频。<br>可选值：<br>- true：默认值，输出有声视频。<br>  <br>- false：输出无声视频。<br>  <br>示例值：true。<br>**watermark**`boolean` （可选） <br>是否添加水印标识，水印位于视频右下角，文案固定为“AI生成”。<br>- false：默认值，不添加水印。<br>  <br>- true：添加水印。<br>  <br>示例值：false。<br>**seed**`integer`（可选）<br>随机数种子，取值范围为`[0, 2147483647]`。<br>未指定时，系统自动生成随机种子。若需提升生成结果的可复现性，建议固定seed值。<br>请注意，由于模型生成具有概率性，即使使用相同 seed，也不能保证每次生成结果完全一致。<br>示例值：12345。 |

|     |     |
| --- | --- |
| #### 响应参数 | 成功响应<br>异常响应<br>请保存 task\_id，用于查询任务状态与结果。<br>```json<br>{<br>    "output": {<br>        "task_status": "PENDING",<br>        "task_id": "0385dc79-5ff8-4d82-bcb6-xxxxxx"<br>    },<br>    "request_id": "4909100c-7b5a-9f92-bfe5-xxxxxx"<br>}<br>```<br>创建任务失败，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "code": "InvalidApiKey",<br>    "message": "No API-key provided.",<br>    "request_id": "7438d53d-6eb8-4596-8835-xxxxxx"<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>**属性**<br>**task\_id**`string`<br>任务ID。查询有效期24小时。<br>**task\_status**`string`<br>任务状态。<br>**枚举值**<br>- PENDING：任务排队中<br>  <br>- RUNNING：任务处理中<br>  <br>- SUCCEEDED：任务执行成功<br>  <br>- FAILED：任务执行失败<br>  <br>- CANCELED：任务已取消<br>  <br>- UNKNOWN：任务不存在或状态未知 |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |
| **code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |  |
| **message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |  |

### 步骤2：根据任务ID查询结果

北京

新加坡

弗吉尼亚

`GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id}`

`GET https://dashscope-intl.aliyuncs.com/api/v1/tasks/{task_id}`

`GET https://dashscope-us.aliyuncs.com/api/v1/tasks/{task_id}`

**说明**

- **轮询建议**：视频生成过程约需数分钟，建议采用 **轮询** 机制，并设置合理的查询间隔（如 15 秒）来获取结果。

- **任务状态流转**：PENDING（排队中）→ RUNNING（处理中）→ SUCCEEDED（成功）/ FAILED（失败）。

- **结果链接**：任务成功后返回视频链接，有效期为 **24 小时**。建议在获取链接后立即下载并转存至永久存储（如 [阿里云 OSS](https://help.aliyun.com/zh/oss/user-guide/what-is-oss "")）。

- **task\_id 有效期**： **24小时**，超时后将无法查询结果，接口将返回任务状态为`UNKNOWN`。

- **QPS 限制**：查询接口默认QPS为20。如需更高频查询或事件通知，建议 [配置异步任务回调](https://help.aliyun.com/zh/model-studio/async-task-api "")。

- **更多操作**：如需批量查询、取消任务等操作，请参见 [管理异步任务](https://help.aliyun.com/zh/model-studio/manage-asynchronous-tasks#f26499d72adsl "")。


|     |     |
| --- | --- |
| #### 请求参数 | 查询任务结果<br>将`{task_id}`完整替换为上一步接口返回的`task_id`的值。<br>```curl<br>curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id} \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY"<br>``` |
| ##### **请求头（Headers）** |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| ##### **URL路径参数（Path parameters）** |
| **task\_id**`string` **（必选）**<br>任务ID。 |

|     |     |
| --- | --- |
| #### **响应参数** | 任务执行成功<br>任务执行失败<br>任务查询过期<br>视频URL仅保留24小时，超时后会被自动清除，请及时保存生成的视频。<br>```json<br>{<br>    "request_id": "caa62a12-8841-41a6-8af2-xxxxxx",<br>    "output": {<br>        "task_id": "eff1443c-ccab-4676-aad3-xxxxxx",<br>        "task_status": "SUCCEEDED",<br>        "submit_time": "2025-12-16 00:25:59.869",<br>        "scheduled_time": "2025-12-16 00:25:59.900",<br>        "end_time": "2025-12-16 00:30:35.396",<br>        "orig_prompt": "character1在沙发上开心的看电影",<br>        "video_url": "https://dashscope-result-sh.oss-accelerate.aliyuncs.com/xxx.mp4?Expires=xxx"<br>    },<br>     "usage": {<br>        "duration": 10.0,<br>        "size": "1280*720",<br>        "input_video_duration": 5,<br>        "output_video_duration": 5,<br>        "video_count": 1,<br>        "SR": 720<br>    }<br>}<br>```<br>若任务执行失败，task\_status将置为 FAILED，并提供错误码和信息。请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "request_id": "e5d70b02-ebd3-98ce-9fe8-759d7d7b107d",<br>    "output": {<br>        "task_id": "86ecf553-d340-4e21-af6e-a0c6a421c010",<br>        "task_status": "FAILED",<br>        "code": "InvalidParameter",<br>        "message": "The size is not match xxxxxx"<br>    }<br>}<br>```<br>task\_id查询有效期为 24 小时，超时后将无法查询，返回以下报错信息。<br>```json<br>{<br>    "request_id": "a4de7c32-7057-9f82-8581-xxxxxx",<br>    "output": {<br>        "task_id": "502a00b1-19d9-4839-a82f-xxxxxx",<br>        "task_status": "UNKNOWN"<br>    }<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>**属性**<br>**task\_id**`string` **（必选）**<br>任务ID。<br>**task\_status**`string`<br>任务状态。<br>**枚举值**<br>- PENDING：任务排队中<br>  <br>- RUNNING：任务处理中<br>  <br>- SUCCEEDED：任务执行成功<br>  <br>- FAILED：任务执行失败<br>  <br>- CANCELED：任务已取消<br>  <br>- UNKNOWN：任务不存在或状态未知<br>  <br>**submit\_time**`string`<br>任务提交时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**scheduled\_time**`string`<br>任务执行时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**end\_time**`string`<br>任务完成时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**video\_url**`string`<br>视频URL。仅在 task\_status 为 SUCCEEDED 时返回。<br>链接有效期24小时，可通过此URL下载视频。视频格式为MP4（H.264 编码）。<br>**orig\_prompt**`string`<br>原始输入的prompt，对应请求参数`prompt`。<br>**code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。<br>**message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |
| **usage**`object`<br>输出信息统计。只对成功的结果计数。<br>**属性**<br>**input\_video\_duration**`integer`<br>输入的参考视频的时长，单位秒。<br>**output\_video\_duration**`integer`<br>输出视频的时长，单位秒。<br>**duration**`float`<br>总视频时长。计费按duration时长计算。<br>计算公式：`duration = input_video_duration + output_video_duration`。<br>**SR**`integer`<br>生成视频的分辨率档位。示例值：720。<br>**size**`string`<br>生成视频的分辨率。格式为“宽\*高 _”_，示例值：1280\*720。<br>**video\_count**`integer`<br>生成视频的数量。固定为1。 |  |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |  |

## **使用限制**

- **数据时效**：任务`task_id`和 视频`video_url`均只保留 24 小时，过期后将无法查询或下载。

- **内容审核**：输入的 prompt 和输出的视频均会经过内容安全审核，包含违规内容的请求将报错“IPInfringementSuspect”或“DataInspectionFailed”，具体参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。

- **网络访问配置**：视频链接存储于阿里云 OSS，如果业务系统因安全策略无法访问外部OSS链接，请将以下 OSS 域名加入网络访问白名单。















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


## **错误码**

如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。