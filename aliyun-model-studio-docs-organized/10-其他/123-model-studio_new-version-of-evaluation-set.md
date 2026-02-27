### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用评测](https://help.aliyun.com/zh/model-studio/application-evaluation/)[新版应用评测](https://help.aliyun.com/zh/model-studio/new-version-of-application-evaluation/)新版评测集

# 新版评测集

更新时间：2026-02-05 20:59:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：评测集](https://help.aliyun.com/zh/model-studio/application-evaluation-dataset)[下一篇：评测任务](https://help.aliyun.com/zh/model-studio/evaluation-task)

该文章对您有帮助吗？

反馈

- 本页导读

功能概述

创建评测集

方式一：手动上传

方式二：从应用观测导入

评测集管理

发布评测集

评测集详情

版本管理

下一步

评测集是应用评测的数据基础，用于存储和管理评测数据。阿里云百炼支持 **智能体**、 **工作流** 和 **自定义** 三种类型的评测集，帮助您构建适合业务需求的评测体系。

## 功能概述

评测集是评测任务的数据来源,当前支持三种评测集类型：

| **类型** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **类型** | **说明** |
| 智能体 | 根据选中智能体应用的出入参形式，定义评测集。适用于智能体应用的评测。 |
| 工作流 | 根据选中工作流应用的出入参形式，定义评测集。适用于工作流应用的评测。 |
| 自定义 | 任意定义评测集的表结构。适用于自定义评测场景。 |

访问 [评测集](https://bailian.console.aliyun.com/cn-beijing/?tab=app#/efm/app_evaluate/tabs?activeKey=evalSet&name=&pageNum=1) 页面开始使用。

**说明**

创建评测集时，请根据评测任务类型选择合适的评测集类型。创建后类型不可修改。

## 创建评测集

### 方式一：手动上传

访问应用评测页面，单击 **创建评测集**：![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4052430771/p1048179.png)

**配置以下信息：**

- **评测集名称：** 自定义评测集名称（必填，最多50个字符）。

- **描述：** 评测集的描述信息（可选，最多200个字符）。

- **立即发布：** 选择是否在创建后立即发布。选择“否”则保存为草稿状态。

- **存储位置**:固定为平台存储。

- **导入方式：** 选择本地上传。

- **类型**：选择 **智能体**、 **工作流** 或 **自定义**。

  - **选择应用**：（智能体/工作流类型）选择要评测的应用和版本，系统会根据应用的出入参形式生成数据模板。

  - **自定义：** 自定义评测集允许您任意定义评测集的表结构，适用于特殊评测场景或自定义评测需求。
- **编辑表结构**：查看或编辑评测集的字段结构。智能体和工作流类型会自动生成结构，自定义类型需手动定义，可点击 **添加列** 按钮，自定义字段名称和类型。

- **请导入数据：** 点击 **EXCEL数据模板** 下载模板文件，填写数据后上传。支持xls/xlsx格式，文件大小限制20MB以内。

- 单击 **确认** 后，评测集将显示在列表中。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4052430771/p1047755.png)

### 方式二：从应用观测导入![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4052430771/p1048175.png)

您可以访问应用观测页面，将真实数据添加到评测集。

## 评测集管理

### 发布评测集

创建的评测集需要发布后才能用于评测任务：访问评测集详情页，单击 **发布**，等待 **发布状态** 显示 **已发布**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4052430771/p1048189.png)

### 评测集详情

在评测集详情页，您可以进行以下操作：

- **查看数据**：浏览评测集中的所有数据条目。

  - **编辑表头**：修改数据内容，添加或删除列等（仅草稿状态）。

  - **添加数据**：追加导入新的数据文件。

  - **导出**：导出评测集数据到文件。
- **删除**：删除评测集（已发布的评测集如被引用则无法删除）。


### 版本管理

评测集支持版本管理，每次发布会生成新版本：创建评测任务时可选择使用特定版本的评测集。

## 下一步

创建评测任务： [评测任务](https://help.aliyun.com/zh/model-studio/evaluation-task "")。