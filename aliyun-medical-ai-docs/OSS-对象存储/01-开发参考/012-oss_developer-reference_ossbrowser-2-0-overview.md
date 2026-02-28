### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)图形化管理工具ossbrowser 2.0（预览版）

# ossbrowser 2.0概述

更新时间：2025-12-09 05:42:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用限制

操作视频

功能优势

适用环境

计费说明

后续步骤

相关文档

ossbrowser 2.0是一款用于管理OSS的免费图形化桌面客户端。该客户端支持Windows、macOS和Linux操作系统，提供直观的图形用户界面，使您能够高效地执行各种操作，包括文件的上传、下载和删除。由于其本地部署特性，ossbrowser 2.0可在您的设备上直接运行，确保操作的流畅性。

**说明**

ossbrowser 2.0作为旧版ossbrowser的升级版本，目前暂未开源。有关各版本的更新详情，请参见 [版本发布记录](https://help.aliyun.com/zh/oss/developer-reference/version-release-record#a67dea2f3exgr "")。

## **使用限制**

- ossbrowser 2.0暂时尚未适配专有云、金融云以及政务云等其他非公共云环境。如果您是非公共云的用户请使用 [图形化管理工具ossbrowser 1.0](https://help.aliyun.com/zh/oss/developer-reference/graphical-management-tools-ossbrowser-1-0/#ariaid-title1 "")。

- 在公网环境下上传或下载超过10 GB的大文件时，容易因网络状况不稳定而导致传输失败。如果您处于非内网环境，并且需要传输超过10 GB的大文件，建议您使用 [命令行工具ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/#2a4b2fbc2f0a3 "")。


## 操作视频

请观看以下视频快速了解如何使用ossbrowser 2.0。

图形化管理工具ossbrowser 2.0（预览版）

## **功能优势**

- 提供直观简洁的界面交互，方便对Bucket进行管理。

- 支持批量文件或目录的上传与下载操作（文件总大小10 GB以内），还可进行在线预览和编辑。

- 通过不同角色对不同资源的授权访问，进一步保障OSS资源的安全。


## 适用环境

**重要**

- Windows系统仅支持Windows 7及以上版本包括Windows Server。

- Linux x64发行版本众多，需要安装图形界面依赖文件，因此不推荐使用。建议您在Windows或macOS上使用ossbrowser 2.0。


| **操作系统** | **系统架构** | **安装包类型** | **安装教程** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **操作系统** | **系统架构** | **安装包类型** | **安装教程** |
| Windows | x86-64 | nsis | [Windows系统](https://help.aliyun.com/zh/oss/developer-reference/installing-the-ossbrowser-2-0#e6fd1cc08cirn "") |
| macOS | x86-64 | dmg | [macOS系统](https://help.aliyun.com/zh/oss/developer-reference/installing-the-ossbrowser-2-0#0239039409759 "") |
| arm64 | dmg |
| Linux | x86-64 | AppImage | [Linux系统](https://help.aliyun.com/zh/oss/developer-reference/installing-the-ossbrowser-2-0#bdb2ae098bwuy "") |

## **计费说明**

ossbrowser软件本身免费，但通过ossbrowser执行相关操作时，其计费方式与在控制台操作相同，都会遵循OSS计费逻辑收取相应费用。例如：

- **本地环境中上传下载文件：** 在本地环境中使用ossbrowser上传和下载文件时，涉及PUT类 [请求费用](https://help.aliyun.com/zh/oss/api-operation-calling-fees#title-ncg-md9-cn6 "")，GET类的 [请求费用](https://help.aliyun.com/zh/oss/api-operation-calling-fees#title-ncg-md9-cn6 "") 和下行 [流量费用](https://help.aliyun.com/zh/oss/traffic-fees#title-e75-3jd-n6l "")。上传文件到OSS后需要根据文件存储类型收取 [存储费用](https://help.aliyun.com/zh/oss/storage-fees#title-9pu-8qw-t8n "")。

- **内网环境中上传下载文件**：在阿里云内网环境中，使用ossbrowser上传和下载文件，只涉及PUT和GET类 [请求费用](https://help.aliyun.com/zh/oss/api-operation-calling-fees#title-ncg-md9-cn6 "") 以及文件 [存储费用](https://help.aliyun.com/zh/oss/storage-fees#title-9pu-8qw-t8n "")。无流量费用。例如可以通过创建ECS实例，并在其上安装ossbrowser后实现在阿里云内网中上传和下载文件。


此外，如果您的业务需要在中国内地与海外地域之间传输数据，使用内外网可能无法满足预期的传输效率。建议开启传输加速服务来提升数据上传下载速度。使用传输加速服务会产生 [传输加速费用](https://help.aliyun.com/zh/oss/transfer-acceleration-fees#title-5v1-jpc-ar2 "")。有关OSS更多增值相关费用，请参见 [增值计费项](https://help.aliyun.com/zh/oss/value-added-billing-item/#6ed25dfd2179t "")。

## **后续步骤**

如需在Windows、macOS及Linux系统中安装ossbrowser 2.0，请参见 [安装ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/installing-the-ossbrowser-2-0#2e1e5eee641da "")。若您已完成ossbrowser 2.0的安装，但在登录环节遇到问题，可参阅 [登录ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/login-to-ossbrowser-2-0#85a24a9dcfg7v "")。

## **相关文档**

- [登录ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/login-to-ossbrowser-2-0#85a24a9dcfg7v "")

- [常用操作](https://help.aliyun.com/zh/oss/developer-reference/commonly-used-function-of-ossbrowser2-0#77df3848adbau "")

- [文件授权](https://help.aliyun.com/zh/oss/developer-reference/document-authorization-using-ossbrowser2-0#949eb71b93qo8 "")

- [新版本下载](https://help.aliyun.com/zh/oss/developer-reference/download-the-latest-minor-version-of-ossbrowser2-0#e1b4e29790294 "")

- [常见问题](https://help.aliyun.com/zh/oss/developer-reference/common-problems#818eab5b35ake "")

- [版本发布记录](https://help.aliyun.com/zh/oss/developer-reference/version-release-record#a67dea2f3exgr "")