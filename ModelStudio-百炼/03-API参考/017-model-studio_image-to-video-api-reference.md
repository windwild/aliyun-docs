### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[视频生成](https://help.aliyun.com/zh/model-studio/video-generation-api/)万相-图生视频-基于首帧

# 万相-图生视频API参考

更新时间：2026-02-10 05:20:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：常见问题](https://help.aliyun.com/zh/model-studio/image-faq)[下一篇：万相-图生视频-视频特效](https://help.aliyun.com/zh/model-studio/wanx-video-effects)

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

万相-图生视频模型根据 **首帧图像** 和 **文本提示词**，生成一段流畅的视频。

**相关文档**： [使用指南](https://help.aliyun.com/zh/model-studio/image-to-video-guide "")

## 适用范围

为确保调用成功，请务必保证模型、endpoint URL 和 API Key 均属于 **同一地域**。跨地域调用将会失败。

- [**选择模型**](https://help.aliyun.com/zh/model-studio/image-to-video-guide#06f39eafa2dwt "")：确认模型所属的地域。

- **选择 URL**：选择对应的地域 Endpoint URL，支持HTTP URL或 DashScope SDK URL。

- **配置 API Key**：获取该地域的 [API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，再 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

- **安装 SDK**：如需通过SDK进行调用，请 [安装DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。


**说明**

本文的示例代码适用于 **北京地域**。

## HTTP调用

图生视频任务耗时较长（通常为1-5分钟），API采用异步调用的方式。整个流程包含 **“创建任务 -\> 轮询获取”** 两个核心步骤，具体如下：

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
| #### 请求参数 | 多镜头叙事<br>自动配音<br>传入音频文件<br>生成无声视频<br>使用Base64<br>使用视频特效<br>使用反向提示词<br>仅wan2.6系列模型支持此功能。<br>可通过设置`"prompt_extend": true`和`"shot_type":"multi"`启用。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.6-i2v-flash",<br>    "input": {<br>        "prompt": "一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。",<br>        "img_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/wpimhv/rap.png",<br>        "audio_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/ozwpvi/rap.mp3"<br>    },<br>    "parameters": {<br>        "resolution": "720P",<br>        "prompt_extend": true,<br>        "duration": 10,<br>        "shot_type":"multi"<br>    }<br>}'<br>```<br>仅wan2.6和wan2.5系列模型支持此功能。<br>若不提供 `input.audio_url` ，模型将根据视频内容自动生成匹配的背景音乐或音效。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.5-i2v-preview",<br>    "input": {<br>        "prompt": "一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。",<br>        "img_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/wpimhv/rap.png"<br>    },<br>    "parameters": {<br>        "resolution": "480P",<br>        "prompt_extend": true,<br>        "duration": 10<br>    }<br>}'<br>```<br>仅wan2.6和wan2.5系列模型支持此功能。<br>如需为视频指定背景音乐或配音，可通过 `input.audio_url` 参数传入自定义音频的 URL。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.5-i2v-preview",<br>    "input": {<br>        "prompt": "一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。",<br>        "img_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/wpimhv/rap.png",<br>        "audio_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/ozwpvi/rap.mp3"<br>    },<br>    "parameters": {<br>        "resolution": "480P",<br>        "prompt_extend": true,<br>        "duration": 10<br>    }<br>}'<br>```<br>仅以下模型支持生成无声视频：<br>- wan2.6-i2v-flash：若需生成无声视频， **必须显式设置**`parameters.audio = false`。<br>  <br>- wan2.2 和wanx2.1系列模型：默认生成无声视频，无需额外参数配置。<br>  <br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.2-i2v-plus",<br>    "input": {<br>        "prompt": "一只猫在草地上奔跑",<br>        "img_url": "https://cdn.translate.alibaba.com/r/wanx-demo-1.png"<br>    },<br>    "parameters": {<br>        "resolution": "480P",<br>        "prompt_extend": true<br>    }<br>}'<br>```<br>通过 `img_url` 参数传入图像的 Base64 编码字符串。<br>关于 Base64 字符串的格式要求，请参见 [传入图像](https://help.aliyun.com/zh/model-studio/image-to-video-guide#32d9db99f1fk0 "")。<br>示例：下载 [img\_base64](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250722/pmcjis/img_base64.txt) 文件，并将完整内容粘贴至`img_url`参数中。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.2-i2v-plus",<br>    "input": {<br>        "prompt": "一只猫在草地上奔跑",<br>        "img_url": "data:image/png;base64,GDU7MtCZzEbTbmRZ......"<br>    },<br>    "parameters": {<br>        "resolution": "480P",<br>        "prompt_extend": true<br>    }<br>}'<br>```<br>- prompt 字段将被忽略，建议留空。<br>  <br>- 特效的可用性与模型相关。调用前请查阅 [万相-图生视频-视频特效](https://help.aliyun.com/zh/model-studio/wanx-video-effects "")，以免调用失败。<br>  <br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wanx2.1-i2v-turbo",<br>    "input": {<br>        "img_url": "https://cdn.translate.alibaba.com/r/wanx-demo-1.png",<br>        "template": "flying"<br>    },<br>    "parameters": {<br>        "resolution": "720P"<br>    }<br>}'<br>```<br>通过 negative\_prompt 指定生成的视频避免出现“花朵”元素。<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \<br>    -H 'X-DashScope-Async: enable' \<br>    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>    -H 'Content-Type: application/json' \<br>    -d '{<br>    "model": "wan2.2-i2v-plus",<br>    "input": {<br>        "prompt": "一只猫在草地上奔跑",<br>        "negative_prompt": "花朵",<br>        "img_url": "https://cdn.translate.alibaba.com/r/wanx-demo-1.png"<br>    },<br>    "parameters": {<br>        "resolution": "480P",<br>        "prompt_extend": true<br>    }<br>}'<br>``` |
| ##### 请求头（Headers） |
| **Content-Type**`string` **（必选）**<br>请求内容类型。此参数必须设置为`application/json`。 |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| **X-DashScope-Async**`string` **（必选）**<br>异步处理配置参数。HTTP请求只支持异步， **必须设置为**`enable`。<br>**重要**<br>缺少此请求头将报错：“current user api does not support synchronous calls”。 |
| ##### 请求体（Request Body） |
| **model**`string` **（必选）**<br>模型名称。模型列表与价格详见 [模型价格](https://help.aliyun.com/zh/model-studio/models#af6bc5a9c3cp9 "")。<br>示例值：wan2.6-i2v-flash。 |
| **input**`object` **（必选）**<br>输入的基本信息，如提示词等。<br>**属性**<br>**prompt**`string` （可选） <br>文本提示词。用来描述生成图像中期望包含的元素和视觉特点。<br>支持中英文，每个汉字/字母占一个字符，超过部分会自动截断。长度限制因模型版本而异：<br>- wan2.6和wan2.5系列模型：长度不超过1500个字符。<br>  <br>- wan2.2 和wanx2.1系列模型：长度不超过800个字符。<br>  <br>当使用视频特效参数（即`template`不为空）时，prompt参数无效，无需填写。<br>示例值：一只小猫在草地上奔跑。<br>提示词使用技巧详见 [文生视频/图生视频Prompt指南](https://help.aliyun.com/zh/model-studio/text-to-video-prompt "")。<br>**negative\_prompt**`string` （可选）<br>反向提示词，用来描述不希望在视频画面中看到的内容，可以对视频画面进行限制。<br>支持中英文，长度不超过500个字符，超过部分会自动截断。<br>示例值：低分辨率、错误、最差质量、低质量、残缺、多余的手指、比例不良等。<br>**img\_url**`string` **（必选）**<br>首帧图像的URL或 Base64 编码数据。<br>图像限制：<br>- 图像格式：JPEG、JPG、PNG（不支持透明通道）、BMP、WEBP。<br>  <br>- 图像分辨率：图像的宽度和高度范围为\[360, 2000\]，单位为像素。<br>  <br>- 文件大小：不超过10MB。<br>  <br>支持输入的格式：<br>1. 公网URL:<br>   <br>   - 支持 HTTP 或 HTTPS 协议。<br>     <br>   - 示例值：https://cdn.translate.alibaba.com/r/wanx-demo-1.png。<br>2. 临时URL：<br>   <br>   - 支持OSS协议，必须通过 [上传文件获取临时 URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。<br>     <br>   - 示例值：oss://dashscope-instant/xxx/xxx.png。<br>3. Base64 编码图像后的字符串：<br>   <br>   - 数据格式：`data:{MIME_type};base64,{base64_data}`。<br>     <br>   - 示例值：data:image/png;base64,GDU7MtCZzEbTbmRZ......。（编码字符串过长，仅展示片段）<br>     <br>   - 详情请参见 [传入图像](https://help.aliyun.com/zh/model-studio/image-to-video-guide#32d9db99f1fk0 "")。<br>**audio\_url**`string` （可选）<br>**支持模型：wan2.6和wan2.5系列模型。**<br>音频文件的 URL，模型将使用该音频生成视频。<br>支持输入的格式：<br>1. 公网URL：<br>   <br>   - 支持 HTTP 和 HTTPS 协议。<br>     <br>   - 示例值：https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/xxx.mp3。<br>2. 临时URL：<br>   <br>   - 支持OSS协议，必须通过 [上传文件获取临时 URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。<br>     <br>   - 示例值：oss://dashscope-instant/xxx/2024-07-18/xxx/xxx.mp3。<br>音频限制：<br>- 格式：wav、mp3。<br>  <br>- 时长：3～30s。<br>  <br>- 文件大小：不超过15MB。<br>  <br>- 超限处理：若音频长度超过 `duration` 值（5秒或10秒），自动截取前5秒或10秒，其余部分丢弃。若音频长度不足视频时长，超出音频长度部分为无声视频。例如，音频为3秒，视频时长为5秒，输出视频前3秒有声，后2秒无声。<br>  <br>示例值：https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/ozwpvi/rap.mp3。<br>**template**`string` （可选）<br>视频特效模板的名称。若未填写，表示不使用任何视频特效。<br>不同模型支持不同的特效模板。调用前请查阅 [万相-图生视频-视频特效](https://help.aliyun.com/zh/model-studio/wanx-video-effects "")，以免调用失败。<br>示例值：flying，表示使用“魔法悬浮”特效。 |
| **parameters**`object` （可选）<br>视频处理参数，如设置视频分辨率、设置视频时长、开启prompt智能改写、添加水印等。<br>**属性**<br>**resolution**`string` （可选）<br>**重要**<br>**resolution** 直接影响费用，同一模型：1080P > 720P > 480P，请在调用前确认 [模型价格](https://help.aliyun.com/zh/model-studio/models#af6bc5a9c3cp9 "")。<br>指定生成的视频分辨率档位，用于调整视频的清晰度（总像素）。模型根据选择的分辨率档位，自动缩放至相近总像素， **视频宽高比将尽量与输入图像 img\_url 的宽高比保持一致**，详见 [常见问题](https://help.aliyun.com/zh/model-studio/image-to-video-api-reference/#2b6ac4aea9h5n "")。<br>此参数的默认值和可用枚举值依赖于 model 参数，规则如下：<br>- wan2.6-i2v-flash：可选值：720P、1080P。默认值为`1080P`。<br>  <br>- wan2.6-i2v ：可选值：720P、1080P。默认值为`1080P`。<br>  <br>- wan2.6-i2v-us ：可选值：720P、1080P。默认值为`1080P`。<br>  <br>- wan2.5-i2v-preview ：可选值：480P、720P、1080P。默认值为`1080P`。<br>  <br>- wan2.2-i2v-flash：可选值：480P、720P、1080P。默认值为`720P`。<br>  <br>- wan2.2-i2v-plus：可选值：480P、1080P。默认值为`1080P`。<br>  <br>- wanx2.1-i2v-turbo：可选值：480P、720P。默认值为`720P`。<br>  <br>- wanx2.1-i2v-plus：可选值：720P。默认值为`720P`。<br>  <br>示例值：1080P。<br>**duration**`integer` （可选）<br>**重要**<br>duration直接影响费用，按秒计费，时间越长费用越高，请在调用前确认 [模型价格](https://help.aliyun.com/zh/model-studio/models#577af209dc0rc "")。<br>生成视频的时长，单位为秒。该参数的取值依赖于 model参数：<br>- wan2.6-i2v-flash：取值为\[2, 15\]之间的整数。默认值为5。<br>  <br>- wan2.6-i2v：取值为\[2, 15\]之间的整数。默认值为5。<br>  <br>- wan2.6-i2v-us：可选值为5、10、15。默认值为5。<br>  <br>- wan2.5-i2v-preview：可选值为5、10。默认值为5。<br>  <br>- wan2.2-i2v-plus：固定为5秒，且不支持修改。<br>  <br>- wan2.2-i2v-flash：固定为5秒，且不支持修改。<br>  <br>- wanx2.1-i2v-plus：固定为5秒，且不支持修改。<br>  <br>- wanx2.1-i2v-turbo：可选值为3、4或5。默认值为5。<br>  <br>示例值：5。<br>**prompt\_extend**`boolean` （可选） <br>是否开启prompt智能改写。开启后使用大模型对输入prompt进行智能改写。对于较短的prompt生成效果提升明显，但会增加耗时。<br>- true：默认值，开启智能改写。<br>  <br>- false：不开启智能改写。<br>  <br>示例值：true。<br>**shot\_type**`string` （可选）<br>**支持模型：wan2.6系列模型。**<br>指定生成视频的镜头类型，即视频是由一个连续镜头还是多个切换镜头组成。<br>生效条件：仅当`"prompt_extend": true` 时生效。<br>参数优先级：`shot_type > prompt`。例如，若 shot\_type设置为"single"，即使 prompt 中包含“生成多镜头视频”，模型仍会输出单镜头视频。<br>可选值：<br>- single：默认值，输出单镜头视频<br>  <br>- multi：输出多镜头视频。<br>  <br>示例值：single。<br>**说明**<br>当希望严格控制视频的叙事结构（如产品展示用单镜头、故事短片用多镜头），可通过此参数指定。<br>**audio**`boolean` （可选）<br>**重要**<br>audio直接影响费用，有声视频与无声视频价格不同，请在调用前确认 [模型价格](https://help.aliyun.com/zh/model-studio/models#577af209dc0rc "")。<br>**支持模型：wan2.6-i2v-flash。**<br>是否生成有声视频。<br>参数优先级：`audio > audio_url`。当 `audio=false`时，即使传入 `audio_url`，输出仍为无声视频，且计费按无声视频计算。<br>可选值：<br>- true：默认值，输出有声视频。<br>  <br>- false：输出无声视频。<br>  <br>示例值：true。<br>**watermark**`boolean` （可选） <br>是否添加水印标识，水印位于视频右下角，文案固定为“AI生成”。<br>- false：默认值，不添加水印。<br>  <br>- true：添加水印。<br>  <br>示例值：false。<br>**seed**`integer`（可选）<br>随机数种子，取值范围为`[0, 2147483647]`。<br>未指定时，系统自动生成随机种子。若需提升生成结果的可复现性，建议固定seed值。<br>请注意，由于模型生成具有概率性，即使使用相同 seed，也不能保证每次生成结果完全一致。<br>示例值：12345。 |

|     |     |
| --- | --- |
| #### 响应参数 | 成功响应<br>异常响应<br>请保存 task\_id，用于查询任务状态与结果。<br>```json<br>{<br>    "output": {<br>        "task_status": "PENDING",<br>        "task_id": "0385dc79-5ff8-4d82-bcb6-xxxxxx"<br>    },<br>    "request_id": "4909100c-7b5a-9f92-bfe5-xxxxxx"<br>}<br>```<br>创建任务失败，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "code": "InvalidApiKey",<br>    "message": "No API-key provided.",<br>    "request_id": "7438d53d-6eb8-4596-8835-xxxxxx"<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>属性<br>**task\_id**`string`<br>任务ID。查询有效期24小时。<br>**task\_status**`string`<br>任务状态。<br>**枚举值**<br>- PENDING：任务排队中<br>  <br>- RUNNING：任务处理中<br>  <br>- SUCCEEDED：任务执行成功<br>  <br>- FAILED：任务执行失败<br>  <br>- CANCELED：任务已取消<br>  <br>- UNKNOWN：任务不存在或状态未知 |
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
| #### **响应参数** | 任务执行成功<br>任务执行失败<br>任务查询过期<br>视频URL仅保留24小时，超时后会被自动清除，请及时保存生成的视频。<br>```json<br>{<br>    "request_id": "2ca1c497-f9e0-449d-9a3f-xxxxxx",<br>    "output": {<br>        "task_id": "af6efbc0-4bef-4194-8246-xxxxxx",<br>        "task_status": "SUCCEEDED",<br>        "submit_time": "2025-09-25 11:07:28.590",<br>        "scheduled_time": "2025-09-25 11:07:35.349",<br>        "end_time": "2025-09-25 11:17:11.650",<br>        "orig_prompt": "一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。",<br>        "video_url": "https://dashscope-result-sh.oss-cn-shanghai.aliyuncs.com/xxx.mp4?Expires=xxx"<br>    },<br>    "usage": {<br>        "duration": 10,<br>        "input_video_duration": 0,<br>        "output_video_duration": 10,<br>        "video_count": 1,<br>        "SR": 720<br>    }<br>}<br>```<br>若任务执行失败，task\_status将置为 FAILED，并提供错误码和信息。请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "request_id": "e5d70b02-ebd3-98ce-9fe8-759d7d7b107d",<br>    "output": {<br>        "task_id": "86ecf553-d340-4e21-af6e-a0c6a421c010",<br>        "task_status": "FAILED",<br>        "code": "InvalidParameter",<br>        "message": "The size is not match xxxxxx"<br>    }<br>}<br>```<br>task\_id查询有效期为 24 小时，超时后将无法查询，返回以下报错信息。<br>```json<br>{<br>    "request_id": "a4de7c32-7057-9f82-8581-xxxxxx",<br>    "output": {<br>        "task_id": "502a00b1-19d9-4839-a82f-xxxxxx",<br>        "task_status": "UNKNOWN"<br>    }<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>**属性**<br>**task\_id**`string`<br>任务ID。查询有效期24小时。<br>**task\_status**`string`<br>任务状态。<br>**枚举值**<br>- PENDING：任务排队中<br>  <br>- RUNNING：任务处理中<br>  <br>- SUCCEEDED：任务执行成功<br>  <br>- FAILED：任务执行失败<br>  <br>- CANCELED：任务已取消<br>  <br>- UNKNOWN：任务不存在或状态未知<br>  <br>**轮询过程中的状态流转：**<br>- PENDING（排队中） → RUNNING（处理中）→ SUCCEEDED（成功）/ FAILED（失败）。<br>  <br>- 初次查询状态通常为 PENDING（排队中）或 RUNNING（处理中）。<br>  <br>- 当状态变为 SUCCEEDED 时，响应中将包含生成的视频url。<br>  <br>- 若状态为 FAILED，请检查错误信息并重试。<br>  <br>**submit\_time**`string`<br>任务提交时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**scheduled\_time**`string`<br>任务执行时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**end\_time**`string`<br>任务完成时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**video\_url**`string`<br>视频URL。仅在 task\_status 为 SUCCEEDED 时返回。<br>链接有效期24小时，可通过此URL下载视频。视频格式为MP4（H.264 编码）。<br>**orig\_prompt**`string`<br>原始输入的prompt，对应请求参数`prompt`。<br>**actual\_prompt**`string`<br>当 `prompt_extend=true` 时，系统会对输入 prompt 进行智能改写，此字段返回实际用于生成的优化后 prompt。<br>- 若 `prompt_extend=false`，该字段不会返回。<br>  <br>- 注意：wan2.6 模型无论 `prompt_extend` 取值如何，均不返回此字段。<br>  <br>**code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。<br>**message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |
| **usage**`object`<br>输出信息统计，只对成功的结果计数。<br>**属性**<br>**wan2.6系列模型返回参数**<br>**input\_video\_duration**`integer`<br>输入的视频的时长，单位秒。当前不支持传入视频，因此固定为0。<br>**output\_video\_duration**`integer`<br>仅在使用 wan2.6 模型时返回。<br>输出视频的时长，单位秒。其值等同于`input.duration`的值。<br>**duration**`integer`<br>总的视频时长，用于计费。<br>计费公式：`duration=input_video_duration+output_video_duration`。<br>**SR**`integer`<br>仅在使用 wan2.6 模型时返回。生成视频的分辨率档位。示例值：720。<br>**video\_count**`integer`<br>生成视频的数量。固定为1。<br>**audio**`boolean`<br>仅在使用wan2.6-i2v-flash模型时返回。表示输出视频是否为有声视频。<br>**wan2.2和wan2.5系列模型返回参数**<br>**duration**`integer`<br>生成视频的时长，单位为秒。枚举值为5、10。<br>计费公式：费用 = 视频秒数 × 单价。<br>**SR**`integer`<br>生成视频的分辨率。枚举值为480、720、1080。<br>**video\_count**`integer`<br>生成视频的数量。固定为1。<br>**wan2.1系列模型返回参数**<br>**video\_duration**`integer`<br>生成视频的时长，单位为秒。枚举值为3、4、5。<br>计费公式：费用 = 视频秒数 × 单价。<br>**video\_ratio**`string`<br>生成视频的比例。固定为standard。<br>**video\_count**`integer`<br>生成视频的数量。固定为1。 |  |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |  |

## DashScope SDK调用

SDK 的参数命名与 [HTTP接口](https://help.aliyun.com/zh/model-studio/image-to-video-api-reference/#42703589880ts "") 基本一致，参数结构根据语言特性进行封装。

由于图生视频任务耗时较长（通常为1-5分钟），SDK 在底层封装了 HTTP 异步调用流程，支持同步、异步两种调用方式。

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

#### **示例代码**

同步调用

异步调用

同步调用会阻塞等待，直到视频生成完成并返回结果。本示例展示三种图像输入方式：公网URL、Base64编码、本地文件路径。

##### 请求示例

```python
import base64
import os
from http import HTTPStatus
from dashscope import VideoSynthesis
import mimetypes
import dashscope

# 以下为北京地域url，获取url：https://help.aliyun.com/zh/model-studio/image-to-video-api-reference
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
# 获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY")

# --- 辅助函数：用于 Base64 编码 ---
# 格式为 data:{MIME_type};base64,{base64_data}
def encode_file(file_path):
    mime_type, _ = mimetypes.guess_type(file_path)
    if not mime_type or not mime_type.startswith("image/"):
        raise ValueError("不支持或无法识别的图像格式")
    with open(file_path, "rb") as image_file:
        encoded_string = base64.b64encode(image_file.read()).decode('utf-8')
    return f"data:{mime_type};base64,{encoded_string}"

"""
图像输入方式说明：
以下提供了三种图片输入方式，三选一即可

1. 使用公网URL - 适合已有公开可访问的图片
2. 使用本地文件 - 适合本地开发测试
3. 使用Base64编码 - 适合私有图片或需要加密传输的场景
"""

# 【方式一】使用公网可访问的图片URL
# 示例：使用一个公开的图片URL
img_url = "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/wpimhv/rap.png"

# 【方式二】使用本地文件（支持绝对路径和相对路径）
# 格式要求：file:// + 文件路径
# 示例（绝对路径）：
# img_url = "file://" + "/path/to/your/img.png"    # Linux/macOS
# img_url = "file://" + "/C:/path/to/your/img.png"  # Windows
# 示例（相对路径）：
# img_url = "file://" + "./img.png"                # 相对当前执行文件的路径

# 【方式三】使用Base64编码的图片
# img_url = encode_file("./img.png")

# 设置音频audio url
audio_url = "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/ozwpvi/rap.mp3"

def sample_call_i2v():
    # 同步调用，直接返回结果
    print('please wait...')
    rsp = VideoSynthesis.call(api_key=api_key,
                              model='wan2.6-i2v-flash',
                              prompt='一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。',
                              img_url=img_url,
                              audio_url=audio_url,
                              resolution="720P",
                              duration=10,
                              prompt_extend=True,
                              watermark=False,
                              negative_prompt="",
                              seed=12345)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print("video_url:", rsp.output.video_url)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    sample_call_i2v()
```

##### 响应示例

> video\_url 有效期24小时，请及时下载视频。

```json
{
    "status_code": 200,
    "request_id": "2794c7a3-fe8c-4dd4-a1b7-xxxxxx",
    "code": null,
    "message": "",
    "output": {
        "task_id": "c15d5b14-07c4-4af5-b862-xxxxxx",
        "task_status": "SUCCEEDED",
        "video_url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/xxx.mp4?Expires=xxx",
        "submit_time": "2026-01-22 23:24:46.527",
        "scheduled_time": "2026-01-22 23:24:46.565",
        "end_time": "2026-01-22 23:25:59.978",
        "orig_prompt": "一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。"
    },
    "usage": {
        "video_count": 1,
        "video_duration": 0,
        "video_ratio": "",
        "duration": 10,
        "input_video_duration": 0,
        "output_video_duration": 10,
        "audio": true,
        "SR": 720
    }
}
```

本示例展示异步调用方式。该方式会立即返回任务ID，需要自行轮询或等待任务完成。

##### 请求示例

```python
import os
from http import HTTPStatus
from dashscope import VideoSynthesis
import dashscope

# 以下为北京地域url，获取url：https://help.aliyun.com/zh/model-studio/image-to-video-api-reference
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
# 获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY")

# 使用公网可访问的图片URL
img_url = "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/wpimhv/rap.png"

# 设置音频audio url
audio_url = "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/ozwpvi/rap.mp3"

def sample_async_call_i2v():
    # 异步调用，返回一个task_id
    rsp = VideoSynthesis.async_call(api_key=api_key,
                                    model='wan2.6-i2v-flash',
                                    prompt='一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。',
                                    img_url=img_url,
                                    audio_url=audio_url,
                                    resolution="720P",
                                    duration=10,
                                    prompt_extend=True,
                                    watermark=False,
                                    negative_prompt="",
                                    seed=12345)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print("task_id: %s" % rsp.output.task_id)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

    # 获取异步任务信息
    status = VideoSynthesis.fetch(task=rsp, api_key=api_key)
    if status.status_code == HTTPStatus.OK:
        print(status.output.task_status)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (status.status_code, status.code, status.message))

    # 等待异步任务结束
    rsp = VideoSynthesis.wait(task=rsp, api_key=api_key)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output.video_url)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    sample_async_call_i2v()
```

##### 响应示例

1、创建任务的响应示例

```json
{
    "status_code": 200,
    "request_id": "6dc3bf6c-be18-9268-9c27-xxxxxx",
    "code": "",
    "message": "",
    "output": {
        "task_id": "686391d9-7ecf-4290-a8e9-xxxxxx",
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
    "request_id": "2794c7a3-fe8c-4dd4-a1b7-xxxxxx",
    "code": null,
    "message": "",
    "output": {
        "task_id": "c15d5b14-07c4-4af5-b862-xxxxxx",
        "task_status": "SUCCEEDED",
        "video_url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/xxx.mp4?Expires=xxx",
        "submit_time": "2026-01-22 23:24:46.527",
        "scheduled_time": "2026-01-22 23:24:46.565",
        "end_time": "2026-01-22 23:25:59.978",
        "orig_prompt": "一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。"
    },
    "usage": {
        "video_count": 1,
        "video_duration": 0,
        "video_ratio": "",
        "duration": 10,
        "input_video_duration": 0,
        "output_video_duration": 10,
        "audio": true,
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

#### **示例代码**

同步调用

异步调用

同步调用会阻塞等待，直到视频生成完成并返回结果。本示例展示三种图像输入方式：公网URL、Base64编码、本地文件路径。

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

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.Base64;
import java.util.HashMap;
import java.util.Map;

public class Image2Video {

    static {
        // 以下为北京地域url，获取url：https://help.aliyun.com/zh/model-studio/image-to-video-api-reference
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey="sk-xxx"
    // 获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    /**
     * 图像输入方式说明：三选一即可
     *
     * 1. 使用公网URL - 适合已有公开可访问的图片
     * 2. 使用本地文件 - 适合本地开发测试
     * 3. 使用Base64编码 - 适合私有图片或需要加密传输的场景
     */

    //【方式一】公网URL
    static String imgUrl = "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/wpimhv/rap.png";

    //【方式二】本地文件路径（file://+绝对路径）
    // static String imgUrl = "file://" + "/your/path/to/img.png";    // Linux/macOS
    // static String imgUrl = "file://" + "/C:/your/path/to/img.png";  // Windows

    //【方式三】Base64编码
    // static String imgUrl = Image2Video.encodeFile("/your/path/to/img.png");

    // 设置音频audio url
    static String audioUrl = "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/ozwpvi/rap.mp3";

    public static void image2video() throws ApiException, NoApiKeyException, InputRequiredException {
        // 设置parameters参数
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("prompt_extend", true);
        parameters.put("watermark", false);
        parameters.put("seed", 12345);

        VideoSynthesis vs = new VideoSynthesis();
        VideoSynthesisParam param =
                VideoSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.6-i2v-flash")
                        .prompt("一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。")
                        .imgUrl(imgUrl)
                        .audioUrl(audioUrl)
                        .duration(10)
                        .parameters(parameters)
                        .resolution("720P")
                        .negativePrompt("")
                        .build();
        System.out.println("please wait...");
        VideoSynthesisResult result = vs.call(param);
        System.out.println(JsonUtils.toJson(result));
    }

     /**
     * 将文件编码为Base64字符串
     * @param filePath 文件路径
     * @return Base64字符串，格式为 data:{MIME_type};base64,{base64_data}
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
            image2video();
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
    "request_id": "87c091bb-7a3c-4904-8501-xxxxxx",
    "output": {
        "task_id": "413ed6e4-5f3a-4f57-8d58-xxxxxx",
        "task_status": "SUCCEEDED",
        "video_url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/xxx.mp4?Expires=xxx",
        "orig_prompt": "一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。",
        "submit_time": "2026-01-22 23:25:45.729",
        "scheduled_time": "2026-01-22 23:25:45.771",
        "end_time": "2026-01-22 23:26:44.942"
    },
    "usage": {
        "video_count": 1,
        "duration": 10.0,
        "input_video_duration": 0.0,
        "output_video_duration": 10.0,
        "SR": "720"
    },
    "status_code": 200,
    "code": "",
    "message": ""
}
```

本示例展示异步调用方式。该方式会立即返回任务ID，需要自行轮询或等待任务完成。

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

public class Image2Video {

    static {
        // 以下为北京地域url，获取url：https://help.aliyun.com/zh/model-studio/image-to-video-api-reference
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey="sk-xxx"
    // 获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    //设置输入图像url
    static String imgUrl = "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/wpimhv/rap.png";

    // 设置音频audio url
    static String audioUrl = "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250925/ozwpvi/rap.mp3";

    public static void image2video() throws ApiException, NoApiKeyException, InputRequiredException {
        // 设置parameters参数
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("prompt_extend", true);
        parameters.put("watermark", false);
        parameters.put("seed", 12345);

        VideoSynthesis vs = new VideoSynthesis();
        VideoSynthesisParam param =
                VideoSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.6-i2v-flash")
                        .prompt("一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。")
                        .imgUrl(imgUrl)
                        .audioUrl(audioUrl)
                        .duration(10)
                        .parameters(parameters)
                        .resolution("720P")
                        .negativePrompt("")
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
            image2video();
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

##### 响应示例

1、创建任务的响应示例

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
    "request_id": "87c091bb-7a3c-4904-8501-xxxxxx",
    "output": {
        "task_id": "413ed6e4-5f3a-4f57-8d58-xxxxxx",
        "task_status": "SUCCEEDED",
        "video_url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/xxx.mp4?Expires=xxx",
        "orig_prompt": "一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。",
        "submit_time": "2026-01-22 23:25:45.729",
        "scheduled_time": "2026-01-22 23:25:45.771",
        "end_time": "2026-01-22 23:26:44.942"
    },
    "usage": {
        "video_count": 1,
        "duration": 10.0,
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

- **数据时效**：任务task\_id和 视频url均只保留 24 小时，过期后将无法查询或下载。

- **内容审核**：输入的内容（如prompt、图像）、输出视频均会经过内容安全审核，含违规内容将返回 “IPInfringementSuspect”或“DataInspectionFailed”错误，详见参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。

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

#### **Q：如何生成特定宽高比（如3:4）的视频？**

**A：** 输出视频的宽高比由 **输入首帧图像（img\_url）** 决定，但 **无法保证精确比例**（如严格3:4），会存在一定偏差。

**为什么会有偏差：** 模型会以您输入图像的比例为基准，结合设置的分辨率档位（resolution）总像素，自动计算出最接近的合法分辨率。由于要求视频的长和宽必须是 16 的倍数，模型会对最终分辨率做微调，因此无法保证输出比例严格等于 3:4，但会非常接近。

**例如**：输入图像750×1000（宽高比 3:4 = 0.75），并设置 resolution = "720P"（目标总像素约 92 万），实际输出816×1104（宽高比 ≈ 0.739，总像素约90万）。

**实践建议**：

1. **输入控制**：尽量使用与目标比例一致的图片作为首帧输入。

2. **后期处理**：如果您对比例有严格要求，建议在视频生成后，使用编辑工具进行简单的裁剪或黑边填充。