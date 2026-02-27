### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[图像生成](https://help.aliyun.com/zh/model-studio/image-editing-and-generation/)[图像编辑](https://help.aliyun.com/zh/model-studio/image-edit-guide/)图像编辑-万相2.5

# 图像编辑-万相2.5

更新时间：2026-02-11 01:58:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：图像编辑-千问](https://help.aliyun.com/zh/model-studio/qwen-image-edit-guide)[下一篇：图像编辑-万相2.1](https://help.aliyun.com/zh/model-studio/wanx-image-edit)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速开始

支持的模型

输入说明

输入图像（images）

可选参数

输出说明

效果展示

多图融合

图像理解

主体特征保持

修改及放大

提取元素

线稿生图

文字生成

去水印

扩图

计费与限流

API参考

常见问题

万相-图像编辑模型（wan2.5）支持多图输入（1-3张）和多图输出（1-4张），通过 **文本指令** 实现主体一致的单图编辑、目标检测与分割以及多图融合等能力。

## **快速开始**

#### **前提条件**

在调用前，先 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，再 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。如需通过SDK进行调用，请 [安装DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

#### **示例代码**

单图输入与多图输入的调用方式基本一致。

本示例以 **多图融合** 为例：在`images`数组中传入2张图像，模型将根据文本提示词输出 1 张融合后的图像。

> 输入提示词：将图1中的闹钟放置到图2的餐桌的花瓶旁边位置。

| **输入图像1** | **输入图像2** | **输出图像** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **输入图像1** | **输入图像2** | **输出图像** |
| ![p1011667 (2)](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9654793671/p1029056.webp) | ![p1011669 (2)](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9654793671/p1029057.webp) | ![p1028883](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1028892.webp) |

同步调用

异步调用

**重要**

**请确保 DashScope Python SDK 版本不低于**`1.25.2` **， DashScope Java SDK 版本不低于**`2.22.2` **。**

若版本过低，可能会触发 “url error, please check url!” 等错误。请参考 [安装或升级SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

Python

Java

本示例支持三种图像输入方式： **公网URL、Base64编码、本地文件路径**。

##### **请求示例**

```python
import base64
import mimetypes
from http import HTTPStatus
from urllib.parse import urlparse, unquote
from pathlib import PurePosixPath
import dashscope
import requests
from dashscope import ImageSynthesis
import os

# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
# 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY")

# --- 输入图片：使用 Base64 编码 ---
# base64编码格式为 data:{MIME_type};base64,{base64_data}
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

# 【方式一】使用公网图片 URL
image_url_1 = "https://img.alicdn.com/imgextra/i3/O1CN0157XGE51l6iL9441yX_!!6000000004770-49-tps-1104-1472.webp"
image_url_2 = "https://img.alicdn.com/imgextra/i3/O1CN01SfG4J41UYn9WNt4X1_!!6000000002530-49-tps-1696-960.webp"

# 【方式二】使用本地文件（支持绝对路径和相对路径）
# 格式要求：file:// + 文件路径
# 示例（绝对路径）：
# image_url_1 = "file://" + "/path/to/your/image_1.png"     # Linux/macOS
# image_url_2 = "file://" + "C:/path/to/your/image_2.png"  # Windows
# 示例（相对路径）：
# image_url_1 = "file://" + "./image_1.png"                 # 以实际路径为准
# image_url_2 = "file://" + "./image_1.png"                # 以实际路径为准

# 【方式三】使用Base64编码的图片
# image_url_1 = encode_file("./image_1.png")               # 以实际路径为准
# image_url_2 = encode_file("./image_2.png")              # 以实际路径为准

print('----sync call, please wait a moment----')
rsp = ImageSynthesis.call(api_key=api_key,
                          model="wan2.5-i2i-preview",
                          prompt="将图1中的闹钟放置到图2的餐桌的花瓶旁边位置",
                          images=[image_url_1, image_url_2],
                          negative_prompt="",
                          n=1,
                          # size="1280*1280",
                          prompt_extend=True,
                          watermark=False,
                          seed=12345)
print('response: %s' % rsp)
if rsp.status_code == HTTPStatus.OK:
    # 在当前目录下保存图片
    for result in rsp.output.results:
        file_name = PurePosixPath(unquote(urlparse(result.url).path)).parts[-1]
        with open('./%s' % file_name, 'wb+') as f:
            f.write(requests.get(result.url).content)
else:
    print('sync_call Failed, status_code: %s, code: %s, message: %s' %
          (rsp.status_code, rsp.code, rsp.message))
```

##### **响应示例**

> url 有效期24小时，请及时下载图像。

```json
{
    "status_code": 200,
    "request_id": "8ad45834-4321-44ed-adf5-xxxxxx",
    "code": null,
    "message": "",
    "output": {
        "task_id": "3aff9ebd-35fc-4339-98a3-xxxxxx",
        "task_status": "SUCCEEDED",
        "results": [\
            {\
                "url": "https://dashscope-result-sh.oss-cn-shanghai.aliyuncs.com/xxx.png?Expires=xxx",\
                "orig_prompt": "将图1中的闹钟放置到图2的餐桌的花瓶旁边位置",\
                "actual_prompt": "将图1中的蓝色闹钟放置在图2餐桌的花瓶右侧，靠近桌布边缘的位置，保持闹钟朝向镜头，与桌面平行，阴影自然投射于桌面。"\
            }\
        ],
        "submit_time": "2025-10-23 16:18:16.009",
        "scheduled_time": "2025-10-23 16:18:16.040",
        "end_time": "2025-10-23 16:19:09.591",
        "task_metrics": {
            "TOTAL": 1,
            "FAILED": 0,
            "SUCCEEDED": 1
        }
    },
    "usage": {
        "image_count": 1
    }
}
```

本示例支持三种图像输入方式：公网URL、Base64编码、本地文件路径。

##### **请求示例**

```java
// Copyright (c) Alibaba, Inc. and its affiliates.
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesis;
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesisParam;
import com.alibaba.dashscope.utils.Constants;
import com.alibaba.dashscope.utils.JsonUtils;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.*;

public class Image2Image {

    static {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey="sk-xxx"
    // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    /**
     * 图像输入方式说明：三选一即可
     *
     * 1. 使用公网URL - 适合已有公开可访问的图片
     * 2. 使用本地文件 - 适合本地开发测试
     * 3. 使用Base64编码 - 适合私有图片或需要加密传输的场景
     */

    //【方式一】公网URL
    static String imageUrl_1 = "https://img.alicdn.com/imgextra/i3/O1CN0157XGE51l6iL9441yX_!!6000000004770-49-tps-1104-1472.webp";
    static String imageUrl_2 = "https://img.alicdn.com/imgextra/i3/O1CN01SfG4J41UYn9WNt4X1_!!6000000002530-49-tps-1696-960.webp";

    //【方式二】本地文件路径（file://+绝对路径 or file:///+绝对路径）
    // static String imageUrl_1 = "file://" + "/your/path/to/image_1.png";    // Linux/macOS
    // static String imageUrl_2 = "file:///" + "C:/your/path/to/image_2.png";  // Windows

    //【方式三】Base64编码
    // static String imageUrl_1 = encodeFile("/your/path/to/image_1.png");
    // static String imageUrl_2 = encodeFile("/your/path/to/image_2.png");

    // 设置待编辑的图片列表
    static List<String> imageUrls = new ArrayList<>();
    static {
        imageUrls.add(imageUrl_1);
        imageUrls.add(imageUrl_2);
    }

    public static void syncCall() {
        // 设置parameters参数
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("prompt_extend", true);
        parameters.put("watermark", false);
        parameters.put("seed", "12345");

        ImageSynthesisParam param =
                ImageSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.5-i2i-preview")
                        .prompt("将图1中的闹钟放置到图2的餐桌的花瓶旁边位置")
                        .images(imageUrls)
                        .n(1)
                         //.size("1280*1280")
                        .negativePrompt("")
                        .parameters(parameters)
                        .build();

        ImageSynthesis imageSynthesis = new ImageSynthesis();
        ImageSynthesisResult result = null;
        try {
            System.out.println("---sync call, please wait a moment----");
            result = imageSynthesis.call(param);
        } catch (ApiException | NoApiKeyException e){
            throw new RuntimeException(e.getMessage());
        }
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
        syncCall();
    }
}
```

##### 响应示例

> url 有效期24小时，请及时下载图像。

```prolog
{
    "request_id": "d362685b-757f-4eac-bab5-xxxxxx",
    "output": {
        "task_id": "bfa7fc39-3d87-4fa7-b1e6-xxxxxx",
        "task_status": "SUCCEEDED",
        "results": [\
            {\
                "orig_prompt": "将图1中的闹钟放置到图2的餐桌的花瓶旁边位置",\
                "actual_prompt": "将图1中的蓝色闹钟放置在图2餐桌的花瓶右侧，靠近桌布边缘的位置，保持闹钟正面朝向镜头，与花瓶平行摆放。",\
                "url": "https://dashscope-result-sh.oss-cn-shanghai.aliyuncs.com/xxx.png?Expires=xxx"\
            }\
        ],
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

**重要**

**请确保 DashScope Python SDK 版本不低于**`1.25.2` **， DashScope Java SDK 版本不低于**`2.22.2` **。**

若版本过低，可能会触发 “url error, please check url!” 等错误。请参考 [安装或升级SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

Python

Java

curl

本示例使用公网URL方式传入图片。

### 请求示例

```python
import os
from http import HTTPStatus
from urllib.parse import urlparse, unquote
from pathlib import PurePosixPath
import dashscope
import requests
from dashscope import ImageSynthesis

# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
# 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY")

# 使用公网图片 URL
image_url_1 = "https://img.alicdn.com/imgextra/i3/O1CN0157XGE51l6iL9441yX_!!6000000004770-49-tps-1104-1472.webp"
image_url_2 = "https://img.alicdn.com/imgextra/i3/O1CN01SfG4J41UYn9WNt4X1_!!6000000002530-49-tps-1696-960.webp"

def async_call():
    print('----create task----')
    task_info = create_async_task()
    print('----wait task----')
    wait_async_task(task_info)

# 创建异步任务
def create_async_task():
    rsp = ImageSynthesis.async_call(api_key=api_key,
                                    model="wan2.5-i2i-preview",
                                    prompt="将图1中的闹钟放置到图2的餐桌的花瓶旁边位置",
                                    images=[image_url_1, image_url_2],
                                    negative_prompt="",
                                    n=1,
                                    # size="1280*1280",
                                    prompt_extend=True,
                                    watermark=False,
                                    seed=12345)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))
    return rsp

# 等待异步任务结束
def wait_async_task(task):
    rsp = ImageSynthesis.wait(task=task, api_key=api_key)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output)
        # save file to current directory
        for result in rsp.output.results:
            file_name = PurePosixPath(unquote(urlparse(result.url).path)).parts[-1]
            with open('./%s' % file_name, 'wb+') as f:
                f.write(requests.get(result.url).content)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

# 获取异步任务信息
def fetch_task_status(task):
    status = ImageSynthesis.fetch(task=task, api_key=api_key)
    print(status)
    if status.status_code == HTTPStatus.OK:
        print(status.output.task_status)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (status.status_code, status.code, status.message))

# 取消异步任务，只有处于PENDING状态的任务才可以取消
def cancel_task(task):
    rsp = ImageSynthesis.cancel(task=task, api_key=api_key)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output.task_status)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    async_call()
```

### 响应示例

1、创建任务的响应示例

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

2、查询任务结果的响应示例

> url 有效期24小时，请及时下载图像。

```json
{
    "status_code": 200,
    "request_id": "8ad45834-4321-44ed-adf5-xxxxxx",
    "code": null,
    "message": "",
    "output": {
        "task_id": "3aff9ebd-35fc-4339-98a3-xxxxxx",
        "task_status": "SUCCEEDED",
        "results": [\
            {\
                "url": "https://dashscope-result-sh.oss-cn-shanghai.aliyuncs.com/xxx.png?Expires=xxx",\
                "orig_prompt": "将图1中的闹钟放置到图2的餐桌的花瓶旁边位置",\
                "actual_prompt": "将图1中的蓝色闹钟放置在图2餐桌的花瓶右侧，靠近桌布边缘的位置，保持闹钟朝向镜头，与桌面平行，阴影自然投射于桌面。"\
            }\
        ],
        "submit_time": "2025-10-23 16:18:16.009",
        "scheduled_time": "2025-10-23 16:18:16.040",
        "end_time": "2025-10-23 16:19:09.591",
        "task_metrics": {
            "TOTAL": 1,
            "FAILED": 0,
            "SUCCEEDED": 1
        }
    },
    "usage": {
        "image_count": 1
    }
}
```

本示例默认使用公网URL方式传入图片。

### 请求示例

```java
// Copyright (c) Alibaba, Inc. and its affiliates.

import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesis;
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesisListResult;
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesisParam;
import com.alibaba.dashscope.aigc.imagesynthesis.ImageSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.task.AsyncTaskListParam;
import com.alibaba.dashscope.utils.Constants;
import com.alibaba.dashscope.utils.JsonUtils;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Image2Image {
    static {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey="sk-xxx"
    // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    //公网URL
    static String imageUrl_1 = "https://img.alicdn.com/imgextra/i3/O1CN0157XGE51l6iL9441yX_!!6000000004770-49-tps-1104-1472.webp";
    static String imageUrl_2 = "https://img.alicdn.com/imgextra/i3/O1CN01SfG4J41UYn9WNt4X1_!!6000000002530-49-tps-1696-960.webp";

    // 设置待编辑的图片列表
    static List<String> imageUrls = new ArrayList<>();
    static {
        imageUrls.add(imageUrl_1);
        imageUrls.add(imageUrl_2);
    }

    public static void asyncCall() {
        // 设置parameters参数
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("prompt_extend", true);
        parameters.put("watermark", false);
        parameters.put("seed", "12345");

        ImageSynthesisParam param =
                ImageSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.5-i2i-preview")
                        .prompt("将图1中的闹钟放置到图2的餐桌的花瓶旁边位置")
                        .images(imageUrls)
                        .n(1)
                        //.size("1280*1280")
                        .negativePrompt("")
                        .parameters(parameters)
                        .build();
        ImageSynthesis imageSynthesis = new ImageSynthesis();
        ImageSynthesisResult result = null;
        try {
            System.out.println("---async call, please wait a moment----");
            result = imageSynthesis.asyncCall(param);
        } catch (ApiException | NoApiKeyException e){
            throw new RuntimeException(e.getMessage());
        }

        System.out.println(JsonUtils.toJson(result));

        String taskId = result.getOutput().getTaskId();

        System.out.println("taskId=" + taskId);

        try {
            result = imageSynthesis.wait(taskId, apiKey);
        } catch (ApiException | NoApiKeyException e){
            throw new RuntimeException(e.getMessage());
        }
        System.out.println(JsonUtils.toJson(result));
        System.out.println(JsonUtils.toJson(result.getOutput()));
    }

    public static void listTask() throws ApiException, NoApiKeyException {
        ImageSynthesis is = new ImageSynthesis();
        AsyncTaskListParam param = AsyncTaskListParam.builder().build();
        param.setApiKey(apiKey);
        ImageSynthesisListResult result = is.list(param);
        System.out.println(result);
    }

    public void fetchTask(String taskId) throws ApiException, NoApiKeyException {
        ImageSynthesis is = new ImageSynthesis();
        // 如果已设置 DASHSCOPE_API_KEY 为环境变量，apiKey 可为空。
        ImageSynthesisResult result = is.fetch(taskId, apiKey);
        System.out.println(result.getOutput());
        System.out.println(result.getUsage());
    }

    public static void main(String[] args) {
        asyncCall();
    }
}
```

### 响应示例

1、创建任务的响应示例

```json
{
	"request_id": "5dbf9dc5-4f4c-9605-85ea-542f97709ba8",
	"output": {
		"task_id": "7277e20e-aa01-4709-xxxxxxxx",
		"task_status": "PENDING"
	}
}
```

2、查询任务结果的响应示例

> url 有效期24小时，请及时下载图片。

```prolog
{
    "request_id": "d362685b-757f-4eac-bab5-xxxxxx",
    "output": {
        "task_id": "bfa7fc39-3d87-4fa7-b1e6-xxxxxx",
        "task_status": "SUCCEEDED",
        "results": [\
            {\
                "orig_prompt": "将图1中的闹钟放置到图2的餐桌的花瓶旁边位置",\
                "actual_prompt": "将图1中的蓝色闹钟放置在图2餐桌的花瓶右侧，靠近桌布边缘的位置，保持闹钟正面朝向镜头，与花瓶平行摆放。",\
                "url": "https://dashscope-result-sh.oss-cn-shanghai.aliyuncs.com/xxx.png?Expires=xxx"\
            }\
        ],
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

本示例包含创建任务和查询结果两个步骤。

**说明**

- 异步调用必须设置 Header 参数`X-DashScope-Async` 为`enable`。

- 异步任务的 `task_id` 查询有效期为 24 小时，过期后任务状态将变为 `UNKNOWN`。

- 新手建议使用 [Postman](https://help.aliyun.com/zh/model-studio/first-call-to-image-and-video-api "") 调用API。


#### **步骤1：发起创建任务请求**

该请求会返回一个任务ID（`task_id`）。

##### **请求示例**

```ada
 curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/image2image/image-synthesis' \
    -H 'X-DashScope-Async: enable' \
    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
    -H 'Content-Type: application/json' \
    -d '{
    "model": "wan2.5-i2i-preview",
    "input": {
        "prompt": "将图1中的闹钟放置到图2的餐桌的花瓶旁边位置",
        "images": [\
            "https://img.alicdn.com/imgextra/i3/O1CN0157XGE51l6iL9441yX_!!6000000004770-49-tps-1104-1472.webp",\
            "https://img.alicdn.com/imgextra/i3/O1CN01SfG4J41UYn9WNt4X1_!!6000000002530-49-tps-1696-960.webp"\
        ]
    },
    "parameters": {
        "n": 1
    }
}'
```

**响应示例**

```json
{
    "output": {
        "task_status": "PENDING",
        "task_id": "0385dc79-5ff8-4d82-bcb6-xxxxxx"
    },
    "request_id": "4909100c-7b5a-9f92-bfe5-xxxxxx"
}
```

#### **步骤2：根据任务ID查询结果**

使用上一步获取的 `task_id`，通过接口轮询任务状态，直到 `task_status` 变为 SUCCEEDED 或 FAILED。

**请求示例**

请将`86ecf553-d340-4e21-xxxxxxxxx`替换为真实的task\_id。

> 若使用新加坡地域的模型，需将base\_url替换为https://dashscope-intl.aliyuncs.com/api/v1/tasks/86ecf553-d340-4e21-xxxxxxxxx

```curl
curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/86ecf553-d340-4e21-xxxxxxxxx \
--header "Authorization: Bearer $DASHSCOPE_API_KEY"
```

**响应示例**

> 图像URL有效期为24小时，请及时下载图像。

```json
{
    "request_id": "d1f2a1be-9c58-48af-b43f-xxxxxx",
    "output": {
        "task_id": "7f4836cd-1c47-41b3-b3a4-xxxxxx",
        "task_status": "SUCCEEDED",
        "submit_time": "2025-09-23 22:14:10.800",
        "scheduled_time": "2025-09-23 22:14:10.825",
        "end_time": "2025-09-23 22:15:23.456",
        "results": [\
            {\
                "orig_prompt": "将图1中的闹钟放置到图2的餐桌的花瓶旁边位置",\
                "url": "https://dashscope-result-sh.oss-cn-shanghai.aliyuncs.com/xxx.png?Expires=xxx"\
            }\
        ],
        "task_metrics": {
            "TOTAL": 1,
            "FAILED": 0,
            "SUCCEEDED": 1
        }
    },
    "usage": {
        "image_count": 1
    }
}
```

## **支持的模型**

模型列表和价格请参见[万相通用图像编辑2.5](https://help.aliyun.com/zh/model-studio/models#4219acf25en2i "")。

## **输入说明**

### **输入图像（images）**

`images`是一个数组，支持传入 **1～3 张** 图片进行编辑或融合。输入图片必须满足以下要求：

- **图片格式：** 支持 JPEG、JPG、PNG （不支持透明通道）、BMP、WEBP。

- **图片分辨率：** 图像的宽高范围均为\[384, 5000\]像素。

- **文件大小：** 单张图片文件大小不得超过 10MB。


```json
// 以下示例仅展示 images 字段结构，输入包含 2 张图像
{
    "images": [\
        "https://img.alicdn.com/imgextra/i4/O1CN01TlDlJe1LR9zso3xAC_!!6000000001295-2-tps-1104-1472.png",\
        "https://img.alicdn.com/imgextra/i4/O1CN01M9azZ41YdblclkU6Z_!!6000000003082-2-tps-1696-960.png"\
    ]
}
```

#### **图像输入顺序**

多图输入时，按照数组顺序定义图像顺序。因此，提示词引用的图像编号需要 **与图像数组中的顺序一一对应**，例如：数组中的第一张图片为“图1”，第二张为“图2”，或者使用标记形式如“\[图1\]”、“\[图2\]”。

| **输入图像** | **输出图像** |
| --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **输入图像** | **输出图像** |
| ![image (19)-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1025838.webp)<br>图1 | ![image (20)-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1025839.webp)<br>图2 | ![04e0fc39-7ad6-41e0-9df9-1f69ac3ce825-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021092.webp)<br>提示词：把图1移动到图2上 | ![36ed450d-bd54-4169-b13f-3d0f26d9d360-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021093.webp)<br>提示词：把图2移动到图1上 |

#### **图像传入方式**

本模型支持通过以下三种方式传入图像：

**方式一：公网URL**

- 提供一个公网可访问的图像地址，支持 HTTP 或 HTTPS 协议。

- 示例值：`https://xxxx/img.png`。

- 适用场景：图片已托管在对象存储（如OSS）或公开图床上。


**方式二：Base64编码**

将图像文件转换为 Base64 编码字符串，并按格式拼接：`data:{MIME_type};base64,{base64_data}`。

- 示例值：`data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABDg......` **（** 因长度限制仅展示片段 **）。** 调用时，需传入完整字符串。

- {base64\_data}：表示图像文件经过 Base64 编码后的字符串。

- {MIME\_type}：表示图像的媒体类型，需与文件格式对应。


|     |     |
| --- | --- |
| **图像格式** | **MIME Type** |
| JPEG | image/jpeg |
| JPG | image/jpeg |
| PNG | image/png |
| BMP | image/bmp |
| WEBP | image/webp |

- 适合场景：私有图片或需要加密传输的场景。


**代码示例：图像Base64编码**

```python
import os
import base64
import mimetypes

# 格式为 data:{mime_type};base64,{base64_data}
def encode_file(file_path):
    mime_type, _ = mimetypes.guess_type(file_path)
    with open(file_path, "rb") as image_file:
        encoded_string = base64.b64encode(image_file.read()).decode('utf-8')
    return f"data:{mime_type};base64,{encoded_string}"


# 调用编码函数，请将 "/path/to/your/image.png" 替换为您的本地图片文件路径，否则无法运行
image = encode_file("/path/to/your/image.png")
```

**方式三：本地文件路径（仅限SDK）**

- **Python SDK**：支持传入文件的 **绝对路径和相对路径**。文件路径规则如下：


|     |     |     |     |
| --- | --- | --- | --- |
| **系统** | **传入的文件路径** | **示例（绝对路径）** | **示例（相对路径）** |
| Linux或macOS系统 | file://{文件的绝对路径或相对路径} | file:///home/images/test.png | file://./images/test.png |
| Windows系统 | file://D:/images/test.png | file://./images/test.png |

- **Java SDK**：仅支持传入文件的 **绝对路径**。文件路径规则如下：


|     |     |     |
| --- | --- | --- |
| **系统** | **传入的文件路径** | **示例（绝对路径）** |
| Linux或macOS系统 | file://{文件的绝对路径} | file:///home/images/test.png |
| Windows系统 | file:///{文件的绝对路径} | file:///D:/images/test.png |

- 适用场景：适合在本地开发环境中快速测试。


### **可选参数**

本模型还提供一些 **可选参数** 用于调整图像生成效果。其中重要参数包括：

- `size`：设置输出图像的分辨率，格式为`宽*高`，单位为像素。默认值为 `1280*1280`。图像分辨率总像素在 \[768\*768, 1280\*1280\] 之间，且宽高比范围为 \[1:4, 4:1\]。



**推荐分辨率及对应宽高比**






  - 1280\*1280：1:1

  - 1024\*1024：1:1

  - 800\*1200：2:3

  - 1200\*800：3:2

  - 960\*1280：3:4

  - 1280\*960：4:3

  - 720\*1280：9:16

  - 1280\*720：16:9

  - 1344\*576：21:9


若未指定 `size`，系统将默认生成 1280\*1280 像素的图像，并近似保持输入图像的宽高比：

  - 单图输入：宽高比与输入图像一致；

  - 多图输入：宽高比与最后一张输入图像一致。
- `n`：设置输出图像的数量。取值范围为1~4张，默认为`4`。测试阶段建议设置为1。

- `negative_prompt`：反向提示词，描述不希望在画面中出现的内容，如“模糊”、“多余的手指”等。仅用于辅助优化生成质量。

- `watermark`：是否添加水印标识，水印位于图片右下角，文案固定为“AI生成”。默认为 `false`，表示不添加水印。

- `seed`：随机数种子。取值范围是`[0, 2147483647]`。如果不提供，则算法自动生成一个随机数作为种子。如果希望生成内容保持相对稳定，可使用相同的seed参数值。


> 注意：由于模型生成具有概率性，相同 seed也不能保证每次生成结果完全一致。


## **输出说明**

- **图片格式**：PNG。

- **图像张数**：1～4张。

- **图像分辨率**：可通过输入参数`size` 指定分辨率；若未指定，请参见 [size参数说明](https://help.aliyun.com/zh/model-studio/wan-image-edit-2-5#9bb5c9b761sfw "")。


> 所有输出图像将采用相同的分辨率。


## **效果展示**

> 图像编辑wan2.5模型暂不支持组图生成。

### **多图融合**

| **输入图像** | **输出图像** |
| --- | --- |

|     |     |
| --- | --- |
| **输入图像** | **输出图像** |
| ![p1020900-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1020979.webp) | ![p1020802-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1020982.webp)<br>把图2的星空画作迁移到图1的手机壳上 |
| ![p1020907-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1020983.webp) | ![p1020740-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1020984.webp)<br>以\[图1\]的字体文字造型“Wan2.5”为唯一依据，保持笔画粗细与曲线不变；将\[图2\]的层叠纸材质精准迁移到文字。 |
| ![p1020909-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1020985.webp) | ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1020755.png)<br>使用两张参考图进行定向重绘：以\[图2\]为包包的造型与结构参考，以\[图1\]中的鹦鹉羽毛为颜色与纹理参考，将鹦鹉羽毛的色彩与纹理质感精准迁移到\[图2\]的包面材质上。 |
| ![p1020912-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1020987.webp) | ![p1020772-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1020988.webp)<br>融合\[图1\]\[图2\]制作太空主题海报：让\[图2\]的玩偶漂浮宇宙中，双手捧起悬浮的\[图1\]logo；logo为发光立体紫色透明材质，具折射与体积光，光晕映照玩偶与周围微尘。背景深空星云与星尘轨迹，右上加入远景环形空间站与灯带细节，主体居中突出、留白均衡。标题置顶“万相发布”：几何无衬线超黑体、字距略宽、纯白主色+紫蓝外发光+细银描边；副标题其下“Unleash Your Creativity”：轻细无衬线、浅紫至青蓝渐变、微内阴影与柔光。整体紫蓝调，高分辨率，不加其他文字。 |
| ![p1020911-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1020989.webp) | ![p1020881-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1020992.webp)<br>以\[图1\]名片设计稿的构图与磨砂玻璃质感为模板，为\[图2\]人物生成竖版工作卡。圆角半透明卡面，柔和高光与浅投影；人物胸像置于中上区域；左下排版姓名/职位/公司/电话，极简无衬线字体，留白均衡。右上角放置\[图1\]人物的可爱3D卡通形象，打破边界半浮出卡片并投下轻影，形成层次与视觉焦点。整体明亮自然光、真实材质细节，不添加多余图案与元素。 |

### **图像理解**

##### **目标检测与定位**

> 检测图像中指定的目标，输出一张带有检测框和标签的图像。

| **输入图像** | **输出图像** |
| --- | --- |

|     |     |
| --- | --- |
| **输入图像** | **输出图像** |
| ![p1020870-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1021007.webp) | ![p1020739-转换自-png (1)](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021008.webp)<br>检测图中的向日葵和南瓜，绘制检测框并标上标签 |

##### **实例分割**

> 模型将为图像中每个独立对象生成一个专属颜色区域，展示其完整轮廓。例如，输出图像的紫色区域代表被分割出的耳机实例。

| **输入图像** | **输出图像** |
| --- | --- |

|     |     |
| --- | --- |
| **输入图像** | **输出图像** |
| ![p1020871-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021003.webp) | ![p1020872-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021006.webp)<br>分割出图中的耳机 |

### **主体特征保持**

| **输入图像** | **输出图像** |
| --- | --- |

|     |     |
| --- | --- |
| **输入图像** | **输出图像** |
| ![p1020767-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1020996.webp) | ![p1020768-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1020997.webp)<br>Generate a highly detailed photo of a girl cosplaying this illustration, at Comiket. It must be a real person cosplaying. Exactly replicate the same pose, body posture, hand gestures, facial expression, and camera framing as in the original illustration. Keep the same angle, perspective, and composition, without any deviation. |
| ![p1020761-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1020998.webp) | ![p1020759-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1020999.webp)<br>在办公室场景中生成3个同样的该照片中的人物，其中一个坐在办公桌前办公，另一个站着在喝咖啡，第三个靠在办公桌前在看书，这3个人是同一个人，都是照片中的那个人物。 |
| ![p1020799-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1021000.webp) | ![p1020756-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1021001.webp)<br>为这张照片生成一个4宫格套图，第一张让这个女孩身体正面面向镜头，第二张让她举起右手撩头发，第三组让她向屏幕前的观众热情地挥手打招呼，第四张她的表情要闭上眼微笑 |

### **修改及放大**

| **功能** | **输入图像** | **输出图像** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **功能** | **输入图像** | **输出图像** |
| 修改元素 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9654793671/p1029064.png) | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9654793671/p1029065.png)<br>将花卉连衣裙换成一件复古风格的蕾丝长裙，领口和袖口有精致的刺绣细节。 |
| 修改光线 | ![p1020752-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021020.webp) | ![p1020753-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021021.webp)<br>在海星表面添加小而闪烁的高光，使其在夕阳背景下呈现出发光的效果。 |
| 放大主体元素 | ![p1020744-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021009.webp) | ![p1020742-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021010.webp)<br>把图中的牛放大 |
| 放大图像细节 | ![image (18)-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1025831.webp) | ![5eecdaf48460cde5c4be102460b058055561df7a15a7389475b8339e1c4c24831b75b38faadcd24bec177c308ebd5304b8b330b51f13ddb214325c71432889afadec7664fb1a132d34d1f46a5de9c95c9f982413966336104fb4c8ed7016461c-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1025836.webp)<br>放大并展现鹦鹉栖息的树枝 |

### **提取元素**

| **输入图像** | **输出图像** |
| --- | --- |

|     |     |
| --- | --- |
| **输入图像** | **输出图像** |
| ![20251029170404](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1020700.jpg) | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1020703.png)<br>将图中人物身穿的服饰单品都提取出来，摆放在白底背景中，整齐地排列。 |

### **线稿生图**

| **输入图像** | **输出图像** |
| --- | --- |

|     |     |
| --- | --- |
| **输入图像** | **输出图像** |
| ![p1020874-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1021016.webp) | ![p1020875-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021017.webp)<br>Generate a new real image based on this sketch, a charming Mediterranean village scene with rustic stone buildings featuring terracotta roofs, wooden shutters, and balconies adorned with hanging laundry. The foreground is filled with lush greenery, including climbing vines and blooming flowers, creating a vibrant and lively atmosphere. The architecture showcases intricate details like arched doorways and patterned stonework, evoking a sense of history and warmth\], \[a bright, sunny day with clear blue skies, casting soft shadows across the cobblestone streets and enhancing the warm tones of the buildings. In the background, rolling hills and distant mountains provide a picturesque setting, adding depth and serenity to the scene. |\
\
### **文字生成**\
\
| **输入图像** | **输出图像** |\
| --- | --- |\
\
|     |     |\
| --- | --- |\
| **输入图像** | **输出图像** |\
| ![p1020745-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1021013.webp) | ![p1020738-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1021014.webp)<br>在图片的左上角添加大号圆角字体的白色标题文字：“微距摄影”，标题文字下面有淡绿色小号副标题：“勤劳就有收获”。 |\
\
### **去水印**\
\
| **输入图像** | **输出图像** |\
| --- | --- |\
\
|     |     |\
| --- | --- |\
| **输入图像** | **输出图像** |\
| ![p1020805-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1021011.webp) | ![p1020743-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1021012.webp)<br>去除左上角所有文字 |\
\
### **扩图**\
\
| **输入图像** | **输出图像** |\
| --- | --- |\
\
|     |     |\
| --- | --- |\
| **输入图像** | **输出图像** |\
| ![image (18)-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7142593671/p1025831.webp) | ![5eecdaf48460cde5c4be102460b058055561df7a15a7389475b8339e1c4c24831b75b38faadcd24bec177c308ebd53049e07d7fc490946139fdff014838b673b9dff828674c79200daa0c9c7ebedc8db2df6ace13bf592fa4fb4c8ed7016461c-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8142593671/p1025832.webp)<br>向外扩图，生成这张图的远景照片 |\
\
## **计费与限流**\
\
- 模型免费额度和计费单价请参见 [模型列表与价格](https://help.aliyun.com/zh/model-studio/models#4219acf25en2i "")。\
\
- 模型限流请参见 [通义万相](https://help.aliyun.com/zh/model-studio/rate-limit#513e0a3df24v7 "")。\
\
- 计费说明：\
\
  - 按成功生成的 **图像张数** 计费。仅当接口返回`task_status`为`SUCCEEDED` 并成功生成图像后，才会计费。\
\
  - 模型调用失败或处理错误不产生任何费用，也不消耗 [免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "")。\
\
## **API参考**\
\
输入和输出参数请参见 [万相-通用图像编辑2.5 API参考](https://help.aliyun.com/zh/model-studio/wan2-5-image-edit-api-reference "")。\
\
## **常见问题**\
\
##### **Q：之前使用通用图像编辑 2.1，现在切换到 wan2.5 模型，SDK调用方式需要调整吗？**\
\
A：需要调整。两个版本的参数设计不同：\
\
- [通用图像编辑2.1](https://help.aliyun.com/zh/model-studio/wanx-image-edit-api-reference "")：需同时传入`prompt`和`function`参数。\
\
- [通用图像编辑2.5](https://help.aliyun.com/zh/model-studio/wan2-5-image-edit-api-reference "")： **仅需** 传入`prompt`，所有编辑操作通过文本指令描述， **不再支持也不需要**`function`参数。