### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)[接入AI工具](https://help.aliyun.com/zh/model-studio/use-coding-plan-in-ai-tools/)OpenClaw

# OpenClaw

更新时间：2026-02-25 21:56:45

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：快速开始](https://help.aliyun.com/zh/model-studio/coding-plan-quickstart)[下一篇：OpenCode](https://help.aliyun.com/zh/model-studio/opencode-coding-plan)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

安装 OpenClaw

在 OpenClaw 中配置 Coding Plan

使用 OpenClaw

OpenClaw （原名Moltbot/Clawdbot ）是一个开源的个人 AI 助手平台，支持通过多种消息渠道与 AI 交互。通过配置可接入阿里云百炼的Coding Plan模型。

接入OpenClaw需要修改配置文件`~/.openclaw/openclaw.json` 中的模型提供商、默认模型和可用模型列表等，下面 [在 OpenClaw 中配置 Coding Plan](https://help.aliyun.com/zh/model-studio/openclaw-coding-plan?spm=a2c4g.11186623.help-menu-2400256.d_0_2_2_0.1a5e4c4d4s2y86#cc5b5358b3woj "") 章节提供了具体配置信息。

## **安装 OpenClaw**

1. 执行以下命令开始安装。






macOS/Linux



Windows

































```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```





在PowerShell中执行以下命令。

















```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

2. 安装结束后会自动出现提示信息，请根据提示信息完成 OpenClaw 配置，参考配置如下：


|     |     |
| --- | --- |
| **配置项** | **配置内容** |
| I understand this is powerful and inherently risky. Continue? | 选择 "Yes" |
| Onboarding mode | 选择 "QuickStart" |
| Model/auth provider | 选择 "Skip for now"，后续可以配置 |
| Filter models by provider | 选择 "All providers" |
| Default model | 使用默认配置 |
| Select channel (QuickStart) | 选择 "Skip for now"，后续可以配置 |
| Configure skills now? (recommended) | 选择 "No"，后续可以配置。 |
| Enable hooks? | 按空格键选中选项，按回车键进入下一步。 |
| How do you want to hatch your bot? | 选择 "Hatch in TUI"。 |


## **在 OpenClaw 中配置 Coding Plan**

1. 打开配置文件。

运行以下命令打开 Web UI，然后在Web UI的左侧菜单栏中选择**Config** \> **Raw**。















```bash
openclaw dashboard
```





**说明**





也可以运行以下命令，在命令行终端中打开配置文件。

















```bash
nano ~/.openclaw/openclaw.json
```

2. 修改配置文件。


1. 在 JSON 根对象中加入如下 `models` 配置（如果已存在则替换）。请将 YOUR\_API\_KEY 替换为您的 Coding Plan [API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)。















      ```json
      "models": {
        "mode": "merge",
        "providers": {
          "bailian": {
            "baseUrl": "https://coding.dashscope.aliyuncs.com/v1",
            "apiKey": "YOUR_API_KEY",
            "api": "openai-completions",
            "models": [\
              {\
                "id": "qwen3.5-plus",\
                "name": "qwen3.5-plus",\
                "reasoning": false,\
                "input": ["text", "image"],\
                "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
                "contextWindow": 1000000,\
                "maxTokens": 65536\
              },\
              {\
                "id": "qwen3-max-2026-01-23",\
                "name": "qwen3-max-2026-01-23",\
                "reasoning": false,\
                "input": ["text"],\
                "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
                "contextWindow": 262144,\
                "maxTokens": 65536\
              },\
              {\
                "id": "qwen3-coder-next",\
                "name": "qwen3-coder-next",\
                "reasoning": false,\
                "input": ["text"],\
                "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
                "contextWindow": 262144,\
                "maxTokens": 65536\
              },\
              {\
                "id": "qwen3-coder-plus",\
                "name": "qwen3-coder-plus",\
                "reasoning": false,\
                "input": ["text"],\
                "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
                "contextWindow": 1000000,\
                "maxTokens": 65536\
              },\
              {\
                "id": "MiniMax-M2.5",\
                "name": "MiniMax-M2.5",\
                "reasoning": false,\
                "input": ["text"],\
                "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
                "contextWindow": 1000000,\
                "maxTokens": 65536\
              },\
              {\
                "id": "glm-5",\
                "name": "glm-5",\
                "reasoning": false,\
                "input": ["text"],\
                "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
                "contextWindow": 202752,\
                "maxTokens": 16384\
              },\
              {\
                "id": "glm-4.7",\
                "name": "glm-4.7",\
                "reasoning": false,\
                "input": ["text"],\
                "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
                "contextWindow": 202752,\
                "maxTokens": 16384\
              },\
              {\
                "id": "kimi-k2.5",\
                "name": "kimi-k2.5",\
                "reasoning": false,\
                "input": ["text", "image"],\
                "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
                "contextWindow": 262144,\
                "maxTokens": 32768\
              }\
            ]
          }
        }
      }
      ```

2. 找到 `agents.defaults` 对象，并替换或添加以下两个字段：















      ```json
      "model": {
        "primary": "bailian/qwen3.5-plus"
      },
      "models": {
        "bailian/qwen3.5-plus": {},
        "bailian/qwen3-max-2026-01-23": {},
        "bailian/qwen3-coder-next": {},
        "bailian/qwen3-coder-plus": {},
        "bailian/MiniMax-M2.5": {},
        "bailian/glm-5": {},
        "bailian/glm-4.7": {},
        "bailian/kimi-k2.5": {}
      }
      ```


以下是修改后的完整配置文件示例

完整配置文件示例（您的实际配置可能包含更多配置项）

注：请将 YOUR\_API\_KEY 替换为您的 Coding Plan API key。

```json
{
  "models": {
    "mode": "merge",
    "providers": {
      "bailian": {
        "baseUrl": "https://coding.dashscope.aliyuncs.com/v1",
        "apiKey": "YOUR_API_KEY",
        "api": "openai-completions",
        "models": [\
          {\
            "id": "qwen3.5-plus",\
            "name": "qwen3.5-plus",\
            "reasoning": false,\
            "input": ["text", "image"],\
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
            "contextWindow": 1000000,\
            "maxTokens": 65536\
          },\
          {\
            "id": "qwen3-max-2026-01-23",\
            "name": "qwen3-max-2026-01-23",\
            "reasoning": false,\
            "input": ["text"],\
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
            "contextWindow": 262144,\
            "maxTokens": 65536\
          },\
          {\
            "id": "qwen3-coder-next",\
            "name": "qwen3-coder-next",\
            "reasoning": false,\
            "input": ["text"],\
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
            "contextWindow": 262144,\
            "maxTokens": 65536\
          },\
          {\
            "id": "qwen3-coder-plus",\
            "name": "qwen3-coder-plus",\
            "reasoning": false,\
            "input": ["text"],\
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
            "contextWindow": 1000000,\
            "maxTokens": 65536\
          },\
          {\
            "id": "MiniMax-M2.5",\
            "name": "MiniMax-M2.5",\
            "reasoning": false,\
            "input": ["text"],\
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
            "contextWindow": 1000000,\
            "maxTokens": 65536\
          },\
          {\
            "id": "glm-5",\
            "name": "glm-5",\
            "reasoning": false,\
            "input": ["text"],\
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
            "contextWindow": 202752,\
            "maxTokens": 16384\
          },\
          {\
            "id": "glm-4.7",\
            "name": "glm-4.7",\
            "reasoning": false,\
            "input": ["text"],\
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
            "contextWindow": 202752,\
            "maxTokens": 16384\
          },\
          {\
            "id": "kimi-k2.5",\
            "name": "kimi-k2.5",\
            "reasoning": false,\
            "input": ["text", "image"],\
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },\
            "contextWindow": 262144,\
            "maxTokens": 32768\
          }\
        ]
      }
    }
  },
  "agents": {
    "defaults": {
      "model": {
        "primary": "bailian/qwen3.5-plus"
      },
      "models": {
        "bailian/qwen3.5-plus": {},
        "bailian/qwen3-max-2026-01-23": {},
        "bailian/qwen3-coder-next": {},
        "bailian/qwen3-coder-plus": {},
        "bailian/MiniMax-M2.5": {},
        "bailian/glm-5": {},
        "bailian/glm-4.7": {},
        "bailian/kimi-k2.5": {}
      }
    }
  },
  "gateway": {
    "mode": "local"
  }
}
```

3. 保存配置。

   - 如果在Web UI中修改，先单击右上角 **Save** 保存，然后单击 **Update** 来使配置生效。

   - 如果在终端中修改，先保存文件并退出，然后运行以下命令来使配置生效。















     ```bash
     openclaw gateway restart
     ```

## **使用** OpenClaw

1. 在终端中运行以下命令，可以分别以 Web UI 和 TUI 的方式使用 OpenClaw。






Web UI



TUI

































```bash
openclaw dashboard
```





![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1774069671/p1050227.png)

















```bash
openclaw tui
```





![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1774069671/p1050228.png)

2. 执行/model命令可以在当前会话中切换模型。例如，执行如下命令可以切换到qwen3-coder-next模型。















```bash
/model qwen3-coder-next
```



注：如需在每次新会话中都使用指定模型，请参考前面的步骤修改配置文件中的primary字段。