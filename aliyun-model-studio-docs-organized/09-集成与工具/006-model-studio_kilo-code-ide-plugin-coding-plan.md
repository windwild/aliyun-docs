### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)[接入AI工具](https://help.aliyun.com/zh/model-studio/use-coding-plan-in-ai-tools/)Kilo Code IDE 插件

# Kilo Code IDE 插件

更新时间：2026-02-26 06:31:50

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Kilo CLI](https://help.aliyun.com/zh/model-studio/kilo-cli-coding-plan)[下一篇：其他工具](https://help.aliyun.com/zh/model-studio/other-tools-coding-plan)

该文章对您有帮助吗？

反馈

本文介绍如何在 Kilo Code IDE 插件中配置与使用阿里云百炼 Coding Plan。

Kilo Code IDE 插件支持在 VSCode、VSCode 系列 IDE（如 Cursor、Trae 等）、JetBrains 系列 IDE（如 IntelliJ IDEA、PyCharm 等）中使用，详情可参考 [Kilo Code 官方文档](https://kilo.ai/docs/code-with-ai)。以下以 VSCode 为例：

1. 打开 VSCode，在扩展市场搜索 Kilo Code，选择信任发布者并安装。安装完成后，在侧边栏打开。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7506980771/p1054374.png)

2. 选择 Bring my own Key。

![截屏2026-02-12 18](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7506980771/p1054375.png)

3. 请按照以下配置填入相关信息：


   - **API Provider**：OpenAI Compatible

   - **Base URL**：`https://coding.dashscope.aliyuncs.com/v1`

   - **API Key**：套餐专属 [API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)，格式为`sk-sp-xxxxx`。

   - **Model**：填写 Coding Plan [支持的模型](https://help.aliyun.com/zh/model-studio/coding-plan-overview "")，单击 Use custom。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7506980771/p1054379.png)

配置完成后单击 **Save** 保存。

4. 开始使用。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7506980771/p1054383.png)