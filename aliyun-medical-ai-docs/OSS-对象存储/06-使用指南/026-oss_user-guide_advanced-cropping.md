### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/) [用户指南](https://help.aliyun.com/zh/oss/user-guide/) [数据处理](https://help.aliyun.com/zh/oss/user-guide/data-transformation/) [图片处理](https://help.aliyun.com/zh/oss/user-guide/overview-17/) [旧版图片处理指南](https://help.aliyun.com/zh/oss/user-guide/earlier-version-of-img/) [图片裁剪](https://help.aliyun.com/zh/oss/user-guide/crop-image/) 高级裁剪

# 高级裁剪

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：索引切割](https://help.aliyun.com/zh/oss/user-guide/indexed-slice-1)[下一篇：图片旋转](https://help.aliyun.com/zh/oss/user-guide/rotate-images/)

该文章对您有帮助吗？

反馈

图片处理可以通过指定起始横坐标、纵坐标、裁剪的宽度和裁剪的高度对图进行高级裁剪。

## 参数

|     |     |     |
| --- | --- | --- |
| **名称** | **描述** | **取值范围** |
| a | 参数的类型：x-y-width-length<br>一共四个参数，每个参数之间以短划线（-）隔开。第一个参数表示起始点x坐标（以左上角为原点），第二个参数表示起始点y坐标，第三个参数表示要裁剪的宽度，第四个参数表示要裁剪的高度。<br>例如：100-50-200-150a表示从点（100, 50）裁剪大小为（200, 150）的图片。<br>**说明** <br>可以将第三、第四个参数置为0，表示裁剪到图片的边缘，如100-50-0-0a表示从点（100, 50）裁剪到图片的最后。 | width、height的范围是1~4096。 |

## 注意事项

- 如果不指定格式，原图将默认转换成JPG，PNG、WEBP、BMP格式的图可能会改变图像的分辨率或比例，导致图像变形。详情请参见 [质量变换](https://help.aliyun.com/zh/oss/user-guide/image-quality-adjustment "") 和 [格式转换](https://help.aliyun.com/zh/oss/user-guide/convert-image-formats "")。

- 如果指定的起始坐标大于原图，将返回BadRequest错误：Advance cut's position is out of image。

- 如果指定的宽度和高度超过原图，将裁剪到原图的结尾。


## 使用示例

- 从（100, 50）裁剪到图的结束。

[https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@100-50-0-0a](https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@100-50-0-0a)

![裁剪1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5697920761/p530648.jpg@100-50-0-0a)

- 从（100, 50）裁剪100px \* 100px。

[https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@100-50-100-100a](https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@100-50-100-100a)

![裁剪2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5697920761/p530650.jpg@100-50-100-100a)