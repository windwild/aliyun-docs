### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)[最佳实践](https://help.aliyun.com/zh/model-studio/coding-plan-best-practices/)添加图片理解Skill

# 添加图片理解Skill

更新时间：2026-02-26 05:04:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：添加联网搜索MCP](https://help.aliyun.com/zh/model-studio/web-search-for-coding-plan)[下一篇：常见问题](https://help.aliyun.com/zh/model-studio/coding-plan-faq)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

视觉支持情况

添加视觉能力

添加Skill

使用示例

百炼 Coding Plan 中的部分模型（如 qwen3.5-plus、kimi-k2.5）原生支持视觉理解，可直接处理图片输入。对于 glm-5、MiniMax-M2.5 等纯文本模型，可通过添加本地 Skill 使其获得视觉能力。本文介绍如何在 Claude Code 中使用模型的视觉理解能力。

**说明**

运行图片理解 Skill 会消耗 Coding Plan 额度，无其他收费项。

## 前提条件

1. 已订阅 [Coding Plan](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)，详情请参见 [快速开始](https://help.aliyun.com/zh/model-studio/coding-plan-quickstart "")。

2. 已在 Coding Plan 工具中完成接入配置，且能正常对话，详情请参见 [接入AI工具](https://help.aliyun.com/zh/model-studio/use-coding-plan-in-ai-tools/ "")。


## 视觉支持情况

| **模型** | **是否支持视觉** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型** | **是否支持视觉** | **说明** |
| - qwen3.5-plus<br>  <br>- kimi-k2.5 | 是 | 无需额外配置，可直接传入图片 |
| - qwen3-max-2026-01-23<br>  <br>- qwen3-coder-next<br>  <br>- qwen3-coder-plus<br>  <br>- glm-5<br>  <br>- glm-4.7<br>  <br>- MiniMax-M2.5 | 否 | 需通过 Skill 辅助模型获得视觉能力 |

如需实现图片理解，请使用qwen3.5-plus和kimi-k2.5模型。若使用Claude Code，可添加 Skill 实现图片理解。

## **添加视觉能力**

### **添加Skill**

在项目目录下的 `.claude` 文件夹中新建 `skills/image-analyzer` 目录，在该目录下创建 `SKILL.md` 文件，并写入以下内容：

```markdown
---
name: image-analyzer
description: 帮助没有视觉能力的模型进行图像理解。当需要分析图像内容、提取图片中的信息、文字、界面元素，或理解截图、图表、架构图等任何视觉内容时，使用此技能，传入图片路径即可获得描述信息。
model: qwen3.5-plus
---
qwen3.5-plus具有视觉理解能力，请直接使用qwen3.5-plus模型进行图片理解。
```

创建完成后的目录结构如下：

```plaintext
.claude/
└── skills/
    └── image-analyzer/
        └── SKILL.md
```

### **使用示例**

以 Claude Code + glm-5 为例：

1. 在项目目录下运行`claude`启动Claude Code，并运行`/model glm-5`切换到`glm-5`模型；

2. 下载[aliyun.png](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20260225/hxwnny/aliyun.png)到项目目录下，并提问：`请加载image-analyzer skill，描述一下 aliyun.png banner位置是什么信息？`可收到如下回复：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5928202771/p1054884.png)