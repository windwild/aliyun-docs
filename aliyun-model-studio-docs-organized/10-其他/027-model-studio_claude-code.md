### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/)Claude Code

# Claude Code

更新时间：2026-02-24 20:37:58

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Cherry Studio](https://help.aliyun.com/zh/model-studio/cherry-studio)[下一篇：Cline](https://help.aliyun.com/zh/model-studio/cline)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速开始

模型配置

支持的模型

模型选型建议

详细步骤

1\. 开通阿里云百炼

2\. 安装 Claude Code

3\. 配置 Base URL、API Key 和模型

4\. 运行 claude code

（可选）更多配置模型的方式

错误码

常见问题

问题1：启动 claude code 后，界面显示“Unable to connect to Anthropic services. Failed to connect to api.anthropic.com: ERR\_BAD\_REQUEST”，该怎么办

问题2：Token 消耗太快了，如何节省 Token？

阿里云百炼的千问系列模型支持 Anthropic API 兼容接口，可以通过 Claude Code 调用千问系列模型。

**重要**

1. 本文档仅适用于中国内地版（北京地域），仅可使用北京地域下创建的百炼 API Key。

2. 旧版兼容接口`https://dashscope.aliyuncs.com/api/v2/apps/claude-code-proxy`仅支持调用`qwen3-coder-plus`模型。指定其他模型将不会生效，系统仍会按`qwen3-coder-plus`进行调用和计费。如需调用其他模型，请按本文配置迁移至新版接口。

3. **本文档仅适用于按量付费模式，Coding Plan 用户请使用专属 Base URL 和 API Key 接入**，详情请参考 [Coding Plan 说明文档](https://help.aliyun.com/zh/model-studio/coding-plan "") 进行配置。


## 快速开始

如果您已经熟悉 Claude Code，可以通过以下命令快速接入阿里云百炼：

```bash
export ANTHROPIC_BASE_URL=https://dashscope.aliyuncs.com/apps/anthropic
export ANTHROPIC_API_KEY=YOUR_DASHSCOPE_API_KEY   # 用百炼 API KEY 替换 YOUR_DASHSCOPE_API_KEY
export ANTHROPIC_MODEL=qwen3.5-plus # 可按需替换为其他支持的模型。
claude
```

如需详细的配置说明，请参考 [详细步骤](https://help.aliyun.com/zh/model-studio/claude-code?spm=a2c4g.11186623.0.0.b58d5b88f8kHp4#f5833365be842 "")。

## 模型配置

### **支持的模型**

百炼提供的 Anthropic API 兼容服务支持以下千问系列模型：

| **模型系列** | **支持的模型名称（model）** |
| --- | --- |

|     |     |
| --- | --- |
| **模型系列** | **支持的模型名称（model）** |
| 千问Max<br>（部分模型支持思考模式） | qwen3-max、qwen3-max-2026-01-23（支持思考模式）、qwen3-max-preview（支持思考模式） [查看更多](https://help.aliyun.com/zh/model-studio/models#d4ccf72f23jh9 "") |
| 千问Plus | qwen3.5-plus、qwen3.5-plus-2026-02-15、qwen-plus、qwen-plus-latest、qwen-plus-2025-09-11 [查看更多](https://help.aliyun.com/zh/model-studio/models#5ef284d4ed42p "") |
| 千问Flash | qwen3.5-flash、qwen3.5-flash-2026-02-23、qwen-flash、qwen-flash-2025-07-28 [查看更多](https://help.aliyun.com/zh/model-studio/models#13ff05e329blt "") |
| 千问Turbo | qwen-turbo、qwen-turbo-latest [查看更多](https://help.aliyun.com/zh/model-studio/models#947fc66bc1ldf "") |
| 千问Coder<br>（不支持思考模式） | qwen3-coder-next、qwen3-coder-plus、qwen3-coder-plus-2025-09-23、qwen3-coder-flash [查看更多](https://help.aliyun.com/zh/model-studio/models#d698550551bob "") |
| 千问VL<br>（不支持思考模式） | qwen3-vl-plus、qwen3-vl-flash、qwen-vl-max、qwen-vl-plus [查看更多](https://help.aliyun.com/zh/model-studio/models#94b18818a6ywy "") |
| 千问开源模型 | qwen3.5-397b-a17b、qwen3.5-120b-a10b、qwen3.5-27b、qwen3.5-35b-a3b |
| 第三方模型 | - kimi-k2.5、kimi-k2-thinking<br>  <br>- glm-5、glm-4.7、glm-4.6<br>  <br>- MiniMax-M2.5、MiniMax-M2.1 |

模型参数及计费规则请参考 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

### 模型选型建议

针对不同任务类型，推荐使用以下模型：

- 复杂推理任务（设计应用架构、实现复杂算法等）：推荐使用千问Plus系列模型（已升级至Qwen3.5）、千问 Max 系列模型、`qwen3-coder-next`（兼具代码能力与响应速度）、`qwen3-coder-plus`。

- 简单编码任务（编写函数、生成代码注释等）：推荐使用千问 Flash 系列模型、`qwen3-coder-next`。


## 详细步骤

### 1\. 开通阿里云百炼

1. **注册账号**：若无阿里云账号，需首先[注册](https://account.alibabacloud.com/register/intl_register.htm)。


> 如遇问题，请参见 [注册阿里云账号](https://help.aliyun.com/zh/account/step-1-register-an-alibaba-cloud-account "")。

2. **开通阿里云百炼：** 使用 **阿里云主账号** 前往[阿里云百炼大模型服务平台](https://bailian.console.aliyun.com/?tab=model#/model-market)，阅读并同意协议后，将自动开通阿里云百炼，如果未弹出服务协议，则表示您已经开通。


> 如果开通服务时提示“您尚未进行实名认证”，请先进行 [实名认证](https://help.aliyun.com/zh/account/verify-your-identity-individual-account "")。


> 首次开通百炼后，您可领取新人免费额度（有效期：百炼开通后90天内），用于模型推理服务。免费额度领取方法和详情，请查看 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "") 页面。

**说明**

1. 超出额度或期限将产生费用，开启 [免费额度用完即停](https://help.aliyun.com/zh/model-studio/new-free-quota#d1cb80ac11i92 "") 功能将避免此情况下产生费用，具体费用请以控制台的实际报价和最终账单为准。

2. Claude Code 无法使用 [Q：如何使用每天 2000 次的免费额度？](https://help.aliyun.com/zh/model-studio/qwen-code#44be39e126jlw "")。


### **2\. 安装 Claude Code**

macOS

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

### 3\. 配置 Base URL、API Key 和模型

要通过兼容 Anthropic API 的方式来接入阿里云百炼的模型服务，需要配置以下环境变量。

1. `ANTHROPIC_BASE_URL`：设置为 `https://dashscope.aliyuncs.com/apps/anthropic`。

2. `ANTHROPIC_API_KEY`或`ANTHROPIC_AUTH_TOKEN`：设置为 [阿里云百炼 API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。


> `ANTHROPIC_API_KEY`或`ANTHROPIC_AUTH_TOKEN`均可作为接入认证，只需要设置其一即可。本文以`ANTHROPIC_API_KEY`为例。

3. `ANTHROPIC_MODEL`：设置为 [模型列表](https://help.aliyun.com/zh/model-studio/claude-code?spm=a2c4g.11186623.0.0.b58d5b88f8kHp4#07833dedefft7 "") 中支持的模型。


macOS

Windows

1. 在终端中执行以下命令，查看默认 Shell 类型。















```bash
echo $SHELL
```

2. 根据 Shell 类型设置环境变量，命令如下：






Zsh



Bash

































```bash
# 用百炼 API KEY 替换 YOUR_DASHSCOPE_API_KEY
echo 'export ANTHROPIC_BASE_URL="https://dashscope.aliyuncs.com/apps/anthropic"' >> ~/.zshrc
echo 'export ANTHROPIC_API_KEY="YOUR_DASHSCOPE_API_KEY"' >> ~/.zshrc
echo 'export ANTHROPIC_MODEL="qwen3.5-plus"' >> ~/.zshrc
```



















```bash
# 用百炼 API Key 替换 YOUR_DASHSCOPE_API_KEY
echo 'export ANTHROPIC_BASE_URL="https://dashscope.aliyuncs.com/apps/anthropic"' >> ~/.bash_profile
echo 'export ANTHROPIC_API_KEY="YOUR_DASHSCOPE_API_KEY"' >> ~/.bash_profile
echo 'export ANTHROPIC_MODEL="qwen3.5-plus"' >> ~/.bash_profile
```

3. 在终端中执行下列命令，使环境变量生效。






Zsh



Bash

































```bash
source ~/.zshrc
```



















```bash
source ~/.bash_profile
```

4. 在终端中执行下列命令，查看环境变量是否生效。















```bash
echo $ANTHROPIC_BASE_URL
echo $ANTHROPIC_API_KEY
echo $ANTHROPIC_MODEL
```


1. 在 Windows 中，可以通过 CMD 或 PowerShell 将阿里云百炼提供的 Base URL 和 [API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 设置为环境变量。






CMD



PowerShell



















1. 在 CMD 中运行以下命令，设置环境变量。















      ```powershell
      REM 用百炼 API Key 替换 YOUR_DASHSCOPE_API_KEY
      setx ANTHROPIC_API_KEY "YOUR_DASHSCOPE_API_KEY"
      setx ANTHROPIC_BASE_URL "https://dashscope.aliyuncs.com/apps/anthropic"
      setx ANTHROPIC_MODEL "qwen3.5-plus"
      ```

2. 打开一个新的 CMD 窗口，运行以下命令，检查环境变量是否生效。















      ```powershell
      echo %ANTHROPIC_API_KEY%
      echo %ANTHROPIC_BASE_URL%
      echo %ANTHROPIC_MODEL%
      ```


1. 在 PowerShell 中运行以下命令，设置环境变量。















      ```powershell
      # 用百炼 API Key 替换 YOUR_DASHSCOPE_API_KEY
      [Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", "YOUR_DASHSCOPE_API_KEY", [EnvironmentVariableTarget]::User)
      [Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://dashscope.aliyuncs.com/apps/anthropic", [EnvironmentVariableTarget]::User)
      [Environment]::SetEnvironmentVariable("ANTHROPIC_MODEL", "qwen3.5-plus", [EnvironmentVariableTarget]::User)
      ```

2. 打开一个新的 PowerShell 窗口，运行以下命令，检查环境变量是否生效。















      ```powershell
      echo $env:ANTHROPIC_API_KEY
      echo $env:ANTHROPIC_BASE_URL
      echo $env:ANTHROPIC_MODEL
      ```


### 4\. 运行 claude code

进入项目目录，在终端执行`claude`命令。

```bash
claude
```

初次使用 claude code 时，可能会强制要求登录 Anthropic 账户。请按以下步骤操作以跳过该流程：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1692159671/p1049602.png)

1. 定位用户主目录下的 `.claude.json` 文件，具体路径如下：

   - macOS / Linux: `~/.claude.json`

   - Windows: `C:\Users\%USERNAME%\.claude.json`
2. 将`hasCompletedOnboarding` 字段的值设置为 `true`















```json
{
     "hasCompletedOnboarding": true
}
```

3. 保存文件，然后在新终端中重新运行 `claude`。


### （可选）更多配置模型的方式

Claude Code 支持以下模型配置方式， **按优先级从高到低排列**，优先级高的配置会覆盖优先级低的配置。

1. **对话期间**：执行`/model <模型名称>`命令切换模型。适用于临时切换模型。















```plaintext
/model qwen3.5-plus
```

2. **启动 claude code 时**：执行`claude --model <模型名称>`指定模型。适用于单次会话。















```plaintext
claude --model qwen3.5-plus
```

3. **设置环境变量**：可按任务复杂度配置不同级别的模型，Claude Code 会根据任务类型自动选择合适的模型。适用于全局生效。















```plaintext
export ANTHROPIC_DEFAULT_OPUS_MODEL="qwen3.5-plus"
export ANTHROPIC_DEFAULT_SONNET_MODEL="qwen3.5-plus"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="qwen3-coder-next"
```



其中：

   - `ANTHROPIC_DEFAULT_OPUS_MODEL`：用于复杂推理、架构设计等高难度任务。

   - `ANTHROPIC_DEFAULT_SONNET_MODEL`：用于代码编写、功能实现等日常任务。

   - `ANTHROPIC_DEFAULT_HAIKU_MODEL`：用于语法检查、文件搜索等简单任务。
4. **在 setting.json 配置文件中永久设置**：在项目根目录或用户主目录创建`settings.json`文件，并写入模型配置信息，可分别进行项目级或用户级的永久配置。















```json
{
     "env": {
       "ANTHROPIC_DEFAULT_OPUS_MODEL": "qwen3.5-plus",
       "ANTHROPIC_DEFAULT_SONNET_MODEL": "qwen3.5-plus",
       "ANTHROPIC_DEFAULT_HAIKU_MODEL": "qwen3-coder-next"
     }
}
```


## **错误码**

| **HTTP状态码** | **错误类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **HTTP状态码** | **错误类型** | **说明** |
| 400 | invalid\_request\_error | 请求格式或内容存在问题。具体原因可能包括：缺少必要的请求参数、参数值的数据类型不正确等。 |
| 400 | Arrearage | 账户欠费导致服务暂停，请充值后重试。 |
| 403 | authentication\_error | API Key 存在问题。具体原因可能包括：请求头中未提供 API Key、提供的 API Key 不正确等。 |
| 404 | not\_found\_error | 未找到请求的资源。具体原因可能包括：兼容接口拼写有误、请求头中的模型不存在等。 |
| 429 | rate\_limit\_error | 账户达到了速率限制，建议降低请求频率。 |
| 500 | api\_error | 发生了一个通用的服务器内部错误，建议稍后重试。 |
| 529 | overloaded\_error | API 服务器当前负载过高，暂时无法处理新的请求。 |

## 常见问题

### 问题1：启动 claude code 后，界面显示“Unable to connect to Anthropic services. Failed to connect to api.anthropic.com: ERR\_BAD\_REQUEST”，该怎么办

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8289749671/p1049322.png)

重新 [配置环境变量](https://help.aliyun.com/zh/model-studio/claude-code?spm=a2c4g.11186623.0.0.b58d5b88f8kHp4#58cb9a24f7bxt "")，然后在终端执行 `claude` 命令。

### 问题2：Token 消耗太快了，如何节省 Token？

Claude Code 会扫描整个项目目录、读取相关代码文件并维护完整对话历史来提供编码建议，因而其 Token 消耗远高于普通对话场景。以下方法可帮助您有效控制消耗：

1. **减少无关文件**：为避免扫描不相关文件而造成 Token 消耗，建议在具体的项目目录中启动 Claude Code，同时仅保留必要的项目文件。

2. **总结对话**：Claude Code 会将历史对话内容作为上下文，当对话长度达到上下文窗口的 95% 时，Claude Code 会自动地总结对话内容。也可以通过执行`/compact`命令来手动地总结对话内容。

3. **精确指令**：模糊的请求会触发非必要的文件扫描，消耗更多的 Token。请在使用 Claude Code 时提出更明确、具体的问题或指令。

4. **分解任务**：在处理复杂任务时，可以将其分解为若干简单任务。

5. **重置上下文**：在开启一个全新的任务之前，使用`/clear`命令重置上下文，避免无关信息消耗 Token。


可以参考 [Claude Code 官方文档](https://docs.anthropic.com/zh-CN/docs/claude-code/costs) 了解更多节省 Token 的技巧。如需查看具体的 Token 消耗量和费用明细，请参考 [账单查询与成本管理](https://help.aliyun.com/zh/model-studio/bill-query-and-cost-management "")。