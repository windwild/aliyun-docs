### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[图像生成](https://help.aliyun.com/zh/model-studio/image-editing-and-generation/)虚拟模特生成

# 虚拟模特生成

更新时间：2026-02-11 01:58:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：图像画面扩展](https://help.aliyun.com/zh/model-studio/image-expansion)[下一篇：鞋靴模特](https://help.aliyun.com/zh/model-studio/shoes-and-boots-model)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

基本介绍

使用场景

特色优势

模型概览

快速开始

virtualmodel-V2（推荐）

wanx-virtualmodel-V1

场景示例

wanx-virtualmodel-V1

virtualmodel-V2

API参考

万相-虚拟模特模型支持在保持真人实拍模特站姿不变的前提下，对拍摄背景图、模特进行替换，快速生成更多模特拍摄图。

**重要**

- 本文档仅适用于“中国内地（北京）”地域，且必须使用该地域的 [API Key](https://bailian.console.aliyun.com/?tab=model#/api-key)。

- wanx-virtualmodel、virtualmodel-v2 模型当前仅提供 **免费体验**，免费额度用完后不可调用且不支持付费，推荐参考 [图像编辑-千问](https://help.aliyun.com/zh/model-studio/qwen-image-edit-guide "") 或 [图像编辑-万相2.1](https://help.aliyun.com/zh/model-studio/wanx-image-edit "") 获取替代方案。


## 基本介绍

万相-虚拟模特可以对上传的真人或者人台实拍商品展示图进行智能生成，将其中的模特和背景替换为心仪的内容，在保持人物姿态不变的情况下，使用虚拟模特对商品进行更加精美、多样的展示。支持各种与模特产生互动的商品，如手持小商品、服装、鞋靴、配饰等。

如想了解功能效果或使用流程，可以在 [万相-虚拟模特](https://tongyi.aliyun.com/wanxiang/app/virtual-model)(V0.7)功能中进行初步体验。

### 使用场景

- 商品模特创意设计：电商商品设计领域，客户上传一张身着基础款连衣裙的模特照片，通过虚拟模特功能，选择维多利亚时代复古风格的虚拟模特与奢华背景，保留原有模特的优雅姿态，将连衣裙材质和色彩自动调整以匹配新场景，实现高端定制系列的视觉预览。

- 珠宝饰品穿戴展示：珠宝商希望突出展示其新款项链，上传佩戴基础项链的半身人台照或者基础模特照，通过AI技术生成更为精致优美的虚拟模特，实现虚拟模特穿戴珠宝的璀璨效果，同时调整背景为高贵典雅的室内环境，提升商品档次感，增加珠宝细节纹理融合。

- 模特鞋靴穿戴展示：设计师为展示新款多功能球鞋，上传穿着新款鞋靴的基础站立姿势的模特照片，利用虚拟模特技术快速更换生成新的虚拟模特，生成一系列从休闲街头风到专业运动风格背景展示图，满足不同顾客群体的场景需求，创造出多样化的时尚造型。

- 童装童鞋模特生成：童装品牌需要展示儿童在多风格场景中的穿着效果，上传基础照片后，使用虚拟模特生成活泼可爱的儿童形象，更换为品牌最新童装系列，背景设置为学校、游乐场等场景，展现孩子们的天真烂漫与服装的舒适度，确保童装新品都能极速展示。


### 特色优势

- 效果业界领先：虚拟模特生成图像语义一致性更精准，AI局部创作布局自然、细节丰富、画面细腻、结果逼真，又保持视觉效果的和谐与专业性，无需担心人工合成的痕迹。

- 稳定、易用平台服务：提供在高并发、大流量下的稳定虚拟模特图片生成响应，可直接调用的简单推理API 接口，服务简单易用，易被集成，兼容性强。

- 模特图高品质生成：支持人台图、真人图、服装图模特生成，支持2:1、16:9、4:3、1:1、3:4、9:16、1:2多比例图片生成，支持最大短边大小到2024，支持背景参考图输入和权重自由配置。


### **模型概览**

|     |     |     |
| --- | --- | --- |
| **模型版本** | **模型名称** | **模型简介** |

| 虚拟模特<br>（V1版本） | wanx-virtualmodel | - 支持真人实拍图上传<br>  <br>- 生成的图片短边：512像素或1024像素 |
| 虚拟模特V2<br>（V2版本） | virtualmodel-v2 | - 支持真人、人台实拍图上传<br>  <br>- 生成的图片短边为：1024像素或2048像素<br>  <br>- 支持改变分辨率，生成图片长宽比可选择：比例不变、2:1、16:9、4:3、1:1、3:4、 9:16、1:2。<br>  <br>- 支持背景参考图权重自由控制<br>  <br>- 文本引导效果更准确 |

| **模型名称** | **计费单价** | **限流（主账号与RAM子账号共用）** | **免费额度** [（查看）](https://help.aliyun.com/zh/model-studio/new-free-quota "") |
| --- | --- | --- | --- |
| **任务下发接口RPS限制** | **同时处理中任务数量** |
| --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型名称** | **计费单价** | **限流（主账号与RAM子账号共用）** | **免费额度** [（查看）](https://help.aliyun.com/zh/model-studio/new-free-quota "") |
| **任务下发接口RPS限制** | **同时处理中任务数量** |
| wanx-virtualmodel | 目前仅供免费体验。<br>> 免费额度用完后不可调用，推荐参考 [图像编辑-千问](https://help.aliyun.com/zh/model-studio/qwen-image-edit-guide "") 或 [图像编辑-万相2.1](https://help.aliyun.com/zh/model-studio/wanx-image-edit "") 获取替代方案。 | 2 | 1 | 500张 |
| virtualmodel-v2 |

## 快速开始

图像关键参数：

- 图像格式：JPEG、JPG、PNG、WEBP。

- 图像大小：建议不超过5MB。

- 图像分辨率：长宽比大于1:2且小于2:1，大于256×256像素，长边小于4096像素，人脸占比不低于128×128像素。

- URL地址中不能包含中文字符。

- V1、V2版本prompt输入支持中英文格式的提示词描述。


### virtualmodel-V2（推荐）

支持输入真人实拍图和英文任务描述，模型在保持人物站姿不变的前提下，重新生成展拍图。

相较于wanx-virtualmodel，virtualmodel-v2对任务文字描述的理解更加准确。

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **原始图像（base\_image\_url）** | **期望保留区域（mask\_image\_url）** | **全身形象描述（prompt）** | **人像面部描述（face\_prompt）** | **背景参考图像（background\_image\_url）** | **输出** |
| ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4644874271/p827236.png) | ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7068778171/p810523.png) | A woman stands on a rural road | good face, beautiful face, best quality. | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4644874271/p827239.png) | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4644874271/p827240.png) |

由于模型计算耗时较长，示例代码展示异步处理的调用方式，以避免请求超时。

您需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

curl

**1、创建虚拟模特生成任务**

接口返回任务ID，可根据任务ID查询图像生成的结果。

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/virtualmodel/generation' \
--header 'X-DashScope-Async: enable' \
--header "Authorization: Bearer $DASHSCOPE_API_KEY" \
--header 'Content-Type: application/json' \
--data '{
  "model": "virtualmodel-v2",
  "input": {
    "base_image_url": "https://huarong123.oss-cn-hangzhou.aliyuncs.com/image/%E7%9C%9F%E4%BA%BA%E6%A8%A1%E7%89%B9%E5%AE%9E%E6%8B%8D-%E5%A5%B3%20%281%29.jpeg",
    "mask_image_url": "https://huarong123.oss-cn-hangzhou.aliyuncs.com/image/image.jpg",
    "prompt": "A woman stands on a rural road",
    "face_prompt": "good face, beautiful face, best quality.",
    "background_image_url": "https://huarong123.oss-cn-hangzhou.aliyuncs.com/image/%E8%99%9A%E6%8B%9F%E6%A8%A1%E7%89%B9%E7%94%9F%E6%88%90%E8%83%8C%E6%99%AF%E5%9B%BE.png"
  },
  "parameters": {
      "short_side_size": "1024",
      "n": 1
  }
}'
```

**2、根据任务ID查询结果**

```curl
curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/{your_task_id} \
     -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
```

### **wanx-virtualmodel-V1**

wanx-virtualmodel，输入真人模特实拍图和中英文任务描述，模型在保持人物站姿不变的前提下，生成展拍图。

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **原始图像（base\_image\_url）** | **期望保留区域（mask\_image\_url）** | **全身形象描述（prompt）** | **人像面部描述（face\_prompt）** | **输出** |
| ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7749386271/p850516.png) | ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7068778171/p810523.png) | 一名年轻女子，身穿白色短裤，极简风格调色板，长镜头，双色效果，暗银色和浅粉色 | 一名年轻女子，面容娇好，最好的品质 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7749386271/p850911.png) |

由于模型计算耗时较长，示例代码展示异步处理的调用方式，以避免请求超时。API调用准备可参考 [虚拟模特](https://help.aliyun.com/zh/model-studio/virtual-model-api-details "")。

curl

**1、创建虚拟模特生成任务**

接口返回任务ID，可根据任务ID查询图像生成的结果。

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/aigc/virtualmodel/generation' \
--header 'X-DashScope-Async: enable' \
--header "Authorization: Bearer $DASHSCOPE_API_KEY" \
--header 'Content-Type: application/json' \
--data '{
  "model": "wanx-virtualmodel",
  "input": {
    "base_image_url": "https://huarong123.oss-cn-hangzhou.aliyuncs.com/image/%E7%9C%9F%E4%BA%BA%E6%A8%A1%E7%89%B9%E5%AE%9E%E6%8B%8D-%E5%A5%B3%20%281%29.jpeg",
    "mask_image_url": "https://huarong123.oss-cn-hangzhou.aliyuncs.com/image/image.jpg",
    "prompt": "一名年轻女子，身穿白色短裤，极简风格调色板，长镜头，双色效果（暗银色和浅粉色）",
    "face_prompt": "年轻女子，面容姣好，最高品质"
  },
  "parameters": {
    "short_side_size": "512",
    "n": 2
  }
}'
```

**2、根据任务ID查询结果**

```curl
curl -X GET https://dashscope.aliyuncs.com/api/v1/tasks/{your_task_id} \
     -H "Authorization: Bearer $DASHSCOPE_API_KEY"
```

## **场景示例**

### wanx-virtualmodel-V1

| **输入图** | **参数配置** | **输出图** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **输入图** | **参数配置** | **输出图** |
| **真人图示例** |
| ![image.jpeg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8068778171/p810512.jpeg) | "prompt":"一位年轻男性站着摆拍，在空荡的卧室里，窗户旁边，阳光照射进来，highly detailed，8K，极简主义风格"<br>"face\_prompt":"英俊的男性，脸好，脸美，质量上乘，杰作，（逼真度：1.4）"<br>"predefined\_face\_id":"boy3" | ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8068778171/p810516.png) |

### virtualmodel-V2

| **输入图** | **参数配置** | **输出图** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **输入图** | **参数配置** | **输出图** |
| **真人图示例** |
| ![image.jpeg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8068778171/p810519.jpeg) | "prompt":"a beautiful chinese girl, she stands in front of a pure pink background, she is smiling"<br>"face\_prompt":"good face, beautiful face, best quality." | ![image.png](<Base64-Image-Removed>) |
| ![image.jpeg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8068778171/p810520.jpeg) | "prompt":"a beautiful chinese girl, at a pastel-themed ice cream pop-up store, the sunny weather casts a warm glow, highlighting the colorful dessert displays and a clear blue sky, she is smiling"<br>"face\_prompt":"good face, beautiful face, best quality." | ![image.png](<Base64-Image-Removed>) |
| ![image.jpeg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8068778171/p810521.jpeg) | "prompt":"A woman stands on a rural road"<br>"face\_prompt":"good face, beautiful face, best quality."<br>"background\_image\_url":![image.png](<Base64-Image-Removed>) | ![image.png](<Base64-Image-Removed>) |
| ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8068778171/p810511.png) | "prompt":"A Europe handsome man, natural light, open subway platform, he is waiting, behind him is an incoming train. the train is coming from left to right"<br>"face\_prompt":"good face, beautiful face, best quality."<br>"aspect\_ratio":"4:3" | ![image.png](<Base64-Image-Removed>) |
| ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7068778171/p810514.png) | "prompt":"A person's hands are holding a bottle for display. The background is saffron yellow, and sunlight is shining on it."<br>"face\_prompt":"good face, beautiful face, best quality." | ![image.png](<Base64-Image-Removed>) |
| **人台图示例** |
| ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8068778171/p810506.png) | "prompt":"A woman stands in front of a quaint French flower shop, the charming streetscape embodying the essence of a picturesque scene in France. Brightly colored flowers in an array of varieties spill out from buckets and vases, creating a vibrant tapestry that decorates the storefront. The cobblestone path tells tales of a city rich in history, and the shop itself, with its traditional façade and large windows, invites passersby to pause and indulge in the visual feast of petals and leaves. good hands"<br>"face\_prompt":"good face, beautiful face, best quality."<br>"aspect\_ratio":"4:3"<br>"background\_image\_url":![image.png](<Base64-Image-Removed>)<br>"realPerson":false | ![image.png](<Base64-Image-Removed>) |
| ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8068778171/p810507.png) | "prompt":"A woman stands beside a luxurious swimming pool, her attire and posture suggesting leisure and relaxation. The pool's calm, crystal-clear waters reflect the surrounding opulent setting, with elegant lounge chairs inviting moments of repose under the sun. Perhaps it's a high-end resort or an upscale private villa, where the tiled pool deck and meticulously landscaped greenery speak of exclusivity and refinement."<br>"face\_prompt":"good face, beautiful face, best quality."<br>"aspect\_ratio":"4:3"<br>"realPerson":false | ![image.png](<Base64-Image-Removed>) |

## **API参考**

API的输入输出参数，请参见 [虚拟模特](https://help.aliyun.com/zh/model-studio/virtual-model-api-details "")。