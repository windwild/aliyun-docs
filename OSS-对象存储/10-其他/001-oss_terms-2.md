### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 基本概念

# OSS产品中涉及的基本概念

更新时间：2024-09-18 06:05:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是对象存储OSS](https://help.aliyun.com/zh/oss/user-guide/what-is-oss)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

存储空间（Bucket）

对象（Object）

ObjectKey

Object类型

Region（地域）

Endpoint（访问域名）

AccessKey（访问密钥）

原子性和强一致性

数据冗余机制

OSS术语表

本文将向您介绍对象存储OSS产品中涉及的几个基本概念，以便于您更好地理解OSS产品。

## 存储空间（Bucket）

存储空间是用户用于存储对象（Object）的容器，所有的对象都必须隶属于某个存储空间。存储空间具有各种配置属性，包括地域、访问权限、存储类型等。用户可以根据实际需求，创建不同类型的存储空间来存储不同的数据。

- 同一个存储空间的内部是扁平的，没有文件系统的目录等概念，所有的对象都直接隶属于其对应的存储空间。

- 每个用户可以拥有多个存储空间。

- 存储空间的名称在OSS范围内必须是全局唯一的。存储空间创建成功后，名称将无法修改。



**说明**





全局唯一表示阿里云所有的用户创建的Bucket名称都不能相同。例如用户A创建了名称为example的Bucket，其他用户无法再次创建名称为example的Bucket。

- 存储空间内部的对象数目没有限制。


存储空间的命名规范如下：

- 只能包括小写字母、数字和短划线（-）。

- 必须以小写字母或者数字开头和结尾。

- 长度必须在3~63字符之间。


## 对象（Object）

对象是OSS存储数据的基本单元，也被称为OSS的文件。和传统的文件系统不同，对象没有文件目录层级结构的关系。对象由元数据（Object Meta）、用户数据（Data）和文件名（Key）组成，并且由存储空间内部唯一的Key来标识。对象元数据是一组键值对，表示了对象的一些属性，例如文件类型、编码方式等信息，同时用户也可以在元数据中存储一些自定义的信息。

对象的生命周期是从上传成功到被删除为止。在整个生命周期内，除使用追加方式上传的Object可以通过继续追加上传写入数据外，使用其他方式上传的Object内容无法编辑，您可以通过重复上传同名的对象来覆盖之前的对象。

对象的命名规范如下：

- 使用UTF-8编码。

- 长度必须在1~1023字符之间。

- 不能以正斜线（/）或者反斜线（\\）开头。



**说明**





对象名称需要区分大小写。如无特殊说明，本文档中的对象、文件称谓等同于Object。


## ObjectKey

在各语言SDK中，ObjectKey、Key以及ObjectName是同一概念，均表示对Object执行相关操作时需要填写的Object名称。例如向某一存储空间上传Object时，ObjectKey表示上传的Object所在存储空间的完整名称，即包含文件后缀在内的完整路径，如填写为`abc/efg/123.jpg`。

## Object类型

Object包含以下三种类型：

- Normal

通过简单上传生成的Object。上传结束之后内容是固定的，只能读取，不能修改。如果Object内容发生了改变，只能重新上传同名的Object来覆盖之前的内容。简单上传适用于上传小于5 GB的单个文件、一次HTTP请求交互即可完成上传的场景。更多信息，请参见 [简单上传](https://help.aliyun.com/zh/oss/user-guide/simple-upload#concept-bws-3bb-5db "")。

- Multipart

通过分片上传生成的Object。上传结束之后内容是固定的，只能读取，不能修改。如果Object内容发生了改变，只能重新上传同名的Object来覆盖之前的内容。分片上传适用于大文件加速上传、网络环境较差、文件大小不确定的场景。更多信息，请参见 [分片上传](https://help.aliyun.com/zh/oss/user-guide/multipart-upload#concept-wzs-2gb-5db "")。

- Appendable

通过追加上传生成的Object。追加上传可在视频数据产生之后即时将数据上传至同一个Object。追加上传适用于视频监控、视频直播等领域生成的实时视频流场景。更多信息，请参见 [追加上传](https://help.aliyun.com/zh/oss/user-guide/append-upload-11#concept-ls5-yhb-5db "")。


**重要**

不支持在不同类型的Object之间相互转换。例如，Normal类型的Object无法转换为Multipart或者Appendable类型。

## Region（地域）

Region表示OSS的数据中心所在物理位置。用户可以根据费用、请求来源等选择合适的地域创建Bucket。一般来说，距离用户更近的Region访问速度更快。更多信息，请参见 [OSS已经开通的Region](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。

Region是在创建Bucket的时候指定的。Bucket创建成功后，Region将无法修改。该Bucket下所有的Object都存储在对应的数据中心，目前不支持Object级别的Region设置。

## Endpoint（访问域名）

Endpoint表示OSS对外服务的访问域名。OSS以HTTP RESTful API的形式对外提供服务，当访问不同的Region的时候，需要不同的域名。通过内网和外网访问同一个Region所需要的Endpoint也是不同的。例如杭州Region的外网Endpoint是oss-cn-hangzhou.aliyuncs.com，内网Endpoint是oss-cn-hangzhou-internal.aliyuncs.com。具体的内容请参见 [各个Region对应的Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。

## AccessKey（访问密钥）

AccessKey简称AK，指的是访问身份验证中用到的AccessKey ID和AccessKey Secret。OSS通过使用AccessKey ID和AccessKey Secret对称加密的方法来验证某个请求的发送者身份。AccessKey ID用于标识用户；AccessKey Secret是用户用于加密签名字符串和OSS用来验证签名字符串的密钥，必须保密。对于OSS来说，AccessKey的来源有：

- Bucket的拥有者申请的AccessKey。

- 被Bucket的拥有者通过RAM授权给第三方请求者的AccessKey。

- 被Bucket的拥有者通过STS授权给第三方请求者的AccessKey。


更多AccessKey介绍请参见 [创建AccessKey](https://help.aliyun.com/document_detail/53045.html#task968 "")。

## 原子性和强一致性

- 原子性

Object操作在OSS上具有原子性，操作要么成功要么失败，不存在中间状态的Object。当Object上传完成时，OSS即可保证读到的Object是完整的，OSS不会返回给用户一个部分上传成功的Object。

- 强一致性

Object操作在OSS同样具有强一致性，当用户收到了上传（PUT）成功的响应时，该上传的Object进入立即可读状态，并且Object的冗余数据已经写入成功。不存在上传的中间状态，即执行read-after-write，却无法读取到数据。对于删除操作，用户删除指定的Object成功之后，该Object立即不存在。


## 数据冗余机制

OSS使用基于纠删码的数据冗余存储机制，确保硬件失效时的数据持久性和可用性。

- OSS Object操作具有强一致性，当用户收到了上传或复制成功的响应时，该上传的Object就已经立即可读，且数据已经冗余写入到多个设备中。

- OSS会通过计算网络流量包的校验和，验证数据包在客户端和服务端之间传输中是否出错，保证数据完整传输。

- OSS的冗余存储机制，可支持两个存储设施并发损坏时，仍维持数据不丢失。

  - 当数据存入OSS后，OSS会检测和修复丢失的冗余，确保数据持久性和可用性。

  - OSS会周期性地通过校验等方式验证数据的完整性，及时发现因硬件失效等原因造成的数据损坏。当检测到数据有部分损坏或丢失时，OSS会利用冗余的数据，进行重建并修复损坏数据。

## OSS术语表

| **英文** | **中文** |
| --- | --- |

|     |     |
| --- | --- |
| **英文** | **中文** |
| Bucket | 存储空间 |
| Object | 对象或者文件 |
| Endpoint | OSS访问域名 |
| Region | 地域或者数据中心 |
| AccessKey | AccessKey ID和AccessKey Secret的统称，访问密钥 |
| Put Object | 简单上传 |
| Post Object | 表单上传 |
| Multipart Upload | 分片上传 |
| Append Object | 追加上传 |
| Get Object | 简单下载 |
| Callback | 回调 |
| Object Meta | 文件元数据。用来描述文件信息，例如文件类型、编码方式等 |
| Data | 文件数据 |
| Key | 文件名 |
| ACL (Access Control List) | 存储空间或者文件的权限 |

**说明**

如果没有特殊说明，本文中出现和术语表中相同的英文和中文，表达的是相同的意思。某些场景下，为了表述方便会混合使用。