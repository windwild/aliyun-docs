### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用运维](https://help.aliyun.com/zh/sae/application-operations-maintenance-new/)切换资源类型

# 切换资源类型

更新时间：2025-12-19 01:45:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：变更实例规格](https://help.aliyun.com/zh/sae/change-the-instance-specifications-of-an-application-2-0)[下一篇：切换安全组和vSwitch](https://help.aliyun.com/zh/sae/change-the-security-group-and-vswitch-of-an-application-2-0)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

操作指引

应用部署到Serverless 应用引擎 SAE（Serverless App Engine）后，您可以按需切换应用的计算资源类型，包括默认类型和海光类型。

## 操作指引

1. 在[SAE应用列表](https://saenext.console.aliyun.com/cn-hangzhou/app-list/micro)中，在顶部选择目标地域和命名空间，点击目标 **应用ID** 跳转到应用详情页。

2. 在 **基础信息** 页签的 **应用信息** 区域，单击 **资源类型** 旁的 **切换资源类型**。

3. 在弹出的对话框中配置以下信息，然后单击 **确定**。

1. **资源类型** 选择 **默认** 或 **海光**。



      **参数说明 \- 资源类型**






      **资源类型** 分为 **默认** 和 **海光**， **海光** 目前处于邀约测试阶段。未参与邀约测试的用户， **资源类型** 自动设置为 **默认**，无需手动选择。



      如需使用 **海光** 资源部署应用，请在钉钉群（群号：32874633）联系相关技术人员开通，并且需要选择支持海光资源的地域和可用区：



      - 上海地域：支持可用区B、可用区G和可用区L。

      - 北京地域：支持可用区H、可用区I。

      - 杭州地域：支持可用区J。


2. 选择所需的 [实例规格](https://help.aliyun.com/zh/sae/product-overview/sae-instance-types "")。

3. 选择应用部署所在的 **vSwitch** 和 **可用区**。
4. 等待应用重新部署成功。