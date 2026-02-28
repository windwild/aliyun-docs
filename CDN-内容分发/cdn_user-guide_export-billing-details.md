### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[用量查询](https://help.aliyun.com/zh/cdn/user-guide/resource-usage/)明细导出

# 明细导出

更新时间：2025-11-17 02:45:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：汇总导出](https://help.aliyun.com/zh/cdn/user-guide/export-resource-usage-data)[下一篇：资源包管理](https://help.aliyun.com/zh/cdn/user-guide/query-the-details-of-resource-plans)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

导出用量明细

相关API

支持按照域名、时间范围、账户等维度灵活筛选计费用量明细，可按需导出明细并下载到本地查看，便于您进行用量分析与费用核对。

## 导出用量明细

**说明**

- 可导出近一年的用量汇总数据，单次最长一个月。

- 用量明细每5分钟一个计费点，以Excel形式展示。


1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，选择 **用量查询**。

3. 选择 **明细导出** 页签，单击 **创建导出任务**。

4. 根据实际需要设置 **任务名称**、 **导出对账类型**、 **查询时间** 等参数，然后单击 **确定**。



![导出](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5249498361/p365705.png)

5. 导出任务创建完成后，单击 **下载** 查看明细。



![导出](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1926057561/p365736.png)


## 相关API

| **相关API** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **相关API** | **说明** |
| [CreateUsageDetailDataExportTask](https://help.aliyun.com/zh/cdn/api-createusagedetaildataexporttask#doc-api-Cdn-CreateUsageDetailDataExportTask "") | 创建用量明细导出任务，生成Excel文件下载。 |
| [DescribeUserUsageDetailDataExportTask](https://help.aliyun.com/zh/cdn/api-describeuserusagedetaildataexporttask#doc-api-Cdn-DescribeUserUsageDetailDataExportTask "") | 查询账户下域名5分钟明细数据导出任务。 |
| [DeleteUsageDetailDataExportTask](https://help.aliyun.com/zh/cdn/api-deleteusagedetaildataexporttask#doc-api-Cdn-DeleteUsageDetailDataExportTask "") | 删除用量明细数据导出任务。 |