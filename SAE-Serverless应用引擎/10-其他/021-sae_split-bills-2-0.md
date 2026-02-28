### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)企业分账

# 企业分账

更新时间：2024-11-29 02:19:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：服务关联角色](https://help.aliyun.com/zh/sae/service-linked-role-2-0)[下一篇：应用托管概述](https://help.aliyun.com/zh/sae/application-deployment-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

背景信息

使用说明

步骤一：设置应用标签

步骤二：在分账管理中查看费用

更多信息

Serverless 应用引擎 SAE（Serverless App Engine）为应用提供了标签功能。您可以为托管在SAE的应用创建并绑定标签，并通过标签的分类实现企业分账管理。本文介绍如何为应用设置标签，以及利用标签按需查看企业的分账费用信息。

## 前提条件

- [已开通阿里云分账账单](https://usercenter2.aliyun.com/finance/split-bill)。

- [已完成准备工作](https://help.aliyun.com/zh/sae/sae-2-preparations#section-cu5-k9p-xuf "")。

准备工作包括开通SAE服务并授权、为RAM用户授权（可选）、创建命名空间和创建VPC。其中，如果RAM用户需要查看分账账单，那么您需要先通过阿里云账号为RAM用户授予AliyunBBSReadOnlyAccess权限，此后RAM用户可在阿里云费用与成本控制台查看账单以及在SAE控制台的 **概览页** 查看资源包用量等信息。

如果RAM用户还需要查看更精细化的账单信息，阿里云账号可以为其授予费用与成本的权限策略。更多信息，请参见 [费用与成本权限策略介绍](https://help.aliyun.com/zh/user-center/ram-policies-for-billing-management#0db08970a5xcv "")。

- [已部署应用到SAE](https://help.aliyun.com/zh/sae/sae-application-deployment/ "")。


## 背景信息

随着创建的应用逐渐增多，利用标签将资源进行分组管理和归类便于搜索、聚合资源，为不同环境或项目等设置不同的标签。示例如下。

- 环境隔离：为不同的环境（例如生产环境和测试环境）、操作系统（例如Windows Server和Linux）或者客户端平台（例如iOS和Android）绑定不同的标签。

- 项目管理：在团队或者项目管理中，添加以群组、项目或部门为维度的标签（例如CostCenter:aliyun），实现分组、分账管理。


![dg_example_of_tag_usage_scenarios](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4600543461/p396525.png)

SAE实现企业分账的操作方法如下。

1. 基于组织或业务维度，为资源（应用）规划标签。（图示中①）

2. 登录 [SAE控制台](http://saenext.console.aliyun.com/)，为应用绑定标签，建立应用和标签的关系。（图示中②）

3. 登录[费用与成本](https://billing-cost.console.aliyun.com/home)，查看费用账单。（图示中③）


## 使用说明

- 标签都由一对键值对（Key:Value）组成。

- 资源的任一标签的标签键（Key）必须唯一。

- 不同地域中的标签信息不互通。

- 解绑标签时，如果解绑之后该标签不再绑定任何资源，该标签会自动被删除。


## 步骤一：设置应用标签

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击 **创建应用**。

![xxQdc1LHvq](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8475962371/p878311.png)

2. 在 **基本信息** 页面 **应用信息** 页签 **应用标签** 区域，单击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0129142271/p825223.png)图标，进入 **编辑标签** 对话框。

您也可以在 **应用列表** 页面，将鼠标悬停至目标应用 **标签** 列的![标签](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2353649951/p96950.png)图标，然后单击标签气泡内的 **绑定**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0129142271/p825225.png)

当应用较多时，您可以在 **应用列表** 页面的搜索栏，选择 **应用名称**、 **应用ID**、 **SLB IP** 或 **实例IP**，并输入相应的参数，单击![bt_search_application](<Base64-Image-Removed>)图标，搜索目标应用。

3. 在 **编辑标签** 对话框，按需管理标签。

   - **新增**：在 **标签键** 和 **标签值** 文本框添加，然后单击 **确定**。



     **说明**





     - 每个应用最多可绑定20个标签。

     - 单次绑定或者解绑标签的数量均不超过20个。


   - **删除**：选择需要删除的键值对，单击其右侧的![bt_delete_label](<Base64-Image-Removed>)图标，然后单击 **确定**。



     **说明**





     应用绑定标签后，如果标签中的标签键值对全部删除，该标签也将被删除。

   - **编辑**：选择需要编辑的键值对，设置标签的 **标签键** 和 **标签值**，然后单击 **确定**。
4. 结果验证。

   - 在 **应用列表** 页面验证。

     1. 在 **应用列表** 页面，将鼠标悬停至目标应用 **标签** 列的![标签](<Base64-Image-Removed>)图标，在标签气泡内查看标签。

     2. **可选：**单击标签气泡内的 **编辑**，在 **编辑标签** 对话框查看标签详情。
   - 在 **基本信息** 页面验证。

     1. 在 **应用列表** 页面，单击目标应用，进入 **基本信息** 页面。

     2. 在 **应用信息** 页签 **应用标签** 区域，单击![image](<Base64-Image-Removed>)图标，在 **编辑标签** 对话框查看标签详情。

## 步骤二：在分账管理中查看费用

1. 登录[费用与成本控制台](https://billing-cost.console.aliyun.com/home)。

2. 在左侧导航栏，选择**成本分摊** \> **费用标签**，启用费用标签。


   - 从未启用过![bt_enable_tagging_fees(next)](<Base64-Image-Removed>)

     1. 在 **费用标签** 页面，单击 **下一步**。

     2. 在 **请选择启用标签** 区域，按需搜索并添加 **标签key**，单击 **下一步**。

     3. 单击 **确认启用**，在弹出的 **提示** 对话框，单击 **确定**。
   - 曾经启用过![sc_enable_tagging_fees_for_acs_sae_namespace](<Base64-Image-Removed>)

     1. 在 **费用标签** 页面的 **标签key** 文本框，输入标签，并单击 **搜索**。

     2. 在搜索结果区域，单击目标标签 **操作** 列的 **启用**。

        如果需要启用多个标签，可选中多个标签，然后单击 **批量启用**。

**重要**

   - 标签区分英文大小写。

   - 2023年03月13日起，新建的应用或重新部署的现有应用，SAE平台会为其绑定系统标签 **acs:sae:namespace**（控制台不可见），您还需要在费用与成本启用该标签。


3. 根据标签分配财务单元。

1. 在左侧导航栏，选择**成本分摊** \> **财务单元**。

2. 在 **财务单元** 页面的左侧导航栏，单击 **财务单元** 右侧的加号图标，在弹出的 **新增单元** 对话框，输入单元名称，然后单击 **确定**。

      ![image](<Base64-Image-Removed>)

3. 在 **财务单元** 页面的左侧导航栏，选择 **所有资源**，在右侧资源列表 **标签** 列单击筛选图标，在弹出的搜索框选中已启用的标签，然后单击 **确定**。

      ![image](<Base64-Image-Removed>)

4. 在筛选结果的 **操作** 列，单击 **分配**，在弹出的 **分配** 对话框的 **请选择** 下拉列表选择已设定的单元名称，然后单击 **确定**。
4. 查看费用信息。

![image](<Base64-Image-Removed>)

1. 在左侧导航栏，选择**成本分摊** \> **分账明细**。

2. 在 **分账明细** 页面，在账单报表的标题栏按需筛选维度，例如筛选已设置的 **财务单元**。



      在 **分账账单** 页面，查看费用信息的搜索结果。您也可以在账单报表右上角，单击 **导出账单CSV** 查看。

## 更多信息

关于分账管理的更多信息，请参见以下文档：

- [费用标签](https://help.aliyun.com/zh/user-center/cost-allocation-tags#topic-2059661 "")

- [财务单元](https://help.aliyun.com/zh/user-center/cost-center-overview#topic-2059648 "")

- [分账账单](https://help.aliyun.com/zh/user-center/user-guide/split-bills-1#topic-2059653 "")