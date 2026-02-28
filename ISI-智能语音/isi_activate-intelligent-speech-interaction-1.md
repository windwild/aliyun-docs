### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 准备账号

# 准备账号

更新时间：2023-02-28 21:18:46

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是智能语音交互](https://help.aliyun.com/zh/isi/product-overview/what-is-intelligent-speech-interaction)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

准备阿里云账号

步骤一：注册阿里云账号

步骤二：阿里云账号实名认证

步骤三：创建访问密钥AccessKey

准备RAM用户

步骤一：创建RAM用户

步骤二：创建访问密钥AccessKey

步骤三：为RAM用户授权

后续步骤

在使用智能语音交互产品前，您需要准备好阿里云账号。本文为您介绍如何创建阿里云账号及配置RAM用户权限等相关准备工作。

## 准备阿里云账号

### 步骤一：注册阿里云账号

1. 打开 [阿里云官网](https://www.aliyun.com/)。

2. 在阿里云官网右上角，单击 **立即注册**。

3. 在 **注册账号** 页面，按照操作提示完成账号注册。

创建成功的阿里云账号，会作为阿里云系统识别的资源消费账户，阿里云账号拥有该账户的所有权限。



**警告**





**为保证账号和密码的安全性，请勿借给他人使用，并定期更新密码。**


### 步骤二：阿里云账号实名认证

**为保证后续操作顺利进行，请务必完成实名认证操作。** 阿里云账号需要进行实名制认证后，才可以购买和使用阿里云的产品。

1. 进入 [账号管理](https://account.console.aliyun.com/#/secure) 页面。

2. 在左侧导航栏，单击 **实名认证**，按照操作提示完成账号实名认证。

如果您是企业用户，推荐进行企业认证，以便获取更多便利。更多实名认证操作信息，请参见 [实名认证](https://help.aliyun.com/zh/account/verify-your-identity-enterprise-account/#topic-2149080 "")。


### 步骤三：创建访问密钥AccessKey

1. 进入 [AccessKey管理](https://ram.console.aliyun.com/manage/ak) 页面。

2. 在 **AccessKey管理** 页面，单击 **创建AccessKey**，系统会自动创建AccessKey。

3. 在 **创建AccessKey** 对话框中，查看AccessKey ID和AccessKey Secret。

您可以单击 **下载CSV文件**，下载AccessKey信息；或者单击 **复制**，复制AccessKey信息。

4. 单击 **关闭**。



**重要**









   - **为保证AccessKey ID和AccessKey Secret的安全性，请勿借给他人使用，一旦有泄漏的风险，请及时禁用或更新AccessKey。**

   - AccessKey Secret只在创建时显示，不支持查询，请妥善保管。

   - 禁用AccessKey后，使用该AccessKey的服务将运行失败并报错，请谨慎操作。如果AccessKey状态变更，需要及时关注使用该AccessKey的产品和服务。


为避免产生项目数据安全性问题，推荐您创建RAM用户并交由其他用户使用，实现对参与智能语音交互项目的人员权限进行严格把控。具体请参见 [准备RAM用户](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1#section-5s8-8ig-h03 "")。

## 准备RAM用户

**重要**

- RAM用户归属于阿里云账号，本身不拥有资源，也没有独立的计量计费机制。

- RAM用户在阿里云各产品中操作产生的费用，将在RAM用户归属的阿里云账号下统一计费。


### 步骤一：创建RAM用户

1. 使用阿里云账号登录 [RAM控制台](https://ram.console.aliyun.com/)。

2. 在左侧导航栏，选择 **身份管理>用户**。

3. 在 **用户** 页面，单击 **创建用户**。

4. 在 **创建用户** 页面的 **用户账号信息** 区域，输入 **登录名称** 和 **显示名称**。



**说明**





单击 **添加用户**，可一次性创建多个RAM用户。

5. 在 **访问方式** 区域，选择访问方式。

   - **控制台访问**：设置控制台登录密码、重置密码策略和多因素认证策略。



     **说明**





     自定义登录密码时，密码必须满足密码复杂度规则。关于如何设置密码复杂度规则，请参见 [设置RAM用户密码强度](https://help.aliyun.com/zh/ram/user-guide/configure-a-password-policy-for-ram-users#task-188785 "")。

   - **OpenAPI调用访问**：自动为RAM用户生成访问密钥（AccessKey），支持通过API或其他开发工具访问阿里云。



     **说明**





     为了保障账号安全，建议仅为RAM用户选择一种登录方式，避免RAM用户离开组织后仍可以通过访问密钥访问阿里云资源。
6. 单击 **确定**。

7. 在 **安全验证** 对话框中按照指引完成验证。


### 步骤二：创建访问密钥AccessKey

**重要**

- 如果阿里云账号允许RAM用户自主管理AccessKey，RAM用户也可以自行创建AccessKey。更多自主管理AccessKey操作，请参见 [设置RAM用户安全策略](https://help.aliyun.com/zh/ram/user-guide/manage-security-settings-of-ram-users#task-188786 "")。

- 一个RAM用户下最多可以创建2个AccessKey。


1. 在左侧导航栏，选择 **身份管理>用户**。

2. 在 **用户** 页面，单击目标RAM用户名称。

3. 在 **用户AccessKey** 区域，单击 **创建AccessKey**，系统会自动创建AccessKey。

4. 在 **创建AccessKey** 对话框中，查看AccessKey ID和AccessKey Secret。

您可以单击 **下载CSV文件**，下载AccessKey信息；或者单击 **复制**，复制AccessKey信息。

5. 单击 **关闭**。



**重要**









   - **为保证AccessKey ID和AccessKey Secret的安全性，请勿借给他人使用，一旦有泄漏的风险，请及时禁用或更新AccessKey。**

   - AccessKey Secret只在创建时显示，不支持查询，请妥善保管。

   - 禁用AccessKey后，使用该AccessKey的服务将运行失败并报错，请谨慎操作。如果AccessKey状态变更，需要及时关注使用该AccessKey的产品和服务。


### 步骤三：为RAM用户授权

1. 在左侧导航栏，选择 **身份管理>用户**。

2. 在 **用户** 页面，单击目标RAM用户 **操作** 列的 **添加权限**。

3. 在 **添加权限** 面板，为RAM用户添加权限。

1. **授权范围** 选择 **整个云账号**。

2. 输入被授权主体。

      被授权主体即需要授权的RAM用户，系统会自动填入当前的RAM用户，您也可以添加其他RAM用户。

3. 选择权限策略。


      1. 选择 **系统策略**，并在下方输入框中输入`nls`，系统将自动匹配出智能语音交互相关的系统策略。

      2. 在权限策略名称列表下单击 **AliyunNLSFullAccess** 权限，添加至右侧已选择权限列表。


![系统策略](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9313562361/p332563.png)智能语音交互相关系统策略如下所示，以供参考。

| 权限策略名称 | 备注 | 说明 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 权限策略名称 | 备注 | 说明 |
| AliyunNLSFullAccess | 管理智能语音交互（NLS）的权限 | 允许访问和操作全部智能语音交互的API接口以及管控台。 |
| AliyunNLSReadOnlyAccess | 只读访问智能语音交互（NLS）的权限 | 允许只读访问全部智能语音交互的API接口以及管控台。 |
| AliyunNLSSpeechServiceAccess | 管理智能语音交互（NLS）语音服务的权限 | 允许调用和操作智能语音交互语音服务相关的API。 |
| AliyunNLSSlpAccess | 管理智能语音交互（NLS）自学习平台的权限 | 允许调用和操作智能语音交互自学习平台的热词以及语言模型的API。 |
4. 单击 **确定**。

5. 单击 **完成**。


## 后续步骤

准备好阿里云账号或RAM用户后，即可开通智能语音交互服务，具体请参见 [开通服务](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction#topic-2117860 "")。