### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据处理](https://help.aliyun.com/zh/oss/user-guide/data-transformation/)[图片处理](https://help.aliyun.com/zh/oss/user-guide/overview-17/)[旧版图片处理指南](https://help.aliyun.com/zh/oss/user-guide/earlier-version-of-img/)[图片缩放](https://help.aliyun.com/zh/oss/user-guide/resize-images/)按比例缩放

# 按比例缩放

更新时间：2025-03-12 23:17:17

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

参数

示例

图片处理支持通过指定百分比参数，让图片根据指定比例进行缩放。

## 参数

| **名称** | **描述** | **取值范围** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **名称** | **描述** | **取值范围** |
| p | 百分比。 | 1~1000<br>其中，小于100表示缩小，大于100表示放大。 |

**说明**

- 如果不指定格式，原图将默认转换成JPG格式；如果原图是PNG、WEBP、BMP格式，可能会导致变形。更多信息，请参见 [质量变换](https://help.aliyun.com/zh/oss/user-guide/image-quality-adjustment#concept-jrn-nm2-xdb "") 和 [格式转换](https://help.aliyun.com/zh/oss/user-guide/convert-image-formats#concept-xbg-x42-xdb "")。

- 当参数p跟w、h合用时，p直接作用于w、h （乘以p%），例如100w\_100h\_200p等效于200w\_200h。

- 图片按倍数放大时，单边最大长度不能超过4096px \* 4 。


## 示例

- 按比例放大两倍。

[https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@200p](https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@200p)

![缩放1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3094920761/p530543.jpg@200p)

- 按比例缩小到原来的1/2。

[https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@50p](https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@50p)

![缩放2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3094920761/p530554.jpg@50p)