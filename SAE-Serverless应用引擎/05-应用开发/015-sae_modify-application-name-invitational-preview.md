### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用运维](https://help.aliyun.com/zh/sae/application-operations-maintenance-new/)修改应用名称（邀测）

# 修改应用名称（邀测）

更新时间：2025-04-10 22:51:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：切换安全组和vSwitch](https://help.aliyun.com/zh/sae/change-the-security-group-and-vswitch-of-an-application-2-0)[下一篇：管理应用标签](https://help.aliyun.com/zh/sae/edit-application-label)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

操作步骤

应用创建完成后，支持修改应用名称。

**重要**

此功能目前处于邀约测试阶段。如果您想使用此功能，请在钉钉群（群号：32874633）联系相关技术人员开通。

## **注意事项**

SAE集成了一些其他阿里云服务，应用改名后会对集成的服务产生一定的影响。具体介绍如下所示。

| **关联的服务** | **相关功能** | **影响说明** | **解决方案** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **关联的服务** | **相关功能** | **影响说明** | **解决方案** |
| ARMS | 调用链查询 | 由于调用链分析是使用应用名称做的索引，更改应用名称后，默认查询不到改名前的数据信息。<br>改名前的数据示例：<br>![h3TLtKjpZO](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1989334471/p940631.png)<br>改名后的数据示例：<br>![tUXXk6PZI7](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1989334471/p940638.png) | 修改完应用名称后，如果您想查询改名前的数据，只需将应用名称修改成旧的应用名称，即可查询到旧的数据。 |

## **操作步骤**

支持通过以下两种方式修改应用名称。

方式一

方式二

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**。

2. 在 **应用列表** 页面，将鼠标悬停在目标应用名称上，然后单击![Yuyd3ALCfg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1989334471/p940256.png)图标。

![41VBbbyZ1r](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1989334471/p940272.png)

3. 在弹出的文本框中修改应用名称，单击 **确定**。


1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

2. 在 **基础信息** 页面的 **应用信息** 页签，将鼠标悬停在应用名称上，单击![WfMN7Or3hp](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1989334471/p940312.png)图标。

![TOKPqrTU2A](<Base64-Image-Removed>)

3. 在弹出的文本框中修改应用名称，单击 **确定**。