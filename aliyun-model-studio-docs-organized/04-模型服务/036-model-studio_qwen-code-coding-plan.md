### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)[接入AI工具](https://help.aliyun.com/zh/model-studio/use-coding-plan-in-ai-tools/)Qwen Code

# Qwen Code

更新时间：2026-02-26 05:04:32

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Cursor](https://help.aliyun.com/zh/model-studio/cursor-coding-plan)[下一篇：Kilo CLI](https://help.aliyun.com/zh/model-studio/kilo-cli-coding-plan)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

安装 Qwen Code

配置与使用 Qwen Code

切换模型

常见终端命令

Qwen Code 进阶功能

错误码

常见问题

Qwen Code 是一款命令行 AI 工作流工具，本文介绍如何在 Qwen Code 中配置与使用阿里云百炼 Coding Plan。

## 安装 Qwen Code

1. 安装或更新 [Node.js](https://nodejs.org/en/download/)（v20.0 或更高版本）。

2. 执行以下命令安装或更新 Qwen Code（版本 `≥ 0.10.1` ）















```zsh
npm install -g @qwen-code/qwen-code@latest
```



查看当前安装版本















```zsh
qwen --version
```


## 配置与使用 Qwen Code

1. 在Qwen Code中配置百炼的Coding Plan。

1. 输入`qwen`启动 Qwen Code。


      > 建议在项目目录下使用Qwen Code。
















      ```bash
      qwen
      ```

2. 看到以下界面后，选择 `API-KEY`。


      > 若默认显示了Coding Plan选项，请直接查看下一步。



      > 若默认进入了对话界面，请执行/auth命令来进入设置界面。


      ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4375790771/p1054453.png)

3. 选择 **Coding Plan（百炼，中国）**，Qwen Code将自动设置Coding Plan的Base URL。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2427151771/p1054560.png)

4. 输入Coding Plan的API Key 。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2427151771/p1054562.png)
2. 开始对话。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4375790771/p1054468.png)


## **切换模型**

输入`/model`，可在阿里云百炼 Coding Plan 支持的模型间切换。

如果所需模型（如 `MiniMax-M2.5`、`glm-5`）未出现在列表中，请更新Qwen Code。

1. 输入 `/quit` 退出当前会话。

2. 执行`npm install -g @qwen-code/qwen-code@latest`命令更新Qwen Code。

3. 重新执行 `qwen` 命令启动 Qwen Code。

4. 再次输入 `/model` 即可选择新添加的模型。


## 常见终端命令

| **命令** | **说明** | **示例** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **命令** | **说明** | **示例** |
| `/model` | 切换当前会话中使用的模型。 | `/model` |
| `/auth` | 更改认证方式。 | `/auth` |
| `/init` | 分析当前目录并创建初始上下文文件（QWEN.md），用于定义项目级指令和上下文。 | `/init` |
| `/clear` | 清除终端屏幕内容，开始全新对话。 | `/clear` |
| `/compress` | 用摘要替换聊天历史以节省 Token。 | `/compress` |
| `/settings` | 打开设置编辑器，可配置语言、主题等。 | `/settings` |
| `/summary` | 根据对话历史生成项目摘要。 | `/summary` |
| `/resume` | 恢复之前的对话会话。 | `/resume` |
| `/stats` | 显示当前会话的详细统计信息。 | `/stats` |
| `/help` | 显示可用命令的帮助信息。 | `/help`或`/?` |
| `/quit` | 退出 Qwen Code。 | `/quit` |

更多 Qwen Code 的进阶功能，可以参考 [Qwen Code 官方文档](https://qwenlm.github.io/qwen-code-docs/zh/users/features/commands/)。

## **Qwen Code 进阶功能**

如需进一步了解 Qwen Code 的子智能体、MCP、Skills等高级功能，请参考 [Qwen Code 官方文档](https://qwenlm.github.io/qwen-code-docs/en/users/overview/)。

## 错误码

请参考 [常见报错及解决方案](https://help.aliyun.com/zh/model-studio/coding-plan-faq#a9248c44029g6 "")。

## 常见问题

请参考 [常见问题](https://help.aliyun.com/zh/model-studio/coding-plan-faq "")。