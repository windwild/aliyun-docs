### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)OSS C SDK

# OSS C SDK

更新时间：2025-11-28 05:00:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

兼容性

示例代码

后续参考

本文档基于OSS C SDK 3.10.0编写。

## 兼容性

OSS C SDK版本兼容性说明如下：

- 对于3.X.X系列SDK：兼容。

- 对于 2.X.X系列SDK：

  - 兼容Windows。

  - 兼容Linux，链表（aos\_list\_t）遍历接口不兼容。

    - aos\_list\_for\_each\_entry

    - aos\_list\_for\_each\_entry\_reverse

    - aos\_list\_for\_each\_entry\_safe

    - aos\_list\_for\_each\_entry\_safe\_reverse
- 对于 1.0.0 系列SDK，除以下结构体和接口不兼容外，其余均兼容。

  - oss\_request\_options\_t

  - oss\_get\_object\_to\_buffer

  - oss\_get\_object\_to\_file

  - oss\_get\_object\_to\_buffer\_by\_url

  - oss\_get\_object\_to\_file\_by\_url

  - oss\_init\_multipart\_upload

  - oss\_complete\_multipart\_upload
- 对于 0.0.X系列SDK：不兼容。


## 示例代码

OSS C SDK提供丰富的示例代码，方便您参考或直接使用。示例代码包括以下内容：

| **示例文件** | **示例内容** |
| --- | --- |

|     |     |
| --- | --- |
| **示例文件** | **示例内容** |
| [oss\_put\_object\_sample](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_put_object_sample.c) | [上传文件](https://help.aliyun.com/zh/oss/developer-reference/overview-32#concept-32136-zh "") |
| - [put\_object\_acl\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_put_object_acl_sample.c)<br>  <br>- [get\_object\_acl\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_get_object_acl_sample.c) | [管理文件访问权限（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/manage-object-acls-11 "") |
| [oss\_get\_object\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_get_object_sample.c) | [下载文件](https://help.aliyun.com/zh/oss/developer-reference/overview-30#concept-32137-zh "") |
| [oss\_append\_object\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_append_object_sample.c) | [追加上传](https://help.aliyun.com/zh/oss/developer-reference/append-upload-8#concept-90215-zh "") |
| [oss\_multipart\_upload\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_multipart_upload_sample.c) | [分片上传](https://help.aliyun.com/zh/oss/developer-reference/multipart-upload-8#concept-90222-zh "") |
| [oss\_resumable\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_resumable_sample.c) | [断点续传上传（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/resumable-upload-7#concept-90219-zh "")、 [断点续传下载（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/perform-resumable-download#concept-90283-zh "") |
| [get\_object\_meta\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_get_object_meta_sample.c) | [管理文件元数据（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/manage-object-metadata-7 "") |
| [oss\_list\_object\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_list_object_sample.c) | [列举文件](https://help.aliyun.com/zh/oss/developer-reference/list-objects-12#concept-90514-zh "") |
| [oss\_delete\_object\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_delete_object_sample.c) | [删除文件（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/delete-objects-6#concept-90493-zh "") |
| [oss\_callback\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_callback_sample.c) | [上传回调（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/upload-callbacks-8#concept-90224-zh "") |
| [oss\_progress\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_progress_sample.c) | [进度条上传](https://help.aliyun.com/zh/oss/developer-reference/progress-bar-4#concept-90225-zh "")、 [进度条下载](https://help.aliyun.com/zh/oss/developer-reference/progress-bars-2#concept-90284-zh "") |
| [oss\_crc\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_crc_sample.c) | 上传、下载时进行CRC校验 |
| [oss\_image\_sample.c](https://github.com/aliyun/aliyun-oss-c-sdk/blob/master/oss_c_sdk_sample/oss_image_sample.c) | [图片处理（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/img-9#concept-48113-zh "") |

**说明**

C SDK源码请参见 [GitHub](https://github.com/aliyun/aliyun-oss-c-sdk/tree/master)。

## **后续参考**

- [安装（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/installation-4 "")

- [初始化（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/initialization-5 "")

- [快速入门（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/getting-started-with-oss-sdk-for-c "")

- [存储空间（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/buckets-9/ "")

- [权限控制（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/access-control-4/ "")

- [对象/文件（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/objects-3/ "")

- [数据安全（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/data-security-4/ "")

- [数据管理（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/data-management-4/ "")

- [图片处理（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/img-9 "")

- [错误处理（C SDK）](https://help.aliyun.com/zh/oss/developer-reference/error-handling-3 "")