### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) qwen-vl-plus-2025-07-10

# qwen-vl-plus-2025-07-10

更新时间：2026-02-12 02:59:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型介绍与计费

限流

如何使用

API参考

qwen-vl-plus-2025-07-10 是千问VL模型的快照版本，进一步增强了在监控视频内容上的理解能力。

**重要**

qwen-vl-plus-2025-07-10 模型目前属于邀测阶段，请您联系销售经理并告知阿里云的 uid 进行申请。

图像 Token 计算器

1\. 上传一张图片

2\. 选择模型

**模型系列:**--请选择--Qwen3-VLQwen2.5-VLQVQ

**具体模型:**--请选择--

3\. 设置参数

**`min_pixels`**

**`max_pixels`**

**高分辨率模式 (`vl_high_resolution_images`)**

不启用

启用


请先上传图片

视频 Token 计算器

1\. 上传一个视频

2\. 选择模型

**模型系列:**--请选择--Qwen3-VLQwen2.5-VLQVQ

**具体模型:**--请选择--

3\. 设置参数

**`fps` (抽帧频率)**

默认值：2.0，每隔1/fps秒提取1帧。

**`min_pixels`**

**`max_pixels`**

**`total_pixels`**

请先上传视频

计算图像Token

计算视频Token

图像 Token 计算器

1\. 上传一张图片

2\. 选择模型

**模型系列:**--请选择--Qwen3-VLQwen2.5-VLQVQ

**具体模型:**--请选择--

3\. 设置参数

**`min_pixels`**

**`max_pixels`**

**高分辨率模式 (`vl_high_resolution_images`)**

不启用

启用


请先上传图片

视频 Token 计算器

1\. 上传一个视频

2\. 选择模型

**模型系列:**--请选择--Qwen3-VLQwen2.5-VLQVQ

**具体模型:**--请选择--

3\. 设置参数

**`fps` (抽帧频率)**

默认值：2.0，每隔1/fps秒提取1帧。

**`min_pixels`**

**`max_pixels`**

**`total_pixels`**

请先上传视频

## **模型介绍与计费**

| **模型名称** | **版本** | **上下文长度** | **最大输入** | **最大输出** | **输入成本** | **输出成本** |
| --- | --- | --- | --- | --- | --- | --- |
| **（Token数）** | **（每千Token）** |
| --- | --- |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型名称** | **版本** | **上下文长度** | **最大输入** | **最大输出** | **输入成本** | **输出成本** |
| **（Token数）** | **（每千Token）** |
| qwen-vl-plus-2025-07-10<br>> 又称 qwen-vl-plus-0710<br>> 增强监控视频内容的理解能力 | 快照版 | 32,768 | 30,720<br>> 单图最大16384 | 8,096 | 0.00015元 | 0.0015元 |

> qwen-vl-plus-latest 模型的能力与 qwen-vl-plus-2025-05-07 相同，并不等同于 qwen-vl-plus-2025-07-10。 qwen-vl-plus-2025-07-10模型无免费额度。

## **限流**

| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| --- | --- |
| **每分钟调用次数（QPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每分钟调用次数（QPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-vl-plus-2025-07-10<br>（qwen-vl-plus-0710） | 60 | 100,000 |

## 如何使用

关于 qwen-vl-plus-2025-07-10 模型的使用方法请参见 [图像与视频理解](https://help.aliyun.com/zh/model-studio/vision "")。

## API参考

关于 qwen-vl-plus-2025-07-10 模型的输入输出参数，请参见 [千问](https://help.aliyun.com/zh/model-studio/qwen-api-reference/ "")。