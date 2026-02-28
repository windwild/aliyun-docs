### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan-guide/)[接入AI工具](https://help.aliyun.com/zh/model-studio/use-coding-plan-in-ai-tools/)Claude Code

# Claude Code

更新时间：2026-02-26 05:04:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OpenCode](https://help.aliyun.com/zh/model-studio/opencode-coding-plan)[下一篇：Claude Code IDE 插件](https://help.aliyun.com/zh/model-studio/claude-code-ide-plugin-coding-plan)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

安装 Claude Code

配置 Coding Plan 接入信息

开始使用

切换模型

能力扩展

常见命令

了解更多

错误码

常见问题

Coding Plan中的模型支持 Anthropic API 兼容接口，可以通过 Claude Code 调用。

## **安装 Claude Code**

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

## 配置 Coding Plan 接入信息

在 Claude Code 中接入百炼 Coding Plan，需要配置以下信息：

1. `ANTHROPIC_BASE_URL`：设置为 `https://coding.dashscope.aliyuncs.com/apps/anthropic`。

2. `ANTHROPIC_AUTH_TOKEN`：设置为[Coding Plan](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/coding_plan)专属 API Key。

3. `ANTHROPIC_MODEL`：设置为 Coding Plan [支持的模型](https://help.aliyun.com/zh/model-studio/coding-plan "")。


macOS/Linux

Windows

1. 创建并打开配置文件`~/.claude/settings.json`。


> `~` 代表用户主目录。如果 `.claude` 目录不存在，需要先行创建。可在终端执行 `mkdir -p ~/.claude` 来创建。
















```bash
nano ~/.claude/settings.json
```

2. 编辑配置文件。将 YOUR\_API\_KEY 替换为 Coding Plan 专属 API Key。















```json
{
       "env": {
           "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY",
           "ANTHROPIC_BASE_URL": "https://coding.dashscope.aliyuncs.com/apps/anthropic",
           "ANTHROPIC_MODEL": "qwen3.5-plus"
       }
}
```



保存配置文件，重新打开一个终端即可生效。

3. 编辑或新增 `~/.claude.json` 文件，将`hasCompletedOnboarding` 字段的值设置为 `true`，并保存文件。















```json
{
     "hasCompletedOnboarding": true
}
```


1. 在 Windows 中，可以通过 CMD 或 PowerShell 将Coding Plan的 Base URL 和 API Key 设置为环境变量。






CMD



PowerShell



















1. 在 CMD 中运行以下命令，设置环境变量。















      ```powershell
      REM 用您的Coding Plan API Key 替换 YOUR_API_KEY
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


1. 在 PowerShell 中运行以下命令，设置环境变量。















      ```powershell
      # 用您的Coding Plan API Key 替换 YOUR_API_KEY
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


2. 编辑或新增 `C:\Users\%USERNAME%\.claude.json` 文件，将`hasCompletedOnboarding` 字段的值设置为 `true`，并保存文件。















```json
{
     "hasCompletedOnboarding": true
}
```


## **开始使用**

1. 打开终端，并进入项目所在的目录。运行以下命令启动程序 Claude Code：















```bash
cd path/to/your_project
claude
```

2. 启动后，需要授权 Claude Code 执行文件。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0924991771/p1040228.png)

3. 输入`/status`确认模型、Base URL、API Key 是否配置正确。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0428202771/p1054776.png)

4. 在 Claude Code 中对话。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8292228671/p1040230.png)


## 切换模型

1. **启动 Claude Code 时切换**：在终端执行`claude --model <模型名称>`指定模型并启动 Claude Code，例如`claude --model qwen3-coder-next`。

2. **会话期间**：在对话框输入`/model <模型名称>`命令切换模型，例如`/model qwen3-coder-next`。


## 能力扩展

Claude Code 支持通过 MCP 和 Skills 扩展自身能力，例如调用联网搜索获取实时信息、使用图片理解 Skill 分析图像内容等。详情请参考 [最佳实践](https://help.aliyun.com/zh/model-studio/coding-plan-best-practices/ "")。

## 常见命令

| **命令** | **说明** | **示例** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **命令** | **说明** | **示例** |
| /init | 在项目根目录生成 CLAUDE.md 文件，用于定义项目级指令和上下文。 | /init |
| /status | 查看当前模型、API Key、Base URL 等配置状态。 | /status |
| /model <模型名称> | 切换模型。 | /model qwen3-coder-next |
| /clear | 清除对话历史，开始全新对话。 | /clear |
| /plan | 进入规划模式，仅分析和讨论方案，不修改代码。 | /plan |
| /compact | 压缩对话历史，释放上下文窗口空间。 | /compact |
| /config | 打开配置菜单，可设置语言、主题等。 | /config |

更多命令与用法详情，请参考 [Claude Code 官方文档](https://code.claude.com/docs/en/overview)。

## **了解更多**

如需进一步了解 Claude Code 的 MCP、Skills、自定义命令、Hooks 等高级功能，请参考 [Claude Code 官方文档](https://code.claude.com/docs/en/overview)。

## 错误码

请参考 [常见报错及解决方案](https://help.aliyun.com/zh/model-studio/coding-plan-faq#a9248c44029g6 "")。

## 常见问题

请参考 [常见问题](https://help.aliyun.com/zh/model-studio/coding-plan-faq "")。