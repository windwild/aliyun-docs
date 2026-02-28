### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[开始使用](https://help.aliyun.com/zh/oss/user-guide/product-introduction/)[快速入门](https://help.aliyun.com/zh/oss/user-guide/get-started-with-oss/)控制台快速入门

# 控制台快速入门

更新时间：2026-02-09 05:19:45

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：快速入门](https://help.aliyun.com/zh/oss/user-guide/get-started-with-oss/)[下一篇：图形化管理工具ossbrowser 2.0快速入门](https://help.aliyun.com/zh/oss/user-guide/ossbrowser)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

步骤一：创建存储空间

步骤二：上传文件

步骤三：下载文件

步骤四：分享文件

步骤五：清理

删除文件

删除存储空间

费用说明

下一步

常见问题

OSS管理控制台是阿里云提供的一款简单且易于上手的OSS网页管理工具。通过本教程，您可以在10分钟内完成创建存储空间、上传文件、分享文件等基础操作，预计费用不超过0.01元。

## 前提条件

- 已[注册阿里云账号](https://account.aliyun.com/register/qr_register.htm?oauth_callback=https%3A%2F%2Fbailian.console.aliyun.com%2F%3FapiKey%3D1)。

- 已 [个人实名认证](https://help.aliyun.com/zh/document_detail/324614.html#task-2020003 "") 或 [企业实名认证](https://help.aliyun.com/zh/account/overview "")。

- 已[开通OSS服务](https://oss.console.aliyun.com/overview)。


> 购买OSS资源包并不等于自动开通OSS，您仍需手动开通OSS服务，并且开通OSS服务是免费的。


## 步骤一：创建存储空间

存储空间（Bucket）是存放文件的容器，开始使用OSS前，需要先创建一个Bucket。

1. 在左侧导航栏进入 **[Bucket列表](https://oss.console.aliyun.com/bucket)** 页面，单击 **创建Bucket**。

2. 配置以下关键参数，其余保留默认值：


   - **Bucket名称**：输入一个全局唯一的名称，为确保唯一，建议使用 **项目名-地域-随机字符串** 的组合，例如`my-project-hangzhou-a1b2c3d4```。

   - **地域**：选择距离您较近的地域，例如华东1（杭州），以降低访问延迟。
3. 单击 **完成创建**。


## 步骤二：上传文件

创建Bucket后，可将图片、视频、文档等各种类型的文件（Object）上传至其中。

> 通过控制台单次可上传不超过5GB的文件。对于更大的文件，推荐使用 [命令行工具ossutil](https://help.aliyun.com/zh/oss/command-line-tools-ossutil-quickstart "")。

1. 如果本地没有合适的测试文件，可先下载此示例文件 [exampleobject.jpg](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20240926/tajhik/exampleobject.jpg) 到本地。

2. 在 **[**Bucket 列表**](https://oss.console.aliyun.com/bucket)** 页面，单击刚刚创建的Bucket名称。

3. 在左侧导航栏进入 **文件管理** \> **文件列表**，然后单击 **上传文件**。

4. 将本地的exampleobject.jpg文件拖拽到 **待上传文件** 区域，或通过 **扫描文件** 选择该文件。

5. 保持其他参数默认，单击 **上传文件**。


此时，您可以在 **上传列表** 页签查看各个文件的上传进度。上传完成后，您可以在目标路径下查看上传文件的文件名、文件大小以及存储类型等信息。

## 步骤三：下载文件

Bucket中的文件可下载至本地。

1. 在 **文件列表** 页面，找到刚才上传的exampleobject.jpg文件。

2. 勾选该文件，然后单击列表下方的 **下载** 按钮。


## 步骤四：分享文件

私有Bucket中的文件，可生成带有时效性的安全链接（URL）进行分享。

1. 在 **文件列表** 页面，单击`exampleobject.jpg`的文件名。

2. 在右侧弹出的 **详情** 面板中，可以按需设置链接的 **过期时间（秒）**（默认为600），然后单击 **复制文件URL**。

   - > **费用：** 此URL使用外网Endpoint，任何通过此URL的下载都会产生 **外网流出流量费**。

   - > **安全：** 分享前，请务必确认文件中不包含任何敏感数据。

   - > **时效**：URL在设定的有效期后会自动失效，如需再次访问，需要重新生成。
3. 将复制的URL粘贴到浏览器地址栏访问。默认行为是直接下载该图片文件，如需在浏览器中预览图片，则需要 [绑定自定义域名](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names#1e43238a95bb6 "")，使用自定义域名生成URL。


## 步骤五：清理

为防止文件持续产生费用，需先清空存储空间内的所有文件，然后删除存储空间本身。 **删除操作不可逆**。

### **删除文件**

1. 在左侧导航栏，选择 **文件管理** > **文件列表**。

2. 勾选已上传的示例文件exampleobject.jpg，

3. 单击列表下方的 **彻底删除**，并在弹窗中单击 **确定**。


### **删除存储空间**

> 删除Bucket后，需要等待数小时（通常为4到8个小时）才能再次创建同名的Bucket。

1. 在 **Bucket 列表** 页面，单击您要删除的存储空间的名称。

2. 在左侧导航栏，单击 **删除Bucket**。

3. 单击 **立即删除**，并按控制台提示完成后续操作。


## 费用说明

本教程涉及的OSS计费项主要包括：

- **存储费用**：文件存放期间，会持续产生标准存储费用。

- **外网下行流量费用**：他人使用分享链接（URL）下载文件，会产生外网流出流量费。

- **请求费用**：上传、下载操作会产生API请求次数费用。


完成本教程（上传一个小于1MB的文件并下载一次）的总费用预计 **低于0.01元**。定价详情参见[OSS产品定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.628c4d22ZdP2B0#/oss/detail/oss)。

## **下一步**

- **深入成本管理：** 通过 [计费概述](https://help.aliyun.com/zh/oss/billing-overview "") 了解费用详情，并通过 [资源包](https://help.aliyun.com/zh/oss/resource-plan/ "") 节省成本。

- **实现自动化**：学习 [SDK快速入门](https://help.aliyun.com/zh/oss/user-guide/oss-sdk-quick-start "")，在应用中通过代码管理OSS。

- **更多文件操作：** 查看 [功能指引](https://help.aliyun.com/zh/oss/user-guide/object-overview#a47cf1e035u7e "")，获取更多管理文件的方法。

- **加固数据安全**：通过配置 [权限与访问控制概述](https://help.aliyun.com/zh/oss/user-guide/permissions-and-access-control-overview "")，精细化管理数据访问权限。



**说明**





通过OSS控制台创建Bucket时默认开启 [阻止公共访问](https://help.aliyun.com/zh/oss/user-guide/block-public-access "")。开启后，不允许创建公共访问权限，包括公共读或者公共读写ACL、以及公共访问语义的Bucket Policy。如果您的业务有公共访问需求，可在Bucket创建后关闭阻止公共访问。


## **常见问题**

- [用量查询](https://help.aliyun.com/zh/oss/usage-query/ "")

- [对象/文件（Object）](https://help.aliyun.com/zh/oss/data-upload-and-download/ "")

- [资源包](https://help.aliyun.com/zh/oss/package-faq/ "")