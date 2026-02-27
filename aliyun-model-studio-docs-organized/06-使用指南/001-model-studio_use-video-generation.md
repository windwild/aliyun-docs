### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[模型推理](https://help.aliyun.com/zh/model-studio/model-inference/)[视频生成](https://help.aliyun.com/zh/model-studio/video-editing-and-generation/)视频生成

# 视频生成

更新时间：2026-02-12 02:59:50

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：涂鸦作画](https://help.aliyun.com/zh/model-studio/sketch-to-image)[下一篇：文生视频](https://help.aliyun.com/zh/model-studio/text-to-video-guide/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型总览

模型选型

支持的模型

万相-文生视频

万相-图生视频-基于首帧

万相-图生视频-基于首尾帧

万相-参考生视频

万相-通用视频编辑

万相-数字人

万相-图生动作

万相-视频换人

舞动人像AnimateAnyone

悦动人像EMO

灵动人像LivePortrait

表情包Emoji

声动人像VideoRetalk

视频风格重绘

阿里云百炼提供丰富的视频生成模型，覆盖 **通用创作**（文生视频、图生视频、参考生视频、视频编辑）与 **垂直场景**（数字人对口型、图生动作、视频换人、表情包制作等）多样化需求。

## **模型总览**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **部署模式**<br>> [查看各模式区别](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") | **中国内地**<br>> 模型推理计算资源仅限中国内地 | **全球**<br>> 模型推理计算资源全球调度 | **国际**<br>> 模型推理计算资源全球调度（不含中国内地） | **美国**<br>> 模型推理计算资源仅限美国境内 |
| 接入地域 | 北京 | 弗吉尼亚 | 新加坡 | 弗吉尼亚 |
| 支持的模型 | [万相-文生视频](https://help.aliyun.com/zh/model-studio/use-video-generation#aba532254b0zr "")<br>[万相-图生视频-基于首帧](https://help.aliyun.com/zh/model-studio/use-video-generation#d1578ff7d2ysd "")<br>[万相-图生视频-基于首尾帧](https://help.aliyun.com/zh/model-studio/use-video-generation#070624c34cmbu "")<br>[万相-参考生视频](https://help.aliyun.com/zh/model-studio/use-video-generation#f436f613d33w8 "")<br>[万相-通用视频编辑](https://help.aliyun.com/zh/model-studio/use-video-generation#d18108de05ayp "")<br>[万相-数字人](https://help.aliyun.com/zh/model-studio/use-video-generation#3fc26709508mi "")<br>[万相-图生动作](https://help.aliyun.com/zh/model-studio/use-video-generation#e3cd6cfdebykt "")<br>[万相-视频换人](https://help.aliyun.com/zh/model-studio/use-video-generation#598720f99fcoo "")<br>[舞动人像AnimateAnyone](https://help.aliyun.com/zh/model-studio/use-video-generation#2096e5d2bfat7 "")<br>[悦动人像EMO](https://help.aliyun.com/zh/model-studio/use-video-generation#81be219ca0ole "")<br>[灵动人像LivePortrait](https://help.aliyun.com/zh/model-studio/use-video-generation#d41e66bc28jj9 "")<br>[表情包Emoji](https://help.aliyun.com/zh/model-studio/use-video-generation#f9d29ac7a1occ "")<br>[声动人像VideoRetalk](https://help.aliyun.com/zh/model-studio/use-video-generation#8cde082c14cvj "")<br>[视频风格重绘](https://help.aliyun.com/zh/model-studio/use-video-generation#8c75981ec6glm "") | [万相-文生视频](https://help.aliyun.com/zh/model-studio/use-video-generation#aba532254b0zr "")<br>[万相-图生视频-基于首帧](https://help.aliyun.com/zh/model-studio/use-video-generation#d1578ff7d2ysd "")<br>[万相-参考生视频](https://help.aliyun.com/zh/model-studio/use-video-generation#f436f613d33w8 "") | [万相-文生视频](https://help.aliyun.com/zh/model-studio/use-video-generation#aba532254b0zr "")<br>[万相-图生视频-基于首帧](https://help.aliyun.com/zh/model-studio/use-video-generation#d1578ff7d2ysd "")<br>[万相-图生视频-基于首尾帧](https://help.aliyun.com/zh/model-studio/use-video-generation#070624c34cmbu "")<br>[万相-参考生视频](https://help.aliyun.com/zh/model-studio/use-video-generation#f436f613d33w8 "")<br>[万相-通用视频编辑](https://help.aliyun.com/zh/model-studio/use-video-generation#d18108de05ayp "")<br>[万相-图生动作](https://help.aliyun.com/zh/model-studio/use-video-generation#e3cd6cfdebykt "")<br>[万相-视频换人](https://help.aliyun.com/zh/model-studio/use-video-generation#598720f99fcoo "") | [万相-文生视频](https://help.aliyun.com/zh/model-studio/use-video-generation#aba532254b0zr "")<br>[万相-图生视频-基于首帧](https://help.aliyun.com/zh/model-studio/use-video-generation#d1578ff7d2ysd "") |

## **模型选型**

- **通用视频生成**
  - 需要将文字转化为视频时，使用 [万相-文生视频](https://help.aliyun.com/zh/model-studio/use-video-generation#aba532254b0zr "")。

  - 有一张图，想生成电影感镜头，使用 [万相-图生视频-基于首帧](https://help.aliyun.com/zh/model-studio/use-video-generation#d1578ff7d2ysd "")。

  - 有开头和结尾两张图，要控制画面变化过程，使用 [万相-图生视频-基于首尾帧](https://help.aliyun.com/zh/model-studio/use-video-generation#070624c34cmbu "")。

  - 有多个视频，想复刻角色的形象和声音表演新剧本，使用 [万相-参考生视频](https://help.aliyun.com/zh/model-studio/use-video-generation#f436f613d33w8 "")。
- **数字人对口型**：让静态照片说话、唱歌或播报。背景保持不变，仅主体面部、头部和肢体运动。
  - 首选 [万相-数字人](https://help.aliyun.com/zh/model-studio/use-video-generation#3fc26709508mi "")，效果自然，含表情和肢体动作（替代 [悦动人像EMO](https://help.aliyun.com/zh/model-studio/use-video-generation#81be219ca0ole "")）。

  - 当需要长视频（>20秒）且头部动作简单（如新闻播报）时，考虑使用 [灵动人像LivePortrait](https://help.aliyun.com/zh/model-studio/use-video-generation#d41e66bc28jj9 "")。
- **视频动作迁移**：保留照片背景，让照片的人参考指定视频动起来，使用 [万相-图生动作](https://help.aliyun.com/zh/model-studio/use-video-generation#e3cd6cfdebykt "")。

- **视频换人**：保留视频背景，把视频的人换成指定图像的人，使用 [万相-视频换人](https://help.aliyun.com/zh/model-studio/use-video-generation#598720f99fcoo "")。

- **跳舞换人**：把跳舞视频的人换成图像的人。推荐选择 [万相-图生动作](https://help.aliyun.com/zh/model-studio/use-video-generation#e3cd6cfdebykt "") 和 [万相-图生动作](https://help.aliyun.com/zh/model-studio/use-video-generation#e3cd6cfdebykt "")（效果佳）；若预算有限，可选 [舞动人像AnimateAnyone](https://help.aliyun.com/zh/model-studio/use-video-generation#2096e5d2bfat7 "")（性价比高）。

- **视频口型替换**：给已有视频改配音口型，使用 [声动人像VideoRetalk](https://help.aliyun.com/zh/model-studio/use-video-generation#8cde082c14cvj "")。

- **表情包制作**：制作固定风格模板的表情包，使用 [表情包Emoji](https://help.aliyun.com/zh/model-studio/use-video-generation#f9d29ac7a1occ "")。

- **视频重绘**：固定风格模板使用 [视频风格重绘](https://help.aliyun.com/zh/model-studio/use-video-generation#8c75981ec6glm "")，通过提示词自由描述风格使用 [万相-通用视频编辑](https://help.aliyun.com/zh/model-studio/use-video-generation#d18108de05ayp "")。

- **视频编辑**：以下需求均选择 [万相-通用视频编辑](https://help.aliyun.com/zh/model-studio/use-video-generation#d18108de05ayp "")。
  - **视频局部编辑**：替换视频中的主体或衣服、删除路人等。

  - **视频延展**：把视频延长，如1秒视频延长为5秒。

  - **视频画面扩展**：横屏变竖屏、补全边界。

  - **多图参考生成**：融合背景图像和主体图像生成视频。

## **支持的模型**

### **万相-文生视频**

**根据文本提示词生成视频**。支持输入文本+音频，输出电影级多镜头视频。

[API参考](https://help.aliyun.com/zh/model-studio/text-to-video-api-reference "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#ba6f7744d5e0o "") ｜ [Prompt指南](https://help.aliyun.com/zh/model-studio/text-to-video-prompt "") ｜在线体验： [北京](https://bailian.console.aliyun.com/cn-beijing?tab=model#/efm/model_experience_center/vision?currentTab=videoGenerate)、 [新加坡](https://modelstudio.console.aliyun.com/ap-southeast-1?tab=dashboard#/efm/model_experience_center/vision?currentTab=videoGenerate)、 [弗吉尼亚](https://modelstudio.console.aliyun.com/us-east-1?tab=dashboard#/efm/model_experience_center/vision?currentTab=videoGenerate)

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

| **输入提示词** | **输出视频（wan2.6，多镜头视频）** |
| --- | --- |

|     |     |
| --- | --- |
| **输入提示词** | **输出视频（wan2.6，多镜头视频）** |
| 一幅史诗级可爱的场景。一只小巧可爱的卡通小猫将军，身穿细节精致的金色盔甲，头戴一个稍大的头盔，勇敢地站在悬崖上。他骑着一匹虽小但英勇的战马，说： **“青海长云暗雪山，孤城遥望玉门关。黄沙百战穿金甲，不破楼兰终不还”**。悬崖下方，一支由老鼠组成的、数量庞大、无穷无尽的军队正带着临时制作的武器向前冲锋。这是一个戏剧性的、大规模的战斗场景，灵感来自中国古代的战争史诗。远处的雪山上空，天空乌云密布。整体氛围是“可爱”与“霸气”的搞笑和史诗般的融合。 |  |

### **万相-图生视频-基于首帧**

**根据给定的首帧图像生成视频**。支持输入文本+首帧图像+音频，输出电影级多镜头视频。

[API参考](https://help.aliyun.com/zh/model-studio/image-to-video-api-reference/ "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#27fb5ee25b6gv "") ｜ [Prompt指南](https://help.aliyun.com/zh/model-studio/text-to-video-prompt "") ｜在线体验： [北京](https://bailian.console.aliyun.com/cn-beijing?tab=model#/efm/model_experience_center/vision?currentTab=videoGenerate)、 [新加坡](https://modelstudio.console.aliyun.com/ap-southeast-1?tab=dashboard#/efm/model_experience_center/vision?currentTab=videoGenerate)、 [弗吉尼亚](https://modelstudio.console.aliyun.com/us-east-1?tab=dashboard#/efm/model_experience_center/vision?currentTab=videoGenerate)

中国内地

全球

国际

美国

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-i2v-flash `推荐` | 有声视频、无声视频<br>多镜头叙事、声画同步 | 文本、图像、音频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 15s\]（整数）<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.6-i2v `推荐` | 有声视频<br>多镜头叙事、声画同步 | 文本、图像、音频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 15s\]（整数）<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.5-i2v-preview | 有声视频<br>声画同步 | 文本、图像、音频 | 分辨率档位：480P、720P、1080P<br>视频时长：5s、10s <br>固定规格：30fps、MP4 (H.264编码) |
| wan2.2-i2v-flash | 无声视频<br>> 较2.1模型速度提升50% | 文本、图像 | 分辨率档位：480P、720P、1080P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.2-i2v-plus | 无声视频<br>> 较2.1模型稳定性与成功率全面提升 | 文本、图像 | 分辨率档位：480P、1080P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wanx2.1-i2v-plus | 无声视频 | 文本、图像 | 分辨率档位：720P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wanx2.1-i2v-turbo | 无声视频 | 文本、图像 | 分辨率档位：480P、720P<br>视频时长：3s、4s、5s<br>固定规格：30fps、MP4 (H.264编码) |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-i2v `推荐` | 有声视频<br>多镜头叙事、声画同步 | 文本、图像、音频 | 分辨率档位：720P、1080P<br>视频时长：5s、10s 、15s<br>固定规格：30fps、MP4 (H.264编码) |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-i2v-flash `推荐` | 有声视频、无声视频<br>多镜头叙事、声画同步 | 文本、图像、音频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 15s\]（整数）<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.6-i2v `推荐` | 有声视频<br>多镜头叙事、声画同步 | 文本、图像、音频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 15s\]（整数）<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.5-i2v-preview | 有声视频<br>声画同步 | 文本、图像、音频 | 分辨率档位：480P、720P、1080P<br>视频时长：5s、10s <br>固定规格：30fps、MP4 (H.264编码) |
| wan2.2-i2v-flash | 无声视频<br>> 较2.1模型速度提升50% | 文本、图像 | 分辨率档位：480P、720P、1080P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.2-i2v-plus | 无声视频<br>> 较2.1模型稳定性与成功率全面提升 | 文本、图像 | 分辨率档位：480P、1080P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.1-i2v-plus | 无声视频 | 文本、图像 | 分辨率档位：720P<br>视频时长：5s<br>固定规格：30fps、MP4 (H.264编码) |
| wan2.1-i2v-turbo | 无声视频 | 文本、图像 | 分辨率档位：480P、720P<br>视频时长：3s、4s、5s<br>固定规格：30fps、MP4 (H.264编码) |

在 [美国部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源仅限于美国境内。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-i2v-us `推荐` | 有声视频<br>多镜头叙事、声画同步 | 文本、图像、音频 | 分辨率档位：720P、1080P<br>视频时长：5s、10s 、15s<br>固定规格：30fps、MP4 (H.264编码) |

| **输入提示词** | **输入首帧图像和音频** | **输出视频（wan2.6，多镜头视频）** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **输入提示词** | **输入首帧图像和音频** | **输出视频（wan2.6，多镜头视频）** |
| 一幅都市奇幻艺术的场景。一个充满动感的涂鸦艺术角色。一个由喷漆所画成的少年，正从一面混凝土墙上活过来。他一边用极快的语速演唱一首英文rap，一边摆着一个经典的、充满活力的说唱歌手姿势。场景设定在夜晚一个充满都市感的铁路桥下。灯光来自一盏孤零零的街灯，营造出电影般的氛围，充满高能量和惊人的细节。视频的音频部分完全由他的rap构成，没有其他对话或杂音。 | ![rap-转换自-png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5568778571/p1011609.webp)<br>输入音频： |  |

### **万相-图生视频-基于首尾帧**

**根据给定的首帧图像和尾帧图像，生成过渡自然的视频**。支持输入文本+首帧图像+尾帧图像+音频，输出电影级多镜头视频。

[API参考](https://help.aliyun.com/zh/model-studio/image-to-video-by-first-and-last-frame-api-reference "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#517789fb633zr "") ｜ [Prompt指南](https://help.aliyun.com/zh/model-studio/text-to-video-prompt "")

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.2-kf2v-flash `推荐` | 无声视频<br>> 较2.1模型稳定性与成功率全面提升 | 文本、图像 | 分辨率档位：480P、720P、1080P<br>视频时长：5s<br>固定规格：30fps、MP4（H.264编码） |
| wanx2.1-kf2v-plus | 无声视频 | 文本、图像 | 分辨率档位：720P<br>视频时长：5s<br>固定规格：30fps、MP4（H.264编码） |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.1-kf2v-plus | 无声视频 | 文本、图像 | 分辨率档位：720P<br>视频时长：5s<br>固定规格：30fps、MP4（H.264编码） |

| **输入首帧图像** | **输入尾帧图像** | **输入提示词** | **输出视频** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **输入首帧图像** | **输入尾帧图像** | **输入提示词** | **输出视频** |
| ![first_frame](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8239161571/p944793.png) | ![last_frame](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9239161571/p944794.png) | 写实风格，一只黑色小猫好奇地看向天空，镜头从平视逐渐上升，最后俯拍小猫好奇的眼神。 |  |

### **万相-参考生视频**

**复刻视频中的角色的形象和声音表演新剧本**。输入视频+文本提示词，输出视频在保持角色一致性的同时，生成多镜头、声画同步的视频。

[API参考](https://help.aliyun.com/zh/model-studio/wan-video-to-video-api-reference "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#5c3d28ad8a4x8 "") ｜ [Prompt指南](https://help.aliyun.com/zh/model-studio/text-to-video-prompt "")

中国内地

全球

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-r2v-flash `推荐` | 有声视频、无声视频<br>参考多角色生视频<br>多镜头叙事、声画同步 | 文本、图像、视频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 10s\]（整数）<br>固定规格：30fps、MP4（H.264编码） |
| wan2.6-r2v | 有声视频<br>参考多角色生视频<br>多镜头叙事、声画同步 | 文本、图像、视频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 10s\]（整数）<br>固定规格：30fps、MP4（H.264编码） |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-r2v `推荐` | 有声视频<br>参考多角色生视频<br>多镜头叙事、声画同步 | 文本、视频 | 分辨率档位：720P、1080P<br>视频时长：5s、10s<br>固定规格：30fps、MP4（H.264编码） |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.6-r2v-flash `推荐` | 有声视频、无声视频<br>参考多角色生视频<br>多镜头叙事、声画同步 | 文本、图像、视频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 10s\]（整数）<br>固定规格：30fps、MP4（H.264编码） |
| wan2.6-r2v | 有声视频<br>参考多角色生视频<br>多镜头叙事、声画同步 | 文本、图像、视频 | 分辨率档位：720P、1080P<br>视频时长：\[2s, 10s\]（整数）<br>固定规格：30fps、MP4（H.264编码） |

| **输入参考视频1（角色为小女孩）** | **输入参考视频2（角色为闹钟）** | **输入提示词** | **输出视频（多角色对话）** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **输入参考视频1（角色为小女孩）** | **输入参考视频2（角色为闹钟）** | **输入提示词** | **输出视频（多角色对话）** |
|  |  | character1对character2说: “I’ll rely on you tomorrow morning!” character2 回答: “You can count on me!” |  |

### **万相-通用视频编辑**

**视频编辑通用模型**。支持输入文本、图像、视频多模态数据，可执行多种视频生成与编辑任务。

[API参考](https://help.aliyun.com/zh/model-studio/wanx-vace-api-reference "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#89e9be041ek81 "")

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wanx2.1-vace-plus | 无声视频<br>多图参考、视频重绘、局部编辑、视频延展、视频画面扩展 | 文本、图像、视频 | 分辨率档位：720P<br>视频时长：不超过5s<br>固定规格：30fps、MP4（H.264编码） |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.1-vace-plus | 无声视频<br>多图参考、视频重绘、局部编辑、视频延展、视频画面扩展 | 文本、图像、视频 | 分辨率档位：720P<br>视频时长：不超过5s<br>固定规格：30fps、MP4（H.264编码） |

- **功能一：多图参考**




| **输入参考图1（参考主体）** | **输入参考图2（参考背景）** | **输入提示词** | **输出视频** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **输入参考图1（参考主体）** | **输入参考图2（参考背景）** | **输入提示词** | **输出视频** |
| ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2786951571/p955656.png) | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2786951571/p955657.png) | 视频中，一位女孩自晨雾缭绕的 **古老森林深处款款走出**，她步伐轻盈，镜头捕捉她每一个灵动瞬间。当她站定，环顾四周葱郁林木时，她 **脸上绽放出惊喜与喜悦交织的笑容**。这一幕，定格在了光影交错的瞬间，记录下她与大自然的美妙邂逅。 |  |

- **功能二：视频重绘**




| **输入视频** | **输入提示词** | **输出视频** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **输入视频** | **输入提示词** | **输出视频** |
|  | 视频展示了一辆黑色的 **蒸汽朋克风格汽车**，绅士驾驶着，车辆装饰着齿轮和铜管。背景是蒸汽驱动的糖果工厂和复古元素，画面复古与趣味 |  |

- **功能三：视频局部编辑**




| **输入视频** | **输入掩码图像（白色区域表示编辑区域）** | **输入提示词** | **输出视频** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **输入视频** | **输入掩码图像（白色区域表示编辑区域）** | **输入提示词** | **输出视频** |
|  | ![mask](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3778351571/p955179.png) | 视频展示了一家巴黎风情的法式咖啡馆，一只 **穿着西装的狮子** 优雅地品着咖啡。它一手端着咖啡杯，轻轻啜饮，神情惬意。咖啡馆装饰雅致，柔和的色调与温暖灯光映照着狮子所在的区域。 |  |

- **功能四：视频延展**




| **输入首片段视频（1秒）** | **输入提示词** | **输出视频（延长后的视频为5秒）** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **输入首片段视频（1秒）** | **输入提示词** | **输出视频（延长后的视频为5秒）** |
|  | 一只戴着墨镜的 **狗在街道上滑滑板**，3D卡通。 |  |

- **功能五：视频画面扩展**




| **输入视频** | **输入提示词** | **输出视频** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **输入视频** | **输入提示词** | **输出视频** |
|  | 一位优雅的女士正在激情演奏小提琴， **她身后是一支完整的交响乐团**。 |  |


### **万相-数字人**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

**图生唱演和播报视频：让图像中人或卡通形象说话、唱歌、播报或表演**。输入图像 \+ 音频，输出视频自动为人物或卡通形象匹配口型、面部表情、头部及身体动作。

[图像检测API参考](https://help.aliyun.com/zh/model-studio/wan-s2v-detect-api "") ｜ [视频生成API参考](https://help.aliyun.com/zh/model-studio/wan-s2v-api "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#6fa00e4db0qlz "")

| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| wan2.2-s2v-detect | 图像检测 | 图像 | 输出检测状态：通过或未通过 |
| wan2.2-s2v | 视频生成<br>有声视频 | 图像、音频 | 分辨率档位：480P、720P<br>视频时长：不超过20s（跟随音频时长）<br>固定规格：<br>- 480P：16fps、MP4（H.264编码）<br>  <br>- 720P：30fps、MP4（H.264编码） |

| **输入示例（人物图像+音频）** | **输出视频（对口型）** |
| --- | --- |

|     |     |
| --- | --- |
| **输入示例（人物图像+音频）** | **输出视频（对口型）** |
| ![p1001125-转换自-jpeg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6760119571/p1012865.webp)<br>输入音频： |  |

### **万相-图生动作**

**让图像的人参考视频动起来**。输入图像 \+ 视频，输出的视频保持图像背景不变，参考视频做动作。

[API参考](https://help.aliyun.com/zh/model-studio/wan-animate-move-api "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#1f708fcd62rdc "")

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.2-animate-move | 有声视频、无声视频（跟随输入视频而定）<br>- 标准模式`wan-std`：生成速度快，性价比高<br>  <br>- 专业模式`wan-pro`：效果更接近真实拍摄 | 图像、视频 | 分辨率档位：720P<br>视频时长：2s＜时长＜30s<br>固定规格：<br>- 标准模式`wan-std`：15fps、MP4（H.264编码）<br>  <br>- 专业模式`wan-pro`：25fps、MP4（H.264编码） |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.2-animate-move | 有声视频、无声视频（跟随输入视频而定）<br>- 标准模式`wan-std`：生成速度快，性价比高<br>  <br>- 专业模式`wan-pro`：效果更接近真实拍摄 | 图像、视频 | 分辨率档位：720P<br>视频时长：2s＜时长＜30s<br>固定规格：<br>- 标准模式`wan-std`：15fps、MP4（H.264编码）<br>  <br>- 专业模式`wan-pro`：25fps、MP4（H.264编码） |

| **输入人物图像** | **输入参考视频** | **输出视频（标准模式**`wan-std` **）** | **输出视频（专业模式**`wan-pro` **）** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **输入人物图像** | **输入参考视频** | **输出视频（标准模式**`wan-std` **）** | **输出视频（专业模式**`wan-pro` **）** |
| ![move_input_image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9815528571/p1008736.jpeg) |  |  |  |

### **万相-视频换人**

**把视频中的人换成图像中的人**。输入视频 \+ 替换图像，输出视频保留原视频背景，实现视频换脸、视频换角色等功能。

[API参考](https://help.aliyun.com/zh/model-studio/wan-animate-mix-api "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#86bd5c57adaos "")

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.2-animate-mix | 有声视频、无声视频（跟随输入视频而定）<br>- 标准模式`wan-std`：生成速度快，性价比高<br>  <br>- 专业模式`wan-pro`：效果更接近真实拍摄 | 图像、视频 | 分辨率档位：720P<br>视频时长：2s＜时长＜30s<br>固定规格：<br>- 标准模式`wan-std`：15fps、MP4（H.264编码）<br>  <br>- 专业模式`wan-pro`：25fps、MP4（H.264编码） |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| wan2.2-animate-mix | 有声视频、无声视频（跟随输入视频而定）<br>- 标准模式`wan-std`：生成速度快，性价比高<br>  <br>- 专业模式`wan-pro`：效果更接近真实拍摄 | 图像、视频 | 分辨率档位：720P<br>视频时长：2s＜时长＜30s<br>固定规格：<br>- 标准模式`wan-std`：15fps、MP4（H.264编码）<br>  <br>- 专业模式`wan-pro`：25fps、MP4（H.264编码） |

| **输入视频** | **输入待替换的人物图像** | **输出视频（标准模式**`wan-std` **）** | **输出视频（专业模式**`wan-pro` **）** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **输入视频** | **输入待替换的人物图像** | **输出视频（标准模式**`wan-std` **）** | **输出视频（专业模式**`wan-pro` **）** |
|  | ![mix_input_image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3025528571/p1008733.jpeg) |  |  |

### **舞动人像AnimateAnyone**

**说明**

- 仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

- 推荐使用 [万相-图生动作](https://help.aliyun.com/zh/model-studio/use-video-generation#e3cd6cfdebykt "") 和 [万相-视频换人](https://help.aliyun.com/zh/model-studio/use-video-generation#598720f99fcoo "") **替换** 舞动人像AnimateAnyone。前两者效果更佳，舞动人像 AnimateAnyone成本较低。


**专为跳舞设计，把视频中跳舞的人换成图像中的人**。输入图像+视频，输出视频支持两种方式：1.保留图像背景不变；2.保留视频背景不变。

[图像检测API参考](https://help.aliyun.com/zh/model-studio/animate-anyone-detect-api "") \| [动作模板生成API参考](https://help.aliyun.com/zh/model-studio/animate-anyone-template-api "") \| [视频生成API参考](https://help.aliyun.com/zh/model-studio/animateanyone-video-generation-api "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#1e75986422adx "")

| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| animate-anyone-detect-gen2 | 图像检测 | 图像 | 输出检测状态：通过或未通过 |
| animate-anyone-template-gen2 | 舞蹈视频模板生成<br>> 从跳舞视频中提取动作模板 | 视频 | 输出舞蹈动作模板ID |
| animate-anyone-gen2 | 视频生成<br>无声视频 | 图像、视频、舞蹈动作模板ID | 视频分辨率档位：720P<br>视频时长：2s≤时长≤60s<br>固定规格：15fps、MP4（H.264编码） |

| **输入人物图像** | **输入跳舞视频** | **输出视频（按图片背景生成）** | **输出视频（按视频背景生成）** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **输入人物图像** | **输入跳舞视频** | **输出视频（按图片背景生成）** | **输出视频（按视频背景生成）** |
| ![05-9_16](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5770383371/p885845.png) |  |  |  |

### **悦动人像EMO**

**说明**

- 仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

- 推荐使用 [万相-数字人](https://help.aliyun.com/zh/model-studio/use-video-generation#3fc26709508mi "") **替换** 悦动人像EMO。前者效果更佳，悦动人像EMO成本较低。


**图生唱演视频：让图像中人唱歌或表演**。输入图像 \+ 音频，输出视频自动为人物匹配口型、面部表情以及头部动作。

[图像检测API参考](https://help.aliyun.com/zh/model-studio/emo-detect-api "") \| [视频生成API参考](https://help.aliyun.com/zh/model-studio/emo-api "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#a54957baf9exo "")

| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| emo-detect-v1 | 图像检测 | 图像 | 输出检测状态：通过或未通过 |
| emo-v1 | 视频生成<br>有声视频 | 图像、音频 | 视频分辨率：<br>- 1:1画幅（宽高比）：固定为512×512<br>  <br>- 3:4画幅（宽高比）：固定为512×704<br>  <br>视频时长：不超过60s<br>固定规格：15fps、MP4（H.264编码） |

| **输入示例（人物肖像图片+音频）** | **输出视频（唱歌对口型）** |
| --- | --- |

|     |     |
| --- | --- |
| **输入示例（人物肖像图片+音频）** | **输出视频（唱歌对口型）** |
| ![上春山](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9239161571/p872312.png)<br>输入音频： |  |

### **灵动人像LivePortrait**

**说明**

- 仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

- 推荐使用 [万相-数字人](https://help.aliyun.com/zh/model-studio/use-video-generation#3fc26709508mi "") **替换** 灵动人像LivePortrait。前者效果更佳，灵动人像LivePortrait成本较低。请注意，当需要长视频（>20秒），可选择灵动人像LivePortrait。


**图生播报视频：让图像中人播报新闻、讲故事**。输入图像 \+ 音频，输出视频自动为人物匹配口型、面部表情以及头部动作（轻微摆动）。

[图像检测API参考](https://help.aliyun.com/zh/model-studio/liveportrait-detect-api "") \| [视频生成API参考](https://help.aliyun.com/zh/model-studio/liveportrait-api "") ｜ [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#563f7f3552k5m "")

| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| liveportrait-detect | 图像检测 | 图像 | 输出检测状态：通过或未通过 |
| liveportrait | 视频生成<br>有声视频 | 图像、音频 | 视频分辨率：跟随输入图片，上限接近4K（4096x4096）<br>视频时长：1s＜时长＜180s<br>视频帧率：15fps≤帧率≤30fps<br>视频格式：MP4（H.264编码） |

| **输入示例（人物肖像图片+音频）** | **输出视频（语音播报对口型）** |
| --- | --- |

|     |     |
| --- | --- |
| **输入示例（人物肖像图片+音频）** | **输出视频（语音播报对口型）** |
| ![素描男孩](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8083702371/p874909.png)<br>输入音频： |  |

### **表情包Emoji**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

**根据固定表情包模板制作表情包**。输入图像+指定表情包ID，输出表情包视频。

[图像检测API参考](https://help.aliyun.com/zh/model-studio/emoji-detect-api "") \|  [视频生成API参考](https://help.aliyun.com/zh/model-studio/emoji-api "") \|  [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#f24425d742a0j "")

| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出说明** |
| emoji-detect-v1 | 图像检测 | 图像 | 输出检测状态：通过或未通过 |
| emoji-v1 | 视频生成<br>无声视频 | 图像、表情包模板ID | 视频分辨率：固定为512x512<br>视频时长：不超过5s（跟随模板时长）<br>固定规格：15fps、MP4（H.264编码） |

| **输入人物肖像图片** | **输出视频（“嫌弃”表情包）** |
| --- | --- |

|     |     |
| --- | --- |
| **输入人物肖像图片** | **输出视频（“嫌弃”表情包）** |
| ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8567357371/p906296.png) |  |

### **声动人像VideoRetalk**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

**视频口型替换：给视频替换配音口型**。输入视频+音频，输出人物口型与音频同步的视频。

[API参考](https://help.aliyun.com/zh/model-studio/videoretalk-api "") \|  [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#5835b4a956h6b "")

| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| videoretalk | 有声视频 | 视频、音频 | 视频分辨率：跟随输入视频，上限接近2K（2048x2048）<br>视频时长：2s＜时长＜120s<br>固定规格：30fps、MP4（H.264编码） |

| **输入示例（人物播报视频+音频）** | **输出视频（口型替换）** |
| --- | --- |

|     |     |
| --- | --- |
| **输入示例（人物播报视频+音频）** | **输出视频（口型替换）** |
| 输入音频： |  |

### **视频风格重绘**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

**根据固定风格模板进行视频重绘**。输入视频+指定重绘风格ID，输出重绘后的视频。

[API参考](https://help.aliyun.com/zh/model-studio/video-style-transform-api-reference "") \|  [模型价格](https://help.aliyun.com/zh/model-studio/model-pricing#48d1e28e3esm4 "")

| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **能力支持** | **输入模态** | **输出视频规格** |
| video-style-transform | 有声视频、无声视频<br>> 跟随输入视频而定 | 视频、重绘风格ID | 视频分辨率：跟随输入视频，上限接近4K（4096x4096）<br>视频时长：不超过30s<br>视频帧率：15fps≤帧率≤25fps<br>视频格式：MP4（H.264编码） |

| **输入视频** | **输出视频（重绘风格选择“日式漫画”）** |
| --- | --- |

|     |     |
| --- | --- |
| **输入视频** | **输出视频（重绘风格选择“日式漫画”）** |
|  |  |