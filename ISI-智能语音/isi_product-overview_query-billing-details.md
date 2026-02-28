### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[产品概述](https://help.aliyun.com/zh/isi/product-overview/)[产品计费](https://help.aliyun.com/zh/isi/product-overview/billing/)查询服务用量和账单明细

# 查询服务用量和账单明细

更新时间：2024-12-27 01:19:44

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：欠费说明](https://help.aliyun.com/zh/isi/product-overview/overdue-payments)[下一篇：功能发布记录](https://help.aliyun.com/zh/isi/product-overview/release-notes)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

查看服务用量

总览

监控报表

设置资源包额度预警

查看账单明细

本文为您介绍如何查询智能语音交互的服务用量和账单明细。

## **查看服务用量**

### **总览**

登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/)，在 **总览** 页面，您可以查看已开通语音服务的用量统计。

**说明**

购买资源包后，隔日显示用量。用量统计和资源包剩余仅计算截止到昨日数据，请根据实际情况评估今日用量，并注意账户可用余量和资金余额，及时补充资源包。

### **监控报表**

登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/)，在 **监控统计** 页面，您可以根据服务、项目和时间范围等过滤条件，筛选并查看对应的监控报表。如果某服务为置灰状态，该服务不可勾选，您需要先将已勾选的其他服务取消勾选，才能选择该服务。

例如，在 **语音识别** 页签，勾选 **服务** 下拉菜单中的 **录音文件识别** 服务，其他过滤条件保持默认，即可查看录音文件识别服务的所有项目在近7日内的调用量和QPS并发量。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2108447661/p511885.png)

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4193837661/p511695.png)

### **设置资源包额度预警**

1. 登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/)。

2. 在 **总览** 页面，鼠标悬停 **告警设置**，单击弹窗中的 **去设置**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0685837171/p806756.png)

3. 在阿里云费用与成本的 **资源包** 页面，单击 **余量预警设置**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0949725371/p893913.png)

4. 在 **余量预警设置** 对话框中，打开 **开启预警** 开关，设置 **剩余额度比例**，然后单击 **确定**。

例如，选择智能语音交互服务对应的资源包，设置剩余额度比例为 **20%**，则在智能语音交互的资源包剩余量为当月总量的20%时给您发送预警通知。



**说明**





仅支持对总量递减类型、包月周期型的资源包设置预警设置。


更多信息，请参见 [资源包预警设置](https://help.aliyun.com/zh/sls/configure-warning-settings-for-a-resource-plan "")。

## **查看账单明细**

登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/)，单击顶部菜单栏的 **费用**，进入 **费用与成本** 页面。

- 在左侧导航栏选择 **账单** > **账单详情**，您可以进行如下操作：

  - **查看总体消费情况**

    您可以在 **账单详情** 页面，通过选择 **账单月份**、 **产品名称** 等查看您的消费情况。

    ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0949725371/p893789.png)

  - **查看具体服务的费用明细**

    **统计项** 选择 **计费项**， **统计周期** 选择 **明细**， **产品名称** 选择 **智能语音交互**，然后单击 **搜索**，查看智能语音交互的费用明细。

    ![image](<Base64-Image-Removed>)

  - **导出账单CSV**

    单击![image](<Base64-Image-Removed>)，选择导出当前已筛选出的部分内容，或者近18个月的内容，单击 **确定**，即可导出。

    ![image](<Base64-Image-Removed>)

  - **导出用量明细CSV**

    单击 **查看用量明细**，选择 **产品名称**、 **产品规格** 和 **使用时间**，单击 **导出**，即可导出用量明细CSV。

    ![image](<Base64-Image-Removed>)
- 在左侧导航栏选择 **账户** > **资源包**， **资源维度** 选择 **资源包**，并切换至 **使用明细** 标签页，查看资源包使用明细。

您还可以结合 **被抵扣资源实例使用开始时间**、 **资源包实例ID**、 **被抵扣实例ID** 进行筛选，完成后单击搜索。

![image](<Base64-Image-Removed>)