### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据处理](https://help.aliyun.com/zh/oss/user-guide/data-transformation/)[图片处理](https://help.aliyun.com/zh/oss/user-guide/overview-17/)[图片处理参数](https://help.aliyun.com/zh/oss/user-guide/img-parameters/)图片水印

# 图片水印

更新时间：2025-05-26 00:00:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用场景

注意事项

参数说明

水印编码

操作方式

常见问题

如何使用网络图片或本地图片作为水印图片？

添加文字水印时提示“font content is too large”怎么办？

私有文件添加图片水印失败怎么办？

添加图片水印时可以为水印增加背景色么？

如何使用签名URL访问图片？

添加水印时支持垂直排列么？

如何根据图片的大小动态调整水印的大小？

可以同时为图片增加几个水印？

为保护OSS存储的图片或文件的所有权，防止资源未经授权被复制或使用，您可以为存储的资源增加水印。

## **使用场景**

- 版权保护：为保护自己的作品不被未授权使用或复制，需要在图片上加上水印来标识版权。

- 品牌推广：企业或个人为了宣传自己的品牌或标识，会在图片、视频或文档上加上带有品牌标志或名称的水印。

- 防止篡改：在某些官方文件、证书或报告上添加水印，可以增加篡改的难度，减少文件被伪造的风险。

- 抵制盗图：在网络环境中，图片很容易被他人下载和再次发布。加水印可以作为一种警示，减少他人直接盗用图片的情况。

- 法律要求：某些情况下，法律或合同条款可能要求在特定内容发布时必须加上水印，以符合规定。


## 注意事项

- 您可以通过文件URL、SDK、API方式设置图片处理参数。本文以文件URL为例进行介绍。文件URL仅适用于公共访问的图片。如果是私有访问的图片，请使用SDK、API处理图片。更多信息，请参见 [图片处理操作方式](https://help.aliyun.com/zh/oss/user-guide/img-implementation-modes#concept-m4f-dcn-vdb "")。


- 图片水印只能使用当前存储空间内的图片，网络或本地图片需上传至当前存储空间内方可使用。

- 图片水印目前仅支持JPG、PNG、BMP、WebP、TIFF格式。

- 单张图片最多支持添加3张不同的图片水印，且各个图片水印的位置不能完全重叠。

- 文字水印暂不支持繁体中文。


## 参数说明

操作名称：watermark

相关参数如下：

- 基础参数




| **参数** | **是否必须** | **描述** | **取值范围** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **是否必须** | **描述** | **取值范围** |
| t | 否 | 指定图片水印或水印文字的透明度。 | \[0,100\] <br>默认值：100， 表示透明度100%（不透明）。 |
| g | 否 | 指定水印在图片中的位置。 | - nw：左上<br>    <br>  - north：中上<br>    <br>  - ne：右上<br>    <br>  - west：左中<br>    <br>  - center：中部<br>    <br>  - east：右中<br>    <br>  - sw：左下<br>    <br>  - south：中下<br>    <br>  - se（默认值）：右下<br>    <br>详情请参见下方基准点图片。 |
| x | 否 | 指定水印的水平边距， 即距离图片边缘的水平距离。这个参数只有当水印位置是左上、左中、左下、右上、右中、右下才有意义。 | \[0,4096\] <br>默认值：10 <br>单位：像素（px） |
| y | 否 | 指定水印的垂直边距，即距离图片边缘的垂直距离， 这个参数只有当水印位置是左上、中上、右上、左下、中下、右下才有意义。 | \[0,4096\] <br>默认值：10 <br>单位：像素（px） |
| voffset | 否 | 指定水印的中线垂直偏移。当水印位置在左中、中部、右中时，可以指定水印位置根据中线往上或者往下偏移。 | \[-1000,1000\] <br>默认值：0<br>单位：像素（px） |
| fill | 否 | 指定是否将图片水印或文字水印铺满原图。<br>**说明**<br>如果您需要使用图片水印平铺功能，请在 [配额中心](https://oss.console.aliyun.com/more-tool/quota-setting) 申请。 | - 1：将图片水印或文字水印铺满原图。<br>    <br>  - 0（默认值）：不将图片水印或文字水印铺满全图。 |
| padx | 否 | 水印平铺时单个水印间的水平间隔。仅在水印平铺开启时有效。 | \[0,4096\]<br>默认值：0<br>单位：像素（px） |
| pady | 否 | 水印平铺时单个水印间的垂直间隔。仅在水印平铺开启时有效。 | \[0,4096\]<br>默认值：0<br>单位：像素（px） |



水平边距、垂直边距、中线垂直偏移不仅可以调节水印在图片中的位置，当图片存在多重水印时，还可以调节水印在图中的布局。



区域数值以及每个区域对应的基准点如下图所示。![origin](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2252359951/p2648.png)

- 图片水印参数




| **参数** | **是否必须** | **描述** | **取值范围** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **是否必须** | **描述** | **取值范围** |
| image | 是 | 用于指定作为图片水印Object的完整名称，Object名称需进行Base64编码。详情请参见 [水印编码](https://help.aliyun.com/zh/oss/user-guide/add-watermarks#watermark "")。请注意，水印图片的完整路径需要进行 URL 安全的 Base64 编码，以确保在 URL 中正确传递。例如，如果水印图片位于 `image` 目录下，文件名为 `panda.png`，则需要对完整路径 `image/panda.png` 进行 URL 安全的 Base64 编码，得到 `aW1hZ2UvcGFuZGEucG5n`。<br>**说明**<br>水印图片只能使用当前存储空间内的Object。 | Base64编码后的字符串。 |

- 水印图片预处理参数

您可以使用 [图片缩放](https://help.aliyun.com/zh/oss/user-guide/resize-images-4#concept-hxj-c4n-vdb "")、 [自定义裁剪](https://help.aliyun.com/zh/oss/user-guide/custom-crop#concept-bbn-14s-vdb "")、 [索引切割](https://help.aliyun.com/zh/oss/user-guide/indexed-slice#concept-ecq-cqs-vdb "")、 [圆角矩形](https://help.aliyun.com/zh/oss/user-guide/rounded-rectangle-4#concept-xts-dss-vdb "") 及 [图片旋转](https://help.aliyun.com/zh/oss/user-guide/auto-rotate-4#concept-ugq-tvs-vdb "") 操作中的所有参数对水印图片进行预处理。此外，水印图片在进行预处理时，还额外支持缩放参数P：




| **参数** | **描述** | **取值范围** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **描述** | **取值范围** |
| P | 指定图片水印按照要添加水印的原图的比例进行缩放，取值为缩放的百分比。如设置参数值为10，如果原图为100×100， 则图片水印大小为10×10。当原图变成了200×200，则图片水印大小为20×20。 | \[1,100\] |

- 文字水印参数




| **参数** | **是否必须** | **描述** | **取值范围** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **是否必须** | **描述** | **取值范围** |
| text | 是 | 指定文字水印的文字内容，文字内容需进行Base64编码。详情请参见 [水印编码](https://help.aliyun.com/zh/oss/user-guide/add-watermarks#watermark "")。 | Base64编码之前中文字符串的最大字节长度为64个字符。 |
| type | 否 | 指定文字水印的字体，字体名称需进行Base64编码。 | 支持的字体及字体编码详情请参见 [文字类型编码对应表](https://help.aliyun.com/zh/oss/user-guide/add-watermarks#table-ipy-1vu-isp "")。<br>默认值：wqy-zenhei（ 编码后的值为d3F5LXplbmhlaQ） |
| color | 否 | 指定文字水印的文字颜色，参数值为RGB颜色值。 | RGB颜色值，例如：000000表示黑色，FFFFFF表示白色。 <br>默认值：000000（黑色） |
| size | 否 | 指定文字水印的文字大小。 | (0,1000\] <br>默认值：40<br>单位：px |
| shadow | 否 | 指定文字水印的阴影透明度。 | \[0,100\]<br>默认值：0，表示没有阴影。 |
| rotate | 否 | 指定文字顺时针旋转角度。 | \[0,360\]<br>默认值：0，表示不旋转。 |



type参数中可选的文字类型及编码如下表所示。




| **参数值** | **中文含义** | **编码值** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数值** | **中文含义** | **编码值** |
| wqy-zenhei | 文泉驿正黑 | d3F5LXplbmhlaQ |
| wqy-microhei | 文泉微米黑 | d3F5LW1pY3JvaGVp |
| fangzhengshusong | 方正书宋 | ZmFuZ3poZW5nc2h1c29uZw |
| fangzhengkaiti | 方正楷体 | ZmFuZ3poZW5na2FpdGk |
| fangzhengheiti | 方正黑体 | ZmFuZ3poZW5naGVpdGk |
| fangzhengfangsong | 方正仿宋 | ZmFuZ3poZW5nZmFuZ3Nvbmc |
| droidsansfallback | DroidSansFallback | ZHJvaWRzYW5zZmFsbGJhY2s |

- 图文混合水印参数




| **参数** | **是否必须** | **描述** | **取值范围** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **是否必须** | **描述** | **取值范围** |
| order | 否 | 指定文字和图片水印的前后顺序。 | 0、1 <br>  - 0（默认值）：表示图片水印在前。<br>    <br>  - 1：表示文字水印在前。 |
| align | 否 | 指定文字水印和图片水印的对齐方式。 | 0、1、2 <br>  - 0：表示文字水印和图片水印上对齐。<br>    <br>  - 1：表示文字水印和图片水印中对齐。<br>    <br>  - 2（默认值）：表示文字水印和图片水印下对齐。 |
| interval | 否 | 指定文字水印和图片水印间的间距。 | \[0,1000\]<br>默认值：0<br>单位：px |


## 水印编码

在添加水印操作中，文字水印的文字内容、文字字体、图片水印的水印图片名称等参数需要进行URL安全的Base64编码。编码步骤如下：

1. 将内容编码成Base64。

2. 将结果中的部分编码替换。

   - 将结果中的加号（+）替换成短划线（-）。

   - 将结果中的正斜线（/）替换成下划线（\_）。

   - 将结果中尾部的所有等号（=）省略。

推荐通过 [base64url encoder](https://simplycalc.com/base64url-encode.php) 对文字水印的文字内容、文字颜色、文字字体、图片水印的水印图片名称等参数进行编码。

**重要**

水印编码后的内容仅应用在水印操作的特定参数中，请勿将其用在签名字符串（Signature）中。

## **操作方式**

对公共读或者公共读写的图片添加水印

对私有图片添加水印

您可以通过在文件URL中直接添加图片处理参数的方式，对公共读或者公共读写的图片添加水印。

#### **示例一：添加文字水印**

以杭州地域名为oss-console-img-demo-cn-hangzhou-3az的Bucket中的图片example.jpg为例，图片访问URL为 [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg)![原图](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6929730761/p529184.jpg)

为example.jpg图片添加文字水印示例如下：

- 快速添加Hello World的文字水印



对文字水印的内容Hello World进行URL安全的Base64编码。具体操作，请参见 [水印编码](https://help.aliyun.com/zh/oss/user-guide/add-watermarks#watermark "")。编码结果为`SGVsbG8gV29ybGQ`，图片处理URL为 [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,text\_SGVsbG8gV29ybGQ](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,text_SGVsbG8gV29ybGQ)。![Hello World](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5929730761/p529185.jpg)

- 添加文字水印时配置多个图片处理参数

为example.jpg图片添加Hello World的文字水印的同时，需要对水印文字以及原图做如下相应处理：


  - 将example.jpg缩略为宽高300：`resize,w_300,h_300`

  - 水印文字字体为文泉驿正黑：`type_d3F5LXplbmhlaQ`（d3F5LXplbmhlaQ是文泉驿正黑经过Base64编码后的值）

  - 水印内容为“Hello World”：`text_SGVsbG8gV29ybGQ`

  - 水印文字颜色为白色、字体大小为30：`color_FFFFFF,size_30`

  - 文字阴影透明度为50%：`shadow_50`

  - 水印文字位置是右下、水平边距10、中线垂直偏移10：`g_se,x_10,y_10`


图片处理的URL为： [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/resize,w\_300,h\_300/watermark,type\_d3F5LXplbmhlaQ,size\_30,text\_SGVsbG8gV29ybGQ,color\_FFFFFF,shadow\_50,t\_100,g\_se,x\_10,y\_10](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/resize,w_300,h_300/watermark,type_d3F5LXplbmhlaQ,size_30,text_SGVsbG8gV29ybGQ,color_FFFFFF,shadow_50,t_100,g_se,x_10,y_10)![图片处理1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6929730761/p529186.jpg)

#### **示例二：添加图片水印**

为example.jpg图片添加图片水印示例如下：

- 快速添加名为 [panda.png](https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/panda.png) 的水印图片



对水印图片名称为panda.png进行URL安全的Base64编码，编码结果为`cGFuZGEucG5n`，图片处理URL为 [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,image\_cGFuZGEucG5n](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,image_cGFuZGEucG5n)。



请注意，水印图片的完整路径需要进行 URL 安全的 Base64 编码，以确保在 URL 中正确传递。例如，如果水印图片位于 `image` 目录下，文件名为 `panda.png`，则需要对完整路径 `image/panda.png` 进行 URL 安全的 Base64 编码，得到 `aW1hZ2UvcGFuZGEucG5n`。




![图片处理2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6929730761/p531303.jpg)

- 添加图片水印时配置多个图片处理参数

为example.jpg图片添加图片水印panda.png的同时，需要对图片水印以及原图做如下相应处理：


  - 将example.jpg缩略为宽高300：`resize,w_300,h_300`

  - 将example.jpg图片质量设为90%：`quality,q_90`

  - 添加水印图片panda.png：`watermark,image_cGFuZGEucG5n`（cGFuZGEucG5n是panda.png进行Base64编码后的值）

  - 水印图片透明度90%：`t_90`

  - 水印图片位于原图的右下方、水平边距10、中线垂直偏移10：`g_se,x_10,y_10`


图片处理的URL为： [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/resize,w\_300,h\_300/quality,q\_90/watermark,image\_cGFuZGEucG5n,t\_90,g\_se,x\_10,y\_10](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/resize,w_300,h_300/quality,q_90/watermark,image_cGFuZGEucG5n,t_90,g_se,x_10,y_10)![图片处理3](<Base64-Image-Removed>)

- 对图片水印进行预处理后配置多个图片处理参数

为example.jpg图片添加图片水印panda.png的同时，需要对图片水印以及原图做如下相应处理：


  - 将example.jpg缩略为宽300：`resize,w_300`

  - 将水印图片panda.png进行预处理（缩放30%）：`image_cGFuZGEucG5nP3gtb3NzLXByb2Nlc3M9aW1hZ2UvcmVzaXplLFBfMzA`（`cGFuZGEucG5nP3gtb3NzLXByb2Nlc3M9aW1hZ2UvcmVzaXplLFBfMzA`为`panda.png?x-oss-process=image/resize,P_30`经过Base64编码后的值）

  - 水印的透明度为90%、位置是右下、水平边距是10、中线垂直偏移是10：`t_90,g_se,x_10,y_10`


图片处理的URL为： [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/resize,w\_300/watermark,image\_cGFuZGEucG5nP3gtb3NzLXByb2Nlc3M9aW1hZ2UvcmVzaXplLFBfMzA,t\_90,g\_se,x\_10,y\_10](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/resize,w_300/watermark,image_cGFuZGEucG5nP3gtb3NzLXByb2Nlc3M9aW1hZ2UvcmVzaXplLFBfMzA,t_90,g_se,x_10,y_10)![图片处理4](<Base64-Image-Removed>)

- 添加多个图片水印

为example.jpg图片添加2张图片水印，即panda.png和Tulips.jpg。


  - 对水印图片名称panda.png进行URL安全的Base64位编码，编码结果为`cGFuZGEucG5n`，图片参数处理结果为`watermark,image_cGFuZGEucG5n`。

  - 对水印图片名称Tulips.jpg进行URL安全的Base64位编码，编码结果为`VHVsaXBzLmpwZw`，图片水印位于原图左中部，水平边距10，中线垂直偏移10，图片参数处理结果为`watermark,image_VHVsaXBzLmpwZw,g_west,x_10,y_10`。


图片处理的URL为：

[https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,image\_cGFuZGEucG5n/watermark,image\_VHVsaXBzLmpwZw,g\_west,x\_10,y\_10](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,image_cGFuZGEucG5n/watermark,image_VHVsaXBzLmpwZw,g_west,x_10,y_10)![2个水印](<Base64-Image-Removed>)

#### **示例三：添加图片和文字混合水印**

为example.jpg图片添加图片和文字混合水印的示例如下：

结合以上示例中panda.png以及Hello World的编码结果，可得出图片处理的URL为 [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,image\_cGFuZGEucG5nP3gtb3NzLXByb2Nlc3M9aW1hZ2UvcmVzaXplLFBfMzA,text\_SGVsbG8gV29ybGQ](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,image_cGFuZGEucG5nP3gtb3NzLXByb2Nlc3M9aW1hZ2UvcmVzaXplLFBfMzA,text_SGVsbG8gV29ybGQ)。![图片处理5](<Base64-Image-Removed>)

您可以通过阿里云SDK以及REST API对私有图片添加水印。

使用阿里云SDK

使用REST API

以下仅列举常见SDK为图片添加水印的代码示例。如需使用其他SDK为图片添加水印的代码示例，请参见 [SDK简介](https://help.aliyun.com/zh/oss/developer-reference/overview-21#concept-dcn-tp1-kfb "")。

Java

PHP

Python

Go

要求使用3.17.4及以上版本的Java SDK。

```java
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.model.GetObjectRequest;
import java.io.File;

public class Demo {
    public static void main(String[] args) throws Throwable {
        // Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 填写Endpoint对应的Region信息，例如cn-hangzhou。
        String region = "cn-hangzhou";
        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
        // 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写Object完整路径。Object完整路径中不能包含Bucket名称。
        String objectName = "src.jpg";
        // 填写本地文件的完整路径，例如D:\\localpath\\example-new.jpg。如果指定的本地文件存在会覆盖，不存在则新建。
        String pathName = "D:\\dest.jpg";

        // 创建OSSClient实例。
        // 当OSSClient实例不再使用时，调用shutdown方法以释放资源。
        ClientBuilderConfiguration clientBuilderConfiguration = new ClientBuilderConfiguration();
        clientBuilderConfiguration.setSignatureVersion(SignVersion.V4);
        OSS ossClient = OSSClientBuilder.create()
                .endpoint(endpoint)
                .credentialsProvider(credentialsProvider)
                .clientConfiguration(clientBuilderConfiguration)
                .region(region)
                .build();

        try {
            // 为图片添加Hello World文字水印。
            String image = "image/watermark,text_SGVsbG8gV29ybGQ";
            GetObjectRequest request = new GetObjectRequest(bucketName, objectName);
            request.setProcess(image);
            // 将处理后的图片命名为example-new.jpg并保存到本地。
            // 如果未指定本地路径只填写了文件名称（例如example-new.jpg），则文件默认保存到示例程序所属项目对应本地路径中。
            ossClient.getObject(request, new File("D:\\dest.jpg"));
        } catch (OSSException oe) {
            System.out.println("Caught an OSSException, which means your request made it to OSS, "
                    + "but was rejected with an error response for some reason.");
            System.out.println("Error Message:" + oe.getErrorMessage());
            System.out.println("Error Code:" + oe.getErrorCode());
            System.out.println("Request ID:" + oe.getRequestId());
            System.out.println("Host ID:" + oe.getHostId());
        } catch (ClientException ce) {
            System.out.println("Caught an ClientException, which means the client encountered "
                    + "a serious internal problem while trying to communicate with OSS, "
                    + "such as not being able to access the network.");
            System.out.println("Error Message:" + ce.getMessage());
        } finally {
            if (ossClient != null) {
                ossClient.shutdown();
            }
        }
    }
}
```

要求使用PHP SDK 2.7.0及以上版本。

```php
<?php
if (is_file(__DIR__ . '/../autoload.php')) {
    require_once __DIR__ . '/../autoload.php';
}
if (is_file(__DIR__ . '/../vendor/autoload.php')) {
    require_once __DIR__ . '/../vendor/autoload.php';
}
use OSS\Credentials\EnvironmentVariableCredentialsProvider;
use OSS\OssClient;

// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
$provider = new EnvironmentVariableCredentialsProvider();
// yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
$endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
// 填写Bucket名称，例如examplebucket。
$bucket= "examplebucket";
// 填写Object完整路径，例如exampledir/exampleobject.jpg。Object完整路径中不能包含Bucket名称。
$object = "src.jpg";
// 填写本地文件的完整路径，例如D:\\localpath\\example-new.jpg。如果指定的本地文件存在会覆盖，不存在则新建。
// 如果未指定本地路径只填写了本地文件名称（例如example-new.jpg），则文件默认保存到示例程序所属项目对应本地路径中。
$download_file = "D:\\dest.jpg";

$config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
        "signatureVersion" => OssClient::OSS_SIGNATURE_VERSION_V4,
        // 填写阿里云通用Region ID。
        "region" => "cn-hangzhou"
    );
$ossClient = new OssClient($config);

// 为图片添加Hello World的文字水印。
$image = "image/watermark,text_SGVsbG8gV29ybGQ";

$options = array(
    OssClient::OSS_FILE_DOWNLOAD => $download_file,
    OssClient::OSS_PROCESS => $image);

// 将处理后的图片保存到本地。
$ossClient->getObject($bucket, $object, $options);
```

要求使用Python SDK 2.18.4及以上版本。

```python
# -*- coding: utf-8 -*-
import oss2
from oss2.credentials import EnvironmentVariableCredentialsProvider

# 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
auth = oss2.ProviderAuthV4(EnvironmentVariableCredentialsProvider())
# yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
## 填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
endpoint = 'https://oss-cn-hangzhou.aliyuncs.com'
# 填写阿里云通用Region ID。
region = 'cn-hangzhou'
bucket = oss2.Bucket(auth, endpoint, 'examplebucket', region=region)
# 指定原图名称。如果图片不在Bucket根目录，需携带图片完整路径，例如exampledir/example.jpg。
key = 'src.jpg'
# 指定处理后的图片名称。
new_pic = 'D:\\dest.jpg'

# 为图片添加Hello World的文字水印。
image = 'image/watermark,text_SGVsbG8gV29ybGQ'
bucket.get_object_to_file(key, new_pic, process=image)
```

要求使用Go SDK 3.0.2及以上版本。

```go
package main

import (
	"fmt"
	"os"

	"github.com/aliyun/aliyun-oss-go-sdk/oss"
)

func HandleError(err error) {
	fmt.Println("Error:", err)
	os.Exit(-1)
}

func main() {
	// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
	provider, err := oss.NewEnvironmentVariableCredentialsProvider()
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(-1)
	}

	// 创建OSSClient实例。
	// yourEndpoint填写Bucket对应的Endpoint，以华东1（杭州）为例，填写为https://oss-cn-hangzhou.aliyuncs.com。其它Region请按实际情况填写。
	client, err := oss.New("https://oss-cn-hangzhou.aliyuncs.com", "", "", oss.SetCredentialsProvider(&provider), oss.AuthVersion(oss.AuthV4), oss.Region("cn-hangzhou"))
	if err != nil {
		HandleError(err)
	}

	// 指定原图所在的Bucket名称，例如examplebucket。
	bucketName := "examplebucket"
	bucket, err := client.Bucket(bucketName)
	if err != nil {
		HandleError(err)
	}

	// 指定原图名称。如果图片不在Bucket根目录，需携带图片完整路径，例如exampledir/example.jpg。
	sourceImageName := "src.jpg"
	// 指定处理后的图片名称。
	targetImageName := "D://dest.jpg"
	// 为图片添加Hello World的文字水印。
	image := "image/watermark,text_SGVsbG8gV29ybGQ"
	err = bucket.GetObjectToFile(sourceImageName, targetImageName, oss.Process(image))
	if err != nil {
		HandleError(err)
	}
}
```

如果您的程序自定义要求较高，您可以直接发起REST API请求。直接发起REST API请求需要手动编写代码计算签名。更多信息，请参见 [签名版本4（推荐）](https://help.aliyun.com/zh/oss/developer-reference/recommend-to-use-signature-version-4 "")。

您可以通过在GetObject接口中添加水印参数的方式来处理图片。

```xml
GET /oss.jpg?x-oss-process=image/watermark,w_100 HTTP/1.1
Host: oss-example.oss-cn-hangzhou.aliyuncs.com
Date: Fri, 28 Oct 2022 06:40:10 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

## 常见问题

### 如何使用网络图片或本地图片作为水印图片？

通过OSS的图片处理为图片添加图片水印时，仅可以使用相同存储空间内的图片作为水印图片。若您希望使用网络图片或本地图片作为水印图片，需要先将图片上传到原图所在存储空间，之后再使用上传的图片作为水印图片处理原图。

### 添加文字水印时提示“font content is too large”怎么办？

通过OSS的图片处理为图片添加文字水印时，最长不能超过64个字符（1个汉字计为3个字符）。当提示“font content is too large”时，建议您缩短文字长度，然后为图片添加文字水印。更多信息，请参见 [示例一：添加文字水印](https://help.aliyun.com/zh/oss/user-guide/add-watermarks#section-tj2-dbv-vdb "")。

### 私有文件添加图片水印失败怎么办？

私有文件的访问URL带有签名。OSS不支持在带签名的URL后直接添加图片处理参数。如果您想要对私有文件进行图片处理，需要将图片处理参数加入到签名中。更多信息，请参见 [生成带图片处理参数的文件签名URL](https://help.aliyun.com/zh/oss/developer-reference/img-2#section-iz9-5lh-m0p "")。

### 添加图片水印时可以为水印增加背景色么？

不可以。

### 如何使用签名URL访问图片？

私有文件的访问URL带有签名。OSS不支持在带签名的URL后直接添加图片处理参数。如果您想要对私有文件进行图片处理，需要将图片处理参数加入到签名中。更多信息，请参见 [图片处理](https://help.aliyun.com/zh/oss/developer-reference/img-2#concept-agt-jgc-kfb "")。

### 添加水印时支持垂直排列么？

如果您希望在添加水印时垂直排列，可以拆分成多个水印操作，通过多个watermark算子实现垂直排列效果。

例如： [https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,text\_SGVsbG8gV29ybGQ/watermark,text\_SGVsbG8gV29ybGQy,y\_60](https://oss-console-img-demo-cn-hangzhou-3az.oss-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/watermark,text_SGVsbG8gV29ybGQ/watermark,text_SGVsbG8gV29ybGQy,y_60)

![垂直水印](<Base64-Image-Removed>)

### 如何根据图片的大小动态调整水印的大小？

OSS的图片处理不支持动态调整水印的大小，在实际应用中，您可能需要编写自定义逻辑来检测图片的尺寸，然后根据一定的比例或规则来决定文字水印的大小。这一步骤需要您在调用OSS接口前，在客户端或服务端代码中实现。

### 可以同时为图片增加几个水印？

3个。如果您需要为图片增加更多水印，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请。