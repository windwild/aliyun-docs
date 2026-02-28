### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据处理](https://help.aliyun.com/zh/oss/user-guide/data-transformation/)[图片处理](https://help.aliyun.com/zh/oss/user-guide/overview-17/)图片处理常见问题

# 图片处理常见问题

更新时间：2025-02-24 01:44:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：错误响应](https://help.aliyun.com/zh/oss/user-guide/common-errors)[下一篇：新旧版本图片处理服务及使用说明](https://help.aliyun.com/zh/oss/user-guide/differences-between-the-old-and-new-versions-of-img)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

为什么不同的图片处理参数返回的ETag值相同

如何通过图片处理持久化存储多个规格的图片

为什么使用浏览器预览图片时直接下载

为什么GIF动图经过图片处理后变成静态图

处理图片时出现MemLimitExceeded报错

访问图片时出现The channel can be only accessed using style报错

旋转图片时出现Picture exceed the maximum allowable rotation range报错

开启了OSS违规检测，图片被判定违规，但是外部还能访问到

通过OSS获取主色调和图片不符

图片水印合成出现黑线

通过CDN回源OSS图片处理不生效

图片压缩后颜色变亮了

图片在本地可以正常打开，进行图片处理时提示已损坏

存储在OSS内的图片旋转了90度

经过CDN加速后图片处理没有效果

使用图片处理出现“Picture exceed the maximum allowable rotation range”报错

苹果手机端携带了图片处理参数访问经过CDN加速的图片时变成空白图片，刷新后可以访问，电脑访问正常

存储在OSS的原图和经过图片处理后的图片都打不开

图片处理完后背景色多了一条分割线

图片处理报错“BadRequest”

图片处理报错“InvalidArgument”

图片处理报错“BadWebPImage”

OSS能否识别请求的自定义query参数动态缩放

一个文字水印是否可以分成两行显示？一个图片是否可以添加多个文字水印？

为何图片经过OSS缩略之后尺寸变大了？

如何通过调整图片的属性来控制图片占用的存储空间大小？

OSS图片处理时同时携带图片处理参数和versionId，versionId不生效，签名URL指向最新版本的文件

本文主要介绍您在使用OSS图片处理时可能遇到的一些常见问题及处理方法。

如果有明显的参数超过显示等问题，使用OSS的 `?x-oss-process=image/info`参数查看图片信息。OSS中的图片单边长度不能超过4096，乘积不能高于4096\*4096 。

## **为什么不同的图片处理参数返回的** ETag **值相同**

图片处理场景下ETag表示原始Object的唯一标志符，该ETag与处理后的结果图片无关。

## 如何通过图片处理持久化存储多个规格的图片

如果您需要存储原图外的小图，可以通过图片处理持久化方式，在请求中添加转存参数，将处理后的图片保存至指定存储空间（Bucket）。更多信息，请参见 [图片处理持久化](https://help.aliyun.com/zh/oss/user-guide/save-processed-images "")。

## 为什么使用浏览器预览图片时直接下载

如果您使用浏览器预览图片时直接进行下载，可能是因为当前浏览器不支持预览的图片格式。建议您更换兼容图片格式的浏览器（例如Chrome浏览器）再次尝试预览。

## 为什么GIF动图经过图片处理后变成静态图

GIF动图在进行图片缩放、裁剪或添加水印操作后仍保留为动图。但如果执行其他图片处理操作，GIF动图会变成静态图。

## 处理图片时出现MemLimitExceeded报错

问题分析：使用图片处理服务时，有图片大小限制，除图片旋转对应的原图高或者宽不能超过4,096 px外，其他图片操作对应的原图高或者宽不能超过30,000 px，且总像素不能超过2.5亿 px。当图片超过限制时，会出现MemLimitExceeded报错。

**说明**

动态图片（例如GIF图片）的像素计算方式为`宽*高*图片帧数`；非动态图片（例如PNG图片）的像素计算方式为`宽*高`。

解决方案：您可以通过图片缩放参数（`resize`），调整OSS内存储的图片大小，以满足图片大小限制。关于如何使用图片缩放参数，请参见 [图片缩放](https://help.aliyun.com/zh/oss/user-guide/resize-images-4#concept-hxj-c4n-vdb "")。

## 访问图片时出现The channel can be only accessed using style报错

问题分析：开启原图保护后，匿名访问者只能使用携带样式参数的请求或通过签名URL访问原图。如果使用图片处理参数设置图片（例如`?x-oss-process=image/format,webp`），将出现该报错。

解决方案：建议您为图片关闭原图保护。关于原图保护的更多信息，请参见 [原图保护](https://help.aliyun.com/zh/oss/user-guide/protect-source-images#concept-dsx-1rc-wdb "")。

## 旋转图片时出现Picture exceed the maximum allowable rotation range报错

问题分析：出现这种问题基本都是原图的单边长度超过了4096的限制，图片宽度\*高度超过了4096\*4096。

排查步骤：

1. 使用OSS的 `?x-oss-process=image/info` 参数获取图片的信息判断是否超过限制。![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6095649951/p34432.png)

2. 查看 `ImageWidth`值是5100，超过4096的限制。


解决方法：使用 `auto-orient,0` 参数关闭自适应，再使用 `resize` 参数调整图片大小，最后旋转图片，确保调整后的图片尺寸在允许的范围内。例如：http://test.oss-cn-beijing.aliyuncs.com/123/myphoto5.jpg?x-oss-process=image/auto-orient,0/resize,m\_lfit,h\_2000,w\_2000,limit\_1/rotate,90

## 开启了OSS违规检测，图片被判定违规，但是外部还能访问到

OSS没有封禁功能，违规图片被冻结后不会在控制台显示，但仍保存在bucket中。如果您不希望违规图片再被访问，需要手动删除。详情请参见 [OSS 违规检测](https://help.aliyun.com/document_detail/28423.html#concept-i31-5cr-52b "")。

## 通过OSS获取主色调和图片不符

问题分析：主色调计算基于整个图片的色调平均值，而非屏幕颜色占比，计算逻辑如下：

1. 计算图片的平均色调 (avg\_hue)。

2. 找出色差大于阈值的“醒目像素”。

3. 计算“醒目像素”的颜色均值，作为主色调。


解决方法：可以使用 `?x-oss-process=image/average-hue` 参数获取OSS图片的主色调参数。

## 图片水印合成出现黑线

![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7095649951/p34601.png)

问题分析：在将两张图片叠加以添加水印时，可能会出现黑线现象。这通常是由于两张图片的RGB值不同，叠加后因色差产生的。这种黑线并非由图片处理工具引起，而是由于图片本身的颜色差异所致。

使用`?x-oss-process=image/average-hue`参数可查询图片RGB的参数，可在图片链接后加这个参数判断两个图片的RGB参数是否一致。有关RGB的介绍，请参见 [RGB](https://yq.aliyun.com/articles/421836?spm=5176.10695662.1996646101.searchclickresult.3bd79460fu5pVr)。

解决方法：案例中背景图RGB参数为 “0x0e0e0e”，水印的 RGB 参数为 “0xffffff”，增加水印会出现类似边框的效果。通过调整水印的透明度参数 `t`（取值范围1-100）来去除边框效果。

例如：http://image-demo.img-cn-hangzhou.aliyuncs.com/example.jpg?x-oss-process=image/resize,w\_300/watermark,image\_cGFuZGEucG5nP3gtb3NzLXByb2Nlc3M9aW1hZ2UvcmVzaXplLFBfMzA,t\_90,g\_se,x\_10,y\_10,t\_50

**说明**

提高水印的透明度可以将边框的影响降低。

## 通过CDN回源OSS图片处理不生效

CDN回源OSS图片处理不生效，请使用OSS的访问域名进行测试，利用以下URL进行基础分析：

http://test.oss-cn-beijing.aliyuncs.com/MomClass/ChuXin/3\_2\_336\_462.jpg@30-30bl

http://test.img-cn-beijing.aliyuncs.com/MomClass/ChuXin/3\_2\_336\_462.jpg@30-30bl

- img-cn-region.aliyuncs.com 是老版本的OSS域名，图片处理的分隔符和语法与新版的 `oss` 域名不同。

- oss-cn-region.aliyuncs.com 是2017年后使用的新域名，不兼容`img`域名的图片处理语法和分隔符 "@" ，需要在OSS控制台上手动执行同步 。


如果将老域名的高斯处理效果搬迁到OSS的新域名，需要按照新的方式处理，如下：

http://test.oss-cn-beijing.aliyuncs.com/MomClass/ChuXin/3\_2\_336\_462.jpg?x-oss-process=image/blur,r\_3,s\_30

## 图片压缩后颜色变亮了

![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7095649951/p34746.png)

处理分析：首先，您可以使用PS等工具获取原图的颜色模式。如果原图是RGB模式，压缩后不会变色。如果原图是CMYK模式，压缩后可能会导致颜色偏差。目前，我们对CMYK的兼容还在支持中。

## 图片在本地可以正常打开，进行图片处理时提示已损坏

![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7095649951/p40239.png)

问题现象：图片文件在本地可以正常打开，但上传到OSS后无法进行图片处理，提示图片损坏。

排查方法：

- 获取原始的OSS URL地址，使用 `?x-oss-process=image/info` 查看原图信息。如果查不到图片信息并报错，说明原图已损坏。

- 可以使用开源的imagemagic工具来验证这个问题，将图片做任意调整，如果出现`error`说明图片损坏。可以使用以下命令进行测试：















```plaintext
convert -resize 1024x768 1123331261_15353307414801n.jpg
```


损坏的图片文件在本地可以显示，因为本地的图片查看工具对图片进行了补偿修复。而OSS不对损坏的图片进行处理，所以在浏览器上无法显示。

## 存储在OSS内的图片旋转了90度

问题现象：通过OSS域名访问图片正常。![图片旋转前](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3667648461/p423974.png)

通过CDN访问，图片被旋转了90度。![图片旋转90度](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3667648461/p423975.png)

问题分析：直接访问OSS正常，说明OSS存储没问题。通过CDN访问时图片被旋转，说明是通过CDN访问时浏览器添加了旋转参数。通过图片处理参数 `?x-oss-process=image/info` 查看，原图带有 `rotation 90` 旋转参数。

解决方法：删除旋转参数即可。

## 经过CDN加速后图片处理没有效果

排查步骤：检查是否开启了CDN的 **过滤参数** 功能，开启后会去除URL中问号（?）之后的参数。参见 [CDN 过滤参数](https://help.aliyun.com/zh/cdn/user-guide/ignore-parameters#concept-l2f-zbm-xdb "")。

## 使用图片处理出现“Picture exceed the maximum allowable rotation range”报错

排查方法：

- 使用ImageMagick工具查看原图是否自带`auto-orient`自适应旋转的属性。

- 使用`auto-orient,0` 参数处理图片，若能正常处理，说明原图带有自适应旋转属性。


## 苹果手机端携带了图片处理参数访问经过CDN加速的图片时变成空白图片，刷新后可以访问，电脑访问正常

问题分析：电脑端访问正常，手机端访问异常，说明OSS正常，否则电脑访问也会异常。

排查步骤：

使用手机直接访问OSS查看图片是否正常。

- 如果正常，通过CDN访问异常，说明是CDN节点网络问题或缓存错误内容

- 如果异常，CDN访问也应异常，刷新后正常可能是CDN缓存问题。


## 存储在OSS的原图和经过图片处理后的图片都打不开

使用ImageMagick排查OSS中的图片的步骤如下：

1. 执行以下命令下载示例图片：















```plaintext
wget https://zh.mobi/test/123.jpg
```



成功返回示例如下。















```plaintext
   --2018-11-22 10:55:16--  https://zh.mobi/test/123.jpg
正在解析主机 zh.mobi (zh.mobi)...
已发出HTTP请求，正在等待回应... 200 OK
长度：4141232 (3.9M) [image/jpeg]
正在保存至: “123.jpg”
100%[========================================================================================>] 4,141,232 12.5MB/s 用时 0.3s
2018-11-2210:55:16 (12.5 MB/s) - 已保存 “123.jpg” [4141232/4141232])
```

2. 下载图片处理工具 [ImageMagick](https://imagemagick.org/script/download.php)。

3. 执行以下命令查看图片的编码构成是否有问题：















```plaintext
identify 123.jpg
```



错误返回示例如下，说明图片编码构成错误，并非存储到OSS后出现的问题，建议您重新上传正确格式的图片：















```plaintext
identify: Not a JPEG file: starts with 0x000x00 `123.jpg' @ error/jpeg.c/JPEGErrorHandler/316.
```


## 图片处理完后背景色多了一条分割线

![图片带分割线](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3667648461/p423972.png)

问题分析：图片中出现的并非是分割线，而是图片处理后色彩构成出现问题。原图是RGB的真彩色`"ImageHeight": {"value": "2560"}, "ImageWidth": {"value": "1440"}`。经过图片处理后，像素被裁剪到h\_1920,w\_1080，导致RGB的像素点位被压缩，图片显示异常。

解决方法：使用`quality,Q_100`参数将图片的绝对质量提高到100。

## 图片处理报错“BadRequest”

```plaintext
<Error>
<Code>BadRequest</Code>
<Message>This image format is not supported.</Message>
<RequestId>62E2288D50ED1C30361E****</RequestId>
<HostId>examplebucket.oss-cn-beijing.aliyuncs.com</HostId>
</Error>
```

排查步骤：

1. 使用imagemagic工具的convert命令看下原图的格式。

2. 确认OSS是否支持该图片格式。有关OSS支持图片格式的更多信息，请参见 [使用限制](https://help.aliyun.com/zh/oss/user-guide/overview-17/#section-bqr-ds6-gus "")。


解决方法：将图片格式转换为OSS支持的格式。

## 图片处理报错“InvalidArgument”

```plaintext
<Error>
<Code>InvalidArgument</Code>
<Message>The value: 0 of parameter: w is invalid.</Message>
<RequestId>62E2288D50ED1C30361E****</RequestId>
<HostId>examplebucket.oss-cn-beijing.aliyuncs.com</HostId>
</Error>
```

在处理图片时，遇到参数错误的情况，首先需要检查原始图片的请求参数。例如，`2018089926****.jpg@0w_2e_1l_1an.src` 是旧域名 `img-cn-xx` 支持的格式。当将其转换为新域名 `oss-cn-xxx` 后，旧域名的请求方式（如 `@` 分隔符）不再被支持，且旧域名不支持 HTTPS 访问方式，因此会导致参数无效的错误。

## 图片处理报错“BadWebPImage”

```plaintext
<Error>
<Code>BadWebPImage</Code>
<Message>The webp image file may be damaged.</Message>
<RequestId>62E2288D50ED1C30361E****</RequestId>
<HostId>examplebucket.oss-cn-beijing.aliyuncs.com</HostId>
</Error>
```

问题原因：

- 原图为损坏的WebP格式图片。

- 原图为未损坏的WebP动图，但未申请白名单。


解决方法：请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请处理未损坏的WebP动图。

**说明**

WebP动图不支持auto-orient参数，您需要移除或修改相关参数。

## OSS能否识别请求的自定义query参数动态缩放

OSS不支持识别请求的自定义query参数动态缩放。

## 一个文字水印是否可以分成两行显示？一个图片是否可以添加多个文字水印？

OSS图片水印不支持将一个文字水印分行显示，且一个图片可以添加多个文字水印。详情请参见 [图片水印](https://help.aliyun.com/zh/oss/user-guide/add-watermarks#concept-hrt-sv5-vdb "")。

## 为何图片经过OSS缩略之后尺寸变大了？

这个问题通常是由于多种原因导致的，为了帮助您解决此问题，请参见 [影响图片文件大小的因素](https://yq.aliyun.com/articles/74634?spm=5176.10695662.1996646101.searchclickresult.672545f3KE153V)。

## **如何通过调整图片的属性来控制图片占用的存储空间大小？**

通过使用OSS的图片处理功能，如缩放、质量变换和格式转换，您可以优化图片大小并覆盖原有文件，以节省存储空间。更多信息，请参见 [图片处理参数](https://help.aliyun.com/zh/oss/user-guide/img-parameters/ "")、 [图片处理操作方式](https://help.aliyun.com/zh/oss/user-guide/img-implementation-modes "")、 [图片处理持久化](https://help.aliyun.com/zh/oss/user-guide/save-processed-images "")。

## **OSS图片处理时同时携带图片处理参数和versionId，versionId不生效，签名URL指向最新版本的文件**

历史版本暂不支持图片处理功能，因此无法通过指定versionId实现对历史版本图片的处理。