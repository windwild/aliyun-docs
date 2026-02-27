### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[视频生成](https://help.aliyun.com/zh/model-studio/video-generation-api/)万相-文生视频

# 万相-文生视频API参考

更新时间：2026-02-10 01:16:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：万相-参考生视频](https://help.aliyun.com/zh/model-studio/wan-video-to-video-api-reference)[下一篇：万相-通用视频编辑](https://help.aliyun.com/zh/model-studio/wanx-vace-api-reference)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

适用范围

HTTP调用

步骤1：创建任务获取任务ID

步骤2：根据任务ID查询结果

DashScope SDK调用

Python SDK调用

Java SDK调用

使用限制

错误码

常见问题

万相文生视频模型基于 **文本提示词**，生成一段流畅的视频。

**相关文档**： [使用指南](https://help.aliyun.com/zh/model-studio/text-to-video-guide "")

## 适用范围

为确保调用成功，请务必保证 **模型、Endpoint URL 和 API Key 均属于同一地域**。跨地域调用将会失败。

- [**选择模型**](https://help.aliyun.com/zh/model-studio/text-to-video-guide#06f39eafa2dwt "")：确认模型所属的地域。

- **选择 URL**：选择对应的地域 Endpoint URL，支持HTTP URL或 DashScope SDK URL。

- **配置 API Key**：获取该地域的 [API Key与API Host](https://help.aliyun.com/zh/model-studio/get-api-key "")，再 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

- **安装 SDK**：如需通过SDK进行调用，请 [安装DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。


**说明**

本文的示例代码适用于 **北京地域**。

## HTTP调用

由于文生视频任务耗时较长（通常为1-5分钟），API采用异步调用。整个流程包含 **“创建任务 -\> 轮询获取”** 两个核心步骤，具体如下：

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
| #### 请求参数 | 多镜头叙事<br>自动配音<br>传入音频文件<br>生成无声视频<br>使用反向提示词<br>仅 wan2.6系列模型支持此功能。<br>可通过设置`"prompt_extend": true`和`"shot_type":"multi"`启用。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.6-t2v",<br>    "input": {<br>        "prompt": "一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。",<br>        "audio_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/hbiayh/%E4%BB%8E%E5%86%9B%E8%A1%8C.mp3"<br>    },<br>    "parameters": {<br>        "size": "1280*720",<br>        "prompt_extend": true,<br>        "duration": 10,<br>        "shot_type":"multi"<br>    }<br>}'<br>```<br>仅wan2.6和wan2.5系列模型支持此功能。<br>若不提供 `input.audio_url` ，模型将根据视频内容自动生成匹配的背景音乐或音效。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.5-t2v-preview",<br>    "input": {<br>        "prompt": "一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。"<br>    },<br>    "parameters": {<br>        "size": "832*480",<br>        "prompt_extend": true,<br>        "duration": 10<br>    }<br>}'<br>```<br>仅wan2.6和wan2.5系列模型支持此功能。<br>可通过 `input.audio_url` 参数传入自定义音频的 URL。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.5-t2v-preview",<br>    "input": {<br>        "prompt": "一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。",<br>        "audio_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/hbiayh/%E4%BB%8E%E5%86%9B%E8%A1%8C.mp3"<br>    },<br>    "parameters": {<br>        "size": "832*480",<br>        "prompt_extend": true,<br>        "duration": 10<br>    }<br>}'<br>```<br>仅wan2.2 和wanx2.1系列模型支持生成无声视频。默认生成无声视频，无需设置。<br>> wan2.6 及wan2.5系列模型默认生成有声视频。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.2-t2v-plus",<br>    "input": {<br>        "prompt": "低对比度，在一个复古的70年代风格地铁站里，街头音乐家在昏暗的色彩和粗糙的质感中演奏。他穿着旧式夹克，手持吉他，专注地弹奏。通勤者匆匆走过，一小群人渐渐聚拢聆听。镜头慢慢向右移动，捕捉到乐器声与城市喧嚣交织的场景，背景中有老式的地铁标志和斑驳的墙面。"<br>    },<br>    "parameters": {<br>        "size": "832*480",<br>        "prompt_extend": true<br>    }<br>}'<br>```<br>通过 negative\_prompt 排除“花朵”元素，避免其出现在视频画面中。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.2-t2v-plus",<br>    "input": {<br>        "prompt": "一只小猫在月光下奔跑",<br>        "negative_prompt": "花朵"<br>    },<br>    "parameters": {<br>        "size": "832*480"<br>    }<br>}'<br>``` |
| ##### 请求头（Headers） |
| **Content-Type**`string` **（必选）**<br>请求内容类型。此参数必须设置为`application/json`。 |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| **X-DashScope-Async**`string` **（必选）**<br>异步处理配置参数。HTTP请求只支持异步， **必须设置为**`enable`。<br>**重要**<br>缺少此请求头将报错：“current user api does not support synchronous calls”。 |
| ##### 请求体（Request Body） |
| **model**`string` **（必选）**<br>模型名称。模型列表与价格详见 [模型价格](https://help.aliyun.com/zh/model-studio/models#577af209dc0rc "")。<br>示例值：wan2.6-t2v。 |
| **input**`object` **（必选）**<br>输入的基本信息，如提示词等。<br>**属性**<br>**prompt**`string` **（必选）**<br>文本提示词。用来描述生成视频中期望包含的元素和视觉特点。<br>支持中英文，每个汉字/字母占一个字符，超过部分会自动截断。长度限制因模型版本而异：<br>- wan2.6和wan2.5系列模型：长度不超过1500个字符。<br>  <br>- wan2.2 和wanx2.1系列模型：长度不超过800个字符。<br>  <br>示例值：一只小猫在月光下奔跑。<br>提示词的使用技巧请参见 [文生视频/图生视频Prompt指南](https://help.aliyun.com/zh/model-studio/text-to-video-prompt "")。<br>**negative\_prompt**`string` （可选）<br>反向提示词，用来描述不希望在视频画面中看到的内容，可以对视频画面进行限制。<br>支持中英文，长度不超过500个字符，超过部分会自动截断。<br>示例值：低分辨率、错误、最差质量、低质量、残缺、多余的手指、比例不良等。<br>**audio\_url**`string` （可选）<br>**支持模型：wan2.6和wan2.5系列模型。**<br>音频文件URL，模型将使用该音频生成视频。<br>支持输入的格式：<br>1. 公网URL：<br>   <br>   - 支持 HTTP 和 HTTPS 协议。<br>     <br>   - 示例值：https://help-static-aliyun-doc.aliyuncs.com/xxx.mp3。<br>2. 临时URL：<br>   <br>   - 支持OSS协议，必须通过 [上传文件获取临时 URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。<br>     <br>   - 示例值：oss://dashscope-instant/xxx/xxx.mp3。<br>音频限制：<br>- 格式：wav、mp3。<br>  <br>- 时长：3～30s。<br>  <br>- 文件大小：不超过15MB。<br>  <br>- 超限处理：若音频长度超过 `duration` 值（ 如5秒），自动截取前5秒，其余部分丢弃。若音频长度不足视频时长，超出音频长度部分为无声视频。例如，音频为3秒，视频时长为5秒，输出视频前3秒有声，后2秒无声。 |
| **parameters**`object` （可选）<br>图像处理参数。如设置视频分辨率、开启prompt智能改写、添加水印等。<br>**属性**<br>**size**`string` （可选）<br>**重要**<br>- size直接影响费用，费用 = 单价（基于分辨率）× 时长（秒）。同一模型：1080P > 720P > 480P，请在调用前确认 [模型价格](https://help.aliyun.com/zh/model-studio/models#577af209dc0rc "")。<br>  <br>- size必须设置为具体数值（如 `1280*720`），而不是 1:1或480P。<br>  <br>指定生成的视频分辨率，格式为`宽*高`。该参数的默认值和可用枚举值依赖于 model 参数，规则如下：<br>- **wan2.6-t2v**：默认值为 `1920*1080`（1080P）。可选分辨率：720P、1080P对应的所有分辨率。<br>  <br>- **wan2.6-t2v-us**：默认值为 `1920*1080`（1080P）。可选分辨率：720P、1080P对应的所有分辨率。<br>  <br>- **wan2.5-t2v-preview**：默认值为 `1920*1080`（1080P）。可选分辨率：480P、720P、1080P对应的所有分辨率。<br>  <br>- **wan2.2-t2v-plus**：默认值为 `1920*1080`（1080P）。可选分辨率：480P、1080P对应的所有分辨率。<br>  <br>- **wanx2.1-t2v-turbo** ：默认值为 `1280*720`（720P）。可选分辨率：480P、720P 对应的所有分辨率。<br>  <br>- **wanx2.1-t2v-plus**：默认值为`1280*720`（720P）。可选分辨率：720P 对应的所有分辨率。<br>  <br>480P档位：可选的视频分辨率及其对应的视频宽高比为：<br>- `832*480`：16:9。<br>  <br>- `480*832`：9:16。<br>  <br>- `624*624`：1:1。<br>  <br>720P档位：可选的视频分辨率及其对应的视频宽高比为：<br>- `1280*720`：16:9。<br>  <br>- `720*1280`：9:16。<br>  <br>- `960*960`：1:1。<br>  <br>- `1088*832`：4:3。<br>  <br>- `832*1088`：3:4。<br>  <br>1080P档位：可选的视频分辨率及其对应的视频宽高比为：<br>- `1920*1080`： 16:9。<br>  <br>- `1080*1920`： 9:16。<br>  <br>- `1440*1440`： 1:1。<br>  <br>- `1632*1248`： 4:3。<br>  <br>- `1248*1632`： 3:4。<br>  <br>**duration**`integer` （可选）<br>**重要**<br>duration直接影响费用。费用 = 单价（基于分辨率）× 时长（秒），请在调用前确认 [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#8e284e51d1nil "")。<br>生成视频的时长，单位为秒。该参数的取值依赖于 model参数：<br>- wan2.6-t2v：取值为\[2, 15\]之间的整数。默认值为5。<br>  <br>- wan2.6-t2v-us：可选值为5、10。默认值为5。<br>  <br>- wan2.5-t2v-preview：可选值为5、10。默认值为5。<br>  <br>- wan2.2-t2v-plus：固定为5秒，且不支持修改。<br>  <br>- wanx2.1-t2v-plus：固定为5秒，且不支持修改。<br>  <br>- wanx2.1-t2v-turbo：固定为5秒，且不支持修改。<br>  <br>示例值：5。<br>**prompt\_extend**`boolean` （可选） <br>是否开启prompt智能改写。开启后使用大模型对输入prompt进行智能改写。对于较短的prompt生成效果提升明显，但会增加耗时。<br>- true：默认值，开启智能改写。<br>  <br>- false：不开启智能改写。<br>  <br>示例值：true。<br>**shot\_type**`string` （可选）<br>**支持模型：wan2.6系列模型。**<br>指定生成视频的镜头类型，即视频是由一个连续镜头还是多个切换镜头组成。<br>生效条件：仅当`"prompt_extend": true` 时生效。<br>参数优先级：`shot_type > prompt`。例如，若 shot\_type设置为"single"，即使 prompt 中包含“生成多镜头视频”，模型仍会输出单镜头视频。<br>可选值：<br>- single：默认值，输出单镜头视频。<br>  <br>- multi：输出多镜头视频。<br>  <br>示例值：single。<br>**说明**<br>当希望严格控制视频的叙事结构（如产品展示用单镜头、故事短片用多镜头），可通过此参数指定。<br>**watermark**`boolean` （可选） <br>是否添加水印标识，水印位于视频右下角，文案固定为“AI生成”。<br>- false：默认值，不添加水印。<br>  <br>- true：添加水印。<br>  <br>示例值：false。<br>**seed**`integer`（可选）<br>随机数种子，取值范围为`[0, 2147483647]`。<br>未指定时，系统自动生成随机种子。若需提升生成结果的可复现性，建议固定seed值。<br>请注意，由于模型生成具有概率性，即使使用相同 seed，也不能保证每次生成结果完全一致。<br>示例值：12345。 |

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
| #### **响应参数** | 任务执行成功<br>任务执行失败<br>任务查询过期<br>视频URL仅保留24小时，超时后会被自动清除，请及时保存生成的视频。<br>```json<br>{<br>    "request_id": "caa62a12-8841-41a6-8af2-xxxxxx",<br>    "output": {<br>        "task_id": "eff1443c-ccab-4676-aad3-xxxxxx",<br>        "task_status": "SUCCEEDED",<br>        "submit_time": "2025-09-29 14:18:52.331",<br>        "scheduled_time": "2025-09-29 14:18:59.290",<br>        "end_time": "2025-09-29 14:23:39.407",<br>        "orig_prompt": "一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。",<br>        "video_url": "https://dashscope-result-sh.oss-accelerate.aliyuncs.com/xxx.mp4?Expires=xxx"<br>    },<br>    "usage": {<br>        "duration": 10,<br>        "size": "1280*720",<br>        "input_video_duration": 0,<br>        "output_video_duration": 10,<br>        "video_count": 1,<br>        "SR": 720<br>    }<br>}<br>```<br>若任务执行失败，task\_status将置为 FAILED，并提供错误码和信息。请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "request_id": "e5d70b02-ebd3-98ce-9fe8-759d7d7b107d",<br>    "output": {<br>        "task_id": "86ecf553-d340-4e21-af6e-a0c6a421c010",<br>        "task_status": "FAILED",<br>        "code": "InvalidParameter",<br>        "message": "The size is not match xxxxxx"<br>    }<br>}<br>```<br>task\_id查询有效期为 24 小时，超时后将无法查询，返回以下报错信息。<br>```json<br>{<br>    "request_id": "a4de7c32-7057-9f82-8581-xxxxxx",<br>    "output": {<br>        "task_id": "502a00b1-19d9-4839-a82f-xxxxxx",<br>        "task_status": "UNKNOWN"<br>    }<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>**属性**<br>**task\_id**`string`<br>任务ID。查询有效期24小时。<br>**task\_status**`string`<br>任务状态。<br>**枚举值**<br>- PENDING：任务排队中<br>  <br>- RUNNING：任务处理中<br>  <br>- SUCCEEDED：任务执行成功<br>  <br>- FAILED：任务执行失败<br>  <br>- CANCELED：任务已取消<br>  <br>- UNKNOWN：任务不存在或状态未知<br>  <br>**轮询过程中的状态流转：**<br>- PENDING（排队中） → RUNNING（处理中）→ SUCCEEDED（成功）/ FAILED（失败）。<br>  <br>- 初次查询状态通常为 PENDING（排队中）或 RUNNING（处理中）。<br>  <br>- 当状态变为 SUCCEEDED 时，响应中将包含生成的视频url。<br>  <br>- 若状态为 FAILED，请检查错误信息并重试。<br>  <br>**submit\_time**`string`<br>任务提交时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**scheduled\_time**`string`<br>任务执行时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**end\_time**`string`<br>任务完成时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**video\_url**`string`<br>视频URL。仅在 task\_status 为 SUCCEEDED 时返回。<br>链接有效期24小时，可通过此URL下载视频。视频格式为MP4（H.264 编码）。<br>**orig\_prompt**`string`<br>原始输入的prompt，对应请求参数`prompt`。<br>**actual\_prompt**`string`<br>当 `prompt_extend=true` 时，系统会对输入 prompt 进行智能改写，此字段返回实际用于生成的优化后 prompt。<br>- 若 `prompt_extend=false`，该字段不会返回。<br>  <br>- 注意：wan2.6 模型无论 `prompt_extend` 取值如何，均不返回此字段。<br>  <br>**code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。<br>**message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |
| **usage**`object`<br>输出信息统计。只对成功的结果计数。<br>**属性**<br>**video\_duration**`integer`<br>仅在使用 wan2.5 及以下版本模型时返回，用于计费。<br>生成视频的时长，单位秒。枚举值为5、10。<br>**duration**`float`<br>仅在使用 wan2.6 模型时返回，用于计费。<br>表示总的视频时长，且`duration=input_video_duration+output_video_duration`。<br>**input\_video\_duration**`integer`<br>仅在使用 wan2.6 模型时返回。固定为0。<br>**output\_video\_duration**`integer`<br>仅在使用 wan2.6 模型时返回。<br>输出视频的时长，单位秒。其值等同于`input.duration`的值。<br>**SR**`integer`<br>仅在使用 wan2.6 模型时返回。生成视频的分辨率档位。示例值：720。<br>**size**`string`<br>仅在使用 wan2.6 模型时返回。生成视频的分辨率。格式为“宽\*高 _”_，示例值：1920\*1080。<br>**video\_ratio**`string`<br>仅 wan2.5 及以下版本模型时返回。生成视频的分辨率。格式为“宽\*高 _”_，示例值：832\*480。<br>**video\_count**`integer`<br>生成视频的数量。固定为1。 |  |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |  |

## DashScope SDK调用

SDK 的参数命名与 [HTTP接口](https://help.aliyun.com/zh/model-studio/text-to-video-api-reference#42703589880ts "") 基本一致，参数结构根据语言特性进行封装。

由于文生视频任务耗时较长（通常为1-5分钟），SDK 在底层封装了 HTTP 异步调用流程，支持同步、异步两种调用方式。

> 具体耗时受限于排队任务数和服务执行情况，请在获取结果时耐心等待。

### Python SDK调用

**重要**

请确保 DashScope Python SDK 版本 **不低于**`1.25.8`，再运行以下代码。

若版本过低，可能会触发 “url error, please check url!” 等错误。请参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

根据模型所在地域设置 `base_http_api_url`:

北京

新加坡

弗吉尼亚

`dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'`

`dashscope.base_http_api_url = 'https://dashscope-intl.aliyuncs.com/api/v1'`

`dashscope.base_http_api_url = 'https://dashscope-us.aliyuncs.com/api/v1'`

同步调用

异步调用

##### 请求示例

```python
from http import HTTPStatus
from dashscope import VideoSynthesis
import dashscope
import os

# 以下为北京地域URL，各地域的URL不同，获取URL：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY")

def sample_sync_call_t2v():
    # call sync api, will return the result
    print('please wait...')
    rsp = VideoSynthesis.call(api_key=api_key,
                              model='wan2.6-t2v',
                              prompt='一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。',
                              audio_url='https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/hbiayh/%E4%BB%8E%E5%86%9B%E8%A1%8C.mp3',
                              size='1280*720',
                              duration=10,
                              negative_prompt="",
                              prompt_extend=True,
                              watermark=False,
                              seed=12345)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output.video_url)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    sample_sync_call_t2v()
```

##### 响应示例

> video\_url 有效期24小时，请及时下载视频。

```json
{
    "status_code": 200,
    "request_id": "167f3beb-3dd0-47fe-a83c-xxxxxx",
    "code": null,
    "message": "",
    "output": {
        "task_id": "5b65411f-d946-4e29-859e-xxxxxx",
        "task_status": "SUCCEEDED",
        "video_url": "https://dashscope-result-bj.oss-accelerate.aliyuncs.com/xxx.mp4?Expires=xxx",
        "submit_time": "2025-10-23 11:47:23.879",
        "scheduled_time": "2025-10-23 11:47:34.351",
        "end_time": "2025-10-23 11:52:35.323",
        "orig_prompt": "一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。"
    },
    "usage": {
        "video_count": 1,
        "video_duration": 0,
        "video_ratio": "",
        "duration": 10,
        "size": "1280*720",
        "input_video_duration": 0,
        "output_video_duration": 10,
        "SR": 720
    }
}
```

##### 请求示例

```python
from http import HTTPStatus
from dashscope import VideoSynthesis
import dashscope
import os

# 以下为北京地域URL，各地域的URL不同，获取URL：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY")

def sample_async_call_t2v():
    # call async api, will return the task information
    # you can get task status with the returned task id.
    rsp = VideoSynthesis.async_call(api_key=api_key,
                                    model='wan2.6-t2v',
                                    prompt='一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。',
                                    audio_url='https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/hbiayh/%E4%BB%8E%E5%86%9B%E8%A1%8C.mp3',
                                    size='1280*720',
                                    duration=10,
                                    negative_prompt="",
                                    prompt_extend=True,
                                    watermark=False,
                                    seed=12345)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print("task_id: %s" % rsp.output.task_id)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

    # get the task information include the task status.
    status = VideoSynthesis.fetch(task=rsp, api_key=api_key)
    if status.status_code == HTTPStatus.OK:
        print(status.output.task_status)  # check the task status
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (status.status_code, status.code, status.message))

    # wait the task complete, will call fetch interval, and check it's in finished status.
    rsp = VideoSynthesis.wait(task=rsp, api_key=api_key)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output.video_url)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    sample_async_call_t2v()
```

##### 响应示例

1、创建任务的响应示例

```json
{
	"status_code": 200,
	"request_id": "c86ff7ba-8377-917a-90ed-xxxxxx",
	"code": "",
	"message": "",
	"output": {
		"task_id": "721164c6-8619-4a35-a6d9-xxxxxx",
		"task_status": "PENDING",
		"video_url": ""
	},
	"usage": null
}
```

2、查询任务结果的响应示例

> video\_url 有效期24小时，请及时下载视频。

```json
{
    "status_code": 200,
    "request_id": "167f3beb-3dd0-47fe-a83c-xxxxxx",
    "code": null,
    "message": "",
    "output": {
        "task_id": "5b65411f-d946-4e29-859e-xxxxxx",
        "task_status": "SUCCEEDED",
        "video_url": "https://dashscope-result-bj.oss-accelerate.aliyuncs.com/xxx.mp4?Expires=xxx",
        "submit_time": "2025-10-23 11:47:23.879",
        "scheduled_time": "2025-10-23 11:47:34.351",
        "end_time": "2025-10-23 11:52:35.323",
        "orig_prompt": "一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。"
    },
    "usage": {
        "video_count": 1,
        "video_duration": 0,
        "video_ratio": "",
        "duration": 10,
        "size": "1280*720",
        "input_video_duration": 0,
        "output_video_duration": 10,
        "SR": 720
    }
}
```

### Java SDK调用

**重要**

请确保 DashScope Java SDK 版本 **不低于**`2.22.6`，再运行以下代码。

若版本过低，可能会触发 “url error, please check url!” 等错误。请参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

根据模型所在地域设置 `baseHttpApiUrl`:

北京

新加坡

弗吉尼亚

`Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";`

`Constants.baseHttpApiUrl = "https://dashscope-intl.aliyuncs.com/api/v1";`

`Constants.baseHttpApiUrl = "https://dashscope-us.aliyuncs.com/api/v1";`

同步调用

异步调用

##### 请求示例

```java
// Copyright (c) Alibaba, Inc. and its affiliates.

import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesis;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisParam;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.JsonUtils;
import com.alibaba.dashscope.utils.Constants;
import java.util.HashMap;
import java.util.Map;

public class Text2Video {

    static {
        // 以下为北京地域url，各地域的url不同，获取url：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
    // 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    public static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    /**
     * Create a video compositing task and wait for the task to complete.
     */
    public static void text2Video() throws ApiException, NoApiKeyException, InputRequiredException {
        VideoSynthesis vs = new VideoSynthesis();
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("prompt_extend", true);
        parameters.put("watermark", false);
        parameters.put("seed", 12345);

        VideoSynthesisParam param =
                VideoSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.6-t2v")
                        .prompt("一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。")
                        .audioUrl("https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/hbiayh/%E4%BB%8E%E5%86%9B%E8%A1%8C.mp3")
                        .negativePrompt("")
                        .size("1280*720")
                        .duration(10)
                        .parameters(parameters)
                        .build();
        System.out.println("please wait...");
        VideoSynthesisResult result = vs.call(param);
        System.out.println(JsonUtils.toJson(result));
    }

    public static void main(String[] args) {
        try {
            text2Video();
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

##### 响应示例

> video\_url 有效期24小时，请及时下载视频。

```json
{
    "request_id": "c1209113-8437-424f-a386-xxxxxx",
    "output": {
        "task_id": "966cebcd-dedc-4962-af88-xxxxxx",
        "task_status": "SUCCEEDED",
        "video_url": "https://dashscope-result-sh.oss-accelerate.aliyuncs.com/xxx.mp4?Expires=xxx",
        "orig_prompt": "一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。",
        "submit_time": "2026-01-22 23:13:40.553",
        "scheduled_time": "2026-01-22 23:13:49.415",
        "end_time": "2026-01-22 23:17:56.380"
    },
    "usage": {
        "video_count": 1,
        "duration": 10.0,
        "size": "1280*720",
        "input_video_duration": 0.0,
        "output_video_duration": 10.0,
        "SR": "720"
    },
    "status_code": 200,
    "code": "",
    "message": ""
}
```

##### 请求示例

```java
// Copyright (c) Alibaba, Inc. and its affiliates.

import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesis;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisListResult;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisParam;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.task.AsyncTaskListParam;
import com.alibaba.dashscope.utils.JsonUtils;
import com.alibaba.dashscope.utils.Constants;
import java.util.HashMap;
import java.util.Map;

public class Text2Video {


    static {
        // 以下为北京地域url，各地域的url不同，获取url：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

     // 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
    // 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    public static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    /**
     * Create a video compositing task and wait for the task to complete.
     */
    public static void text2Video() throws ApiException, NoApiKeyException, InputRequiredException {
        VideoSynthesis vs = new VideoSynthesis();
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("prompt_extend", true);
        parameters.put("watermark", false);
        parameters.put("seed", 12345);

        VideoSynthesisParam param =
                VideoSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.6-t2v")
                        .prompt("一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。")
                        .audioUrl("https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/hbiayh/%E4%BB%8E%E5%86%9B%E8%A1%8C.mp3")
                        .negativePrompt("")
                        .size("1280*720")
                        .duration(10)
                        .parameters(parameters)
                        .build();

        // 异步调用
        VideoSynthesisResult task = vs.asyncCall(param);
        System.out.println(JsonUtils.toJson(task));
        System.out.println("please wait...");

        //获取结果
        VideoSynthesisResult result = vs.wait(task, apiKey);
        System.out.println(JsonUtils.toJson(result));
    }

    // 获取任务列表
    public static void listTask() throws ApiException, NoApiKeyException {
        VideoSynthesis is = new VideoSynthesis();
        AsyncTaskListParam param = AsyncTaskListParam.builder().build();
        param.setApiKey(apiKey);
        VideoSynthesisListResult result = is.list(param);
        System.out.println(result);
    }

    // 获取单个任务结果
    public static void fetchTask(String taskId) throws ApiException, NoApiKeyException {
        VideoSynthesis is = new VideoSynthesis();
        // 如果已设置 DASHSCOPE_API_KEY 为环境变量，apiKey 可为空
        VideoSynthesisResult result = is.fetch(taskId, apiKey);
        System.out.println(result.getOutput());
        System.out.println(result.getUsage());
    }

    public static void main(String[] args) {
        try {
            text2Video();
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

##### 响应示例

1、创建任务的响应示例。

```json
{
        "request_id": "5dbf9dc5-4f4c-9605-85ea-xxxxxxxx",
	"output": {
		"task_id": "7277e20e-aa01-4709-xxxxxxxx",
		"task_status": "PENDING"
	}
}
```

2、查询任务结果的响应示例

> video\_url 有效期24小时，请及时下载视频。

```json
{
    "request_id": "c1209113-8437-424f-a386-xxxxxx",
    "output": {
        "task_id": "966cebcd-dedc-4962-af88-xxxxxx",
        "task_status": "SUCCEEDED",
        "video_url": "https://dashscope-result-sh.oss-accelerate.aliyuncs.com/xxx.mp4?Expires=xxx",
        "orig_prompt": "一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。",
        "submit_time": "2026-01-22 23:13:40.553",
        "scheduled_time": "2026-01-22 23:13:49.415",
        "end_time": "2026-01-22 23:17:56.380"
    },
    "usage": {
        "video_count": 1,
        "duration": 10.0,
        "size": "1280*720",
        "input_video_duration": 0.0,
        "output_video_duration": 10.0,
        "SR": "720"
    },
    "status_code": 200,
    "code": "",
    "message": ""
}
```

## **使用限制**

- **数据时效**：任务`task_id`和 视频`video_url`均只保留 24 小时，过期后将无法查询或下载。

- **内容审核**：输入内容和输出视频均会经过内容安全审核，包含违规内容的请求将报错“IPInfringementSuspect”或“DataInspectionFailed”，具体参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。

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

## **常见问题**

#### **Q: 如何将临时的视频链接转为永久链接？**

A: 不能直接转换该链接。正确的做法是：后端服务获取到url后，通过代码下载该视频文件，然后将其上传到永久对象存储服务（如阿里云 OSS），生成一个新的、永久访问链接。

**示例代码：下载视频到本地**

```python
import requests

def download_and_save_video(video_url, save_path):
    try:
        response = requests.get(video_url, stream=True, timeout=300) # 设置超时
        response.raise_for_status() # 如果HTTP状态码不是200，则引发异常
        with open(save_path, 'wb') as f:
            for chunk in response.iter_content(chunk_size=8192):
                f.write(chunk)
        print(f"视频已成功下载到: {save_path}")
        # 此处可以接上传到永久存储的逻辑
    except requests.exceptions.RequestException as e:
        print(f"下载视频失败: {e}")

if __name__ == '__main__':
    video_url = "http://dashscope-result-sh.oss-cn-shanghai.aliyuncs.com/xxxx"
    save_path = "video.mp4"
    download_and_save_video(video_url, save_path)
```

#### **Q: 返回的视频链接可以在浏览器中直接播放吗？**

A: 不建议这样做，因为链接会在 24 小时后失效。最佳实践是后端下载转存后，使用永久链接进行视频播放。