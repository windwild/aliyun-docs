### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 添加应用

# 添加应用

更新时间：2026-01-05 03:14:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是日志服务](https://help.aliyun.com/zh/sls/what-is-log-service)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

添加应用

获取应用ID

后续步骤

移动运维监控应用用于管理已接入的监控数据。本文介绍添加应用的操作步骤。

**警告**

目前移动运维监控应用不支持新增用户，已开通移动运维监控应用的用户可以继续使用。

## 前提条件

已创建Project。具体操作，请参见 [管理Project](https://help.aliyun.com/zh/sls/manage-a-project/#section-ahq-ggx-ndb "")。

## 添加应用

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。

2. 在**日志应用** \> **智能运维**页签，单击 **移动运维监控**。

3. 单击 **添加应用**。

4. 在 **添加应用** 面板中，配置如下参数，然后单击 **确定**。






| **参数** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **描述** |
| **应用名称** | 移动运维监控应用的名称。 |
| **应用描述** | 移动运维监控应用的描述信息。 |
| **项目Project** | 用于存储监控数据的Project。 |
| **地域** | 显示您所选择的Project的所在地域。 |
| **选择类型** | 监控数据的来源。 |
| **角色权限** | 日志服务使用AliyunLogETLRole访问LogStore中的数据。<br>如果您使用的阿里云账号还未完成AliyunLogETLRole授权，请单击 **您需要授权系统角色AliyunLogETLRole**，根据页面提示完成授权。<br>如果您要使用RAM用户操作，则使用阿里云账号完成AliyunLogETLRole授权后，还需要使用阿里云账号授予RAM用户数据加工操作权限。更多信息，请参见 [授权RAM用户操作数据加工](https://help.aliyun.com/zh/sls/authorized-ram-user-operation-data-processing#task-2005445 "")。 |


## 获取应用ID

您可以在 **修改应用** 面板中，获取应用ID。

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。

2. 在 **日志应用** 区域，单击 **移动运维监控**。

3. 在应用列表中，找到目标应用，单击 **修改**。

4. 在 **修改应用** 面板中，获取应用ID。



请记录该ID，在上传数据时您需要输入该ID。


## 后续步骤

接入数据：

- [接入Android App监控数据](https://help.aliyun.com/zh/sls/collect-metric-data-from-android-apps#concept-2085372 "")

- [接入iOS App监控数据](https://help.aliyun.com/zh/sls/collect-metric-data-from-ios-apps#concept-2085373 "")