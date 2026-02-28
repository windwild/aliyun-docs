### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[命名空间](https://help.aliyun.com/zh/sae/namespace/)管理命名空间

# 管理命名空间

更新时间：2025-11-12 02:09:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：将Dubbo应用平滑迁移至SAE](https://help.aliyun.com/zh/sae/smoothly-migrate-dubbo-applications-to-sae2)[下一篇：创建定时启停规则](https://help.aliyun.com/zh/sae/create-timed-start-stop-rules)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

前提条件

创建命名空间

编辑命名空间

删除命名空间

切换专有网络VPC

命名空间为您的应用提供逻辑隔离的运行环境，方便应用的服务调用，以及分布式配置推送。如果您有开发环境、测试环境和生产环境等场景，建议使用命名空间，将不同场景下的应用进行逻辑隔离，便于管理应用及一键启停应用，提高应用安全性。本文介绍如何在SAE控制台管理命名空间，包括创建、编辑、删除等操作。

## **背景信息**

SAE为每个地域提供一个默认命名空间，无需您手动创建；如果默认命名空间不能满足您的业务场景，您可以根据本文介绍的方法创建并管理命名空间。

## **前提条件**

已创建专有网络VPC。具体操作，请参见 [创建和管理专有网络](https://help.aliyun.com/zh/vpc/user-guide/create-and-manage-a-vpc "")。

## **创建命名空间**

1. 在[SAE命名空间](https://saenext.console.aliyun.com/cn-hangzhou/namespace)中，在顶部选择目标地域，点击 **创建命名空间**。

2. 在弹出的 **创建命名空间** 面板，根据下表说明配置相关信息，然后单击 **确定**。




| **配置项** | **说明** | **示例** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **配置项** | **说明** | **示例** |
| **命名空间名称** | 自定义命名空间名称。 | 测试 |
| **命名空间ID** | - 前缀不支持编辑，根据所选地域确定，例如华南1（深圳）地域的前缀为`cn-shenzhen`。<br>     <br>   - 后缀支持自定义。命名空间创建后，不支持修改命名空间ID。 | demo |
| **描述** | 命名空间的描述信息，自定义。 | 测试 |
| **专有网络VPC** | 选择已创建的VPC。一个部署环境只能关联一个VPC，但一个VPC能被多个命名空间关联。命名空间创建成功后，您可以根据需求切换关联的VPC。<br>**说明**<br>如果您需要切换目标命名空间关联的VPC，请先删除当前VPC内的所有应用，之后再进行专有网络VPC的切换。 | vpc-wz9i4zexkzbqceo5n\*\*\*\* |



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4772222271/p805171.png)

命名空间创建成功后，可以在 **命名空间** 页面查看详情，进行编辑或删除操作。


## **编辑命名空间**

如果需要修改命名空间的名称及描述，您可以在 **命名空间** 页面，单击目标命名空间 **操作** 列的 **编辑**，修改命名空间信息。

## **删除命名空间**

如果需要删除不再使用的命名空间，您可以在 **命名空间** 页面，单击目标命名空间 **操作** 列的 **删除**，在弹出的对话框中，单击 **确认**。

## **切换专有网络VPC**

1. 在[SAE命名空间](https://saenext.console.aliyun.com/cn-hangzhou/namespace)中，在顶部选择目标地域，点击目标 **命名空间名称** 跳转到命名空间详情页。

2. 在 **基础信息** 页面的 **基本信息** 区域，单击 **专有网络VPC** 右侧的![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6373466961/p723392.png)图标 。

3. 在弹出的 **绑定VPC** 面板，单击 **专有网络VPC** 对应的下拉框，选择目标VPC，然后单击 **确定**。

切换VPC成功后，可以在 **基本信息** 区域查看更新后的VPC。