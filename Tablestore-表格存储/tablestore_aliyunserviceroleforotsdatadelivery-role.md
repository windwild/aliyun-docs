### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[安全合规](https://help.aliyun.com/zh/tablestore/security-and-compliance/)[使用RAM进行访问控制](https://help.aliyun.com/zh/tablestore/use-ram-for-access-control-for-tablestore/)表格存储服务关联角色

# 表格存储服务关联角色

更新时间：2024-03-10 23:24:44

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：表格存储自定义权限策略参考](https://help.aliyun.com/zh/tablestore/tablestore-custom-permission-policy-reference)[下一篇：使用资源组进行精细化资源控制](https://help.aliyun.com/zh/tablestore/fine-grained-resource-control-using-resource-groups-50)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

应用场景

RAM用户使用服务关联角色需要的权限

创建服务关联角色

查看服务关联角色

删除服务关联角色

常见问题

使用表格存储数据湖投递功能时，需要具有OSS资源的访问权限，此时可以通过表格存储控制台自动创建表格存储服务关联角色AliyunServiceRoleForOTSDataDelivery用于获取对OSS资源的访问权限。

## **背景信息**

服务关联角色是一种可信实体为阿里云服务的RAM角色。表格存储使用服务关联角色获取其他云服务或云资源的访问权限。

通常情况下，服务关联角色是在您执行某项操作时，由系统自动创建。在自动创建服务关联角色失败或表格存储不支持自动创建时，您需要手动创建服务关联角色。

阿里云访问控制为每个服务关联角色提供了一个系统权限策略，该策略不支持修改。如果您想了解该系统策略的具体内容，可前往指定服务关联角色的详情页面查看。

**说明**

关于服务关联角色的更多信息，请参见 [服务关联角色](https://help.aliyun.com/zh/ram/user-guide/service-linked-roles#concept-2448621 "")。

## **应用场景**

在使用表格存储的数据湖投递功能时，表格存储会自动创建服务关联角色AliyunServiceRoleForOTSDataDelivery，用于允许表格存储访问OSS资源。

## RAM用户使用服务关联角色需要的权限

如果使用RAM用户创建或删除服务关联角色，必须联系管理员为该RAM用户授予管理员权限（AliyunXXXFullAccess）或在自定义权限策略的`Action`语句中为RAM用户添加以下权限：

- 创建服务关联角色：`ram:CreateServiceLinkedRole`

- 删除服务关联角色：`ram:DeleteServiceLinkedRole`


关于授权的详细操作，请参见 [创建和删除服务关联角色所需的权限](https://help.aliyun.com/zh/ram/user-guide/service-linked-roles#concept-2448621/section-x3u-5xc-09l "")。

## 创建服务关联角色

使用表格存储数据湖投递功能时，通过表格存储控制台可以自动创建表格存储服务关联角色AliyunServiceRoleForOTSDataDelivery。

表格存储服务关联角色AliyunServiceRoleForOTSDataDelivery对应的权限策略为AliyunServiceRolePolicyForOTSDataDelivery，支持的OSS操作为PutObject、AbortMultipartUpload、PutObjectTagging、GetObject和DeleteObjectTagging。

## **查看服务关联角色**

当服务关联角色创建成功后，您可以在 [RAM控制台的角色页面](https://ram.console.aliyun.com/roles)，通过搜索AliyunServiceRoleForOTSDataDelivery查看该服务关联角色的以下信息：

- **基本信息**

在AliyunServiceRoleForOTSDataDelivery角色详情页面的 **基本信息** 区域，查看角色基本信息，包括角色名称、创建时间、角色ARN和备注等。

- **权限策略**

在AliyunServiceRoleForOTSDataDelivery角色详情页面的 **权限管理** 页签，单击权限策略名称，查看权限策略内容以及该角色可授权访问哪些云资源。

- **信任策略**

在AliyunServiceRoleForOTSDataDelivery角色详情页的 **信任策略** 页签，查看信任策略内容。信任策略是描述RAM角色可信实体的策略，可信实体是指可以扮演RAM角色的实体用户身份。服务关联角色的可信实体为云服务，您可以通过信任策略中的`Service`字段查看。


关于如何查看服务关联角色的详细操作，请参见 [查看RAM角色](https://help.aliyun.com/zh/ram/user-guide/view-the-information-about-a-ram-role#task-188120 "")。

## 删除服务关联角色

请确保当前账号下所有实例均未使用数据湖投递功能，才能删除表格存储服务关联角色（AliyunServiceRoleForOTSDataDelivery）。

**重要**

删除表格存储服务关联角色后，当前账号下的数据将无法投递到OSS。

删除服务关联角色的操作步骤如下：

1. 登录[RAM控制台](https://ram.console.aliyun.com/)。

2. 在左侧导航栏中，选择 **身份管理** > **角色**。

3. 在 **角色** 页面的搜索框中，输入AliyunServiceRoleForOTSDataDelivery，单击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0847210171/p776624.png)图标或者按【Enter】键。

4. 在RAM角色右侧 **操作** 列，单击 **删除角色**。

5. 在 **删除角色** 对话框，输入角色名称确认删除操作，单击 **删除角色**。

   - 如果当前账号下有实例使用数据湖投递功能，将无法删除该角色。请删除实例下的投递任务后重试删除操作。

   - 如果当前账号下所有实例均未使用数据湖投递功能，则可直接删除该角色。

## 常见问题

为什么使用RAM用户无法自动创建表格存储服务关联角色（AliyunServiceRoleForOTSDataDelivery）？

只有拥有指定权限的用户，才能自动创建或删除表格存储服务关联角色。当RAM用户无法自动创建表格存储服务关联角色时，需要为RAM用户添加如下权限策略。

使用时请将 _主账号ID_ 替换为实际的阿里云账号（主账号）ID。

```json
{
    "Statement": [\
        {\
            "Action": [\
                "ram:CreateServiceLinkedRole"\
            ],\
            "Resource": "acs:ram:*: 主账号ID :role/*",\
            "Effect": "Allow",\
            "Condition": {\
                "StringEquals": {\
                    "ram:ServiceName": [\
                        "arms.aliyuncs.com"\
                    ]\
                }\
            }\
        }\
    ],
    "Version": "1"
}
```