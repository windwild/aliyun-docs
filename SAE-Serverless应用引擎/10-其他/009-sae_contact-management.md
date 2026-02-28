### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[权限管理](https://help.aliyun.com/zh/sae/permission-management-overview-new/)联系人管理

# 联系人管理

更新时间：2025-03-18 22:29:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：为RAM角色授权](https://help.aliyun.com/zh/sae/grant-permissions-to-a-ram-role-2-0)[下一篇：操作审批](https://help.aliyun.com/zh/sae/approval-configuration)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

步骤一：为RAM用户（子账号）授予ListUsers权限

1\. 创建自定义权限策略

2\. 为子账号（RAM用户）授权

步骤二：创建联系人

步骤三：管理联系人

SAE允许您为指定联系人设置权限规则，并配置通知发送等功能。当需要进行权限审批或触发报警时，SAE会通过邮件、钉钉机器人或企业微信机器人等方式向相关联系人发送通知。本文详细说明如何在SAE控制台中完成联系人的创建、查看、编辑及删除操作。

## 背景信息

一个阿里云账号（主账号）下可以创建多个RAM用户（子账号），对应企业内的员工、系统或应用程序；ARMS联系人是处理告警的运维人员，联系人可以通过设定的联系方式查看、处理和解决告警。其中，SAE的联系人起着承上启下的作用。通过设置SAE联系人，SAE将原本互相独立的RAM用户与ARMS联系人打通，达到三个云产品间信息互通的效果。具体过程如下。

通过SAE设置联系人时，需输入用户名（阿里云账号或RAM用户）和手机号码，然后通过关联手机号码，可以将现有的ARMS联系人与SAE联系人相匹配。同时，ARMS联系人的姓名会以RAM用户的名称进行覆盖更新。

![dg_sae_contact_workflow](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7611266361/p347157.png)

在SAE新建联系人时会遇到以下情况：

- 手机号码在ARMS侧没有被新建过，则会新建一个ARMS联系人，该联系人会与SAE的联系人进行绑定。

- 手机号码已经存在于某一个ARMS联系人中，同时该ARMS联系人还未被该阿里云账号（主账号）下的其他SAE联系人（通过手机号码）匹配（即绑定），则会将SAE联系人与ARMS联系人进行绑定。

- 手机号码已经存在于某一个ARMS联系人中，但是该ARMS联系人已经被该阿里云账号（主账号）下的其他SAE联系人（通过手机号码）匹配（即绑定），则会新建失败，需要更换设置手机号码。


一旦经过初次绑定，只要不触发重新绑定（合并联系人），后续在SAE控制台修改通信信息（包括手机号码）都不会影响绑定，同时会覆盖更新ARMS联系人的通信信息。

**重要**

SAE联系人的通信信息，随ARMS的信息变更而变更。导致SAE事件通知失效的注意事项如下。

- 请勿在ARMS控制台手动删除名字以`sae:`前缀开头的联系人、联系人组和通知策略。

- 请谨慎在ARMS控制台修改联系人组。


## **步骤一：为** RAM用户（子账号） **授予** ListUsers权限

如果您操作的是子账号，并且需要添加多个子账号为联系人，请按照以下步骤为子账号授予`ListUsers`权限。

**重要**

如果您操作的账号是阿里云账号（主账号），则无需为主账号添加以下的权限，请跳过此步骤。

### **1\. 创建自定义权限策略**

1. 使用阿里云账号（主账号）登录 [RAM控制台](https://ram.console.aliyun.com/overview?activeTab=overview)，在左侧导航栏选择**权限管理** \> **权限策略**，在 **权限策略** 页面单击 **创建权限策略**。

2. 在 **创建权限策略** 页面，单击 **脚本编辑** 页签，将以下权限策略粘贴到控制台，然后单击 **确定**。















```json
{
     "Version": "1",
     "Statement": [\
       {\
         "Effect": "Allow",\
         "Action": [\
           "ram:ListUsers",\
           "ram:GetUser"\
         ],\
         "Resource": "*"\
       }\
     ]
}
```



![PoJZojMNep](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9716399371/p917946.png)

3. 在弹出的 **创建权限策略** 对话框，自定义权限的 **名称** 和 **备注**，然后单击 **确定**。


### **2\. 为子账号（RAM用户）授权**

1. 在左侧导航栏选择**身份管理** \> **用户**，在用户页面单击需要授权的用户登录名称。

2. 在用户的详情页面，单击 **权限管理** 页签，然后在 **个人权限** 页签单击 **新增授权**。

![aCXSLDJXKj](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2088339371/p913106.png)

3. 在弹出的 **新增授权** 面板的 **权限策略** 区域，在权限类型的下拉框中选择 **自定义权限**，勾选上一步骤创建的自定义权限，然后单击 **确认新增授权**。

![58Vob1j4c0](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9716399371/p918176.png)

授权完成后，可以在RAM用户的 **个人权限** 页签查看为用户授予的全部权限。


## 步骤二：创建联系人

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)，在左侧导航栏选择**企业级特性** \> **联系人管理**。

2. 在 **联系人管理** 页面，单击 **创建联系人**。

3. 在弹出的 **新建联系人** 面板，按照表格说明配置参数信息，然后单击 **确定**。




| **配置项** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **配置项** | **说明** |
| **用户名（阿里云登录账号）** | 支持以下两种方式添加账号信息：<br>   - 阿里云账号：通过手动输入。<br>     <br>   - RAM用户：通过下拉列表选择。<br>     <br>最多支持创建100个联系人。<br>**重要**<br>   - 阿里云账号（主账号）可以把所有子账号创建为联系人，也可以管理所有子账号创建的联系人。<br>     <br>   - 如果子账号（RAM用户）没有`ListUsers`权限，只能添加自己为联系人，如果有`ListUsers`权限，可添加其他RAM用户为联系人。添加权限的具体步骤，请参见 [为RAM用户（子账号）授予ListUsers权限](https://help.aliyun.com/zh/sae/contact-management#b668b07d46282 "")。 |
| **手机号码** | 每个手机号码只能用于一个联系人。输入正确的中国内地（不含中国香港、中国澳门、中国台湾）手机号码，例如1381111\*\*\*\*。 |
| **邮箱** | 填写用于接收消息通知的邮箱号。输入正确的邮箱格式，例如username@example.com。 |
| **钉钉机器人** | 填写钉钉机器人的Webhook地址。获取钉钉机器人地址的方式，请参见 [获取钉钉机器人Webhook地址](https://help.aliyun.com/zh/sae/contact#da1e52604cdg7 "")。 |
| **企业微信机器人** | 填写企业微信机器人的Webhook地址。获取企业微信机器人的方式，请参见 [企业微信机器人](https://help.aliyun.com/zh/arms/alarm-operation-center/wecom-chatbots "")。 |


## 步骤三：管理联系人

创建联系人后，您可以在 **联系人管理** 页面查询、 **编辑**、 **删除** 或 **合并联系人**。

![Ax1uN34RNO](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9716399371/p917782.png)

- **查询：** 支持通过 **用户名**、 **手机号码** 或 **邮箱** 进行筛选。默认以用户名作为筛选条件，您可以在下拉框中选择其他筛选条件，并在文本框中输入具体的筛选内容。

- **编辑：** 单击 **操作** 列的 **编辑**，在 **编辑联系人** 对话框中编辑信息，然后单击 **确定**。

- **删除：** 单击 **操作** 列的 **删除**，然后在 **删除联系人** 对话框中单击 **确定**。



**重要**





联系人删除成功后，会同步删除ARMS的联系人。

- **合并联系人：** 单击 **合并联系人**，然后在 **合并联系人** 对话框中单击 **确** 定。

合并联系人会将RAM用户与ARMS已有的通知告警联系人以手机号进行关联，并且会以RAM用户名更新覆盖ARMS联系人名称。若RAM用户信息中的手机号码在ARMS联系人中不存在，则会以该号码新建一个联系人。