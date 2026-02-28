### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 百炼RAM权限

# 百炼RAM权限

更新时间：2025-02-14 02:32:59

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

系统策略

自定义策略

常见问题

如果您的RAM用户（子账号）或RAM角色需要管理百炼、使用百炼的知识库，或希望通过API使用数据管理、Prompt工程及长期记忆等功能，请先为其配置相应的RAM权限。

> **RAM权限：** 可以分为 [系统策略](https://help.aliyun.com/zh/model-studio/bailian-ram-permission#37eb3ef09cs85 "") 和 [自定义策略](https://help.aliyun.com/zh/model-studio/bailian-ram-permission#3d1b4dd02cdbv "") **。** 系统策略旨在帮助您快速配置权限，满足大多数常见场景。如果您需要对权限进行精细化管控（例如，限制特定RAM用户调用 [API目录](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-dir/ "") 下的某个具体的API），您可以选择使用自定义策略。当然您也可以将这两种策略结合起来使用，更多说明请参见 [权限策略概览](https://help.aliyun.com/zh/ram/policy-overview "")。

## **系统策略**

由阿里云创建和管理的一组权限集合，RAM用户（子账号）或 [RAM角色](https://help.aliyun.com/zh/ram/user-guide/ram-role-overview "") 只能使用，无法修改，策略的版本更新由阿里云负责维护。百炼提供以下系统策略：

> 请您先阅读 [权限管理](https://help.aliyun.com/zh/model-studio/permission-management-overview "")，以了解如何使用和选择系统策略。

> [开通百炼](https://help.aliyun.com/zh/model-studio/permission-management-overview#c1ff829039x59 "") 的主账号默认拥有 **AliyunBailianFullAccess** 系统策略，以及所有业务空间的权限。

| **系统策略名称** | **系统策略说明** | **管控层权限说明** | **数据权限说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **系统策略名称** | **系统策略说明** | **管控层权限说明** | **数据权限说明** |
| **AliyunBailianFullAccess** | 拥有所有 [管控层权限](https://help.aliyun.com/zh/model-studio/permission-management-overview#62bd3c8691osd "") 和 [数据权限](https://help.aliyun.com/zh/model-studio/grant-data-access-permission-to-ram-user "")。<br>> 请注意，这里不是数据层权限，因此不包含业务空间的权限。 | 拥有所有管控层权限，包括：<br>- 百炼业务空间、账号以及全部 [API-KEY](https://help.aliyun.com/zh/model-studio/videos/api-key-management "") 的管理权限。<br>  <br>- 首次开通百炼功能特性的权限（例如 [应用观测](https://help.aliyun.com/zh/model-studio/application-observation "")）。<br>  <br>- 支付预付费类订单所必须的基础权限。 [了解还需要哪些权限](https://help.aliyun.com/zh/model-studio/bailian-ram-permission#c27328f24a24q "")。 | 拥有数据管理权限，包括：<br>- 可以创建、管理和访问 [结构化知识库](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#d422eac95494v "")。<br>  <br>- 可以使用知识库的 [命中测试](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#b17217c68dmif "") 功能。<br>  <br>- 可以调用 [API目录](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-dir/ "") 下的所有API。 |
| **AliyunBailianReadOnlyAccess** | 拥有部分管控层权限（只读权限）和部分数据权限（只读权限）。<br>> 请注意，这里不是数据层权限，因此不包含业务空间的权限。 | 拥有部分管控层权限（只读权限），包括：<br>- 百炼业务空间、账号、全部API-KEY的只读权限。<br>  <br>- 无开通百炼功能特性的权限。<br>  <br>- 支付预付费订单所必须的基础权限。 [了解还需要哪些权限](https://help.aliyun.com/zh/model-studio/bailian-ram-permission#c27328f24a24q "")。 | 拥有数据只读权限。<br>- 无法创建、管理和访问 [结构化知识库](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#d422eac95494v "")。<br>  <br>- 无法使用知识库的 [命中测试](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#b17217c68dmif "") 功能。<br>  <br>- 无法调用 [API目录](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-dir/#table-qwe-lcc-8lo "") 下的增删改类API，例如 [Retrieve](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-retrieve "")、 [AddFile](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-addfile "")、 [CreateIndex](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-createindex "") 以及 [UpdateMemory](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updatememory "")等。<br>  <br>- 可以调用 [API目录](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-dir/#table-qwe-lcc-8lo "") 下的只读类API，例如 [DescribeFile](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-describefile "")、 [GetIndexJobStatus](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getindexjobstatus "") 等。 |
| **AliyunBailianControlFullAccess** | 仅拥有部分管控层权限（部分管理权限）。 | 拥有部分管控层权限（部分管理权限），包括：<br>- 百炼业务空间、账号以及全部API-KEY的管理权限。<br>  <br>- 无开通百炼功能特性的权限。<br>  <br>- 支付预付费订单所必须的基础权限。 [了解还需要哪些权限](https://help.aliyun.com/zh/model-studio/bailian-ram-permission#c27328f24a24q "")。 | 无权限。 |
| **AliyunBailianControlReadOnlyAccess** | 仅拥有部分管控层权限（只读权限）。 | 拥有部分管控层权限（只读权限），包括：<br>- 百炼业务空间、账号以及全部API-KEY的只读权限。<br>  <br>- 无开通百炼功能特性的权限。<br>  <br>- 支付预付费订单所必须的基础权限。 [了解还需要哪些权限](https://help.aliyun.com/zh/model-studio/bailian-ram-permission#c27328f24a24q "")。 | 无权限。 |
| **AliyunBailianDataFullAccess** | 仅拥有数据权限。<br>> 请注意，这里不是数据层权限，因此不包含业务空间的权限。 | 无权限。 | 拥有数据管理权限，包括：<br>- 可以创建、管理和访问 [结构化知识库](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#d422eac95494v "")。<br>  <br>- 可以使用知识库的 [命中测试](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#b17217c68dmif "") 功能。<br>  <br>- 可以调用 [API目录](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-dir/#table-qwe-lcc-8lo "") 下的所有API。 |
| **AliyunBailianDataReadOnlyAccess** | 仅拥有部分数据权限（只读权限）。<br>> 请注意，这里不是数据层权限，因此不包含业务空间的权限。 | 无权限。 | 拥有数据只读权限。<br>- 无法创建、管理和访问 [结构化知识库](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#d422eac95494v "")。<br>  <br>- 无法使用知识库的 [命中测试](https://help.aliyun.com/zh/model-studio/rag-knowledge-base#b17217c68dmif "") 功能。<br>  <br>- 无法调用 [API目录](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-dir/#table-qwe-lcc-8lo "") 下的增删改类API，例如 [Retrieve](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-retrieve "")、 [AddFile](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-addfile "")、 [CreateIndex](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-createindex "") 以及 [UpdateMemory](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updatememory "")等。<br>  <br>- 可以调用 [API目录](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-dir/#table-qwe-lcc-8lo "") 下的只读类API，例如 [DescribeFile](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-describefile "")、 [GetIndexJobStatus](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getindexjobstatus "") 等。 |

## **自定义策略**

由用户（可以是主账号或具有`AliyunRAMFullAccess`系统策略的RAM用户）自行创建和管理的一组权限集合，策略的版本更新由用户维护，自定义策略中的权限可以随时更新或删除。

> 目前知识库、数据管理、Prompt工程及长期记忆的API已支持自定义策略。您可以根据需要，从下方列表中选择所需权限创建自定义策略，并授予RAM用户以实现最小授权，操作步骤请参见 [配置自定义策略](https://help.aliyun.com/zh/model-studio/grant-data-access-permission-to-ram-user#18ae698512yhe "")。

| **功能特性** | **API** | **调用此API所需的权限名称** | **权限说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能特性** | **API** | **调用此API所需的权限名称** | **权限说明** |
| **知识库** | [CreateIndex - 创建索引](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-createindex "") | **sfm:CreateIndex** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-createindex#api-detail-31 "")。 |
| [GetIndexJobStatus - 查询索引创建任务状态](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getindexjobstatus "") | **sfm:GetIndexJobStatus** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getindexjobstatus#api-detail-31 "")。 |
| [SubmitIndexJob - 提交索引创建任务](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-submitindexjob "") | **sfm:SubmitIndexJob** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-submitindexjob#api-detail-31 "")。 |
| [SubmitIndexAddDocumentsJob - 提交索引追加任务](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-submitindexadddocumentsjob "") | **sfm:SubmitIndexAddDocumentsJob** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-submitindexadddocumentsjob#api-detail-31 "")。 |
| [Retrieve - 检索知识索引](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-retrieve "") | **sfm:Retrieve** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-retrieve#api-detail-31 "")。 |
| [ListIndexDocuments - 查询索引下的文档列表](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listindexdocuments "") | **sfm:ListIndexFiles** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listindexdocuments#api-detail-31 "")。 |
| [ListChunks - 查询索引下的分片列表](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listchunks "") | **sfm:ChunkList** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listchunks#api-detail-31 "")。 |
| [ListIndices - 查询索引列表](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listindices "") | **sfm:ListIndex** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listindices#api-detail-31 "")。 |
| [DeleteIndex - 删除知识库索引](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deleteindex "") | **sfm:DeleteIndex** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deleteindex#api-detail-31 "")。 |
| [DeleteIndexDocument - 删除知识库索引文档](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deleteindexdocument "") | **sfm:DeleteIndexDocument** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deleteindexdocument#api-detail-31 "")。 |
| **数据管理** | [AddCategory - 新增类目](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-addcategory "") | **sfm:AddCategory** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-addcategory#api-detail-31 "")。 |
| [ListCategory - 类目列表](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listcategory "") | **sfm:ListCategory** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listcategory#api-detail-31 "")。 |
| [DeleteCategory - 删除类目](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deletecategory "") | **sfm:DeleteCategory** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deletecategory#api-detail-31 "")。 |
| [ApplyFileUploadLease - 申请文档上传租约](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-applyfileuploadlease "") | **sfm:ApplyFileUploadLease** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-applyfileuploadlease#api-detail-31 "")。 |
| [AddFile - 添加文档](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-addfile "") | **sfm:AddFile** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-addfile#api-detail-31 "")。 |
| [DescribeFile - 查询文档状态](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-describefile "") | **sfm:DescribeFile** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-describefile#api-detail-31 "")。 |
| [ListFile - 文档列表](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listfile "") | **sfm:ListFile** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listfile#api-detail-31 "")。 |
| [DeleteFile - 删除文档](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deletefile "") | **sfm:DeleteFile** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deletefile#api-detail-31 "")。 |
| [UpdateFileTag - 更新文档标签](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updatefiletag "") | **sfm:UpdateFileTag** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updatefiletag#api-detail-31 "")。 |
| **Prompt工程** | [CreatePromptTemplate - 创建Prompt模板](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-createprompttemplate "") | **sfm:CreatePromptTemplate** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-createprompttemplate#api-detail-31 "")。 |
| [GetPromptTemplate - 获取Prompt模板](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getprompttemplate "") | **sfm:GetPromptTemplate** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getprompttemplate#api-detail-31 "")。 |
| [UpdatePromptTemplate - 更新Prompt模板](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updateprompttemplate "") | **sfm:UpdatePromptTemplate** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updateprompttemplate#api-detail-31 "")。 |
| [DeletePromptTemplate - 删除Prompt模板](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deleteprompttemplate "") | **sfm:DeletePromptTemplate** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deleteprompttemplate#api-detail-31 "")。 |
| [ListPromptTemplates - 获取Prompt模板列表](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listprompttemplates "") | **sfm:ListPromptTemplates** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listprompttemplates#api-detail-31 "")。 |
| **长期记忆** | [CreateMemory - 创建长期记忆体](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-creatememory "") | **sfm:CreateMemory** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-creatememory#api-detail-31 "")。 |
| [GetMemory - 获取长期记忆体](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getmemory "") | **sfm:GetMemory** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getmemory#api-detail-31 "")。 |
| [UpdateMemory - 更新长期记忆体](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updatememory "") | **sfm:UpdateMemory** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updatememory#api-detail-31 "")。 |
| [DeleteMemory - 删除长期记忆体](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deletememory "") | **sfm:DeleteMemory** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deletememory#api-detail-31 "")。 |
| [ListMemories - 获取长期记忆体列表](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listmemories "") | **sfm:ListMemories** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listmemories#api-detail-31 "")。 |
| [CreateMemoryNode - 创建长期记忆节点](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-creatememorynode "") | **sfm:CreateMemoryNode** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-creatememorynode#api-detail-31 "")。 |
| [GetMemoryNode - 获取长期记忆节点](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getmemorynode "") | **sfm:GetMemoryNode** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-getmemorynode#api-detail-31 "")。 |
| [UpdateMemoryNode - 更新长期记忆节点](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updatememorynode "") | **sfm:UpdateMemoryNode** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-updatememorynode#api-detail-31 "")。 |
| [DeleteMemoryNode - 删除长期记忆节点](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deletememorynode "") | **sfm:DeleteMemoryNode** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-deletememorynode#api-detail-31 "")。 |
| [ListMemoryNodes - 获取长期记忆节点列表](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listmemorynodes "") | **sfm:ListMemoryNodes** | 请参见 [授权信息](https://help.aliyun.com/zh/model-studio/api-bailian-2023-12-29-listmemorynodes#api-detail-31 "")。 |

## **常见问题**

**使用RAM用户（或RAM角色）时，首次开通模型调用、应用观测等功能时需要哪些RAM权限？**

|     |     |
| --- | --- |
| **功能名称** | **需要开通的RAM权限** |
| **模型调用** | 请使用主账号在 [RAM控制台](https://ram.console.aliyun.com/) 中为您的RAM用户（或RAM角色）配置`AliyunBailianFullAccess`系统策略（其它管控层权限不可以）。 |
| **应用观测** | 请使用主账号在 [RAM控制台](https://ram.console.aliyun.com/) 中为您的RAM用户（或RAM角色）配置`AliyunBailianFullAccess`（其它管控层权限不可以）、`AliyunRAMFullAccess`和`AliyunTracingAnalysisFullAccess`系统策略。 |
| **支付预付费订单** | 请使用主账号在 [RAM控制台](https://ram.console.aliyun.com/) 中为您的RAM用户（或RAM角色）配置`AliyunBSSOrderAccess`系统策略与 [百炼的管控层权限](https://help.aliyun.com/zh/model-studio/permission-management-overview#580f5d631f2zm "")（从`AliyunBailianFullAccess`、`AliyunBailianReadOnlyAccess`、`AliyunBailianControlFullAccess`、`AliyunBailianControlReadOnlyAccess`中四选一）。 |

**AdministratorAccess包含AliyunBailianFullAccess系统策略吗？**

是的，`AdministratorAccess`包含`AliyunBailianFullAccess`系统策略。拥有`AdministratorAccess`系统策略的RAM用户（子账号）默认具备所有 [管控层权限](https://help.aliyun.com/zh/model-studio/permission-management-overview#62bd3c8691osd "") 和 [数据权限](https://help.aliyun.com/zh/model-studio/grant-data-access-permission-to-ram-user "")。

> 请注意，这里不是数据层权限，因此不包含业务空间的权限。