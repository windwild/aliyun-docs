### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[模型推理](https://help.aliyun.com/zh/model-studio/model-inference/)[视频生成](https://help.aliyun.com/zh/model-studio/video-editing-and-generation/)文生视频

# 文生视频

更新时间：2026-02-12 02:59:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：视频生成](https://help.aliyun.com/zh/model-studio/use-video-generation)[下一篇：图生视频-基于首帧](https://help.aliyun.com/zh/model-studio/image-to-video-guide)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速开始

适用范围

核心能力

制作多镜头视频

实现声画同步

生成无声视频

如何传入音频

输出视频

计费与限流

API文档

常见问题

万相-文生视频模型支持 **多模态输入**（文本/图像/音频），可生成最长15秒、分辨率为1080P的视频。

- **基础能力**：支持整数级视频时长（2～15 秒）、指定视频分辨率（480P/720P/1080P）、智能改写prompt、添加水印。

- **音频能力**：支持自动配音，或传入自定义音频文件，实现声画同步。 **（wan2.5、wan2.6支持）**

- **多镜头叙事**：支持生成包含多个镜头的视频，在镜头切换的同时保持主体一致。 **（仅wan2.6支持）**


**快速入口：** 在线体验（ [北京](https://bailian.console.aliyun.com/cn-beijing?tab=model#/efm/model_experience_center/vision?currentTab=videoGenerate) ｜ [新加坡](https://modelstudio.console.aliyun.com/ap-southeast-1?tab=dashboard#/efm/model_experience_center/vision?currentTab=videoGenerate) ｜ [弗吉尼亚](https://modelstudio.console.aliyun.com/us-east-1?tab=dashboard#/efm/model_experience_center/vision?currentTab=videoGenerate)） **｜** [API参考](https://help.aliyun.com/zh/model-studio/text-to-video-api-reference "") **｜** [Prompt指南](https://help.aliyun.com/zh/model-studio/text-to-video-prompt "")

## **快速开始**

|     |     |
| --- | --- |
| **输入提示词** | **输出视频（多镜头，有声视频）** |
| 一段紧张刺激的侦探追查故事，展现电影级叙事能力。第1个镜头\[0-3秒\] 全景：雨夜的纽约街头，霓虹灯闪烁，一位身穿黑色风衣的侦探快步行走。 第2个镜头\[3-6秒\] 中景：侦探进入一栋老旧建筑，雨水打湿了他的外套，门在他身后缓缓关闭。 第3个镜头\[6-9秒\] 特写：侦探的眼神坚毅专注，远处传来警笛声，他微微皱眉思考。 第4个镜头\[9-12秒\] 中景：侦探在昏暗走廊中小心前行，手电筒照亮前方。 第5个镜头\[12-15秒\] 特写：侦探发现关键线索，脸上露出恍然大悟的表情。 |  |

在调用前，先 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，再 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。通过SDK进行调用，请 [安装DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

Python SDK

Java SDK

curl

**重要**

请确保 DashScope Python SDK 版本 **不低于**`1.25.8`，再运行以下代码。

若版本过低，可能会触发 “url error, please check url!” 等错误。请参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

```python
import os
from http import HTTPStatus
from dashscope import VideoSynthesis
import dashscope

# 以下为北京地域URL，各地域的URL不同，获取URL：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY", "YOUR_API_KEY")

print('please wait...')
rsp = VideoSynthesis.call(api_key=api_key,
                          model='wan2.6-t2v',
                          prompt='一段紧张刺激的侦探追查故事，展现电影级叙事能力。第1个镜头[0-3秒] 全景：雨夜的纽约街头，霓虹灯闪烁，一位身穿黑色风衣的侦探快步行走。 第2个镜头[3-6秒] 中景：侦探进入一栋老旧建筑，雨水打湿了他的外套，门在他身后缓缓关闭。 第3个镜头[6-9秒] 特写：侦探的眼神坚毅专注，远处传来警笛声，他微微皱眉思考。 第4个镜头[9-12秒] 中景：侦探在昏暗走廊中小心前行，手电筒照亮前方。 第5个镜头[12-15秒] 特写：侦探发现关键线索，脸上露出恍然大悟的表情。',
                          size="1280*720",
                          duration=15,
                          shot_type="multi",
                          prompt_extend=True,
                          watermark=True)
print(rsp)
if rsp.status_code == HTTPStatus.OK:
    print("video_url:", rsp.output.video_url)
else:
    print('Failed, status_code: %s, code: %s, message: %s' % (rsp.status_code, rsp.code, rsp.message))
```

**重要**

请确保 DashScope Java SDK 版本 **不低于**`2.22.6`，再运行以下代码。

若版本过低，可能会触发 “url error, please check url!” 等错误。请参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

```java
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesis;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisParam;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.JsonUtils;
import com.alibaba.dashscope.utils.Constants;

public class Text2Video {

    static {
        // 以下为北京地域url，各地域的URL不同，获取URL：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey="sk-xxx"
    // 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    public static void text2video() throws ApiException, NoApiKeyException, InputRequiredException {
        VideoSynthesis vs = new VideoSynthesis();
        VideoSynthesisParam param =
                VideoSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.6-t2v")
                        .prompt("一段紧张刺激的侦探追查故事，展现电影级叙事能力。第1个镜头[0-3秒] 全景：雨夜的纽约街头，霓虹灯闪烁，一位身穿黑色风衣的侦探快步行走。 第2个镜头[3-6秒] 中景：侦探进入一栋老旧建筑，雨水打湿了他的外套，门在他身后缓缓关闭。 第3个镜头[6-9秒] 特写：侦探的眼神坚毅专注，远处传来警笛声，他微微皱眉思考。 第4个镜头[9-12秒] 中景：侦探在昏暗走廊中小心前行，手电筒照亮前方。 第5个镜头[12-15秒] 特写：侦探发现关键线索，脸上露出恍然大悟的表情。")
                        .duration(15)
                        .size("1280*720")
                        .shotType("multi")
                        .promptExtend(true)
                        .watermark(true)
                        .build();
        System.out.println("please wait...");
        VideoSynthesisResult result = vs.call(param);
        System.out.println(JsonUtils.toJson(result));
    }

    public static void main(String[] args) {
        try {
            text2video();
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

**步骤1：创建任务获取任务ID**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \
    -H 'X-DashScope-Async: enable' \
    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
    -H 'Content-Type: application/json' \
    -d '{
    "model": "wan2.6-t2v",
    "input": {
        "prompt": "一段紧张刺激的侦探追查故事，展现电影级叙事能力。第1个镜头[0-3秒] 全景：雨夜的纽约街头，霓虹灯闪烁，一位身穿黑色风衣的侦探快步行走。 第2个镜头[3-6秒] 中景：侦探进入一栋老旧建筑，雨水打湿了他的外套，门在他身后缓缓关闭。 第3个镜头[6-9秒] 特写：侦探的眼神坚毅专注，远处传来警笛声，他微微皱眉思考。 第4个镜头[9-12秒] 中景：侦探在昏暗走廊中小心前行，手电筒照亮前方。 第5个镜头[12-15秒] 特写：侦探发现关键线索，脸上露出恍然大悟的表情。"
    },
    "parameters": {
        "size": "1280*720",
        "prompt_extend": true,
        "watermark": true,
        "duration": 15,
        "shot_type":"multi"
    }
}'
```

**步骤2：根据任务ID获取结果**

将`{task_id}`完整替换为上一步接口返回的`task_id`的值。

```curl
curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id} \
--header "Authorization: Bearer $DASHSCOPE_API_KEY"
```

**输出示例**

> `video_url` 有效期24小时，请及时下载视频。

```json
{
    "request_id": "c1209113-8437-424f-a386-xxxxxx",
    "output": {
        "task_id": "966cebcd-dedc-4962-af88-xxxxxx",
        "task_status": "SUCCEEDED",
        "video_url": "https://dashscope-result-sh.oss-accelerate.aliyuncs.com/xxx.mp4?Expires=xxx",
         ...
    },
    ...
}
```

## **适用范围**

各地域支持的模型有所差异，且资源相互独立。调用时，确保 **模型、Endpoint URL 和 API Key 均属于同一地域**，跨地域调用将会失败。

**支持的模型**：

中国内地

全球

国际

美国

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-t2v `推荐` | 有声视频<br>多镜头叙事、声画同步 | 文本、音频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 15s\]（整数）<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.5-t2v-preview `推荐` | 有声视频<br>声画同步 | 文本、音频 | 分辨率档位：480P、720P、1080P<br>视频时长：5s、10s <br>固定规格：30fps、MP4 (H.264编码) |
| wan2.2-t2v-plus | 无声视频<br>> 较2.1模型稳定性与成功率全面提升 | 文本 | 分辨率档位：480P、1080P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wanx2.1-t2v-turbo | 无声视频 | 文本 | 分辨率档位：480P、720P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wanx2.1-t2v-plus | 无声视频 | 文本 | 分辨率档位：720P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-t2v `推荐` | 有声视频<br>多镜头叙事、声画同步 | 文本、音频 | 分辨率档位：720P、1080P<br>视频时长：5s、10s 、15s<br>固定规格：30fps、MP4 (H.264编码) |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-t2v `推荐` | 有声视频<br>多镜头叙事、声画同步 | 文本、音频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 15s\]（整数）<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.5-t2v-preview `推荐` | 有声视频<br>声画同步 | 文本、音频 | 分辨率档位：480P、720P、1080P<br>视频时长：5s、10s <br>固定规格：30fps、MP4 (H.264编码) |
| wan2.2-t2v-plus | 无声视频<br>> 较2.1模型稳定性与成功率全面提升 | 文本 | 分辨率档位：480P、1080P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.1-t2v-turbo | 无声视频 | 文本 | 分辨率档位：480P、720P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.1-t2v-plus | 无声视频 | 文本 | 分辨率档位：720P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |

在 [美国部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源仅限于美国境内。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-t2v-us `推荐` | 有声视频<br>多镜头叙事、声画同步 | 文本、音频 | 分辨率档位：720P、1080P<br>视频时长：5s、10s 、15s<br>固定规格：30fps、MP4 (H.264编码) |

**说明**

本文的示例代码适用于 **北京地域**。

## **核心能力**

### **制作多镜头视频**

**支持模型**：`wan2.6系列模型`。

**功能介绍**：模型可自动进行分镜切换，例如从全景切换到特写，适合制作MV等场景。

**参数设置**：

- `shot_type`: 必须设为 `"multi"`。

- `prompt_extend`: 必须设为 `true`（开启智能改写以优化分镜描述）。


|     |     |
| --- | --- |
| **输入提示词** | **输出视频（多镜头视频）** |
| 展现未来科技与自然和谐共存的美好愿景。 第1个镜头\[0-2秒\] 未来城市的空中花园全景，悬浮植物在微风中摇曳。 第2个镜头\[2-4秒\] 机器人园丁正在精心修剪植物，动作精准而优雅。 第3个镜头\[4-7秒\] 阳光透过透明穹顶洒下，照亮整个花园，展现科技与自然的完美融合。 第4个镜头\[7-10秒\] 镜头拉远，展现整个未来城市的壮观景象，空中花园只是其中的一部分。 |  |

Python SDK

Java SDK

curl

> 请确保 DashScope Python SDK 版本不低于 `1.25.8`，可参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

```python
import os
from http import HTTPStatus
from dashscope import VideoSynthesis
import dashscope

# 以下为北京地域URL，各地域的URL不同，获取URL：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY")

def sample_async_call_t2v():
    # 异步调用，返回一个task_id
    rsp = VideoSynthesis.async_call(api_key=api_key,
                                    model='wan2.6-t2v',
                                    prompt='展现未来科技与自然和谐共存的美好愿景。 第1个镜头[0-2秒] 未来城市的空中花园全景，悬浮植物在微风中摇曳。 第2个镜头[2-4秒] 机器人园丁正在精心修剪植物，动作精准而优雅。 第3个镜头[4-7秒] 阳光透过透明穹顶洒下，照亮整个花园，展现科技与自然的完美融合。 第4个镜头[7-10秒] 镜头拉远，展现整个未来城市的壮观景象，空中花园只是其中的一部分。',
                                    size='1280*720',
                                    shot_type="multi",  # 多镜头
                                    duration=10,
                                    prompt_extend=True,
                                    watermark=True,
                                    negative_prompt="",
                                    seed=12345)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print("task_id: %s" % rsp.output.task_id)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' % (rsp.status_code, rsp.code, rsp.message))

    # 等待异步任务结束
    rsp = VideoSynthesis.wait(task=rsp, api_key=api_key)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output.video_url)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' % (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    sample_async_call_t2v()
```

> 请确保 DashScope Java SDK 版本不低于 `2.22.6`，可参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

```java
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesis;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisParam;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.JsonUtils;
import com.alibaba.dashscope.utils.Constants;

public class Text2Video {
    static {
        // 以下为北京地域url，各地域的url不同，获取url：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey="sk-xxx"
    // 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    public static void text2Video() throws ApiException, NoApiKeyException, InputRequiredException {
        VideoSynthesis vs = new VideoSynthesis();
        VideoSynthesisParam param =
                VideoSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.6-t2v")
                        .prompt("展现未来科技与自然和谐共存的美好愿景。 第1个镜头[0-2秒] 未来城市的空中花园全景，悬浮植物在微风中摇曳。 第2个镜头[2-4秒] 机器人园丁正在精心修剪植物，动作精准而优雅。 第3个镜头[4-7秒] 阳光透过透明穹顶洒下，照亮整个花园，展现科技与自然的完美融合。 第4个镜头[7-10秒] 镜头拉远，展现整个未来城市的壮观景象，空中花园只是其中的一部分。")
                        .negativePrompt("")
                        .size("1280*720")
                        .shotType("multi")
                        .duration(10)
                        .promptExtend(true)
                        .watermark(true)
                        .seed(12345)
                        .build();
        // 异步调用
        VideoSynthesisResult task = vs.asyncCall(param);
        System.out.println(JsonUtils.toJson(task));
        System.out.println("please wait...");

        //获取结果
        VideoSynthesisResult result = vs.wait(task, apiKey);
        System.out.println(JsonUtils.toJson(result));
    }

    public static void main(String[] args) {
        try {
            text2video();
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

**步骤1：创建任务获取任务ID**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \
    -H 'X-DashScope-Async: enable' \
    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
    -H 'Content-Type: application/json' \
    -d '{
    "model": "wan2.6-t2v",
    "input": {
        "prompt": "展现未来科技与自然和谐共存的美好愿景。 第1个镜头[0-2秒] 未来城市的空中花园全景，悬浮植物在微风中摇曳。 第2个镜头[2-4秒] 机器人园丁正在精心修剪植物，动作精准而优雅。 第3个镜头[4-7秒] 阳光透过透明穹顶洒下，照亮整个花园，展现科技与自然的完美融合。 第4个镜头[7-10秒] 镜头拉远，展现整个未来城市的壮观景象，空中花园只是其中的一部分。"
    },
    "parameters": {
        "size": "1280*720",
        "watermark": true,
        "prompt_extend": true,
        "duration": 10,
        "shot_type":"multi"
    }
}'
```

**步骤2：根据任务ID获取结果**

将`{task_id}`完整替换为上一步接口返回的`task_id`的值。

```curl
curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id} \
--header "Authorization: Bearer $DASHSCOPE_API_KEY"
```

### **实现声画同步**

**支持模型**：`wan2.5和wan2.6系列模型`。

**功能介绍**：让照片中的人物“开口说话”或唱歌，嘴型与音频匹配。更多示例请参见 [视频声音生成](https://help.aliyun.com/zh/model-studio/text-to-video-prompt#df26af6f91bkq "")。

**参数设置：**

- **传入音频文件**：传入 `audio_url`。模型会根据音频文件对齐口型。

- **自动配音**：默认输出有声视频，无需传入 `audio_url`。模型会根据画面自动生成背景音效、音乐或人声。


|     |     |
| --- | --- |
| **输入示例** | **输出视频（有声视频）** |
| **输入提示词**：一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说： **“青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还”**。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。<br>**输入音频**： |  |

Python SDK

Java SDK

curl

> 请确保 DashScope Python SDK 版本不低于 `1.25.8`，可参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

```python
import os
from http import HTTPStatus
from dashscope import VideoSynthesis
import dashscope

# 以下为北京地域URL，各地域的URL不同，获取URL：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY")

def sample_async_call_t2v():
    # 异步调用，返回一个task_id
    rsp = VideoSynthesis.async_call(api_key=api_key,
                                    model='wan2.6-t2v',
                                    prompt='一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。',
                                    audio_url='https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/hbiayh/%E4%BB%8E%E5%86%9B%E8%A1%8C.mp3',
                                    size='1280*720',
                                    duration=10,
                                    shot_type="multi",  # 多镜头
                                    prompt_extend=True,
                                    watermark=True,
                                    negative_prompt="",
                                    seed=12345)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print("task_id: %s" % rsp.output.task_id)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' % (rsp.status_code, rsp.code, rsp.message))

    # 等待异步任务结束
    rsp = VideoSynthesis.wait(task=rsp, api_key=api_key)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output.video_url)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' % (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    sample_async_call_t2v()
```

> 请确保 DashScope Java SDK 版本不低于 `2.22.6`，可参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

```java
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesis;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisParam;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.JsonUtils;
import com.alibaba.dashscope.utils.Constants;

public class Text2Video {
    static {
        // 以下为北京地域url，各地域的url不同，获取url：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey="sk-xxx"
    // 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    public static void text2Video() throws ApiException, NoApiKeyException, InputRequiredException {
        VideoSynthesis vs = new VideoSynthesis();
        VideoSynthesisParam param =
                VideoSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.6-t2v")
                        .prompt("一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。")
                        .audioUrl("https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/hbiayh/%E4%BB%8E%E5%86%9B%E8%A1%8C.mp3")
                        .negativePrompt("")
                        .size("1280*720")
                        .shotType("multi")
                        .duration(10)
                        .promptExtend(true)
                        .watermark(true)
                        .seed(12345)
                        .build();
        // 异步调用
        VideoSynthesisResult task = vs.asyncCall(param);
        System.out.println(JsonUtils.toJson(task));
        System.out.println("please wait...");

        //获取结果
        VideoSynthesisResult result = vs.wait(task, apiKey);
        System.out.println(JsonUtils.toJson(result));
    }

    public static void main(String[] args) {
        try {
            text2video();
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

**步骤1：创建任务获取任务ID**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \
    -H 'X-DashScope-Async: enable' \
    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
    -H 'Content-Type: application/json' \
    -d '{
    "model": "wan2.6-t2v",
    "input": {
        "prompt": "一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说：”青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还。“。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。",
        "audio_url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/hbiayh/%E4%BB%8E%E5%86%9B%E8%A1%8C.mp3"
    },
    "parameters": {
        "size": "1280*720",
        "watermark": true,
        "prompt_extend": true,
        "duration": 10,
        "shot_type":"multi"
    }
}'
```

**步骤2：根据任务ID获取结果**

将`{task_id}`完整替换为上一步接口返回的`task_id`的值。

```curl
curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id} \
--header "Authorization: Bearer $DASHSCOPE_API_KEY"
```

### **生成无声视频**

**支持模型**：`wan2.2系列模型`、`wanx2.1系列模型`。

**功能介绍**：适用于无需音频的纯视觉展示场景，如动态海报、无声短视频等。

**参数设置**：wan2.2及以下版本模型，默认生成无声视频，无需额外配置。

|     |     |
| --- | --- |
| **输入提示词** | **输出视频（无声视频）** |
| 低对比度，在一个复古的70年代风格地铁站里，街头音乐家在昏暗的色彩和粗糙的质感中演奏。他穿着旧式夹克，手持吉他，专注地弹奏。通勤者匆匆走过，一小群人渐渐聚拢聆听。镜头慢慢向右移动，捕捉到乐器声与城市喧嚣交织的场景，背景中有老式的地铁标志和斑驳的墙面。 |  |

Python SDK

Java SDK

curl

> 请确保 DashScope Python SDK 版本不低于 `1.25.8`，可参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

```python
import os
from http import HTTPStatus
from dashscope import VideoSynthesis
import dashscope

# 以下为北京地域URL，各地域的URL不同，获取URL：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
api_key = os.getenv("DASHSCOPE_API_KEY")

def sample_async_call_t2v():
    # 异步调用，返回一个task_id
    rsp = VideoSynthesis.async_call(api_key=api_key,
                                    model='wan2.2-t2v-plus',
                                    prompt='低对比度，在一个复古的70年代风格地铁站里，街头音乐家在昏暗的色彩和粗糙的质感中演奏。他穿着旧式夹克，手持吉他，专注地弹奏。通勤者匆匆走过，一小群人渐渐聚拢聆听。镜头慢慢向右移动，捕捉到乐器声与城市喧嚣交织的场景，背景中有老式的地铁标志和斑驳的墙面。',
                                    prompt_extend=True,
                                    size='832*480',
                                    negative_prompt="",
                                    watermark=True,
                                    seed=12345)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print("task_id: %s" % rsp.output.task_id)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' % (rsp.status_code, rsp.code, rsp.message))

    # 等待异步任务结束
    rsp = VideoSynthesis.wait(task=rsp, api_key=api_key)
    print(rsp)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output.video_url)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' % (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    sample_async_call_t2v()
```

> 请确保 DashScope Java SDK 版本不低于 `2.22.6`，可参考 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

```java
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesis;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisParam;
import com.alibaba.dashscope.aigc.videosynthesis.VideoSynthesisResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.JsonUtils;
import com.alibaba.dashscope.utils.Constants;

public class Text2Video {
    static {
        // 以下为北京地域url，各地域的url不同，获取url：https://help.aliyun.com/zh/model-studio/text-to-video-api-reference
        Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
    }

    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey="sk-xxx"
    // 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    static String apiKey = System.getenv("DASHSCOPE_API_KEY");

    public static void text2video() throws ApiException, NoApiKeyException, InputRequiredException {
        VideoSynthesis vs = new VideoSynthesis();
        VideoSynthesisParam param =
                VideoSynthesisParam.builder()
                        .apiKey(apiKey)
                        .model("wan2.2-t2v-plus")
                        .prompt("低对比度，在一个复古的70年代风格地铁站里，街头音乐家在昏暗的色彩和粗糙的质感中演奏。他穿着旧式夹克，手持吉他，专注地弹奏。通勤者匆匆走过，一小群人渐渐聚拢聆听。镜头慢慢向右移动，捕捉到乐器声与城市喧嚣交织的场景，背景中有老式的地铁标志和斑驳的墙面。")
                        .size("832*480")
                        .promptExtend(true)
                        .watermark(true)
                        .seed(12345)
                        .build();
        // 异步调用
        VideoSynthesisResult task = vs.asyncCall(param);
        System.out.println(JsonUtils.toJson(task));
        System.out.println("please wait...");

        //获取结果
        VideoSynthesisResult result = vs.wait(task, apiKey);
        System.out.println(JsonUtils.toJson(result));
    }

    public static void main(String[] args) {
        try {
            text2video();
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

**步骤1：创建任务获取任务ID**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \
    -H 'X-DashScope-Async: enable' \
    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
    -H 'Content-Type: application/json' \
    -d '{
    "model": "wan2.2-t2v-plus",
    "input": {
        "prompt": "低对比度，在一个复古的70年代风格地铁站里，街头音乐家在昏暗的色彩和粗糙的质感中演奏。他穿着旧式夹克，手持吉他，专注地弹奏。通勤者匆匆走过，一小群人渐渐聚拢聆听。镜头慢慢向右移动，捕捉到乐器声与城市喧嚣交织的场景，背景中有老式的地铁标志和斑驳的墙面。"
    },
    "parameters": {
        "size": "832*480",
        "prompt_extend": true,
        "watermark": true
    }
}'
```

**步骤2：根据任务ID获取结果**

将`{task_id}`完整替换为上一步接口返回的`task_id`的值。

```curl
curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/{task_id} \
--header "Authorization: Bearer $DASHSCOPE_API_KEY"
```

## 如何传入音频

- **音频数量**：1个。

- **输入方式**：
  - **公网 URL**：支持 HTTP 或 HTTPS 协议。

  - **临时URL**：支持OSS协议，必须通过 [上传文件获取临时 URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。

## **输出视频**

- **视频个数量**：1个。

- **视频规格**：格式为MP4。具体请参见 [视频规格](https://help.aliyun.com/zh/model-studio/text-to-video-guide/#06f39eafa2dwt "")。

- **视频URL有效期**： **24小时**。

- **视频尺寸**：由 [参数size](https://help.aliyun.com/zh/model-studio/text-to-video-api-reference#2e0de6a5b1aw8 "") 指定的分辨率决定。例如，当 `size` 设置为 `1280*720` 时，输出视频的宽高比为 **16:9**。


## **计费与限流**

- 模型免费额度和计费单价请参见 [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#ba6f7744d5e0o "")。

- 模型限流请参见 [通义万相系列](https://help.aliyun.com/zh/model-studio/rate-limit#a729d7b6bar7y "")。

- 计费说明：
  - 输入不计费，输出计费。按成功生成的 **视频秒数** 计费。

  - 模型调用失败或处理错误不产生任何费用，也不消耗 [免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "")。

  - 文生视频还支持 [节省计划](https://help.aliyun.com/zh/model-studio/billing-for-model-studio#b0a1f8c35b9wo "")。

## **API文档**

[文生视频API参考](https://help.aliyun.com/zh/model-studio/text-to-video-api-reference "")

## **常见问题**

#### **Q: 如何设置视频宽高比（如 16:9）？**

A：通过 `size` 参数指定视频分辨率，系统将根据该分辨率自动确定宽高比。

例如，设置 `size=1280*720` 即可输出 **16:9** 的视频。每个 [size](https://help.aliyun.com/zh/model-studio/text-to-video-api-reference#2e0de6a5b1aw8 "") 对应一个固定的宽高比，请根据目标比例选择合适的分辨率。

#### **Q: 为什么运行SDK代码时出现 “url error, please check url!” 错误？**

A：请确保：

- DashScope Python SDK 版本不低于 `1.25.8`。

- DashScope Java SDK 版本不低于 `2.22.6`。


若版本过低，可能会触发 “url error, please check url!” 的错误。请参考 [升级SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 进行更新。

#### **Q：** 调用时报错 Model not exist **？**

A：请依次检查：

- 模型拼写是否正确。

- 模型、Endpoint URL和API Key是否属于同一地域。跨地域调用会报此错误。


各地域上架的模型，请参见 [支持的模型](https://help.aliyun.com/zh/model-studio/text-to-video-guide/#06f39eafa2dwt "")。