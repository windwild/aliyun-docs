### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)[接入AI工具](https://help.aliyun.com/zh/model-studio/use-coding-plan-in-ai-tools/)Cursor

# Cursor

更新时间：2026-02-26 06:32:39

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Cline](https://help.aliyun.com/zh/model-studio/cline-coding-plan)[下一篇：Qwen Code](https://help.aliyun.com/zh/model-studio/qwen-code-coding-plan)

该文章对您有帮助吗？

反馈

阿里云百炼 Coding Plan 支持 Cursor，可参考本文进行配置与使用。

**说明**

由于 Cursor 的产品限制，仅订阅 **Cursor Pro** 及以上套餐的用户支持自定义配置模型，否则会报错“The model xxx does not work with your current plan or api key”。

1. 通过 [Cursor 官网](https://cursor.com/features) 下载并安装 Cursor。

2. 在 Cursor 中，点击![2026-02-03_16-52-37](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0376170771/p1052115.jpg)图标，单击 **Cursor Settings**，选择 **Models** 页面。

3. 开启 **OpenAI API Key**，填入您的Coding Plan [API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)。

4. 开启 **Override OpenAI Base URL**，填入`https://coding.dashscope.aliyuncs.com/v1`。

5. 在 **Add or search model** 文本框中，输入Coding Plan [支持的模型](https://help.aliyun.com/zh/model-studio/coding-plan-overview "") 中的模型名称，点击 **Add Custom Model**。

在Cursor中，请将kimi-k2.5模型名称写为 **kimi-k2-5**，将glm-4.7模型名称写为 **glm-4-7**


配置完成后，在聊天面板中选择相应的模型即可开始使用。

> 如果找不到添加的模型，请在聊天面板中点击并关闭 **Auto** 模式，再从模型下拉栏中选择。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0376170771/p1053930.png)