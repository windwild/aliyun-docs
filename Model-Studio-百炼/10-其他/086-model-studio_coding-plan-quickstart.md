### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)快速开始

# 快速开始使用Coding Plan

更新时间：2026-02-26 05:04:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Coding Plan概述](https://help.aliyun.com/zh/model-studio/coding-plan)[下一篇：OpenClaw](https://help.aliyun.com/zh/model-studio/openclaw-coding-plan)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

订阅 Coding Plan

获取套餐专属 API Key 和 Base URL

选择AI工具

配置AI工具

本文介绍如何快速完成 Coding Plan 订阅和编程工具配置。

## **订阅 Coding Plan**

1. 访问[阿里云百炼控制台](https://bailian.console.aliyun.com/cn-beijing?tab=model#/efm/coding_plan)，单击左侧导航栏的 **订阅套餐**，根据实际需求选择并购买套餐。Coding Plan 仅支持阿里云主账号进行订阅和使用，不支持 RAM 用户订阅。

2. 购买完成后，您可以在订阅套餐页面，查看套餐用量、升级与续费套餐。

![2026-02-25_15-48-31](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3997802771/p1054819.jpg)


## **获取套餐专属 API Key 和 Base URL**

您需要获取并配置套餐专属的 API Key 和 Base URL，才能正确使用并抵扣套餐额度。

- **API Key**：访问[Coding Plan 页面](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)，获取Coding Plan 专属 API Key（格式为`sk-sp-xxxxx`）。

![20260128233128](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0432269671/p1050434.jpg)

- **Base URL**：根据 AI 工具支持的 API 协议，使用以下对应的 Base URL。


  - **OpenAI 兼容协议**：`https://coding.dashscope.aliyuncs.com/v1`

  - **Anthropic 兼容协议**：`https://coding.dashscope.aliyuncs.com/apps/anthropic`


> 各工具使用的兼容协议请参见对应的接入文档。

**说明**

Coding Plan 专属的 API Key 和 Base URL 与百炼按量计费的 API Key（`sk-xxxxx`）和Base URL（`https://dashscope.aliyuncs.com/xxxxxx`）不互通，请勿混用。

## **选择AI工具**

Coding Plan 支持主流的AI工具，可按需选择。

|     |     |     |
| --- | --- | --- |
| [**OpenClaw**\<br>\<br>开源、自托管个人 AI 助手](https://help.aliyun.com/zh/model-studio/openclaw-coding-plan) | [**OpenCode**\<br>\<br>开源 AI 编程代理工具](https://help.aliyun.com/zh/model-studio/opencode-coding-plan) | [**Claude Code**\<br>\<br>AI 终端编码助手，支持自然语言编程](https://help.aliyun.com/zh/model-studio/claude-code-coding-plan) |
| [**Claude Code IDE 插件**\<br>\<br>在 VS Code 等 IDE 中使用 Claude Code](https://help.aliyun.com/zh/model-studio/claude-code-ide-plugin-coding-plan) | [**Qwen Code**\<br>\<br>专为 Qwen3-Coder 优化的开源命令行 AI 工具](https://help.aliyun.com/zh/model-studio/qwen-code-coding-plan) | [**Cline**\<br>\<br>VS Code 扩展，智能代码补全和调试](https://help.aliyun.com/zh/model-studio/cline-coding-plan) |
| [**Codex**\<br>\<br>OpenAI 推出的命令行编程工具](https://help.aliyun.com/zh/model-studio/codex-coding-plan) | [**Cursor**\<br>\<br>AI 原生代码编辑器](https://help.aliyun.com/zh/model-studio/cursor-coding-plan) | [**Kilo CLI**\<br>\<br>轻量高性能命令行编程工具](https://help.aliyun.com/zh/model-studio/kilo-cli-coding-plan) |
| [**Kilo Code IDE 插件**\<br>\<br>VS Code 扩展，高效编码助手](https://help.aliyun.com/zh/model-studio/kilo-code-ide-plugin-coding-plan) | [**其他工具**\<br>\<br>更多支持的编码工具持续扩展中](https://help.aliyun.com/zh/model-studio/other-tools-coding-plan) |  |

## **配置AI工具**

OpenClaw

Claude Code

接入OpenClaw需要修改配置文件`~/.openclaw/openclaw.json` 中的模型提供商、默认模型和可用模型列表等，下面 [在 OpenClaw 中配置 Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-quickstart#oc03config "") 章节提供了具体配置信息。

### **安装 OpenClaw**

1. 执行以下命令开始安装。






macOS/Linux



Windows

































```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```





在 PowerShell 中执行以下命令。

















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


### **在 OpenClaw 中配置 Coding Plan**

1. 打开配置文件。

运行以下命令打开 Web UI，然后在 Web UI 的左侧菜单栏中选择**Config** \> **Raw**。















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


以下是修改后的完整配置文件示例。

完整配置文件示例（您的实际配置可能包含更多配置项）

注：请将 YOUR\_API\_KEY 替换为您的 Coding Plan API key。若开启思考模式后无输出，请更新 OpenClaw 至最新版本。

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

   - 如果在 Web UI 中修改，先单击右上角 **Save** 保存，然后单击 **Update** 来使配置生效。

   - 如果在终端中修改，先保存文件并退出，然后运行以下命令来使配置生效。















     ```bash
     openclaw gateway restart
     ```

### **使用 OpenClaw**

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

2. 执行 `/model` 命令可以在当前会话中切换模型。例如，执行如下命令可以切换到qwen3-coder-next模型。















```bash
/model qwen3-coder-next
```




> 如需在每次新会话中都使用指定模型，请参考前面的 [在 OpenClaw 中配置 Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-quickstart#oc03config "") 修改配置文件中的 `agents.defaults.model.primary` 字段。


接入 Claude Code 需要配置以下信息。

1. `ANTHROPIC_BASE_URL`：设置为 `https://coding.dashscope.aliyuncs.com/apps/anthropic`。

2. `ANTHROPIC_AUTH_TOKEN`：设置为Coding Plan专属 [API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)。

3. `ANTHROPIC_MODEL`：设置为Coding Plan [支持的模型](https://help.aliyun.com/zh/model-studio/coding-plan-overview "")。


### **安装 Claude Code**

macOS/Linux

Windows

1. 安装或更新 [Node.js](https://nodejs.org/en/download/)（v18.0 或更高版本）。

2. 在终端中执行下列命令，安装 Claude Code。















```bash
npm install -g @anthropic-ai/claude-code
```

3. 运行以下命令验证安装。若有版本号输出，则表示安装成功。















```bash
claude --version
```


在 Windows 上使用 Claude Code，需要安装 WSL 或 [Git for Windows](https://git-scm.com/install/windows)，然后在 WSL 或 Git Bash 中执行以下命令。

```bash
npm install -g @anthropic-ai/claude-code
```

> 详情可以参考Claude Code官方文档的 [Windows安装教程](https://docs.anthropic.com/en/docs/claude-code/setup#windows-setup)。

### **在** Claude Code 中配置 Coding Plan

macOS/Linux

Windows

1. 创建并打开配置文件`~/.claude/settings.json`。


> `~` 代表用户主目录。如果 `.claude` 目录不存在，需要先行创建。可在终端执行 `mkdir -p ~/.claude` 来创建。
















```bash
nano ~/.claude/settings.json
```

2. 编辑配置文件。将 YOUR\_API\_KEY 替换为Coding Plan专属 [API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)，将ANTHROPIC\_MODEL设置为 [支持的模型](https://help.aliyun.com/zh/model-studio/coding-plan-overview "")。















```json
{
       "env": {
           "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY",
           "ANTHROPIC_BASE_URL": "https://coding.dashscope.aliyuncs.com/apps/anthropic",
           "ANTHROPIC_MODEL": "qwen3.5-plus"
       }
}
```

3. 打开一个新的终端使环境变量配置生效。


1. 在 Windows 中，可以通过 CMD 或 PowerShell 将Coding Plan的 Base URL 和 API Key 设置为环境变量。






CMD



PowerShell



















1. 在 CMD 中运行以下命令，设置环境变量。请将 YOUR\_API\_KEY 替换为Coding Plan专属 [API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)，将ANTHROPIC\_MODEL设置为 [Coding Plan概述](https://help.aliyun.com/zh/model-studio/coding-plan-overview#b01f82a4218kx "")。















      ```powershell
      setx ANTHROPIC_AUTH_TOKEN "YOUR_API_KEY"
      setx ANTHROPIC_BASE_URL "https://coding.dashscope.aliyuncs.com/apps/anthropic"
      setx ANTHROPIC_MODEL "qwen3.5-plus"
      ```

2. 打开一个新的 CMD 窗口，运行以下命令，检查环境变量是否生效。















      ```powershell
      echo %ANTHROPIC_AUTH_TOKEN%
      echo %ANTHROPIC_BASE_URL%
      echo %ANTHROPIC_MODEL%
      ```


1. 在 PowerShell 中运行以下命令，设置环境变量。请将 YOUR\_API\_KEY 替换为Coding Plan专属 [API Key](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)，将ANTHROPIC\_MODEL设置为 [Coding Plan概述](https://help.aliyun.com/zh/model-studio/coding-plan-overview#b01f82a4218kx "")。















      ```powershell
      [Environment]::SetEnvironmentVariable("ANTHROPIC_AUTH_TOKEN", "YOUR_API_KEY", [EnvironmentVariableTarget]::User)
      [Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://coding.dashscope.aliyuncs.com/apps/anthropic", [EnvironmentVariableTarget]::User)
      [Environment]::SetEnvironmentVariable("ANTHROPIC_MODEL", "qwen3.5-plus", [EnvironmentVariableTarget]::User)
      ```

2. 打开一个新的 PowerShell 窗口，运行以下命令，检查环境变量是否生效。















      ```powershell
      echo $env:ANTHROPIC_AUTH_TOKEN
      echo $env:ANTHROPIC_BASE_URL
      echo $env:ANTHROPIC_MODEL
      ```


### **使用 Claude Code**

1. 打开终端，并进入项目所在的目录。运行以下命令启动程序 Claude Code：















```bash
cd path/to/your_project
claude
```



启动后，选择信任此文件夹，允许 Claude Code 在该文件夹中访问、编辑与执行文件。


> 如果 Claude Code 启动时要求登录 Anthropic 账号，请找到 `~/.claude.json`（macOS/Linux）或 `C:\Users\%USERNAME%\.claude.json`（Windows）文件。将`hasCompletedOnboarding` 字段的值设置为 `true`，保存后重新启动即可。

2. 切换模型。

1. **启动 Claude Code 时切换**：执行`claude --model <模型名称>`指定模型，例如`claude --model qwen3-coder-next`。

2. **对话期间**：执行`/model <模型名称>`命令切换模型，例如`/model qwen3-coder-next`。
3. 在 Claude Code 中对话。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8292228671/p1040230.png)