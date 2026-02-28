### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 前言（Go SDK V1）

# 前言（Go SDK V1）

更新时间：2025-11-28 02:40:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

SDK源码和API文档

示例程序

了解OSS Go SDK V2

本文基于V1（aliyun-oss-go-sdk）代码库，介绍对象存储OSS的Go SDK各种使用场景下示例代码。

## SDK源码和API文档

请访问 [GitHub](https://github.com/aliyun/aliyun-oss-go-sdk) 获取OSS Go SDK源码。更多信息，请参见 [OSS Go SDK API文档](https://godoc.org/github.com/aliyun/aliyun-oss-go-sdk/oss)。

## 示例程序

OSS Go SDK提供丰富的示例程序，方便您参考或直接使用。示例包括以下内容：

| **示例文件** | **示例内容** |
| --- | --- |

|     |     |
| --- | --- |
| **示例文件** | **示例内容** |
| [new\_bucket.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/new_bucket.go) | [初始化Client](https://help.aliyun.com/zh/oss/initialization-9#concept-52931-zh "") |
| [create\_bucket.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/create_bucket.go) | [创建存储空间（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/create-buckets-2#section-zgm-l1b-kfb "") |
| [bucket\_acl.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_acl.go) | [管理存储空间的读写权限（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/manage-bucket-acls-1#concept-2352309 "") |
| [bucket\_policy.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_policy.go) | [授权策略](https://help.aliyun.com/zh/oss/developer-reference/bucket-policies-1#concept-2429834 "") |
| [bucket\_referer.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_referer.go) | [防盗链（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/go-hotlink-protection#concept-32155-zh "") |
| [bucket\_lifecycle.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_lifecycle.go) | [生命周期](https://help.aliyun.com/zh/oss/developer-reference/lifecycle-3#concept-32152-zh "") |
| [bucket\_logging.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_logging.go) | [访问日志](https://help.aliyun.com/zh/oss/developer-reference/logging-5#concept-32153-zh "") |
| [bucket\_cors.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_cors.go) | [跨域访问](https://help.aliyun.com/zh/oss/developer-reference/cors-5#concept-32156-zh "") |
| [bucket\_website.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_website.go) | [静态网站托管（镜像回源）（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/static-website-hosting-5#concept-32154-zh "") |
| [bucket\_encryption.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_encryption.go) | [服务端加密（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/server-side-encryption-2#concept-265990 "") |
| [bucket\_requestpayment.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_requestpayment.go) | [请求者付费模式（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/pay-by-requester-3#concept-944152 "") |
| [bucket\_inventory.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_inventory.go) | [存储空间清单（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/bucket-inventory-3#concept-2404009 "") |
| [bucket\_accessmonitor.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_accessmonitor.go) | [访问跟踪（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/access-tracking-14#concept-2270901 "") |
| [bucket\_metaquery.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_metaquery.go) | [数据索引（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/go-sdk-data-indexing#concept-2248522 "") |
| [list\_buckets.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/list_buckets.go) | [列举存储空间（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-2#concept-2352302 "") |
| [bucket\_stat.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_stat.go) | [获取存储空间的存储容量（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/query-the-storage-capacity-of-a-bucket-14#concept-2248725 "") |
| [bucket\_tagging.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/bucket_tagging.go) | [存储空间标签（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/manage-bucket-tagging#concept-265987 "") |
| [put\_object.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/put_object.go) | 上传文件，包括 [简单上传（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/simple-upload-4#concept-88601-zh "")、 [断点续传上传（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/perform-resumable-upload#concept-88603-zh "") 等 |
| [append\_object.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/append_object.go) | [追加上传](https://help.aliyun.com/zh/oss/developer-reference/perform-append-upload#concept-88602-zh "") |
| [get\_object.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/get_object.go) | 下载文件，包括 [流式下载（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/streaming-download-5#concept-88617-zh "")、 [限定条件下载（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/go-sdk-conditional-download#concept-88623-zh "") 等 |
| [delete\_object.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/delete_object.go) | [删除文件（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/delete-objects-11#concept-88644-zh "") |
| [copy\_object.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/copy_object.go) | [拷贝文件（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/copy-an-object-1#concept-88645-zh "") |
| [list\_objects.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/list_objects.go) | [列举文件（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/list-objects-10#concept-88639-zh "") |
| [archive.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/archive.go) | [解冻文件（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/restore-an-object#concept-88647-zh "") |
| [object\_acl.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/object_acl.go) | [管理文件读写权限](https://help.aliyun.com/zh/oss/developer-reference/manage-object-acls-10#concept-88634-zh "") |
| [sign\_url.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/sign_url.go) | [生成带签名的URL](https://help.aliyun.com/zh/oss/authorize-access-5#concept-59670-zh "") |
| [object\_tagging.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/object_tagging.go) | [对象标签](https://help.aliyun.com/zh/oss/developer-reference/configure-object-tagging-7#concept-710957 "") |
| [select\_object.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/select_object.go) | [查询文件（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/query-objects-1#concept-2200187 "") |
| [object\_meta.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/object_meta.go) | [管理文件元数据（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/manage-object-metadata-6#concept-88638-zh "") |
| [livechannel.go](https://github.com/aliyun/aliyun-oss-go-sdk/blob/master/sample/livechannel.go) | [LiveChannel管理（Go SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/common-operations-on-livechannels-1#concept-2164037 "") |

## 了解OSS Go SDK V2

OSS Go SDK V2（alibabacloud-oss-go-sdk-v2）是对V1（aliyun-oss-go-sdk）代码库的重大改写。V2是一个全新的版本，基于GO 1.18+构建，简化了底层操作例如身份验证、自动请求重试及错误处理等；提供了灵活友好的参数配置以及丰富的高级接口，例如分页器、传输管理器 、File-like接口等，全面提升了开发效率和体验。

- 开始使用V2，请参见 [alibabacloud-oss-go-sdk-v2开发者指南](https://github.com/aliyun/alibabacloud-oss-go-sdk-v2/blob/master/DEVGUIDE-CN.md)。

- 从V1升级为V2，请参见 [迁移指南](https://github.com/aliyun/alibabacloud-oss-go-sdk-v2/blob/master/DEVGUIDE-CN.md#%E8%BF%81%E7%A7%BB%E6%8C%87%E5%8D%97)。