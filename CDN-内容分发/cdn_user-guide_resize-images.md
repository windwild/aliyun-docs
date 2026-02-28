### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[性能优化](https://help.aliyun.com/zh/cdn/user-guide/performance-optimization/)[图像处理](https://help.aliyun.com/zh/cdn/user-guide/image-editing/)图片缩放

# 图片缩放

更新时间：2024-11-15 00:51:13

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：图片裁剪](https://help.aliyun.com/zh/cdn/user-guide/crop-images)[下一篇：图片旋转](https://help.aliyun.com/zh/cdn/user-guide/rotate-images)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

参数说明

操作示例

图片缩放包含按原图比例缩放、按条件缩放、自适应等比缩放和指定宽高缩放。当平台或应用程序对图片尺寸有特定要求，例如头像、封面图片等，可以通过图片缩放按特定尺寸或比例进行缩放，以适应不同的显示要求。

**说明**

- 阿里云CDN、DCDN和OSS的图片处理都是独立的功能，不能相互混用。

- 图像处理为付费服务，公测期间 **暂不收费**，收费时间另行通知。

- 当您使用图像处理功能时，由于不同图片格式在压缩算法上存在较大差异，因此不同图片格式之间相互转换可能会导致图片体积变大，例如：jpeg转webp、jpeg转png、png转webp。如果您需要降低图片文件的体积，建议您通过调整质量参数`quality`降低图片质量来实现。


## 参数说明

操作名称：`resize`

参数说明见下表。

**说明**

- 当任意参数值为负数时，将不对图片进行任何处理直接返回原图。

- 目前， **图片缩放** 功能仅支持缩小图片尺寸，尚不支持放大处理。若指定的参数超过原图的实际尺寸，则输出图片将以原图大小为准。


| **参数** | **说明** | **取值范围** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **说明** | **取值范围** |
| w | 指定目标缩放图的宽度。 | 默认值为0，宽×高不能超过16777216 px。 |
| h | 指定目标缩放图的高度。 |
| l | 指定目标缩放图的最长边。 |
| s | 指定目标缩放图的最短边。 |
| fw、fh | 指定目标缩放图的宽高。 |
| p | 按原图长宽比例进行缩放。 | \[0,100\] |

## 操作示例

下表列出了图片缩放方式和示例。

| **图片缩放方式** | **说明** | **示例** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **图片缩放方式** | **说明** | **示例** |
| 原图比例缩放 | 按原图长宽比例进行缩放。 | ```plaintext<br>example.com/image01.png?image_process=resize,p_80<br>``` |
| 按条件缩放 | 当图片大于等于1024000字节时，进行缩放，单位为Byte。<br>**说明**<br>这里的1024000为举例所用的示例值，实际取值需根据您的实际情况设置。 | ```plaintext<br>example.com/image01.png?image_process=resize,l_200/threshold,1024000<br>``` |
| 按长边固定自适应等比缩放 | 长边固定长度，短边自适应缩放。 | ```plaintext<br>example.com/image01.png?image_process=resize,l_200<br>``` |
| 按短边固定自适应等比缩放 | 短边固定长度，长边自适应缩放。 | ```plaintext<br>example.com/image01.png?image_process=resize,s_200<br>``` |
| 按宽固定自适应等比缩放 | 固定宽度，长度自适应。 | ```plaintext<br>example.com/image01.png?image_process=resize,w_200<br>``` |
| 按高固定自适应等比缩放 | 固定高度，宽边自适应。 | ```plaintext<br>example.com/image01.png?image_process=resize,h_200<br>``` |
| 指定宽高缩放 | 指定缩放的宽高。 | ```plaintext<br>example.com/image01.png?image_process=resize,fw_200,fh_200<br>``` |