### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[了解计费](https://help.aliyun.com/zh/oss/understanding-billing/)计费项检测

# 计费项检测

更新时间：2025-01-06 20:40:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

操作步骤

常见问题

检测到已产生费用，但是当前账号下未找到关联账单？

您可以通过OSS计费项检测工具了解您当前OSS资源的部分用量数据，同时为您推荐适合您使用场景的资源包，降低使用成本。

## **背景信息**

如果您同时使用了OSS的多种功能，例如使用OSS存储文本、图片、音视频等文件会产生对应类型的存储费用。通过外网浏览或者下载OSS文件时会产生下行流量费用等。关于OSS计费项的更多信息，请参见 [产品计费](https://help.aliyun.com/zh/oss/billing-overview#section-dkl-nex-469 "")。

针对以上情况，您可以通过OSS计费项检测工具一站式了解当前使用OSS资源产生的存储、请求、流量以及传输加速的用量数据。

## **操作步骤**

1. 登录[OSS管理控制台](https://oss.console.aliyun.com/)。

2. 在左侧导航栏，选择 **资源用量** > **计费项检测**。

3. 在OSS计费项检测工具页面，您可以查看当前账号最近3天或者最近7天指定地域或者全部地域因使用OSS资源产生的部分计费项。



**重要**





   - 如果您希望通过RAM用户使用计费项检测，您需要拥有`AliyunCloudMonitorReadOnlyAccess`和`AliyunBSSFullAccess`权限。具体操作，请参见 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "")。

   - 当前页面用量及费用数据仅作为预估参考，不作为实际出账依据。且因账单出账存在延迟，费用信息并非实时数据。


如下图所示，说明当前账号下共有5个地域产生了标准存储（本地冗余）计费项。其中，华东2（上海）以及华北2（北京）地域产生费用的原因为该计费项的用量超出了资源包规格，建议 [升级资源包](https://help.aliyun.com/zh/oss/upgrade-resource-plans "")。因不同原因产生费用后，您可以通过单击 **查看地域详情**，了解具体的用量情况以及推荐操作。

![计费项.jpg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6523719071/p770273.jpg)

## **常见问题**

### **检测到已产生费用，但是当前账号下未找到关联账单？**

问题原因：当存在财务关联的情况下，如果计费项检测显示已产生费用，请注意不要仅依据计费项检测提供的计费原因进行判断，实际产生费用的原因可能是费用出账到了财务关联的账号。

解决办法：建议检查关联账号的账单详情。