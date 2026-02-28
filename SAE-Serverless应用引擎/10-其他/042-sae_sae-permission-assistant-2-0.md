### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[权限管理](https://help.aliyun.com/zh/sae/permission-management-overview-new/)SAE权限助手

# SAE权限助手

更新时间：2025-01-23 04:35:28

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：权限策略和示例](https://help.aliyun.com/zh/sae/policies-and-examples-2-0)[下一篇：为RAM用户授权](https://help.aliyun.com/zh/sae/grant-permissions-to-a-ram-user-2-0)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

背景信息

步骤一：在SAE控制台创建权限策略

步骤二：在RAM控制台创建自定义权限策略

步骤三：在RAM控制台为RAM用户添加授权

Serverless 应用引擎 SAE（Serverless App Engine）提供权限助手功能，简化SAE相关的RAM权限策略配置。本文介绍如何通过SAE权限助手快速创建权限语句，并在RAM控制台完成最终的权限策略配置。

## 前提条件

[创建RAM用户](https://help.aliyun.com/zh/sae/grant-permissions-to-a-ram-user-2-0#section-qaf-me1-om9 "")

## 背景信息

SAE权限助手是一个生成RAM权限策略的工具，能够协助您对SAE的权限进行可视化配置，精确到应用、任务的读写操作，并在SAE控制台生成对应的权限语句，避免因直接在RAM控制台手动编辑权限语句而出现纰漏。然后，您可以在RAM控制台创建对应的自定义权限策略，将权限策略的策略内容修改为该权限语句，并为需要该项SAE权限的RAM用户授予权限。

阿里云账号（主账号）和RAM用户（子账号）均可在SAE控制台通过权限助手创建权限策略草稿，但该策略只有在部署到RAM控制台后，才具备实际的限制能力。

## 步骤一：在SAE控制台创建权限策略

1. 在 [SAE控制台](http://saenext.console.aliyun.com/) 左侧导航栏，选择**企业级特性** \> **权限管理**。然后在 **权限助手** 页面，单击 **新建权限策略**。

2. 在 **新建权限策略** 面板的 **权限策略配置** 配置向导，完成以下操作并单击 **下一步**。


1. 输入 **策略名称** 和 **备注**。






      | **配置项** | **说明** |
      | --- | --- |



      |     |     |
      | --- | --- |
      | **配置项** | **说明** |
      | **策略名称** | 权限策略的自定义名称。必须以字母开头，允许数字、字母、下划线（\_）以及短划线（-）组合，不超过36个字符。 |
      | **备注** | 权限策略的说明。 |

2. 单击 **新增权限语句**，在 **新增权限语句** 面板完成以下操作并单击 **确定**。






      | **配置项** | **说明** |
      | --- | --- |



      |     |     |
      | --- | --- |
      | **配置项** | **说明** |
      | **授权资源** | 在下拉列表中依次选择资源维度。<br>      - 地域：支持单选。<br>        <br>      - 命名空间：支持单选。<br>        <br>      - 应用或任务：支持多选。 |
      | **授权操作** | 在 **可选权限** 复选框内选中需要授予的权限，在 **已选权限** 预览框内查看已选权限。授权操作的限制如下：<br>      - **搜索操作** 文本框支持模糊搜索，区分英文字母大小写。<br>        <br>      - **已选权限** 复选框默认显示 **系统默认读权限**。<br>        <br>      - 读写操作具有联动性，因此在选择读写权限时，系统会自动判断并帮您勾选相关的权限。例如当您在写权限下选中**应用** \> **发布变更**时，系统会自动勾选与其相关的读权限。 |





      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3860222271/p826008.png)


您可以在 **权限策略配置** 配置向导查看已添加的权限语句，按需执行 **查看权限**、 **克隆**、 **编辑** 或 **删除** 操作。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0901092371/p826010.png)

**说明**

   - 如果您需要对多个命名空间的资源进行权限设置，请新增多条权限语句。

   - 如果您需要复制现有的权限语句或在其基础上进行编辑新增，可以单击 **克隆**，进入 **克隆** 权限语句面板，按需编辑并新增权限语句。


3. 在 **权限策略预览** 配置向导，检查生成的权限语句，然后单击 **完成**。



您可以单击 **一键复制**，复制的RAM授权语句将用于 [步骤二：在RAM控制台创建自定义权限策略](https://help.aliyun.com/zh/sae/sae-permission-assistant-2-0#section-s0w-yq9-m5h "")。





控制台面板将会返回 **权限助手** 页面，您可以查看新建的权限策略，并按需执行 **查看权限**、 **一键复制RAM授权语句**、 **编辑** 或 **删除** 操作。





**重要**





   - 通过SAE权限助手生成的权限策略仅适用于操作SAE的资源，且不能超过20条。

   - 当SAE上线新功能时，您需要重新生成RAM权限语句，否则可能会导致原有权限策略下的RAM用户不具备该新功能的权限。


## 步骤二：在RAM控制台创建自定义权限策略

在RAM控制台创建自定义策略时，您需要将权限策略的内容修改为 [步骤一：在SAE控制台创建权限策略](https://help.aliyun.com/zh/sae/sae-permission-assistant-2-0#section-zif-s3a-o0c "") 生成的权限语句。

1. 使用RAM管理员登录 [RAM控制台](https://ram.console.aliyun.com/)。

2. 在左侧导航栏，选择**权限管理** \> **权限策略**。

3. 在 **权限策略** 页面，单击 **创建权限策略**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4370193371/p886177.png)

4. 在 **创建权限策略** 页面，单击 **脚本编辑** 页签。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6370193371/p886214.png)

5. 输入权限策略内容。



关于权限策略语法结构的详情，请参见 [权限策略语法和结构](https://help.aliyun.com/zh/ram/policy-structure-and-syntax#concept-srq-fbk-xdb "")。

6. 单击页面上方的 **可选：高级策略优化**，然后单击 **执行**，对权限策略内容进行高级优化。

高级权限策略优化功能会完成以下任务：

   - 拆分不兼容操作的资源或条件。

   - 收缩资源到更小范围。

   - 去重或合并语句。
7. 在 **创建权限策略** 页面，单击 **确定**。

8. 在 **创建权限策略** 对话框，输入权限策略 **名称** 和 **备注**，然后单击 **确定**。


## 步骤三：在RAM控制台为RAM用户添加授权

成功创建自定义权限策略后，您需要在RAM控制台为需要该项权限的RAM用户授权。本文以在用户页面为RAM用户授权的方式为例，操作步骤如下所示。更多方式，请参见 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user#task-187800 "")。

1. 使用RAM管理员登录 [RAM控制台](https://ram.console.aliyun.com/)。

2. 在左侧导航栏，选择**身份管理** \> **用户**。

3. 在 **用户** 页面，单击目标RAM用户 **操作** 列的 **添加权限**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7307214171/p794639.png)

您也可以选中多个RAM用户，单击用户列表下方的 **添加权限**，为RAM用户批量授权。

4. 在 **新增授权** 面板，为RAM用户添加权限。


1. 选择资源范围。

      - **账号级别**：权限在当前阿里云账号内生效。

      - **资源组级别**：权限在指定的资源组内生效。



        **重要**





        指定资源组授权生效的前提是该云服务及资源类型已支持资源组，详情请参见 [支持资源组的云服务](https://help.aliyun.com/zh/resource-management/resource-group/product-overview/services-that-work-with-resource-group#concept-flc-p3m-4fb "")。资源组授权示例，请参见 [使用资源组限制RAM用户管理指定的ECS实例](https://help.aliyun.com/zh/ram/use-cases/use-a-resource-group-to-manage-an-ecs-instance "")。
2. 选择授权主体。

      授权主体即需要添加权限的RAM用户。系统会自动选择当前的RAM用户。

3. 选择权限策略。

      权限策略是一组访问权限的集合，分为以下两种。支持批量选中多条权限策略。

      - 系统策略：由阿里云创建，策略的版本更新由阿里云维护，用户只能使用不能修改。更多信息，请参见 [支持RAM的云服务](https://help.aliyun.com/zh/ram/product-overview/services-that-work-with-ram "")。



        **说明**





        系统会自动标识出高风险系统策略（例如：AdministratorAccess、AliyunRAMFullAccess等），授权时，尽量避免授予不必要的高风险权限策略。

      - 自定义策略：由用户管理，策略的版本更新由用户维护。用户可以自主创建、更新和删除自定义策略。更多信息，请参见 [创建自定义权限策略](https://help.aliyun.com/zh/ram/create-a-custom-policy "")。
4. 单击 **确认新增授权**。


5. 单击 **关闭**。