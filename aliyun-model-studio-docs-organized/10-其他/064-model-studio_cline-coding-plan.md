### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)[接入AI工具](https://help.aliyun.com/zh/model-studio/use-coding-plan-in-ai-tools/)Cline

# Cline

更新时间：2026-02-26 05:04:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Codex](https://help.aliyun.com/zh/model-studio/codex-coding-plan)[下一篇：Cursor](https://help.aliyun.com/zh/model-studio/cursor-coding-plan)

该文章对您有帮助吗？

反馈

Cline 是一款VSCode智能编程的插件。阿里云百炼 Coding Plan 支持 Cline，可参考本文进行配置与使用。

1. 在 [VSCode](https://code.visualstudio.com/) IDE的扩展商店中搜索并安装 Cline。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2061045471/p947567.png)

2. 安装完成后，单击左侧边栏的 Cline 图标。单击 **Bring my own API key**，在弹出窗口选择 **OpenAI Compatible** 作为 API Provider，并配置如下参数。


> 如果您之前使用过 Cline，请单击右上角的设置按钮后进行配置。





| **配置项** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **配置项** | **说明** |
| API Provider | 设置为OpenAI Compatible |
| Base URL | 设置为https://coding.dashscope.aliyuncs.com/v1 |
| OpenAI Compatible API Key | 填入 Coding Plan 专属 [API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)（sk-sp-xxxxxxx） |
| Model ID | 填入 Coding Plan [支持的模型](https://help.aliyun.com/zh/model-studio/coding-plan-overview "")，如qwen3.5-plus |



配置完成后，单击右上角 **Done**。

3. 在 Cline 中使用。单击右上角齿轮设置按钮，修改 Model ID 即可切换模型。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8292228671/p1040271.png)