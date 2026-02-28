### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用广场](https://help.aliyun.com/zh/model-studio/application-gallery/)[官方应用-全妙轻应用系列](https://help.aliyun.com/zh/model-studio/quanmiao-light-application-series/)[计费说明（全妙轻应用）](https://help.aliyun.com/zh/model-studio/light-application-billing-document/)作文批改计费

# 作文批改计费

更新时间：2026-02-11 02:16:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费说明

开通产品&产品控制台

计费详情

账单地址

相关文档

常见问题

如果任务运行到中途失败了，怎么计费？

全妙产品矩阵包含4个SaaS产品妙笔/妙策/妙搜/妙读和若干个AI Agent（场景化能力），本文档主要介绍AI Agent中作文批改应用的计费。

## **计费说明**

系统将根据您实际使用的模型所产生的输入与输出 Tokens 总量进行计费，采用后付费模式，按量结算。

## **开通产品&产品控制台**

- 开通产品：点击 [作文批改开通页面](https://common-buy.aliyun.com/?commodityCode=sfm_quanmiaoAPI_public_cn) 可开通作文批改产品服务；

- 产品控制台：点击 [产品控制台](https://bailian.console.aliyun.com/?spm=5176.30275541.J_ZGek9Blx07Hclc3Ddt9dg.4.1d6c2f3deJ9i11&scm=20140722.S_card%40%40%E4%BA%A7%E5%93%81%40%402983180.S_new%7EUND%7Ecard.ID_card%40%40%E4%BA%A7%E5%93%81%40%402983180-RL_%E7%99%BE%E7%82%BC%E5%A4%A7%E6%A8%A1%E5%9E%8B-LOC_2024SPSearchCard-OR_ser-PAR1_2150420317622352750362019e6447-V_4-RE_new5-P0_0-P1_0&tab=app&productCode=p_efm&switchAgent=10680836#/app/app-market/quanmiao/homework-correction) 进行产品体验。


## **计费详情**

| 模型 | 输入价格 | 输出价格 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 模型 | 输入价格 | 输出价格 |
| 作文批改模型1&2 | ¥0.015/千tokens | ¥0.015/千tokens |
| 作文批改轻量模型 | ¥0.0015/千tokens | ¥0.0015/千tokens |
| 作文OCR识别 | ¥0.01/千tokens | ¥0.01/千tokens |

## **账单地址**

账单查询地址： [账单详情](https://usercenter2.aliyun.com/finance/expense-report/expense-detail?spm=a2c4g.11186623.0.0.619355efACwmfT)。

## **相关文档**

接口文档： [作文批改接口](https://help.aliyun.com/zh/model-studio/api-quanmiaolightapp-2024-08-01-runessaycorrection "")。

## **常见问题**

- ### **如果任务运行到中途失败了，怎么计费？**



当任务运行到中途失败时，主要是看最后一个事件消息的event，如果是task-failed，就不计费；其他运行成功部分计费，失败部分不计费。在产品客户端页面立即中断并展示状态。