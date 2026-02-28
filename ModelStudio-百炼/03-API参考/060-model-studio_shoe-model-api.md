### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[图像生成](https://help.aliyun.com/zh/model-studio/image-generation/)鞋靴模特

# 鞋靴模特API参考

更新时间：2026-02-11 02:22:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：虚拟模特](https://help.aliyun.com/zh/model-studio/virtual-model-api-details)[下一篇：创意海报生成](https://help.aliyun.com/zh/model-studio/creative-poster-generation-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型概览

前提条件

HTTP调用

步骤1：创建任务获取任务ID

步骤2：根据任务ID查询结果

错误码

本文介绍鞋靴模特模型的输入输出参数。鞋靴模特模型支持输入多视角鞋靴系列图片，同时对输入模特模板图的鞋子区域进行鞋靴AI试穿，实现模特鞋靴布局重绘生成，最终生成图片的效果布局自然、细节丰富、画面细腻、试穿结果逼真。可用于模特商品图设计、新鞋AI试穿、模特穿戴布局重绘等场景。

**相关指南**： [鞋靴模特](https://help.aliyun.com/zh/model-studio/shoes-and-boots-model "")

**重要**

- 本文档仅适用于“中国内地（北京）”地域，且必须使用该地域的 [API Key](https://bailian.console.aliyun.com/?tab=model#/api-key)。

- shoemodel-v1 模型当前仅提供 **免费体验**，免费额度用完后不可调用且不支持付费。


## **模型概览**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型名** | **免费额度** [（查看）](https://help.aliyun.com/zh/model-studio/new-free-quota "") | **计费单价** | **限流（含主账号与RAM子账号）** |
| **任务下发接口QPS限制** | **同时处理中任务数量** |
| shoemodel-v1 | 500张 | 目前仅供免费体验。<br>> 免费额度用完后不可调用，敬请关注后续动态。 | 2 | 1 |

## **前提条件**

您需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

## HTTP调用

为了减少等待时间并且避免请求超时，服务采用异步方式提供。您需要发起两个请求：

- **创建任务**：首先发送一个请求创建鞋靴模特任务，该请求会返回任务ID。

- **根据任务ID查询结果**：使用上一步获得的任务ID，查询模型生成的结果。


### **步骤1：创建任务获取任务ID**

`POST https://dashscope.aliyuncs.com/api/v1/services/aigc/virtualmodel/generation/`

|     |     |
| --- | --- |
| #### **请求头（Headers）** | 鞋靴模特试穿<br>```curl<br>curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/virtualmodel/generation/' \<br>--header 'X-DashScope-Async: enable' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>--header 'Content-Type: application/json' \<br>--data '{<br>    "model": "shoemodel-v1",<br>    "input": {<br>        "template_image_url": "http://xxx/1.jpg",<br>        "shoe_image_url": ["http://xxx/2.jpg"]<br>    },<br>    "parameters": <br>    {<br>        "n": 1<br>    }<br>}'<br>``` |
| **Authorization** _string_ **必选**<br>推荐您使用阿里云百炼API-Key，也可填DashScope API-Key。例如：Bearer d1xxx2a。 |
| **X-DashScope-Async** _string_ **必选**<br>是否使用DashScope异步调用。HTTP只支持异步调用，设置为`enable`。 |
| **Content-Type** _string_ **必选**<br>请求内容类型。固定为`application/json`。 |
| #### **请求体（Request Body）** |
| **model** _string_ **必选**<br>调用模型。鞋靴模特生成模型为`shoemodel-v1`。 |
| **parameters** Integer **必选**<br>图片生成的数量，目前支持 1~4 张，默认值 1。 |
| **input** _object_ **必选**<br>输入图像的基本信息，比如图像URL地址。<br>**属性**<br>**template\_image\_url** _string_ **必选**<br>模板模特图片的URL地址。<br>URL 需为公网可访问的地址，并支持 HTTP 或 HTTPS 协议。您也可在此 [获取临时公网URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。 <br>图像限制：<br>- 图片大小建议小于5M。<br>  <br>- 图像格式：jpg、png、jpeg、bmp、webp、avif。<br>  <br>- 图像比例：图长边与短边的比例需在`[2:3, 3:2]` 范围内，推荐比例为`4:3`。<br>  <br>**shoe\_image\_url** _list_ **必选**<br>鞋靴多视角图片URL地址。<br>URL 需为公网可访问的地址，并支持 HTTP 或 HTTPS 协议。您也可在此 [获取临时公网URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。 <br>- 图片大小建议小于5M。<br>  <br>- 图像格式：jpg、png、jpeg、bmp、webp、avif。<br>  <br>- 图像比例：图长边与短边的比例需在`[2:3, 3:2]` 范围内，推荐与模特模板一样，比例为`4:3`。<br>  <br>- 多视角图片张数小于3。<br>  <br>**scale** _float_ 可选<br>控制生成强度。<br>范围在\[2.0,8.0\]，默认为5.0，数值越大，颜色越鲜亮。 |

|     |     |
| --- | --- |
| #### **响应** | 正常响应<br>异常响应<br>```json<br>{<br>    "output": {<br>	"task_id": "d76ec1e8-ea27-4038-8913-xxxxxxxxxxxx", <br>        "task_status": "PENDING"<br>    }<br>    "request_id": "7574ee8f-38a3-4b1e-9280-11c33ab46e51"<br>}<br>```<br>```json<br>{<br>    "code":"InvalidApiKey",<br>    "message":"Invalid API-key provided.",<br>    "request_id":"fb53c4ec-1c12-4fc4-a580-cdb7c3261fc1"<br>}<br>``` |
| **output** _object_<br>任务输出信息。<br>**属性**<br>**task\_id** _string_<br>任务id。<br>**task\_status** _string_<br>任务状态。<br>- PENDING：排队中<br>  <br>- RUNNING：处理中<br>  <br>- SUSPENDED：挂起<br>  <br>- SUCCEEDED：执行成功<br>  <br>- FAILED：执行失败 |
| **code** _string_<br>任务执行失败的错误码。 |
| **message** _string_<br>任务执行失败的详细信息。 |
| **request\_id** _string_<br>请求唯一标识。可用于请求明细溯源和问题排查。 |

### **步骤2：根据任务ID查询结果**

`GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id}`

|     |     |
| --- | --- |
| #### **请求头（Headers）** | 获取任务结果<br>```curl<br>curl --location --request GET 'https://dashscope.aliyuncs.com/api/v1/tasks/{task_id}' \<br>--header "Authorization: Bearer $DASHSCOPE_API_KEY"<br>``` |
| **Authorization** _string_ **必选**<br>推荐使用阿里云百炼API-Key，也可填DashScope API-Key。例如：Bearer d1xxx2a。 |
| #### **URL路径参数（Path parameters）** |
| **task\_id** _string_ **必选**<br>任务id。 |

|     |     |
| --- | --- |
| #### **响应** | 任务执行成功<br>任务执行中<br>任务执行失败<br>```json<br>{<br>    "request_id":"<your request id>",<br>    "output":{<br>        "task_id":"<your task id>",<br>        "task_status":"SUCCEEDED",<br>        "submit_time":"2024-05-16 13:50:xx.xxx",<br>        "scheduled_time":"2024-05-16 13:50:xx.xxx",<br>        "end_time":"2024-05-16 13:50:xx.xxx",<br>        "error_message":"Success",<br>        "start_time":"2024-05-16 13:50:xx.xxx",<br>        "model_index":0,<br>        "error_code":0,<br>        "result_url":"http://oss.aliyuncs.com/xxx/abc.jpg"<br>    },<br>    "usage":{<br>        "image_count":1<br>    }<br>}<br>```<br>```json<br>{<br>    "request_id":"e5d70b02-ebd3-98ce-9fe8-759d7d7b107d",<br>    "output":{<br>        "task_id":"86ecf553-d340-4e21-af6e-a0c6a421c010",<br>        "task_status":"RUNNING",<br>        "task_metrics":{<br>            "TOTAL":1,<br>            "SUCCEEDED":1,<br>            "FAILED":0<br>        }<br>    }<br>}<br>```<br>```json<br>{<br>  "request_id": "<your request id>",<br>  "output": {<br>    "task_id": "<your task id>",<br>    "task_status": "FAILED",<br>    "submit_time": "2024-05-16 13:50:xx.xxx",<br>    "scheduled_time": "2024-05-16 13:50:xx.xxx",<br>    "end_time": "2024-05-16 13:50:xx.xxx",<br>    "code": "InvalidImageResolution",<br>    "message": "The input image resolution is too large or small"<br>  },<br>  "usage": {<br>    "image_num": 0<br>  }<br>}<br>``` |
| **output** _object_<br>任务输出信息。<br>**属性**<br>**task\_id** _string_<br>任务id。<br>**task\_status** _string_<br>任务状态。<br>- PENDING：排队中<br>  <br>- RUNNING：处理中<br>  <br>- SUSPENDED：挂起<br>  <br>- SUCCEEDED：执行成功<br>  <br>- FAILED：执行失败<br>  <br>**task\_metrics** _object_<br>任务信息统计指标。 <br>**属性**<br>**TOTAL** _integer_<br>总的任务数。<br>**SUCCEEDED** _integer_<br>任务状态为成功的任务数。<br>**FAILED** _integer_<br>任务状态为失败的任务数。<br>**submit\_time** _string_<br>任务提交时间。<br>**scheduled\_time** _string_<br>任务排期执行时间。<br>**end\_time** _string_<br>任务完成时间。<br>**result\_url** _string_<br>输出图片url。<br>**code** _string_<br>任务执行失败的错误码。<br>**message** _string_<br>任务执行失败的详细信息。 |
| **request\_id** _string_<br>请求唯一标识。可用于请求明细溯源和问题排查。 |
|  |

## **错误码**

如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。

此API还有特定状态码，具体如下所示。

| **HTTP状态码** | **接口错误码（code）** | **接口错误信息（message）** | **含义说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **HTTP状态码** | **接口错误码（code）** | **接口错误信息（message）** | **含义说明** |
| 400 | InvalidParameter | Required parameter(s) missing or invalid, please check the request parameters.（可根据实际情况修改） | 接口调用参数不合法 |
| 400 | InvalidFile.Content | The input image has no human body or has unclear human body. Please upload other image. | 输入图片中人体不完整或者没有人体 |
| 400 | InvalidParameter | The request is missing required parameters or in a wrong format, please check the parameters that you send. | 入参格式不对 |
| 400 | InvalidURL | The request URL is invalid, please check the request URL is available and the request image format is one of the following types: JPEG, JPG, PNG, BMP, and WEBP. | 输入图片下载失败，请检查网络或者输入格式 |
| 400 | InvalidFile.Resolution | The image resolution is invalid, please make sure that the aspect ratio is smaller than 3:2, and largest length of image is smaller than 4096. | 上传图片大小不符合要求 |
| 500 | InternalError.Algo | An internal error occurs during computation, please try this model later. | 算法运行错误 |