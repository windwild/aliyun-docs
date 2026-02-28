### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据处理](https://help.aliyun.com/zh/oss/user-guide/data-transformation/)[基本概念](https://help.aliyun.com/zh/oss/user-guide/basic-concepts/)任务

# 任务

更新时间：2024-12-26 04:34:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

创建任务

查询任务

更多参考

异步处理以任务的形式对文件进行处理，请求完成时会返回任务ID，之后可以通过任务ID查询任务状态。本文介绍如何使用异步任务进行文件处理。

**说明**

新版数据处理功能API、SDK支持通过 [IMM服务接入点](https://help.aliyun.com/zh/imm/developer-reference/api-imm-2020-09-30-endpoint "") 进行使用。

## **创建任务**

1. 登录 [OSS管理控制台](https://oss.console.aliyun.com/overview)。

2. 在左侧导航栏，单击 **Bucket列表**，然后单击目标Bucket。

3. 在左侧导航栏，选择 **数据处理** **。**

4. 根据需要异步处理的文件类型，选择 **文档处理**、 **媒体处理**，或选择其他由智能媒体管理 (IMM) 提供的数据处理能力。

5. 选中 **任务** 页签，单击 **创建任务**。

6. 在 **创建任务** 面板配置相关参数信息，如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8598911861/p627911.png)




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| 输入存储桶 | 当前需要创建任务的文件所在的Bucket。 |
| 输入路径 | 选择需要处理的文件的存储路径。 |
| 样式 | 选择文件的处理样式。如果没有可以选择的样式，可单击下拉列表中的 **添加样式**，添加新的样式。 |
| 输出路径 | 选择任务结束时输出文件的存储路径。<br>不支持以正斜线（/）结尾的路径，支持使用变量。具体操作，请参见相关文档中的 [变量](https://help.aliyun.com/zh/oss/user-guide/variables "") 部分。 |
| 消息队列 | 选择MNS主题。<br>任务结束时支持以消息通知的方式将处理结果发送到MNS。更多信息，请参见 [快速入门概述](https://help.aliyun.com/zh/mns/getting-started/overview-of-getting-started-1 "") 和 [异步通知消息格式](https://help.aliyun.com/zh/imm/developer-reference/asynchronous-notification-message-examples "")。 |

7. 单击 **确定**。


## **查询任务**

1. 登录 [OSS管理控制台](https://oss.console.aliyun.com/overview)。

2. 在左侧导航栏，单击 **Bucket列表**，然后单击目标Bucket。

3. 在左侧导航栏，选择 **数据处理** **。**

4. 根据需要异步处理的文件类型，选择 **文档处理**、 **媒体处理**，或选择其他由智能媒体管理 (IMM) 提供的数据处理能力。

5. 选中 **任务** 页签，查看任务列表，单击页面下方翻页按钮可查看上一页或下一页。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3745442661/p485888.png)

6. 在 **任务ID** 搜索框输入任务ID（任务ID可以通过任务列表接口 [ListTasks - 列出任务](https://help.aliyun.com/zh/imm/developer-reference/api-imm-2020-09-30-listtasks "") 获取到任务列表，返回的`TaskId`字段即为任务ID），单击搜索按钮可以搜索指定的任务，选择 **开始日期** 和 **结束日期** 可以查询执行日期范围内的任务。

7. 单击 **操作** 列的 **任务详情** 可以查看任务的详细信息。


## **更多参考**

关于如何使用智能媒体管理IMM的SDK，请参见 [概述](https://help.aliyun.com/zh/imm/developer-reference/overview "")。