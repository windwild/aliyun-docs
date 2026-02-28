### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[对象/文件（Object）](https://help.aliyun.com/zh/oss/data-upload-and-download/)[下载文件](https://help.aliyun.com/zh/oss/download-file-faq/)报错ApkDownloadForbidden怎么处理？

# 报错ApkDownloadForbidden怎么处理？

更新时间：2024-07-03 04:32:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：报错ExternalRedirectForbidden怎么处理](https://help.aliyun.com/zh/oss/how-to-deal-with-externalredirectforbidden-reporting-errors)[下一篇：如何修改、更新、编辑文件？](https://help.aliyun.com/zh/oss/how-do-i-modify-update-and-edit-objects)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

问题现象

问题原因

解决方法

附录

本文介绍访问文件时报错ApkDownloadForbidden的原因和解决方法。

## **问题现象**

通过Bucket外网域名（`bucketname.oss-[region].aliyuncs.com`）或者传输加速域名（`bucketname.oss-accelerate.aliyuncs.com`或`bucketname.oss-accelerate-overseas.aliyuncs.com`），以文件URL或者匿名请求的形式访问后缀为.apk文件、.ipa文件、MIME类型（即响应头中content-type）为`application/vnd.android.package-archive`或者`application/iphone`的文件时，服务器返回400错误，错误码为`ApkDownloadForbidden`。

## **问题原因**

出于安全考虑，通过文件URL或者匿名请求的方式访问指定类型文件，请求被阻断。

- 自2023年08月15日00:00:00起，通过Bucket外网域名访问该日期之后创建的Bucket内后缀为.apk或者.ipa文件。

- 自2023年08月15日00:00:00起，通过传输加速域名访问该日期之后开启传输加速的Bucket内后缀为.apk或者.ipa文件。

- 自2024年08月05日00:00:00起，通过Bucket外网域名访问该日期之后创建的Bucket内MIME类型（即响应头中content-type）为`application/vnd.android.package-archive`或者`application/iphone`的文件。

- 自2024年08月05日00:00:00起，通过传输加速域名访问该日期之后开启传输加速的Bucket内MIME类型（即响应头中content-type）为`application/vnd.android.package-archive`或者`application/iphone`的文件。


## **解决方法**

通过自定义域名访问后缀为.apk文件、.ipa文件、MIME类型（即响应头中content-type）为`application/vnd.android.package-archive`或者`application/iphone`的文件。具体步骤，请参见 [绑定自定义域名至Bucket默认域名](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names "")。

## **附录**

以下表格详细列举了哪个时间点创建的Bucket以及哪个时间点开启传输加速后，使用哪种域名类型或者指定方式可以正常访问指定后缀以及MIME类型的文件。

| **文件类型** | **时间** | **访问方式** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **文件类型** | **时间** | **访问方式** |
| 后缀为.apk或者.ipa文件 | 2023年08月15日00:00:00之前创建的Bucket | Bucket外网域名 |
| 2023年08月15日00:00:00之前为Bucket开启传输加速 | 传输加速域名 |
| 任意时间创建的Bucket | Bucket内网域名 |
| 自定义域名 |
| 在Header中包含签名 |
| 阿里云CDN回源OSS（源站指定为OSS） |
| MIME类型（即响应头中content-type）为`application/vnd.android.package-archive`或者`application/iphone`的文件 | 2024年08月05日00:00:00之前创建的Bucket | Bucket外网域名 |
| 2024年08月05日00:00:00之前为Bucket开启传输加速 | 传输加速域名 |
| 任意时间创建的Bucket | Bucket内网域名 |
| 自定义域名 |
| 在Header中包含签名 |
| 阿里云CDN回源OSS（源站指定为OSS） |