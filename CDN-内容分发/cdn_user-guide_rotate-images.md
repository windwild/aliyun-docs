### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[性能优化](https://help.aliyun.com/zh/cdn/user-guide/performance-optimization/)[图像处理](https://help.aliyun.com/zh/cdn/user-guide/image-editing/)图片旋转

# 图片旋转

更新时间：2024-12-04 00:17:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：图片缩放](https://help.aliyun.com/zh/cdn/user-guide/resize-images)[下一篇：图片色彩](https://help.aliyun.com/zh/cdn/user-guide/change-the-color-of-an-image)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

图片自动旋转

图片旋转处理参数

参数说明

操作示例

图片旋转包含图片自动旋转和按指定方向旋转，您可以通过图片旋转操作，改变图片的方向或角度。

**说明**

- 阿里云CDN、DCDN和OSS的图片处理都是独立的功能，不能相互混用。

- 图像处理为付费服务，公测期间 **暂不收费**，收费时间另行通知。

- 当您使用图像处理功能时，由于不同图片格式在压缩算法上存在较大差异，因此不同图片格式之间相互转换可能会导致图片体积变大，例如：jpeg转webp、jpeg转png、png转webp。如果您需要降低图片文件的体积，建议您通过调整质量参数`quality`降低图片质量来实现。


## 图片自动旋转

某些手机拍摄出来的照片可能带有旋转参数，图片自动旋转只对带有旋转参数的图片生效。开启图片自动旋转，可自动调正图片，方便用户查看。通过控制台开启图片自动旋转，请参见 [图片处理操作方法](https://help.aliyun.com/zh/cdn/user-guide/image-processing-operation-method "")。

**重要**

开启该功能后，短时间内会导致命中率下降，过后会自动恢复正常，请勿在业务高峰期开启。

操作名称：`auto-orient`

操作示例

```plaintext
example.com/image01.png?image_process=auto-orient
```

## 图片旋转处理参数

### **参数说明**

指定旋转方向是指将图片按顺时针和指定的角度进行旋转，只支持90°、180°和270°三个旋转角度。

操作名称：`rotate`

### **操作示例**

将原图按顺时针旋转180°，图片处理URL为：`http(s)://example.com/image01.png?image_process=rotate,180`