### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)图形化管理工具ossbrowser 1.0

# 图形化管理工具ossbrowser 1.0

更新时间：2025-04-16 05:44:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

版本升级

使用限制

操作视频

适用环境

计费说明

相关文档

ossbrowser 1.0是一款用于管理OSS的免费图形化桌面客户端。该客户端支持Windows、macOS和Linux操作系统，提供直观的图形用户界面，使您能够高效地执行各种操作，包括文件的上传、下载和删除。由于其本地部署特性，ossbrowser 1.0可在您的设备上直接运行，确保操作的流畅性。

## **版本升级**

推荐您使用全新升级的ossbrowser 2.0，快速安装并使用，请参见 [安装ossbrowser 2.0](https://help.aliyun.com/zh/oss/developer-reference/installing-the-ossbrowser-2-0#2e1e5eee641da "")。

ossbrowser 2.0重点功能如下：

- **全新的视觉交互体验**：页面设计美观且简洁，各项功能操作更加方便、快捷。

- **多种登录方式**：新增 **阿里云APP**、 **支付宝**、 **钉钉** 扫码登录，也可以手动输入 **阿里云** 或 **RAM用户** 账户密码登录，还支持 **手机号** 获取验证码登录。

- **文件预览编辑**：预览文本文件时，最大可支持100 MB的文本文件，并且支持在预览过程中直接进行编辑。

- **文件下载性能**：使用内网域名下载文件性能得到优化。


## **使用限制**

在公网环境下上传或下载超过10 GB的大文件时，容易因网络状况不稳定而导致传输失败。如果您处于非内网环境，并且需要传输超过10 GB的大文件，建议您使用 [命令行工具ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/#2a4b2fbc2f0a3 "")。

## 操作视频

观看以下视频快速了解如何快速使用ossbrowser 1.0。

图形化管理工具ossbrowser 1.0

## 适用环境

| **操作系统** | **下载地址** | **说明** | **安装教程** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **操作系统** | **下载地址** | **说明** | **安装教程** |
| Windows | [oss-browser-win32-ia32.zip（x86-64位）](https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-win32-ia32.zip) | - 仅支持Windows 7及以上版本。<br>  <br>- 如果遇到安装ossbrowser后无法正常使用的问题，请参见 [Windows系统安装某软件后无法打开ossbrowser](https://help.aliyun.com/zh/oss/developer-reference/faq-8#section-vlq-30o-60r "")。<br>  <br>- 不推荐在Windows Server安装ossbrowser。如果您在使用Windows Server安装ossbrowser时遇到问题，您可以构建 [源码](https://github.com/aliyun/oss-browser) 解决兼容性问题。 | [Windows系统](https://help.aliyun.com/zh/oss/developer-reference/install-ossbrowser-1-0#9e154cd152iwk "") |
| [oss-browser-win32-x64.zip（x86-32位）](https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-win32-x64.zip) |
| macOS | [oss-browser-darwin-x64.zip](https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-darwin-x64.zip) | macOS默认无法打开未验证的开发者应用。如果出现该问题，您需要修改系统安全设置。详情请参见 [macOS系统无法打开ossbrowser](https://help.aliyun.com/zh/oss/developer-reference/faq-8#section-uyz-2i7-4vm "")。 | [macOS系统](https://help.aliyun.com/zh/oss/developer-reference/install-ossbrowser-1-0#0c6d4b85dbdki "") |
| Linux x64 | [oss-browser-linux-x64.zip](https://gosspublic.alicdn.com/ossbrowser/1.18.0/oss-browser-linux-x64.zip) | - 不推荐在Linux x64使用ossbrowser。建议您在Windows或者macOS，使用ossbrowser。Linux x64发行版本众多，需要安装图形界面和多种依赖文件。本文以CentOS 7、CentOS 8、Ubuntu 14等为例说明如何安装ossbrowser。<br>  <br>- 如果您在Linux x64安装ossbrowser时遇到问题，您可以下载 [源码](https://github.com/aliyun/oss-browser) 编译排查。 | [Linux 系统](https://help.aliyun.com/zh/oss/developer-reference/install-ossbrowser-1-0#353ef4f47crpv "") |

## **计费说明**

ossbrowser软件本身免费，但通过ossbrowser执行相关操作时，其计费方式与在控制台操作相同，都会遵循OSS计费逻辑收取相应费用。例如：

- **本地环境中上传下载文件：** 在本地环境中使用ossbrowser上传和下载文件时，涉及PUT类 [请求费用](https://help.aliyun.com/zh/oss/api-operation-calling-fees#title-ncg-md9-cn6 "")，GET类的 [请求费用](https://help.aliyun.com/zh/oss/api-operation-calling-fees#title-ncg-md9-cn6 "") 和下行 [流量费用](https://help.aliyun.com/zh/oss/traffic-fees#title-e75-3jd-n6l "")。上传文件到OSS后需要根据文件存储类型收取 [存储费用](https://help.aliyun.com/zh/oss/storage-fees#title-9pu-8qw-t8n "")。

- **内网环境中上传下载文件**：在阿里云内网环境中，使用ossbrowser上传和下载文件，只涉及PUT和GET类 [请求费用](https://help.aliyun.com/zh/oss/api-operation-calling-fees#title-ncg-md9-cn6 "") 以及文件 [存储费用](https://help.aliyun.com/zh/oss/storage-fees#title-9pu-8qw-t8n "")。无流量费用。例如可以通过创建ECS实例，并在其上安装ossbrowser后实现在阿里云内网中上传和下载文件。


此外，使用传输加速服务会产生 [传输加速费用](https://help.aliyun.com/zh/oss/transfer-acceleration-fees#title-5v1-jpc-ar2 "")。有关OSS更多增值相关费用，请参见 [增值计费项](https://help.aliyun.com/zh/oss/value-added-billing-item/#6ed25dfd2179t "")。

## **相关文档**

- 安装ossbrowser 1.0，请参见 [安装ossbrowser 1.0](https://help.aliyun.com/zh/oss/developer-reference/install-ossbrowser-1-0#title-uv8-64i-xrd "")。

- 若您想要快速了解并上手使用ossbrowser 1.0版本，可参见 [常用操作](https://help.aliyun.com/zh/oss/developer-reference/use-ossbrowser#title-kzi-qkt-skx "") 文档。此外，当您有需求为特定用户授予访问Bucket内特定资源的权限时，请参考 [权限管理](https://help.aliyun.com/zh/oss/developer-reference/permission-management-1#title-v3d-1di-l26 "") 完成权限配置操作。

- 有关使用ossbrowser 1.0过程中遇到的常见问题，请参见 [常见问题](https://help.aliyun.com/zh/oss/developer-reference/faq-8#title-d2t-2pd-sn5 "")。