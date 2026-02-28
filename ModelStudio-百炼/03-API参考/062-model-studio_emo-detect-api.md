### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[视频生成](https://help.aliyun.com/zh/model-studio/video-generation-api/)[图生唱演视频-悦动人像EMO](https://help.aliyun.com/zh/model-studio/emo-quick-start/)EMO 图像检测

# EMO图像检测API参考

更新时间：2026-02-11 02:24:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：图生唱演视频-悦动人像EMO](https://help.aliyun.com/zh/model-studio/emo-quick-start/)[下一篇：EMO 视频生成](https://help.aliyun.com/zh/model-studio/emo-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型概览

HTTP调用接口

功能描述

前提条件

输入限制

请求接口

状态码说明

EMO-detect模型，用于确认输入的人物肖像图片是否符合EMO视频生成模型的输入规范。本文档介绍了该模型提供的图像检测能力的API调用方法。

**重要**

本文档仅适用于“中国内地（北京）”地域，且必须使用该地域的 [API Key](https://bailian.console.aliyun.com/?tab=model#/api-key)。

## 模型概览

| **模型名** | **模型简介** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名** | **模型简介** |
| emo-detect-v1 | emo-detect-v1是一个特定的图像检测模型，用于检测输入的图片是否满足emo模型所需的人物肖像图片规范。 |

## HTTP调用接口

### 功能描述

该模型用于检测输入的图片是否满足“ [EMO 视频生成](https://help.aliyun.com/zh/model-studio/emo-api "")”所需的人物肖像图片规范。

### 前提条件

- 已开通服务并获得API-KEY： [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。


### **输入限制**

- 图像格式：格式为jpg，jpeg，png，bmp，webp。

- 图像分辨率：图像最小边长≥400像素，最大边长≤7000像素。

- 上传图片仅支持HTTP链接方式，不支持本地链接方式。


### 请求接口

```http
POST https://dashscope.aliyuncs.com/api/v1/services/aigc/image2video/face-detect
```

#### **入参描述**

| **字段** | **类型** | **传参方式** | **必选** | **描述** | **示例值** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **字段** | **类型** | **传参方式** | **必选** | **描述** | **示例值** |
| Content-Type | String | Header | 是 | 请求类型：application/json。 | application/json |
| Authorization | String | Header | 是 | API-Key，例如：Bearer d1\*\*2a。 | Bearer d1\*\*2a |
| model | String | Body | 是 | 指明需要调用的模型，此处用emo-detect-v1。<br>**说明**<br>若调用独立部署模型，则改为填入 **部署成功的模型名称** | emo-detect-v1 |
| input.image\_url | String | Body | 是 | - 需要检测的图像URL。<br>  <br>- 图像最小边长≥400像素，最大边长≤7000像素。<br>  <br>- 格式支持：jpg、jpeg、png、bmp、webp。<br>  <br>**说明**<br>上传文件支持HTTP或HTTPS链接方式，不支持本地链接方式。您也可在此 [获取临时公网URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。 | http://a/a.jpg |
| parameters.ratio | String | Body | 是 | 希望检测确认的画幅，可选 "1:1"或"3:4"。默认值为"1:1"。<br>- 1:1适用于头像图片。<br>  <br>- 3:4适用于半身像图片。 | "ratio": "1:1" |

#### **出参描述**

| **字段** | **类型** | **描述** | **示例值** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **类型** | **描述** | **示例值** |
| output.check\_pass | Bool | 客户提交的图像列表对应的检查结果。true表示检测通过，false表示检测不通过。 | true |
| output.face\_bbox | Array | - 算法检测到的人脸区域bbox，可将该值作为EMO视频生成API的入参。<br>  <br>- 人脸区域坐标（x1，y1，x2，y2），对应左上和右下两个点的坐标。 | \[10,20,30,40\] |
| output.ext\_bbox | Array | - 算法预测的动态区域bbox，可将该值作为EMO视频生成API的入参。该区域的宽高比与入参画幅一致。<br>  <br>- 动态区域坐标（x1，y1，x2，y2），对应左上和右下两个点的坐标。 | \[10,20,30,40\] |
| usage.image\_count | Integer | 检测的图像张数。用于计费。 | 1 |
| code | String | 请求失败时返回的错误码，详情请参见 [状态码说明](https://help.aliyun.com/zh/model-studio/emo-api#933856b630hez "")。 | InvalidApiKey |
| message | String | 请求失败时返回的详细错误信息，详情请参见 [状态码说明](https://help.aliyun.com/zh/model-studio/emo-api#933856b630hez "")。 | No API-key provided. |
| request\_id | String | 本次请求的系统唯一码。 | 7574ee8f-38a3-4b1e-9280-xxxxx |

#### **请求示例**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/image2video/face-detect' \
--header "Authorization: Bearer $DASHSCOPE_API_KEY" \
--header 'Content-Type: application/json' \
--data-raw '{
  "model": "emo-detect-v1",
  "input": {
      "image_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20251225/onmomb/emo.png"
  },
  "parameters": {
      "ratio": "1:1"
  }
}'
```

#### **响应示例（请求成功）**

图像检测通过

图像检测不通过

```json
{
    "output":{
        "check_pass": true,
        "face_bbox":[302,286,610,593], #人脸bbox
        "ext_bbox":[71,9,840,778] #动态区域bbox
    },
    "usage":{
        "image_count":1
    },
    "request_id":"c56f62df-724e-9c19-96bd-xxxxxx"
}
```

```json
{
    "output":{
      "check_pass": false,
      "code": "",
      "message": ""
    },
    "usage":{
        "image_count":1
    },
    "request_id":"c56f62df-724e-9c19-96bd-xxxxxx"
}
```

#### **响应示例（请求失败）**

```json
{
    "code": "InvalidApiKey",
    "message": "No API-key provided.",
    "request_id": "7438d53d-6eb8-4596-8835-xxxxxx"
}
```

## 状态码说明

大模型服务平台通用状态码请查阅： [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。