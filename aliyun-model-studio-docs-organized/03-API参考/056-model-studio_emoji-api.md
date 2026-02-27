### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/) [API参考（模型）](https://help.aliyun.com/zh/model-studio/model-api-reference/) [视频生成](https://help.aliyun.com/zh/model-studio/video-generation-api/) [图生表情包视频-表情包Emoji](https://help.aliyun.com/zh/model-studio/emoji-quick-start/) Emoji 视频生成

# Emoji 视频生成API参考

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Emoji 图像检测](https://help.aliyun.com/zh/model-studio/emoji-detect-api)[下一篇：视频风格重绘](https://help.aliyun.com/zh/model-studio/video-style-transform-api-reference)

该文章对您有帮助吗？

反馈

表情包emoji-v1模型可基于 **人物肖像图片和预设模板ID**，生成人脸表情包视频。

**重要**

本文档仅适用于“中国大陆（北京）”地域，且必须使用该地域的 [API Key](https://bailian.console.aliyun.com/?tab=model#/api-key)。

## **模型概览**

|     |     |
| --- | --- |
| **模型名称** | **模型简介** |
| emoji-v1 | 输入通过检测的人物肖像图片、对应的人脸区域、动态表情区域坐标以及表情包模板ID，生成人脸表情包视频。 |

## 前提条件

1. 您需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

2. 输入图像已通过 [Emoji 图像检测](https://help.aliyun.com/zh/model-studio/emoji-detect-api "")，并获得对应人脸区域和动态表情区域的坐标作为入参。


## **HTTP调用**

由于视频生成任务耗时较长（通常为1-5分钟），API采用异步调用。整个流程包含 **“创建任务 -\> 轮询获取”** 两个核心步骤，具体如下：

> 模型耗时受限于排队任务数和服务执行情况，请在获取结果时耐心等待。

### 步骤1：创建任务获取任务ID

`POST https://dashscope.aliyuncs.com/api/v1/services/aigc/image2video/video-synthesis`

|     |     |
| --- | --- |
| #### 请求参数 | ## 表情包视频生成<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/image2video/video-synthesis' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--header 'X-DashScope-Async: enable' \<br>--header 'Content-Type: application/json' \<br>--data '{<br>    "model": "emoji-v1",<br>    "input": {<br>        "image_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250912/uopnly/emoji-%E5%9B%BE%E5%83%8F%E6%A3%80%E6%B5%8B.png",<br>        "driven_id": "mengwa_kaixin",<br>        "face_bbox": [212,194,460,441],<br>        "ext_bbox": [63,30,609,575]<br>    }<br>}'<br>``` |
| ##### 请求头（Headers） |
| **Content-Type**`string` **（必选）**<br>请求内容类型。此参数必须设置为`application/json`。 |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| **X-DashScope-Async**`string` **（必选）**<br>异步处理配置参数。HTTP请求只支持异步， **必须设置为**`enable`。<br>**重要** <br>缺少此请求头将报错：“current user api does not support synchronous calls”。 |
| ##### 请求体（Request Body） |
| **model**`string` **（必选）**<br>模型名称。固定为`emoji-v1`。 |
| **input**`object` **（必选）**<br>输入的基本信息，如人脸图像、人脸区域、表情包区域等。<br>**属性**<br>**image\_url**`string` **（必选）**<br>人脸正面肖像图像的公网 URL。支持 HTTP 或 HTTPS 协议。本地文件可通过 [上传文件获取临时URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。 <br>图像限制：<br>- 图像格式：JPEG、JPG、PNG、BMP、WEBP。<br>  <br>- 图像分辨率：图像的宽度和高度均在\[400, 7000\]像素之间。<br>  <br>- 文件大小：不超过10MB。<br>  <br>- 此图像必须通过 [Emoji 图像检测](https://help.aliyun.com/zh/model-studio/emoji-detect-api "")。<br>  <br>示例值：https://help-static-aliyun-doc.aliyuncs.com/xxx.png。<br>**face\_bbox**`array of integer` **（必选）**<br>图片中人脸区域坐标，格式为 \[x1, y1, x2, y2\]，单位为像素，对应左上和右下两个点的坐标。<br>此参数需填入 [Emoji 图像检测](https://help.aliyun.com/zh/model-studio/emoji-detect-api "") 接口响应中的`output.bbox_face` 字段的值。<br>示例值：\[212,194,460,441\]。<br>**ext\_bbox**`array of integer` **（必选）**<br>动态表情区域坐标，该区域的宽高比约为1:1，格式为 \[x1, y1, x2, y2\]，单位为像素，对应左上和右下两个点的坐标。<br>此参数需填入 [Emoji 图像检测](https://help.aliyun.com/zh/model-studio/emoji-detect-api "") 接口响应中的`output.ext_bbox_face`字段的值。<br>示例值：\[63,30,609,575\]。<br>> 说明：动态表情区域指的是模型进行视频生成时实际关注的正方形图像区域，它通常比人脸区域稍大，以包含部分背景和肩膀，确保动画效果自然。<br>**driven\_id**`string` **（必选）**<br>预设模板ID，可选值参见 [表情包模板ID列表](https://help.aliyun.com/zh/model-studio/emoji-api#552aacbdadtaq "")。<br>示例值：mengwa\_kaixin。 |

|     |     |
| --- | --- |
| #### 响应参数 | ### 成功响应<br>请保存 task\_id，用于查询任务状态与结果。<br>```json<br>{<br>    "output": {<br>        "task_status": "PENDING",<br>        "task_id": "0385dc79-5ff8-4d82-bcb6-xxxxxx"<br>    },<br>    "request_id": "4909100c-7b5a-9f92-bfe5-xxxxxx"<br>}<br>```<br>### 异常响应<br>创建任务失败，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "code":"InvalidApiKey",<br>    "message":"Invalid API-key provided.",<br>    "request_id":"fb53c4ec-1c12-4fc4-a580-xxxxxx"<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>属性<br>**task\_id**`string`<br>任务ID。查询有效期24小时。<br>**task\_status**`string`<br>任务状态。<br>**枚举值**<br>- PENDING：任务排队中<br>  <br>- RUNNING：任务处理中<br>  <br>- SUCCEEDED：任务执行成功<br>  <br>- FAILED：任务执行失败<br>  <br>- CANCELED：任务已取消<br>  <br>- UNKNOWN：任务不存在或状态未知 |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |
| **code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |  |
| **message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |  |

### 步骤2：根据任务ID查询结果

`GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id}`

**说明**

- **轮询建议**：视频生成过程约需数分钟，建议采用 **轮询** 机制，并设置合理的查询间隔（如 15 秒）来获取结果。

- **任务状态流转**：PENDING（排队中）→ RUNNING（处理中）→ SUCCEEDED（成功）/ FAILED（失败）。

- **结果链接**：任务成功后返回视频链接，有效期为 **24 小时**。建议在获取链接后立即下载并转存至永久存储（如 [阿里云 OSS](https://help.aliyun.com/zh/oss/user-guide/what-is-oss "")）。

- **task\_id 有效期**： **24小时**，超时后将无法查询结果，接口将返回任务状态为`UNKNOWN`。

- **QPS 限制**：查询接口默认QPS为20。如需更高频查询或事件通知，建议 [配置异步任务回调](https://help.aliyun.com/zh/model-studio/async-task-api "")。

- **更多操作**：如需批量查询、取消任务等操作，请参见 [管理异步任务](https://help.aliyun.com/zh/model-studio/manage-asynchronous-tasks#f26499d72adsl "")。


|     |     |
| --- | --- |
| #### 请求参数 | ## 查询任务结果<br>请将`86ecf553-d340-4e21-xxxxxxxxx`替换为真实的task\_id。<br>```curl<br>curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/86ecf553-d340-4e21-xxxxxxxxx \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY"<br>``` |
| ##### **请求头（Headers）** |
| **Authorization**`string` **（必选）**<br>请求身份认证。接口使用阿里云百炼API-Key进行身份认证。示例值：Bearer sk-xxxx。 |
| ##### **URL路径参数（Path parameters）** |
| **task\_id**`string` **（必选）**<br>任务ID。 |

|     |     |
| --- | --- |
| #### **响应参数** | ## 任务执行成功<br>视频URL仅保留24小时，超时后会被自动清除，请及时保存生成的视频。<br>```json<br>{<br>    "request_id": "ad225054-6c94-47e5-9356-xxxxxxx",<br>    "output": {<br>        "task_id": "b56f509a-3ea9-4cfe-848d-xxxxxxx",<br>        "task_status": "SUCCEEDED",<br>        "submit_time": "2025-10-14 11:28:04.372",<br>        "scheduled_time": "2025-10-14 11:28:04.400",<br>        "end_time": "2025-10-14 11:29:03.924",<br>        "video_url": "http://dashscope-result-sh.oss-cn-shanghai.aliyuncs.com/xx.mp4?Expires=xxx"<br>    },<br>    "usage": {<br>        "video_duration": 2,<br>        "video_ratio": "standard"<br>    }<br>}<br>```<br>## 任务执行失败<br>若任务执行失败，task\_status将置为 FAILED，并提供错误码和信息。请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。<br>```json<br>{<br>    "request_id": "e5d70b02-ebd3-98ce-9fe8-759d7d7b107d",<br>    "output": {<br>        "task_id": "86ecf553-d340-4e21-af6e-a0c6a421c010",<br>        "task_status": "FAILED",<br>        "code": "InvalidParameter",<br>        "message": "The size is not match xxxxxx"<br>    }<br>}<br>```<br>## 任务查询过期<br>task\_id查询有效期为 24 小时，超时后将无法查询，返回以下报错信息。<br>```json<br>{<br>    "request_id": "a4de7c32-7057-9f82-8581-xxxxxx",<br>    "output": {<br>        "task_id": "502a00b1-19d9-4839-a82f-xxxxxx",<br>        "task_status": "UNKNOWN"<br>    }<br>}<br>``` |
| **output**`object`<br>任务输出信息。<br>**属性**<br>**task\_id**`string`<br>任务ID。查询有效期24小时。<br>**task\_status**`string`<br>任务状态。<br>**枚举值**<br>- PENDING：任务排队中<br>  <br>- RUNNING：任务处理中<br>  <br>- SUCCEEDED：任务执行成功<br>  <br>- FAILED：任务执行失败<br>  <br>- CANCELED：任务已取消<br>  <br>- UNKNOWN：任务不存在或状态未知<br>  <br>**轮询过程中的状态流转：**<br>- PENDING（排队中） → RUNNING（处理中）→ SUCCEEDED（成功）/ FAILED（失败）。<br>  <br>- 初次查询状态通常为 PENDING（排队中）或 RUNNING（处理中）。<br>  <br>- 当状态变为 SUCCEEDED 时，响应中将包含生成的视频url。<br>  <br>- 若状态为 FAILED，请检查错误信息并重试。<br>  <br>**submit\_time**`string`<br>任务提交时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**scheduled\_time**`string`<br>任务执行时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**end\_time**`string`<br>任务完成时间。格式为 YYYY-MM-DD HH:mm:ss.SSS。<br>**video\_url**`string`<br>视频URL。仅在 task\_status 为 SUCCEEDED 时返回。<br>链接有效期24小时，可通过此URL下载视频。视频格式为MP4（H.264 编码）。<br>**code**`string`<br>请求失败的错误码。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。<br>**message**`string`<br>请求失败的详细信息。请求成功时不会返回此参数，详情请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。 |
| **usage**`object`<br>输出信息统计，只对成功的结果计数。<br>**属性**<br>**video\_duration**`integer`<br>生成视频的时长，单位为秒。<br>> 计费公式：费用 = 视频秒数 × 单价。<br>**video\_ratio**`string`<br>生成视频的画幅，固定为standard，表示生成1:1画幅的视频。 |  |
| **request\_id**`string`<br>请求唯一标识。可用于请求明细溯源和问题排查。 |  |

## **计费与限流**

- 模型免费额度和计费单价请参见 [模型价格](https://help.aliyun.com/zh/model-studio/models#f62472e1b6m3b "")。

- 模型限流请参见 [限流](https://help.aliyun.com/zh/model-studio/rate-limit "")。


## **错误码**

如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。

## **附录：表情包模板ID列表**

参数设置示例：{ "input": { "driven\_id": "mengwa\_kaixin" } }。

**说明**

- 以下生成效果，由集成了“表情包Emoji”的通义APP生成。

- 表情包Emoji模型生成的内容为人物视频，不包含贴纸和文字。


|     |     |     |     |
| --- | --- | --- | --- |
| **模板 ID (driven\_id)** | **效果示意** | **模板 ID (driven\_id)** | **效果示意** |
| mengwa\_kaixin | ![1_mengwa_kaixin](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3667357371/p906418.gif) | dagong\_zhuakuang | ![10_dagong_zhuakuang](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4667357371/p906428.gif) |
| mengwa\_dengyan | ![7_mengwa_dengyan](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3667357371/p906425.gif) | dagong\_wunai | ![15_dagong_wunai](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4667357371/p906434.gif) |
| mengwa\_gandong | ![16_mengwan_gandong](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3667357371/p906435.gif) | dagong\_weixiao | ![17_dagong_weixiao](<Base64-Image-Removed>) |
| mengwa\_renzhen\_1 | ![18_mengwa_renzhen_1](<Base64-Image-Removed>) | dagong\_ganji | ![20_dagong_ganji](<Base64-Image-Removed>) |
| mengwa\_jidong | ![8_mengwa_jidong](<Base64-Image-Removed>) | jingdian\_tiaopi | ![4_jingdian_tiaopi](<Base64-Image-Removed>) |
| mengwa\_kun\_1 | ![11_mengwa_kun_1](<Base64-Image-Removed>) | jingdian\_deyi\_1 | ![5_jingdian_deyi_1](<Base64-Image-Removed>) |
| mengwa\_jiaoxie | ![19_mengwa_renzhen_1](<Base64-Image-Removed>) | jingdian\_qidai | ![6_jingdian_qidai](<Base64-Image-Removed>) |
| dagong\_kaixin | ![2_dagong_kaixin](<Base64-Image-Removed>) | jingdian\_landuo\_1 | ![12_jingdian_landuo_1](<Base64-Image-Removed>) |
| dagong\_yangwang | ![3_dagong_yangwang](<Base64-Image-Removed>) | jingdian\_xianqi | ![13_jingdian_xianqi](<Base64-Image-Removed>) |
| dagong\_kunhuo | ![9_dagong_kunhuo](<Base64-Image-Removed>) | jingdian\_lei | ![14_jingdian_lei](<Base64-Image-Removed>) |