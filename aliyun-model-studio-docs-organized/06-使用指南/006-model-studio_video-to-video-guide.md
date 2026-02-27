### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[模型推理](https://help.aliyun.com/zh/model-studio/model-inference/)[视频生成](https://help.aliyun.com/zh/model-studio/video-editing-and-generation/)参考生视频

# 参考生视频

更新时间：2026-02-27 03:38:37

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：图生视频-基于首尾帧](https://help.aliyun.com/zh/model-studio/image-to-video-first-and-last-frames-guide)[下一篇：通用视频编辑](https://help.aliyun.com/zh/model-studio/wan-vace-guide)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

适用范围

核心能力

多角色互动

单角色表演

生成无声视频

如何输入参考素材

输入图像

输入视频

输出视频

计费与限流

API文档

常见问题

万相-参考生视频模型支持 **多模态输入**（文本/图像/视频），可将人物或物体作为主角，根据提示词生成自然生动的表演视频。

- **基础能力**：设置整数级视频时长（2～10秒）、指定视频分辨率（720P/1080P）、添加水印。

- **角色扮演**：基于参考图像或视频还原角色形象；若参考素材为视频，还支持参考音色，支持单人表演或多角色互动。

- **多镜头叙事**：具备多镜头智能调度能力，支持自然对话与稳定互动，同时保持主体一致性。


**快速入口：** [API参考](https://help.aliyun.com/zh/model-studio/wan-video-to-video-api-reference "") **｜** [Prompt指南](https://help.aliyun.com/zh/model-studio/text-to-video-prompt "")

## **适用范围**

各地域支持的模型有所差异，且资源相互独立。调用时，请务必确保模型、接入地址及 API Key **均属于同一地域**，否则将导致调用失败。

**支持的模型**：

中国内地

全球

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-r2v-flash `推荐` | 有声视频、无声视频<br>单角色/多角色生视频<br>多镜头叙事、声画同步<br>> 生成速度更快，性价比高 | 文本、图像、视频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 10s\]（整数）<br>固定规格：30fps、MP4（H.264编码） |
| wan2.6-r2v | 有声视频<br>单角色/多角色生视频<br>多镜头叙事、声画同步 | 文本、图像、视频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 10s\]（整数）<br>固定规格：30fps、MP4（H.264编码） |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-r2v `推荐` | 有声视频<br>单角色/多角色生视频<br>多镜头叙事、声画同步 | 文本、视频 | 分辨率档位：720P、1080P<br>视频时长：5s、10s<br>固定规格：30fps、MP4（H.264编码） |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-r2v-flash `推荐` | 有声视频、无声视频<br>单角色/多角色生视频<br>多镜头叙事、声画同步<br>> 生成速度更快，性价比高 | 文本、图像、视频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 10s\]（整数）<br>固定规格：30fps、MP4（H.264编码） |
| wan2.6-r2v | 有声视频<br>单角色/多角色生视频<br>多镜头叙事、声画同步 | 文本、图像、视频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 10s\]（整数）<br>固定规格：30fps、MP4（H.264编码） |

**说明**

本文的示例代码适用于 **北京地域**。如使用其他地域，请参见 [API参考](https://help.aliyun.com/zh/model-studio/wan-video-to-video-api-reference "")。

## **核心能力**

### **多角色互动**

**支持模型**：所有模型。

**功能介绍**：支持最多5个角色合拍，生成自然对话和互动，适用于访谈、对话、教学等场景。

**参数设置：**

- `reference_urls`：最多传入 **5个** URL。每个URL可以指向一张图像或一段视频。

  - 图像数量：0～5。参考图可以是人物、物体和背景。

  - 视频数量：0～3。推荐用于人物或物体参考，不建议使用背景或空镜视频。

  - 每个参考素材（视频或图像）仅包含单一角色。
- `shot_type`：推荐设置为`multi`，用于多镜头切换，增强互动表现力；也支持设置为`single`，单镜头固定视角。

- `prompt`：提示词通过“ **character1、character2**”这类标识引用角色。角色顺序与 `reference_urls` 数组一一对应，即第 1 个 URL 为 character1，第 2 个为 character2，依此类推。


参考图像和视频

参考视频

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **输入提示词**：character2 坐在靠窗的椅子上，手持 character3，在 character4 旁演奏一首舒缓的美国乡村民谣。character1 对character2开口说道：“听起来不错”。 |
| **输入视频character1**<br>> 参考人物 | **输入视频character2**<br>> 参考人物 | **输入图像character3**<br>> 参考物体 | **输入图像character4**<br>> 参考背景 | **输出视频（多镜头，有声视频）** |
|  |  | ![wan-r2v-object4](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9459060771/p1052555.png) | ![wan-r2v-backgroud5](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9459060771/p1052556.png) |  |

|     |     |     |
| --- | --- | --- |
| **输入提示词**：一段温馨有趣的宠物短视频。第1个镜头\[0-2秒\] character1对着镜头微笑挥手，背景是充满活力的城市街道。第2个镜头\[2-4秒\] 突然一只可爱的狗狗 character2从画面外跳入，扑向年轻人。第3个镜头\[4-6秒\] character1和character2开心互动，狗狗character2摇尾巴，character1抚摸character2的头。第4个镜头\[6-8秒\] 镜头切换到狗狗character2的视角，展现它眼中的主人character1。第5个镜头\[8-10秒\] character1和character2合影，营造温馨欢乐的氛围。 |
| **输入视频character1**<br>> 参考人物 | **输入视频character2**<br>> 参考物体 | **输出视频（多镜头，有声视频）** |
|  |  |  |

curl

**步骤1：创建任务获取任务ID**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \
    -H 'X-DashScope-Async: enable' \
    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
    -H 'Content-Type: application/json' \
    -d '{
    "model": "wan2.6-r2v-flash",
    "input": {
        "prompt": "Character2 坐在靠窗的椅子上，手持 character3，在 character4 旁演奏一首舒缓的美国乡村民谣。Character1 对Character2开口说道：“听起来不错”",
        "reference_urls": [\
            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260129/hfugmr/wan-r2v-role1.mp4",\
            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260129/qigswt/wan-r2v-role2.mp4",\
            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260129/qpzxps/wan-r2v-object4.png",\
            "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260129/wfjikw/wan-r2v-backgroud5.png"\
        ]
    },
    "parameters": {
        "size": "1280*720",
        "duration": 10,
        "audio": true,
        "shot_type": "multi",
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

### **单角色表演**

**支持模型**：所有模型。

**功能介绍**：基于参考视频和参考图像中的角色在不同场景中展现完整表演，适用于个人品牌、产品代言、教育培训等。

**参数设置**：

- `reference_urls`：传入1个视频或1张图像。

- `shot_type`：推荐设置为`multi`，用于多镜头切换，增强互动表现力；也支持设置为`single`，单镜头固定视角。

- `prompt`：使用“character1”引用参考素材中的角色。


|     |     |     |
| --- | --- | --- |
| **输入提示词** | **输入视频character1** | **输出视频（多镜头，有声视频）** |
| 展示最新款智能手表的多功能性和时尚设计。第1个镜头\[0-3秒\] character1在办公室中抬起手腕查看手表，屏幕显示日程提醒。第2个镜头\[3-5秒\] 特写镜头，手表屏幕切换到健康监测界面，显示心率和步数数据。第3个镜头\[5-8秒\] character1在健身房运动，手表自动识别运动模式并开始记录。第4个镜头\[8-10秒\] 手表收到消息通知，character1轻触屏幕查看详情，操作流畅自然。 |  |  |

curl

**步骤1：创建任务获取任务ID**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \
    -H 'X-DashScope-Async: enable' \
    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
    -H 'Content-Type: application/json' \
    -d '{
    "model": "wan2.6-r2v-flash",
    "input": {
        "prompt": "展示最新款智能手表的多功能性和时尚设计。第1个镜头[0-3秒] character1在办公室中抬起手腕查看手表，屏幕显示日程提醒。第2个镜头[3-5秒] 特写镜头，手表屏幕切换到健康监测界面，显示心率和步数数据。第3个镜头[5-8秒] character1在健身房运动，手表自动识别运动模式并开始记录。第4个镜头[8-10秒] 手表收到消息通知，character1轻触屏幕查看详情，操作流畅自然。",
        "reference_urls":["https://cdn.wanx.aliyuncs.com/static/demo-wan26/vace.mp4"]
    },
    "parameters": {
        "size": "1280*720",
        "duration": 10,
        "shot_type":"multi",
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

### **生成无声视频**

**支持模型**：`wan2.6-r2v-flash`。

**功能介绍**：适用于无需音频的纯视觉展示场景，如动态海报、无声短视频等。

**参数设置**：

- `audio`：若需生成无声视频，必须 **显式设置**`audio = false`。

- `prompt`：传入一个参考素材时，使用“character1”引用角色。


|     |     |     |
| --- | --- | --- |
| **输入提示词** | **输入视频character1** | **输出视频（无声视频）** |
| character1一边喝奶茶，一边随着音乐即兴跳舞。 |  |  |

curl

**步骤1：创建任务获取任务ID**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/video-generation/video-synthesis' \
    -H 'X-DashScope-Async: enable' \
    -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
    -H 'Content-Type: application/json' \
    -d '{
    "model": "wan2.6-r2v-flash",
    "input": {
        "prompt": "character1一边喝奶茶，一边随着音乐即兴跳舞。",
        "reference_urls":["https://cdn.wanx.aliyuncs.com/static/demo-wan26/vace.mp4"]
    },
    "parameters": {
        "size": "1280*720",
        "duration": 5,
        "shot_type":"multi",
        "audio": false,
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

## 如何输入参考素材

### **输入图像**

- **图像数量**：最多5张。

- **总数限制**：图像 \+ 视频 ≤ 5。

- **输入方式**：

  - **公网URL**：支持 HTTP 或 HTTPS 协议。示例：https://xxxx/xxx.png。

  - **临时URL**：支持OSS协议，必须通过 [上传文件获取临时 URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。示例：oss://dashscope-instant/xxx/xxx.png。

### **输入视频**

- **视频数量**：最多3个。

- **总数限制**：图像 \+ 视频 ≤ 5。

- **输入方式**：

  - **公网URL**：支持 HTTP 或 HTTPS 协议。示例：https://xxxx/xxx.mp4。

  - **临时URL**：支持OSS协议，必须通过 [上传文件获取临时 URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")。示例：oss://dashscope-instant/xxx/xxx.mp4。

## **输出视频**

- **视频个数**：1个。

- **视频规格**：格式为MP4。详细规格请参见 [支持的模型](https://help.aliyun.com/zh/model-studio/video-to-video-guide#06f39eafa2dwt "")。

- **视频URL有效期**： **24小时**。

- **视频尺寸**：由 [size](https://help.aliyun.com/zh/model-studio/wan-video-to-video-api-reference#2e0de6a5b1aw8 "") 指定的分辨率决定。例如，当 `size` 设置为 `1280*720` 时，输出视频的宽高比为 **16:9**。


## **计费与限流**

- 模型免费额度和计费单价请参见 [万相-参考生视频](https://help.aliyun.com/zh/model-studio/model-pricing#5c3d28ad8a4x8 "")。

- 模型限流请参见 [万相系列](https://help.aliyun.com/zh/model-studio/rate-limit#a729d7b6bar7y "")。

- 计费说明：

  - 输入图像不计费，输入视频和输出视频计费，按 **视频秒数** 计费。

  - 模型调用失败或处理错误不产生任何费用，也不消耗 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "")。

  - 有声视频与无声视频价格不同（如wan2.6-r2v-flash）。
- 计费时长计算规格：

  - **总计费时长 = 输入视频时长（上限5秒）\+ 输出视频时长**。

  - **输入视频计费时长**：总输入视频计费时长不超过 **5 秒**。

    - 计算规则：按参考素材总数（图像 \+ 视频）均分，作为单个视频的截断上限。每个视频按 `min(实际时长, 截断上限)` 计费，多个视频计费时长累计相加。

    - 示例：输入 3 个素材（1 张图像 + 2 个视频），单视频截断上限为 1.65 秒，则：

      输入计费时长 = `min(视频1时长, 1.65s) + min(视频2时长, 1.65s)`，图像不计费。
  - **输出视频计费时长**：模型 **成功生成的视频秒数**。

**更多示例：输入视频计费时长计算**

- **输入1个参考素材：单视频截断上限为5秒。**

  - 若为视频：`输入计费时长=min(视频时长，5s)`。

  - 若为图像：免费。
- **输入2个参考素材：单视频截断上限为2.5秒。**

  - 若1个视频+1张图像：`输入计费时长=min(视频1时长，2.5s)`。

  - 若2个视频：`输入计费时长=min(视频1时长，2.5s)+ min(视频2时长，2.5s)`。
- **输入3个参考素材：单视频截断上限为1.65秒。**

  - 若1个视频+2张图像：`输入计费时长=min(视频1长度，1.65s)`。

  - 若3个视频：`输入计费时长=min(视频1长度，1.65s)+ min(视频2长度，1.65s)+min(视频3长度，1.65s)`。
- **输入4个参考素材：单视频截断上限为1.25秒。**

  - 若2个视频+2张图像：`输入计费时长=min(视频1长度，1.25s)+ min(视频2长度，1.25s)`。

  - 若3个视频+1张图像：`输入计费时长=min(视频1长度，1.25s)+ min(视频2长度，1.25s)+min(视频3长度，1.25s)`。
- **输入5个参考素材：单视频截断上限为1秒。**

  - 若1个视频+4张图像：`输入计费时长=min(视频1长度，1s)`。

  - 若3个视频+2张图像：`输入计费时长=min(视频1长度，1s)+ min(视频2长度，1s)+min(视频3长度，1s)`。

## **API文档**

[参考生视频API参考](https://help.aliyun.com/zh/model-studio/wan-video-to-video-api-reference "")

## **常见问题**

#### **Q：如何设置视频宽高比（如 16:9）？**

A：通过 `size` 参数指定视频分辨率，系统将根据该分辨率自动确定宽高比。

例如，设置 `size=1280*720` 即可输出 **16:9** 的视频。每个 [size](https://help.aliyun.com/zh/model-studio/wan-video-to-video-api-reference#2e0de6a5b1aw8 "") 对应一个固定的宽高比，请根据目标比例选择合适的分辨率。

#### **Q：如何在提示词中引用参考素材中的角色？**

A：每个参考素材（视频或图像）仅包含单一角色。使用 `character1`、`character2` 这类标识引用参考素材中的角色，顺序对应 `reference_urls` 数组的顺序。例如：

```json
"reference_urls":[\
    "https://example.com/girl.mp4",   // character1\
    "https://example.com/clock.png"   // character2\
]
```